# ADR 001 — Escolha do Banco de Dados

← [Voltar para Arquitetura](../overview.md) · [Próximo: ADR 002 →](./002-autenticacao.md) · [Voltar ao índice](../../README.md)

**Status:** Aceito
**Data:** Sprint 0

---

## Contexto

O Caixa Fácil é uma aplicação web multi-usuário que armazena transações financeiras, contas, categorias, orçamentos e alertas. O banco precisa suportar múltiplos usuários simultâneos com operações de escrita frequentes — especialmente o registro de transações, que é o fluxo mais crítico do produto. A aplicação será deployada em produção com URL pública, descartando soluções adequadas apenas para uso local ou embedded.

O Rails oferece suporte nativo a múltiplos bancos relacionais. As duas alternativas mais relevantes para este projeto são SQLite e PostgreSQL.

---

## Alternativas Consideradas

### SQLite
**Prós:**
- Configuração zero — não requer servidor separado
- Banco como arquivo único, fácil de versionar e fazer backup
- Padrão do Rails 8 para desenvolvimento local
- Muito rápido para leituras em single-user

**Contras:**
- Escritas concorrentes limitadas: mesmo com WAL mode, suporta apenas um escritor por vez — múltiplos usuários registrando transações simultaneamente podem gerar erros `SQLITE_BUSY`
- Não recomendado para aplicações multi-usuário em produção
- Tipagem dinâmica menos estrita pode mascarar bugs de tipo em desenvolvimento
- Sem controle de acesso nativo ao banco

### PostgreSQL
**Prós:**
- MVCC (Multi-Version Concurrency Control) nativo — múltiplos escritores concorrentes sem bloqueio entre si
- Tipo `DECIMAL` com precisão configurável — essencial para valores monetários sem erros de arredondamento de ponto flutuante
- Padrão da indústria para aplicações Rails em produção
- Suportado nativamente pelas principais plataformas de deploy (Render, Railway, Fly.io)
- Controle de acesso e autenticação por banco
- Escalável do MVP até versões futuras de maior volume

**Contras:**
- Requer instalação e configuração de servidor local em desenvolvimento
- Ligeiramente mais complexo de configurar que SQLite para iniciantes

---

## Decisão

**PostgreSQL.**

Três razões centrais justificam a escolha. Primeira: o Caixa Fácil é multi-usuário em produção — o modelo de escritas concorrentes do SQLite é inadequado para esse contexto. Segunda: valores monetários exigem precisão decimal garantida, eliminando riscos de arredondamento. Terceira: paridade entre desenvolvimento e produção é um princípio fundamental de engenharia — usar bancos diferentes nos dois ambientes é fonte conhecida de bugs sutis e difíceis de reproduzir.

O custo adicional de configurar PostgreSQL em desenvolvimento (instalação local ou via Docker) é pago uma única vez. Os benefícios são permanentes.

---

## Consequências

- Projeto iniciado com `rails new caixa_facil --database=postgresql`
- Todos os campos de valor monetário usarão `t.decimal :amount, precision: 10, scale: 2` nas migrations
- Ambiente de desenvolvimento requer PostgreSQL local ou via Docker
- A plataforma de deploy deve ter suporte nativo a PostgreSQL (Render, Railway ou Fly.io são candidatos — decisão registrada em ADR de deploy futuro)
- SQLite não será usado em nenhum ambiente do projeto

---

## Fontes
- Bluetick Consultants — *SQLite vs PostgreSQL in Rails 8* · https://bluetickconsultants.medium.com/sqlite-vs-postgresql-in-rails-8-6150b46cce5b
- DEV Community — *PostgreSQL vs SQLite: Dive into Two Very Different Databases* · https://dev.to/lovestaco/postgresql-vs-sqlite-dive-into-two-very-different-databases-5a90
- Boltic — *PostgreSQL vs SQLite: A Guide to Choosing the Right Database* · https://www.boltic.io/blog/postgresql-vs-sqlite
- Quora — *Is it bad practice to use SQLite for development and PostgreSQL for production?* · https://www.quora.com/Is-it-bad-practice-to-use-SQLite-for-development-and-PostgreeSQL-for-production-when-building-Rails-apps

---

← [Voltar para Arquitetura](../overview.md) · [Próximo: ADR 002 →](./002-autenticacao.md) · [Voltar ao índice](../../README.md)
