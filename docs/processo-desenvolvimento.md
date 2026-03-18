# Processo de Desenvolvimento — Portfólio de Engenharia de Software

## Motivação

A maioria dos portfólios de desenvolvedores mostra o produto final: um repositório no GitHub, um README com instruções de instalação e, quando bem feito, prints da interface. O que raramente aparece é o **raciocínio por trás das decisões** — por que esse produto foi escolhido, por que essa arquitetura, por que esse MVP e não outro.

Este projeto nasce com uma premissa diferente: **o processo é tão importante quanto o produto.**

A ideia é documentar o ciclo de vida completo de um software — da concepção ao deploy — de forma que qualquer pessoa que leia o repositório consiga entender não só *o que foi construído*, mas *como e por que cada decisão foi tomada*. Isso transforma um projeto técnico em evidência de maturidade de engenharia.

---

## Público-alvo deste documento

- Recrutadores técnicos avaliando capacidade de raciocínio de produto e arquitetura
- Engenheiros sêniores avaliando senioridade e processo
- O próprio autor, como registro de aprendizado e referência futura

---

## Fases do Ciclo de Vida

### Fase 1 — Descoberta e Concepção de Produto

**Objetivo:** Entender o problema antes de pensar em solução.

Antes de qualquer linha de código, é preciso responder: *qual dor estamos resolvendo, para quem, e por que vale a pena construir isso?*

Entregas desta fase:
- Definição do problema central
- Personas e usuários-alvo
- Hipóteses de valor (o que acreditamos ser verdade sobre o usuário)
- Análise de alternativas existentes no mercado
- Decisão justificada sobre o que construir

**Por que documentar isso:** Demonstra visão de produto e capacidade de questionar premissas antes de se comprometer com uma solução.

---

### Fase 2 — Definição do Produto

**Objetivo:** Transformar o problema em direção concreta.

Com o problema validado, esta fase define o escopo, as funcionalidades e os critérios de sucesso do produto.

Entregas desta fase:
- Jornada do usuário principal
- Funcionalidades mapeadas (com priorização MoSCoW ou similar)
- Métricas de sucesso do produto
- Documento de visão do produto (product brief)

**Por que documentar isso:** Mostra capacidade de traduzir necessidade de usuário em requisitos funcionais — uma habilidade cada vez mais valorizada em engenheiros.

---

### Fase 3 — Arquitetura e Decisões Técnicas

**Objetivo:** Tomar e registrar as decisões que serão difíceis de reverter depois.

Esta é uma das fases mais críticas do ciclo. Escolhas de banco de dados, estrutura da aplicação, autenticação, organização de código e estratégia de deploy têm custo alto de mudança. Por isso, cada decisão deve ser registrada com seu contexto, alternativas consideradas e justificativa.

Entregas desta fase:
- Diagrama de arquitetura da aplicação
- Modelagem de dados (ERD)
- Decisões técnicas documentadas (formato ADR — Architecture Decision Records)
- Estrutura de diretórios do projeto Rails
- Estratégia de testes
- Estratégia de deploy e infraestrutura

**Por que documentar isso:** ADRs são uma prática de engenharia madura usada em times de alto desempenho. Ter esse registro demonstra que você pensa além do código.

---

### Fase 4 — Definição do MVP

**Objetivo:** Delimitar o menor produto que valida a hipótese central.

MVP não é "versão incompleta". É a versão que responde à pergunta mais importante com o menor esforço possível. Esta fase define o que entra no MVP, o que fica para versões futuras e, principalmente, *por que*.

Entregas desta fase:
- Escopo do MVP com critérios de inclusão e exclusão
- User stories priorizadas
- Definição de "pronto" (Definition of Done)
- Roadmap de versões (v1.0, v1.1, v2.0...)

**Por que documentar isso:** Demonstra capacidade de priorização e entendimento de trade-offs — essencial tanto para engenheiros quanto para PMs.

---

### Fase 5 — Planejamento de Sprints

**Objetivo:** Transformar o backlog em trabalho executável e cadenciado.

Com o MVP definido, o trabalho é quebrado em sprints de uma a duas semanas. Cada sprint tem objetivo claro, histórias comprometidas e critérios de conclusão.

Entregas desta fase:
- Backlog refinado e estimado
- Planejamento da Sprint 1 (e subsequentes)
- Board de acompanhamento (Kanban ou Scrum)
- Registro de impedimentos e decisões tomadas durante a sprint

**Por que documentar isso:** Planejamento iterativo é o coração de times de software modernos. Documentar esse processo mostra organização e disciplina de execução.

---

### Fase 6 — Desenvolvimento Iterativo

**Objetivo:** Construir o produto com qualidade e rastreabilidade.

O desenvolvimento segue os princípios de código limpo, com commits semânticos, pull requests descritivos e testes automatizados. Cada funcionalidade entregue é registrada com seu contexto.

Práticas adotadas:
- Commits semânticos (Conventional Commits)
- Branches por feature/fix
- Code review documentado (mesmo que solo, via PR descriptions)
- Testes unitários e de integração
- Refatorações registradas como decisões técnicas

**Por que documentar isso:** A qualidade do histórico de commits e PRs é uma das primeiras coisas que engenheiros experientes olham em um portfólio.

---


## Stack e Contexto Técnico

| Componente | Tecnologia | Justificativa |
|---|---|---|
| Backend / Full-stack | Ruby on Rails | Framework maduro, opinionado e altamente produtivo para MVPs |
| Linguagem | Ruby | Elegante, expressiva e com ecossistema rico |
| Banco de dados | A definir na Fase 3 | Decisão documentada via ADR |
| Testes | RSpec (planejado) | Padrão da comunidade Rails |
| Deploy | A definir na Fase 3 | Decisão documentada via ADR |

---

## Estrutura de Documentação do Repositório

```
/docs
  /product
    - problem-statement.md
    - personas.md
    - product-brief.md
  /architecture
    - overview.md
    - erd.md
    /adr
      - 001-escolha-do-banco.md
      - 002-estrategia-autenticacao.md
      - ...
  /planning
    - mvp-scope.md
    - roadmap.md
    /sprints
      - sprint-01.md
      - sprint-02.md
      - ...
  /retrospectives
    - sprint-01-retro.md
    - final-retro.md
README.md
```

---

## Princípios que guiam este projeto

1. **Decisões têm contexto.** Toda escolha técnica ou de produto será documentada com as alternativas consideradas e a justificativa da decisão final.

2. **O MVP não é o mínimo viável de esforço — é o mínimo viável de aprendizado.** O objetivo é validar hipóteses, não apenas entregar features.

3. **Processo é produto.** A documentação do ciclo de vida é parte integrante do portfólio, não um apêndice.

4. **Honestidade intelectual.** Erros, mudanças de direção e débitos técnicos serão registrados. Um portfólio que documenta apenas sucessos não é confiável.

5. **Iteração deliberada.** Cada versão do produto existe por uma razão. Nada é adicionado por acidente.

---

*Este documento é vivo e será atualizado ao longo do projeto conforme as fases evoluírem.*
