# Cacheese 🧀

> Gestão financeira pessoal com o menor atrito possível.

Cacheese é um projeto de portfólio desenvolvido em Ruby on Rails que documenta o **ciclo de vida completo de um software**, da concepção ao deploy. 

O objetivo aqui é demonstrar entendimento e exercitar diferentes processos da engenharia de software, ao passo que aprendo um novo framework (Ruby On Rails) e resolvo um problema coletivo: Organização financeira facilitada.

Esse processo foi muito inspirado no livro [Engenharia de Software Moderna - Marco Tulio Valente](https://engsoftmoderna.info/cap0.html) e na cadeira de Desenvolvimento de Software que paguei no Centro de Informática da UFPE.

## Stack

- **Backend:** Ruby on Rails 8
- **Banco de dados:** PostgreSQL
- **Autenticação:** Rails 8 Auth Generator
- **Testes:** RSpec + FactoryBot
- **Bot:** Telegram + OpenAI API

## Documentação do processo

Todo o ciclo de desenvolvimento está documentado em `/docs`:

- [Processo de desenvolvimento](./docs/processo-desenvolvimento.md)
- [Fase 1 — Empatize e Defina](./docs/product/problem-statement.md)
- [Fase 2 — Definição do Produto](./docs/product/product-brief.md)
- [Fase 3 — Arquitetura](./docs/architecture/overview.md)
- [Planejamento de Sprints](./docs/planning/mvp-scope.md)

## Status do projeto

🚧 Em desenvolvimento — [Sprint 00 — Fundação Técnica](./docs/planning/sprints/sprint-00.md)

( ✓ ) [S0-01] Inicializar repositório e estrutura de documentação

( ) [S0-02] Tomar e documentar decisões arquiteturais (ADRs)

( ) [S0-03] Inicializar projeto Rails

( ) [S0-04] Configurar banco de dados e ferramentas de qualidade

( ) [S0-05] Configurar pipeline de CI

( ) [S0-06] Refinar backlog das Sprints 1 a 4

---

## Sobre o uso de IA:

Nesse projeto, desde a etapa de concepção ao deploy foram usados alguns modelos de LLMs para seu desenvolvimento. <br>

Na etapa de concepção, a IA foi usada principalmente para as etapas de pesquisa de mercado e coleta de dados na internet para entender o problema. Além disso, ainda nessa fase a IA contribuiu com a geração e seleção das ideias, além do planejamento das sprints.

Já na etapa de desenvolvimento (aqui estou abrangendo decisões arquiteturais e desenvolvimento), tal ferramenta serviu como um "sênior amigo", um lugar de consulta para destravar eventuais bloqueios no processo de aprendizagem do RoR.
