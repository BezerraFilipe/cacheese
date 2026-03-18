# ADR 003 — Estratégia de Integração e Isolamento do Bot do Telegram

← [ADR 002](./002-autenticacao.md) · [Voltar para Arquitetura](../overview.md) · [Voltar ao índice](../../README.md)

**Status:** Aceito
**Data:** Sprint 0

---

## Contexto

O MVP do Caixa Fácil inclui um bot do Telegram como canal alternativo de registro de transações por linguagem natural (texto ou voz). Esta é uma funcionalidade diferenciadora do produto — mas também a de maior complexidade técnica e maior número de dependências externas: a API do Telegram, uma API de LLM para parsing de linguagem natural, e um mecanismo de webhook para receber as mensagens.

A decisão central deste ADR não é *se* o bot será construído, mas *como* ele será integrado à aplicação principal de forma que sua eventual indisponibilidade não comprometa o funcionamento do app web.

Duas estratégias de integração foram avaliadas.

---

## Alternativas Consideradas

### Integração Acoplada
O bot do Telegram opera como parte integrante da aplicação Rails — compartilhando o mesmo ciclo de request, controllers e tratamento de erros. Uma falha na comunicação com a API do Telegram ou na API de LLM poderia bloquear o processamento de outras requisições ou tornar partes do app instáveis.

**Prós:**
- Implementação mais simples inicialmente
- Menos abstração para um desenvolvedor iniciante

**Contras:**
- Falha em dependência externa (Telegram API, LLM API) pode propagar para o app principal
- Difícil de testar isoladamente
- Qualquer manutenção ou debugging do bot impacta o app inteiro
- Viola o princípio de responsabilidade única

### Integração Isolada (chosen)
O bot opera como um módulo completamente independente dentro da aplicação Rails. Ele tem seu próprio controller de webhook (`TelegramWebhooksController`), seu próprio fluxo de processamento encapsulado em um service object, e falha silenciosamente sem afetar nenhuma outra parte do app.

**Prós:**
- O app web funciona normalmente mesmo com o bot indisponível
- Testável de forma independente com stubs da API do Telegram
- Responsabilidades claramente separadas
- Falhas do Telegram ou da LLM são capturadas e logadas sem propagar exceções
- Mais fácil de evoluir ou substituir no futuro

**Contras:**
- Requer disciplina maior na implementação para manter o isolamento
- Ligeiramente mais código de estrutura inicial

---

## Decisão

**Integração Isolada.**

O princípio fundamental é: **a indisponibilidade do bot nunca deve degradar a experiência do app web**. O bot é um canal alternativo de entrada, não uma dependência do produto. Portanto, toda a lógica do bot deve ser encapsulada de forma que falhas externas sejam contidas dentro do módulo do bot.

---

## Arquitetura de Implementação

### Fluxo de mensagens

```
Usuário (Telegram)
    │
    ▼
Telegram API
    │  POST /telegram/webhook
    ▼
TelegramWebhooksController#create
    │  (responde 200 OK imediatamente)
    ▼
TelegramBotJob (Active Job — processamento assíncrono)
    │
    ▼
TelegramBotService
    ├── Identifica o usuário via TelegramAccount
    ├── Chama LlmParserService (OpenAI API)
    │       └── Extrai: valor, descrição, categoria sugerida
    ├── Envia mensagem de confirmação ao usuário via Telegram API
    └── Aguarda confirmação → cria Transaction
```

### Componentes

**`TelegramWebhooksController`**
- Recebe o webhook do Telegram
- Responde `200 OK` imediatamente (o Telegram exige resposta rápida — timeout de 5s)
- Enfileira um `TelegramBotJob` para processamento assíncrono
- Não tem acesso a nenhuma lógica de negócio diretamente

**`TelegramBotJob` (Active Job)**
- Processa a mensagem de forma assíncrona, fora do ciclo de request
- Captura todas as exceções e as loga sem re-raise
- Se a API do Telegram ou da LLM estiver fora do ar, o job falha silenciosamente (com log) sem afetar nenhuma outra parte do app

**`TelegramBotService`**
- Orquestra o fluxo: identificar usuário → parsear mensagem → confirmar → registrar transação
- Encapsula toda a lógica do bot em um único service object
- Testável independentemente com doubles/stubs das APIs externas

**`LlmParserService`**
- Responsável exclusivamente por chamar a API do **Google Gemini Flash** e extrair os dados da transação
- Retorna um objeto com `amount`, `description`, `suggested_category` ou um erro estruturado
- Timeout configurado para evitar que uma chamada lenta bloqueie o job indefinidamente
- Gemini Flash foi escolhido pelo free tier generoso, qualidade excelente para extração de entidades financeiras em português e integração via gem `google-generative-ai`

**`TelegramAccount` (model)**
- Representa o vínculo entre um `User` do Caixa Fácil e um `chat_id` do Telegram
- Permite que o bot identifique qual usuário está enviando a mensagem

### Modo de desenvolvimento vs. produção

| Ambiente | Modo | Como funciona |
|----------|------|---------------|
| Desenvolvimento | Poller | A gem `telegram-bot` faz polling da API do Telegram sem necessidade de HTTPS ou domínio público |
| Produção | Webhook | O Telegram envia POSTs para `https://seudominio.com/telegram/webhook` — exige HTTPS |

### Gem escolhida

**`telegram-bot` (telegram-bot-rb)** — gem Ruby com integração nativa ao Rails, suporte a webhook e poller, helpers de rota, stubs para testes e suporte a ActiveJob para envio assíncrono. É a mais mantida e documentada do ecossistema Ruby para bots do Telegram.

---

## Consequências

- O `TelegramWebhooksController` retorna `200 OK` imediatamente para todo webhook recebido, independente do resultado do processamento
- Todo processamento de mensagem acontece em background via Active Job
- Exceções nas chamadas às APIs externas são capturadas, logadas e não relançadas
- O acesso ao bot requer que o usuário primeiro faça a vinculação no app web (gera um código de vinculação único)
- Em desenvolvimento, será usada a gem em modo poller — sem necessidade de ngrok ou HTTPS local
- Em produção, será necessário registrar o webhook no Telegram com a URL HTTPS do app
- O `LlmParserService` terá timeout de 10 segundos configurado — mensagens que excederem esse limite resultarão em resposta de erro amigável ao usuário

---

## Fontes
- GitHub — *telegram-bot-rb/telegram-bot: Ruby gem for building Telegram Bot with optional Rails integration* · https://github.com/telegram-bot-rb/telegram-bot
- Rubyroid Labs — *Creating Telegram Bot that Stores State: Full Guide* · https://rubyroidlabs.com/blog/2016/06/telegram-bot/
- Medium — *Telegram bot. Rails way.* · https://medium.com/@maxmelentiev/telegram-bot-rails-way-7e050d5dddbd
- Medium — *Deploying a Telegram Bot using ChatGPT and Whisper APIs with Railway* · https://medium.com/@andrea.faviait/deploying-a-telegram-bot-using-chatgpt-and-whisper-apis-with-railway-ef79e6cff955

---

← [ADR 002](./002-autenticacao.md) · [Voltar para Arquitetura](../overview.md) · [Voltar ao índice](../../README.md)
