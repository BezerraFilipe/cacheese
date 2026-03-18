← [Sprint 03](./sprint-03.md) · [Voltar ao Planejamento](../mvp-scope.md) · [Voltar ao índice](../../README.md)

# Sprint 4 — Bot do Telegram, Deploy e Definition of Done

**[S4-01] Vincular conta do Telegram ao usuário** · Tamanho: M

*Como usuário, quero vincular minha conta do Telegram ao Cacheese, para que eu possa registrar transações pelo bot.*

- **Dado** que acesso as configurações, **quando** clico em "Conectar Telegram", **então** recebo um código de vinculação único com instruções de uso
- **Dado** que envio o código correto para o bot, **quando** ele processa, **então** minha conta é vinculada e recebo confirmação
- **Dado** que minha conta já está vinculada, **quando** acesso as configurações, **então** vejo que está conectada e tenho opção de desvincular

---

**[S4-02] Registrar transação por texto em linguagem natural** · Tamanho: GG

*Como usuário, quero enviar uma mensagem para o bot e ter a transação registrada após confirmar os dados, para que eu possa lançar gastos sem abrir o app.*

- **Dado** que minha conta está vinculada, **quando** envio "gastei 35 reais no almoço", **então** o bot responde com os dados interpretados (valor, categoria sugerida, descrição) e pergunta se confirmo
- **Dado** que confirmo os dados, **quando** respondo "sim", **então** a transação é registrada e o bot confirma com o novo saldo
- **Dado** que os dados estão incorretos, **quando** corrijo um campo, **então** o bot atualiza e pede nova confirmação
- **Dado** que o bot está indisponível, **quando** uso o app web, **então** ele funciona normalmente sem nenhuma degradação
- **Dado** que envio uma mensagem que o bot não consegue interpretar, **quando** a LLM não extrai dados financeiros válidos, **então** o bot responde com mensagem de ajuda e exemplos de comandos válidos

---

**[S4-03] Registrar transação por comando de voz** · Tamanho: M

*Como usuário, quero enviar um áudio para o bot e ter a transação interpretada e registrada, para que eu possa lançar gastos sem digitar.*

- **Dado** que envio um áudio dizendo "gastei cinquenta reais no supermercado", **quando** o Telegram transcreve e o bot processa, **então** o fluxo é idêntico ao de mensagem de texto
- **Dado** que o áudio é inaudível, **quando** o bot não consegue transcrever, **então** ele responde pedindo que o usuário repita ou use texto

---

**[S4-04] Deploy em produção** · Tamanho: G

*Como desenvolvedor, quero a aplicação deployada em produção com URL pública, para que o MVP seja considerado completo e utilizável.*

- **Dado** que o deploy é concluído, **quando** acesso a URL pública, **então** a aplicação carrega com HTTPS
- **Dado** que a aplicação está em produção, **quando** registro uma transação, **então** os dados são persistidos corretamente
- **Dado** que o bot está configurado em produção, **quando** envio uma mensagem, **então** o webhook aponta para a URL de produção e a resposta chega corretamente
- **Dado** que monitoro o uptime por 48 horas após o deploy, **então** a disponibilidade é ≥ 99%

---

**[S4-05] Verificação final do Definition of Done do MVP** · Tamanho: M

Checklist de encerramento — todos os itens devem estar marcados antes de considerar o MVP concluído:

- [ ] Fluxo completo (cadastro → conta → transação → dashboard) executável em menos de 3 minutos
- [ ] Alertas visuais de orçamento funcionando para 80% e 100%
- [ ] Email de alerta enviado e recebido corretamente
- [ ] Bot do Telegram interpreta linguagem natural e registra transação após confirmação
- [ ] App web funciona normalmente com bot indisponível
- [ ] URL de produção pública com HTTPS funcionando
- [ ] Cobertura de testes ≥ 70% nas models e controllers críticos
- [ ] Pipeline de CI verde no estado final
- [ ] Zero vulnerabilidades críticas no relatório do Brakeman
- [ ] Todos os commits seguem Conventional Commits
- [ ] Documentação `/docs` atualizada e navegável

### Riscos identificados
- Integração com API de LLM pode ter latência variável — implementar timeout e fallback com mensagem amigável ao usuário
- Webhook do Telegram em produção requer HTTPS — garantir certificado SSL no deploy (Let's Encrypt ou plataforma gerenciada)
- Deploy é a etapa com mais variáveis desconhecidas para um desenvolvedor iniciante em Rails — reservar tempo generoso para troubleshooting de configurações de ambiente

---
← [Sprint 03](./sprint-03.md) · [Voltar ao Planejamento](../mvp-scope.md) · [Voltar ao índice](../../README.md)
