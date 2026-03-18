# Modelagem de Dados — ERD
### Caixa Fácil · Diagrama Entidade-Relacionamento

← [Anterior: Visão Geral da Arquitetura](./overview.md) · [Voltar ao índice](../README.md)

---

## Diagrama de Relacionamentos

```
┌──────────────┐        ┌──────────────────┐
│     users    │        │     sessions     │
├──────────────┤        ├──────────────────┤
│ id           │◄───────│ id               │
│ name         │  1:N   │ user_id (FK)     │
│ email_address│        │ ip_address       │
│ password_    │        │ user_agent       │
│  digest      │        │ created_at       │
│ created_at   │        └──────────────────┘
│ updated_at   │
└──────┬───────┘        ┌──────────────────────┐
       │                │   telegram_accounts  │
       │ 1:1            ├──────────────────────┤
       │                │ id                   │
       └───────────────►│ user_id (FK)         │
       │                │ chat_id              │
       │                │ username             │
       │                │ linked_at            │
       │                └──────────────────────┘
       │
       │ 1:N            ┌──────────────┐
       ├───────────────►│   accounts   │
       │                ├──────────────┤
       │                │ id           │
       │                │ user_id (FK) │
       │                │ name         │
       │                │ account_type │
       │                │ balance      │
       │                │ active       │
       │                │ created_at   │
       │                │ updated_at   │
       │                └──────┬───────┘
       │                       │ 1:N
       │                       ▼
       │ 1:N            ┌──────────────────┐
       ├───────────────►│  transactions    │
       │                ├──────────────────┤
       │                │ id               │
       │                │ user_id (FK)     │
       │                │ account_id (FK)  │
       │                │ category_id (FK) │
       │                │ amount           │
       │                │ transaction_type │
       │                │ description      │
       │                │ date             │
       │                │ created_at       │
       │                │ updated_at       │
       │                └──────────────────┘
       │
       │ 1:N            ┌──────────────┐
       ├───────────────►│  categories  │
       │                ├──────────────┤
       │                │ id           │
       │                │ user_id (FK) │ ← NULL = categoria padrão
       │                │ name         │
       │                │ color        │
       │                │ icon         │
       │                │ default      │
       │                │ created_at   │
       │                │ updated_at   │
       │                └──────┬───────┘
       │                       │ 1:N
       │                       ▼
       │ 1:N            ┌──────────────┐
       ├───────────────►│   budgets    │
       │                ├──────────────┤
       │                │ id           │
       │                │ user_id (FK) │
       │                │ category_id  │
       │                │  (FK)        │
       │                │ amount_limit │
       │                │ month        │ ← DATE (primeiro dia do mês)
       │                │ created_at   │
       │                │ updated_at   │
       │                └──────┬───────┘
       │                       │ 1:N
       │                       ▼
       │ 1:N            ┌──────────────┐
       └───────────────►│   alerts     │
                        ├──────────────┤
                        │ id           │
                        │ user_id (FK) │
                        │ budget_id    │
                        │  (FK)        │
                        │ alert_type   │ ← 'warning_80' | 'exceeded_100'
                        │ triggered_at │
                        │ email_sent   │
                        │ created_at   │
                        └──────────────┘
```

---

## Descrição das Entidades

### `users`
Usuário da aplicação. Criado pelo Rails 8 Auth Generator com adaptações.

| Coluna | Tipo | Descrição |
|--------|------|-----------|
| `id` | bigint | Chave primária |
| `name` | string | Nome de exibição |
| `email_address` | string | Email único (normalizado em lowercase) |
| `password_digest` | string | Hash BCrypt da senha (via `has_secure_password`) |
| `created_at` | datetime | — |
| `updated_at` | datetime | — |

Índice único em `email_address`.

---

### `sessions`
Rastreia sessões ativas por usuário. Gerado pelo Rails 8 Auth Generator.

| Coluna | Tipo | Descrição |
|--------|------|-----------|
| `id` | bigint | Chave primária |
| `user_id` | bigint (FK) | Referência ao usuário |
| `ip_address` | string | IP da sessão |
| `user_agent` | string | Browser/dispositivo |
| `created_at` | datetime | Início da sessão |

---

### `telegram_accounts`
Vínculo entre um `User` do Caixa Fácil e uma conta do Telegram.

| Coluna | Tipo | Descrição |
|--------|------|-----------|
| `id` | bigint | Chave primária |
| `user_id` | bigint (FK) | Referência ao usuário |
| `chat_id` | string | ID único do chat no Telegram |
| `username` | string | Username do Telegram (opcional) |
| `linked_at` | datetime | Data de vinculação |

Índice único em `chat_id`. Índice único em `user_id` (relação 1:1 com `users`).

---

### `accounts`
Representa uma conta financeira do usuário (corrente, poupança, cartão, carteira).

| Coluna | Tipo | Descrição |
|--------|------|-----------|
| `id` | bigint | Chave primária |
| `user_id` | bigint (FK) | Dono da conta |
| `name` | string | Nome da conta (ex: "Nubank", "Carteira") |
| `account_type` | string | Enum: `checking`, `savings`, `credit_card`, `wallet` |
| `balance` | decimal(10,2) | Saldo atual calculado |
| `active` | boolean | Soft delete — contas inativas são preservadas |
| `created_at` | datetime | — |
| `updated_at` | datetime | — |

> **Nota:** O campo `balance` é denormalizado intencionalmente para performance do dashboard. É atualizado a cada criação, edição ou exclusão de transação via callback no model `Transaction`.

---

### `categories`
Categorias de transação. Pode ser padrão do sistema (user_id NULL) ou personalizada pelo usuário.

| Coluna | Tipo | Descrição |
|--------|------|-----------|
| `id` | bigint | Chave primária |
| `user_id` | bigint (FK, nullable) | NULL = categoria padrão do sistema |
| `name` | string | Nome da categoria |
| `color` | string | Cor em hex (ex: `#FF5733`) |
| `icon` | string | Nome do ícone (ex: `shopping-cart`) |
| `default` | boolean | Indica se é categoria padrão |
| `created_at` | datetime | — |
| `updated_at` | datetime | — |

As categorias padrão são criadas via seed: alimentação, transporte, moradia, saúde, lazer, educação, salário, outros.

---

### `transactions`
Registro de uma receita ou despesa. Entidade central da aplicação.

| Coluna | Tipo | Descrição |
|--------|------|-----------|
| `id` | bigint | Chave primária |
| `user_id` | bigint (FK) | Dono da transação |
| `account_id` | bigint (FK) | Conta vinculada |
| `category_id` | bigint (FK) | Categoria da transação |
| `amount` | decimal(10,2) | Valor absoluto (sempre positivo) |
| `transaction_type` | string | Enum: `income`, `expense` |
| `description` | string | Descrição livre |
| `date` | date | Data da transação (não datetime) |
| `created_at` | datetime | Data de registro no sistema |
| `updated_at` | datetime | — |

Índice composto em `[user_id, date]` para filtros por período no histórico.

---

### `budgets`
Limite mensal de gasto definido pelo usuário para uma categoria.

| Coluna | Tipo | Descrição |
|--------|------|-----------|
| `id` | bigint | Chave primária |
| `user_id` | bigint (FK) | Dono do orçamento |
| `category_id` | bigint (FK) | Categoria monitorada |
| `amount_limit` | decimal(10,2) | Limite mensal definido |
| `month` | date | Primeiro dia do mês de referência (ex: `2025-03-01`) |
| `created_at` | datetime | — |
| `updated_at` | datetime | — |

Índice único em `[user_id, category_id, month]` — impede orçamentos duplicados para a mesma categoria no mesmo mês.

---

### `alerts`
Alerta gerado quando um orçamento atinge 80% ou 100% do limite.

| Coluna | Tipo | Descrição |
|--------|------|-----------|
| `id` | bigint | Chave primária |
| `user_id` | bigint (FK) | Usuário notificado |
| `budget_id` | bigint (FK) | Orçamento que disparou o alerta |
| `alert_type` | string | Enum: `warning_80`, `exceeded_100` |
| `triggered_at` | datetime | Momento em que o alerta foi gerado |
| `email_sent` | boolean | Controle de deduplicação de emails |
| `created_at` | datetime | — |

Índice único em `[budget_id, alert_type]` — garante no máximo um alerta de cada tipo por orçamento. Esta é a chave da lógica de deduplicação: o `AlertGeneratorService` usa `find_or_create_by` nesse índice.

---

## Resumo dos Relacionamentos

| Relacionamento | Cardinalidade |
|---|---|
| User → Sessions | 1:N |
| User → TelegramAccount | 1:1 |
| User → Accounts | 1:N |
| User → Transactions | 1:N |
| User → Categories (personalizadas) | 1:N |
| User → Budgets | 1:N |
| User → Alerts | 1:N |
| Account → Transactions | 1:N |
| Category → Transactions | 1:N |
| Category → Budgets | 1:N |
| Budget → Alerts | 1:N |

---

← [Anterior: Visão Geral da Arquitetura](./overview.md) · [Voltar ao índice](../README.md)
