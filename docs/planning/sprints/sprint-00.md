← [Voltar ao Planejamento](../mvp-scope.md) · [Voltar ao índice](../../README.md) · [Sprint 01 →](./sprint-01.md)


# Sprint 00 — Fundação Técnica

**Duração:** 1 semana · **Tipo:** Preparação — sem entrega de funcionalidade ao usuário

### Objetivo
Ao final da Sprint 0, o projeto deve ter: 
- Ambiente de desenvolvimento funcionando
- Repositório estruturado com a pasta `/docs` 
- Decisões arquiteturais registradas em ADRs
- Banco de dados configurado
- Projeto Rails inicializado com a stack definida 
- Backlog das próximas sprints refinado e estimado. 

---

**[S0-01] Inicializar repositório e estrutura de documentação** · Tamanho: P
- Criar repositório GitHub com branch `main` protegida
- Criar estrutura `/docs` 
- Configurar `.gitignore`, `README.md` raiz e licença
- Configurar Conventional Commits e template de mensagem de commit

**[S0-02] Tomar e documentar decisões arquiteturais (ADRs)** · Tamanho: M
- ADR 001: Escolha do banco de dados 
- ADR 002: Estratégia de autenticação 
- ADR 003: Estratégia de isolamento do bot do Telegram

**[S0-03] Inicializar projeto Rails** · Tamanho: M
- Criar aplicação Rails com as flags corretas 
- Instalar e configurar RSpec, FactoryBot e Faker
- Configurar variáveis de ambiente com `.env` e `dotenv-rails`
- Verificar que `rails server` sobe sem erros em desenvolvimento

**[S0-04] Configurar banco de dados e ferramentas de qualidade** · Tamanho: P
- Criar bancos de dados de desenvolvimento e teste
- Instalar e configurar RuboCop com regras do projeto
- Configurar SimpleCov para relatório de cobertura de testes
- Instalar Brakeman para auditoria de segurança

**[S0-05] Configurar pipeline de CI** · Tamanho: M
- Configurar GitHub Actions para rodar testes e RuboCop a cada push
- Verificar que o pipeline passa no estado inicial do projeto

**[S0-06] Refinar backlog das Sprints 1 a 4** · Tamanho: M
- Detalhar e estimar todas as histórias das próximas sprints
- Revisar critérios de aceitação com base nas decisões dos ADRs
- Confirmar sequência de dependências entre histórias

### Critério de saída da Sprint 0
A Sprint 0 está concluída quando: `rails server` sobe sem erros, o pipeline de CI está verde, os três ADRs estão escritos e o backlog das Sprints 1–4 está refinado e estimado.

---

← [Voltar ao Planejamento](../mvp-scope.md) · [Voltar ao índice](../../README.md) · [Sprint 01 →](./sprint-01.md)
