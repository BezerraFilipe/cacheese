# ADR 004 — Plataforma de Deploy

← [ADR 003](./003-telegram-bot.md) · [Voltar para Arquitetura](../overview.md) · [Voltar ao índice](../../README.md)

**Status:** Aceito
**Data:** Sprint 0

---

## Contexto

O Cacheese precisa de uma plataforma de deploy que suporte: aplicação Rails com PostgreSQL, HTTPS automático (obrigatório para o webhook do Telegram), variáveis de ambiente gerenciadas com segurança e um fluxo de deploy simples o suficiente para um desenvolvedor iniciante em Rails. A plataforma será usada desde o primeiro deploy do MVP até as versões futuras do produto.

Três plataformas foram avaliadas: Render, Railway e Fly.io.

---

## Alternativas Consideradas

### Render
Plataforma de cloud com foco em simplicidade de deploy para aplicações web.

**Prós:**
- Detecta projetos Rails automaticamente ao conectar o repositório GitHub — zero configuração de build na maioria dos casos
- PostgreSQL gerenciado disponível no plano gratuito
- HTTPS automático com certificado Let's Encrypt provisionado sem configuração
- Interface clara para gerenciar variáveis de ambiente
- Deploy automático a cada push na branch `main`
- Suporte nativo a webhooks (URL pública fixa desde o primeiro deploy)
- Documentação oficial de Rails bem mantida

**Contras:**
- No plano gratuito, o serviço "hiberna" após 15 minutos de inatividade — o primeiro request após inatividade pode demorar até 30 segundos para "acordar"
- Recursos de CPU e memória limitados no plano gratuito

### Railway
Plataforma similar ao Render, muito popular na comunidade Rails.

**Prós:**
- Interface moderna e intuitiva
- PostgreSQL gerenciado incluso
- Deploy simples via GitHub
- Sem hibernação no plano gratuito (créditos mensais)

**Contras:**
- Modelo de precificação baseado em créditos mensais pode ser menos previsível que um plano fixo gratuito
- Plano gratuito limitado a US$ 5 de créditos/mês — dependendo do uso, pode esgotar

### Fly.io
Plataforma baseada em containers com presença global de regiões.

**Prós:**
- Alta performance e flexibilidade
- Sem hibernação mesmo no plano gratuito
- Ideal para aplicações que precisam de baixa latência global

**Contras:**
- Requer criação de `Dockerfile` — configuração significativamente mais complexa para iniciantes
- CLI própria com curva de aprendizado maior
- PostgreSQL não é gerenciado da mesma forma simples que Render/Railway

---

## Decisão

**Render.**

Para um desenvolvedor iniciante em Rails em seu primeiro deploy em produção, eliminar variáveis desconhecidas é mais valioso do que otimizar performance. O Render oferece o fluxo de deploy mais direto do mercado para aplicações Rails: conecta o GitHub, detecta o projeto, provisiona o banco e configura HTTPS — sem Dockerfile, sem CLI adicional, sem configuração manual de certificados.

A hibernação do plano gratuito é um trade-off aceitável para o MVP: o Cacheese é um projeto de portfólio, não um produto com SLA de disponibilidade. Quando o projeto evoluir para versões com usuários reais, a migração para um plano pago no próprio Render ou para outra plataforma é trivial.

O suporte a webhooks com URL pública fixa desde o primeiro deploy é especialmente importante — é o que permite registrar o webhook do bot do Telegram na Sprint 4 sem workarounds.

---

## Consequências

- O deploy em produção será feito no Render via integração com o repositório GitHub
- O banco de dados de produção será o PostgreSQL gerenciado pelo Render (plano gratuito)
- HTTPS estará disponível automaticamente — a URL de produção terá formato `https://cacheese.onrender.com` ou domínio customizado
- O webhook do Telegram será registrado apontando para a URL de produção do Render
- Variáveis de ambiente de produção (chaves de API, credenciais do banco) serão configuradas no painel do Render — nunca commitadas no repositório
- O arquivo `config/database.yml` será configurado para ler a variável `DATABASE_URL` em produção, que o Render provisiona automaticamente
- Um arquivo `render.yaml` será criado na raiz do projeto na Sprint 4 para declarar a infraestrutura como código (Infrastructure as Code)

---

## Fontes
- Render Docs — *Deploy a Rails App* · https://render.com/docs/deploy-rails
- Render Docs — *PostgreSQL on Render* · https://render.com/docs/databases
- Bootrails — *How to deploy Rails app on Render.com* · https://www.bootrails.com/blog/how-to-deploy-rails-app-on-render/
- Railway Docs — *Deploy a Rails app* · https://docs.railway.app/getting-started

---

← [ADR 003](./003-telegram-bot.md) · [Voltar para Arquitetura](../overview.md) · [Voltar ao índice](../../README.md)
