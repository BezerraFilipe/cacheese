# Fase 3 — Arquitetura e Decisões Técnicas
### Caixa Fácil · Visão Geral

← [Anterior: Definição do Produto](../product/product-brief.md) · [Voltar ao índice](../README.md) · [Próximo: Modelagem de Dados →](./erd.md)

---

## Visão Geral da Aplicação

O Caixa Fácil é uma aplicação Rails full-stack no padrão MVC, com uma camada de service objects para lógica de negócio complexa e um módulo isolado para o bot do Telegram. A aplicação segue as convenções do Rails — "convention over configuration" — com desvios explicitamente documentados nos ADRs.

```
┌─────────────────────────────────────────────────┐
│                  CLIENTE                        │
│         Browser (web responsivo)                │
└────────────────────┬────────────────────────────┘
                     │ HTTP/HTTPS
┌────────────────────▼────────────────────────────┐
│              RAILS APPLICATION                  │
│                                                 │
│  ┌─────────────┐     ┌──────────────────────┐   │
│  │  Web Stack  │     │    Telegram Module   │   │
│  │             │     │    (isolado)         │   │
│  │ Controllers │     │                      │   │
│  │   Views     │     │ TelegramWebhooks     │   │
│  │  (Hotwire)  │     │ Controller           │   │
│  └──────┬──────┘     └──────────┬───────────┘   │
│         │                       │               │
│  ┌──────▼───────────────────────▼───────────┐   │
│  │           Service Objects                │   │
│  │  BudgetCalculatorService                 │   │
│  │  AlertGeneratorService                   │   │
│  │  TelegramBotService                      │   │
│  │  LlmParserService                        │   │
│  └──────────────────┬───────────────────────┘   │
│                     │                           │
│  ┌──────────────────▼───────────────────────┐   │
│  │              Models (ActiveRecord)        │   │
│  │  User · Session · Account · Transaction  │   │
│  │  Category · Budget · Alert               │   │
│  │  TelegramAccount                         │   │
│  └──────────────────┬───────────────────────┘   │
│                     │                           │
│  ┌──────────────────▼───────────────────────┐   │
│  │           Active Job (Background)         │   │
│  │  TelegramBotJob · AlertMailerJob          │   │
│  └──────────────────────────────────────────┘   │
└─────────────────────────────────────────────────┘
          │                        │
┌─────────▼──────┐      ┌──────────▼────────────┐
│  PostgreSQL    │      │   APIs Externas        │
│  (produção)    │      │   Telegram Bot API     │
│                │      │   OpenAI API (LLM)     │
└────────────────┘      └───────────────────────┘
```

---

## Decisões Arquiteturais (ADRs)

| # | Decisão | Status | Link |
|---|---------|--------|------|
| 001 | Escolha do banco de dados → **PostgreSQL** | ✅ Aceito | [Ver ADR](./adr/001-banco-de-dados.md) |
| 002 | Estratégia de autenticação → **Rails 8 Generator** | ✅ Aceito | [Ver ADR](./adr/002-autenticacao.md) |
| 003 | Integração do bot do Telegram → **Módulo isolado** | ✅ Aceito | [Ver ADR](./adr/003-telegram-bot.md) |
| 004 | Plataforma de deploy → **Render** | ✅ Aceito | [Ver ADR](./adr/004-deploy.md) |

---

## Stack Definida

| Componente | Tecnologia | Justificativa |
|---|---|---|
| Framework | Ruby on Rails 8 | Convention over configuration, produtividade, ecossistema maduro |
| Banco de dados | PostgreSQL | Multi-usuário, precisão decimal, padrão de produção — [ADR 001](./adr/001-banco-de-dados.md) |
| Autenticação | Rails 8 Auth Generator | Código transparente, aprendizado, sem dependência externa — [ADR 002](./adr/002-autenticacao.md) |
| Frontend | Hotwire (Turbo + Stimulus) | Nativo do Rails 8, evita SPA desnecessária, reatividade com HTML |
| CSS | Tailwind CSS | Utility-first, sem build complexo com importmap |
| Testes | RSpec + FactoryBot + Faker | Padrão da comunidade Rails |
| Cobertura | SimpleCov | Relatório de cobertura integrado ao RSpec |
| Lint | RuboCop | Qualidade e consistência de código |
| Segurança | Brakeman | Análise estática de vulnerabilidades |
| Background Jobs | Active Job + Solid Queue | Nativo do Rails 8, sem dependência de Redis para o MVP |
| Email | Action Mailer + Mailpit (dev) | Nativo do Rails, Mailpit para captura local |
| Bot Telegram | gem `telegram-bot` (telegram-bot-rb) | Integração Rails nativa, suporte a webhook e poller — [ADR 003](./adr/003-telegram-bot.md) |
| LLM Parser | Google Gemini Flash | Free tier, qualidade para extração em português — [ADR 003](./adr/003-telegram-bot.md) |
| CI | GitHub Actions | Integrado ao repositório, gratuito para projetos públicos |
| Deploy | A definir (Render ou Fly.io) | Ambos suportam PostgreSQL e HTTPS nativo |

---

## Estrutura de Diretórios do Projeto Rails

```
caixa_facil/
├── app/
│   ├── controllers/
│   │   ├── application_controller.rb
│   │   ├── dashboard_controller.rb
│   │   ├── accounts_controller.rb
│   │   ├── transactions_controller.rb
│   │   ├── categories_controller.rb
│   │   ├── budgets_controller.rb
│   │   ├── alerts_controller.rb
│   │   ├── sessions_controller.rb       ← gerado pelo auth generator
│   │   ├── passwords_controller.rb      ← gerado pelo auth generator
│   │   └── telegram_webhooks_controller.rb
│   ├── models/
│   │   ├── user.rb
│   │   ├── session.rb                   ← gerado pelo auth generator
│   │   ├── account.rb
│   │   ├── transaction.rb
│   │   ├── category.rb
│   │   ├── budget.rb
│   │   ├── alert.rb
│   │   └── telegram_account.rb
│   ├── services/
│   │   ├── budget_calculator_service.rb
│   │   ├── alert_generator_service.rb
│   │   ├── telegram_bot_service.rb
│   │   └── llm_parser_service.rb
│   ├── jobs/
│   │   ├── telegram_bot_job.rb
│   │   └── alert_mailer_job.rb
│   ├── mailers/
│   │   └── alert_mailer.rb
│   └── views/
│       ├── dashboard/
│       ├── accounts/
│       ├── transactions/
│       ├── categories/
│       ├── budgets/
│       └── mailers/
│           └── alert_mailer/
├── spec/
│   ├── models/
│   ├── controllers/
│   ├── services/
│   ├── mailers/
│   ├── requests/
│   └── factories/
├── docs/                                ← documentação do projeto
└── config/
    ├── routes.rb
    └── environments/
```

---

## Modelagem de Dados

→ [Ver ERD completo](./erd.md)

---

## Estratégia de Testes

A cobertura de testes segue uma pirâmide com três camadas:

**Models (base da pirâmide — maior cobertura)**
Validações, associações, callbacks e métodos de instância. Todo comportamento de negócio encapsulado no model é testado unitariamente.

**Services (camada crítica)**
Os service objects (`BudgetCalculatorService`, `AlertGeneratorService`, `LlmParserService`) têm testes unitários com doubles/stubs das dependências externas. São os componentes com lógica mais complexa.

**Request Specs (topo — fluxos integrados)**
Testes de request spec cobrindo os fluxos CRUD principais e os cenários críticos de cada módulo. Testam o comportamento end-to-end da requisição HTTP até a resposta.

Meta de cobertura: **≥ 70%** nas models e controllers — conforme Definition of Done do MVP.

---

← [Anterior: Definição do Produto](../product/product-brief.md) · [Voltar ao índice](../README.md) · [Próximo: Modelagem de Dados →](./erd.md)
