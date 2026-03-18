# Planejamento de Sprints — Caixa Fácil
### MVP · Sprint 0 a Sprint 4

← [Anterior: Definição do Produto](../product/product-brief.md) · [Voltar ao índice](../README.md) · [Ver Sprints →](./sprints/)

---

## Visão Geral

O MVP do Caixa Fácil será desenvolvido em **5 sprints**, totalizando **9 semanas de trabalho**. A Sprint 0, com duração de uma semana, serve como fase de preparação rápida do planejamento e da arquitetura. As Sprints 1 a 4, com duas semanas cada, cobrem o desenvolvimento iterativo dos 8 módulos definidos na [Fase 2](../product/definicao-do-produto.md).

Ter uma sprint 0 foi uma escolha de planejamento para possibilitar que a sprint 1 represente o início com força total do projeto. Nela estou redigindo esses vários markdowns em /docs que vão servir de guia durante o processo de desenvolvimento e de entendimento do produto.


| Sprint | Duração | Período | Objetivo central |
|--------|---------|---------|-----------------|
| Sprint 0 | 1 semana | Semana 1 | Fundação técnica e arquitetural |
| Sprint 1 | 2 semanas | Semanas 2–3 | Autenticação, contas e transações |
| Sprint 2 | 2 semanas | Semanas 4–5 | Categorias, dashboard e orçamento |
| Sprint 3 | 2 semanas | Semanas 6–7 | Alertas, email e qualidade |
| Sprint 4 | 2 semanas | Semanas 8–9 | Bot do Telegram, deploy e DoD |

---

## Convenções deste documento

**Formato de User Story:** `Como [persona], quero [ação], para que [benefício].`

**Formato de Critério de Aceitação (Given/When/Then):**
> **Dado** que [estado inicial do sistema] · **Quando** [ação executada] · **Então** [resultado esperado]

**Estimativas (T-shirt sizing):**
- **P** — até meio dia de trabalho
- **M** — 1 dia
- **G** — 2 a 3 dias
- **GG** — 4 dias ou mais

**Definition of Done global:** Uma história está concluída quando o código está commitado com mensagem semântica, os critérios de aceitação foram verificados manualmente, os testes automatizados relevantes foram escritos e passam, e não há warnings ou erros no console.

---

## Sprint 0 — Fundação Técnica
**Duração:** 1 semana · **Tipo:** Preparação — sem entrega de funcionalidade ao usuário

### Objetivo
Ao final da Sprint 0, o projeto deve ter: 
- Ambiente de desenvolvimento funcionando
- Repositório estruturado com a pasta `/docs` 
- Decisões arquiteturais registradas em ADRs
- Banco de dados configurado
- Projeto Rails inicializado com a stack definida 
- Backlog das próximas sprints refinado e estimado. 

Para mais informações acesse [sprint-00.md](./sprints/sprint-00.md)

---


## Sprint 1 — Autenticação, Contas e Transações
**Duração:** 2 semanas · **Módulos:** 1 (Autenticação), 2 (Contas Financeiras), 3 (Transações)

### Objetivo
Ao final da Sprint 1, um usuário deve:
- Conseguir criar uma conta
- Fazer login
- Cadastrar suas contas financeiras 
- Registrar sua primeira transação 

Definição das histórias / features: [sprint-01.md](./sprints/sprint-01.md)

---

## Sprint 2 — Categorias, Dashboard e Orçamento
**Duração:** 2 semanas · **Módulos:** 4 (Categorias), 5 (Dashboard), 6 (Orçamento)

### Objetivo
Ao final da Sprint 2, o usuário deve: 
- conseguir visualizar sua situação financeira completa no dashboard 
- Definir limites de orçamento por categoria

Para mais informações acesse [sprint-02.md](./sprints/sprint-02.md)


---

## Sprint 3 — Alertas, Email e Qualidade
**Duração:** 2 semanas · **Módulos:** 6 (Alertas), 7 (Email), Testes

### Objetivo
Ao final da Sprint 3, o sistema:
- Gera e envia alertas automaticamente quando limites de orçamento são atingidos, com notificação por email
- Tem uma cobertura de teste de 70%. 

É também a sprint dedicada a refatorar débitos técnicos acumulados nas sprints anteriores.

Para mais informações acesse [sprint-03.md](./sprints/sprint-03.md)


---

## Sprint 4 — Bot do Telegram, Deploy e Definition of Done
**Duração:** 2 semanas · **Módulo:** 8 (Telegram), Infraestrutura

### Objetivo
Sprint final do MVP. Ao final da Sprint 4: 
- O bot do Telegram estará operacional como canal alternativo de registro
- A aplicação estará deployada em produção com URL pública
- Todos os critérios do Definition of Done do MVP terão sido verificados e marcados


Para mais informações acesse [sprint-04.md](./sprints/sprint-04.md)

---

## Backlog consolidado

| ID | História | Sprint | Tamanho | Módulo |
|----|----------|--------|---------|--------|
| S0-01 | Repositório e estrutura de docs | 0 | P | Infra |
| S0-02 | ADRs arquiteturais | 0 | M | Arquitetura |
| S0-03 | Inicializar projeto Rails | 0 | M | Infra |
| S0-04 | Banco de dados e ferramentas de qualidade | 0 | P | Infra |
| S0-05 | Configurar CI | 0 | M | Infra |
| S0-06 | Refinar backlog | 0 | M | Planejamento |
| S1-01 | Cadastro de usuário | 1 | M | Autenticação |
| S1-02 | Login e logout | 1 | P | Autenticação |
| S1-03 | Criar e gerenciar contas financeiras | 1 | M | Contas |
| S1-04 | Registrar transação | 1 | G | Transações |
| S1-05 | Listar e filtrar transações | 1 | M | Transações |
| S2-01 | Gerenciar categorias | 2 | M | Categorias |
| S2-02 | Dashboard principal | 2 | G | Dashboard |
| S2-03 | Definir orçamento por categoria | 2 | M | Orçamento |
| S2-04 | Indicadores visuais de orçamento | 2 | M | Orçamento |
| S3-01 | Alerta ao atingir 80% | 3 | M | Alertas |
| S3-02 | Alerta ao atingir 100% | 3 | M | Alertas |
| S3-03 | Notificação por email | 3 | G | Email |
| S3-04 | Cobertura de testes | 3 | GG | Qualidade |
| S4-01 | Vincular conta do Telegram | 4 | M | Telegram |
| S4-02 | Registrar transação por texto | 4 | GG | Telegram |
| S4-03 | Registrar transação por voz | 4 | M | Telegram |
| S4-04 | Deploy em produção | 4 | G | Infra |
| S4-05 | Verificação do DoD final | 4 | M | Qualidade |

---

## Fontes

- BMC Software — *Sprint Zero Explained* · https://www.bmc.com/blogs/sprint-zero/
- Project Management Pathways — *Sprint 0 Guide: Master Your Agile Project Setup* · https://www.projectmanagementpathways.com/project-management-articles/sprint-zero-guide
- Scrum.org — *Concept of Sprint Zero* · https://www.scrum.org/forum/scrum-forum/7331/concept-sprint-zero
- Atlassian — *User stories with examples and a template* · https://www.atlassian.com/agile/project-management/user-stories
- Atlassian — *What is acceptance criteria? Definition and Best Practices* · https://www.atlassian.com/work-management/project-management/acceptance-criteria
- AltexSoft — *Acceptance Criteria: Purposes, Types, Examples and Best Practices* · https://www.altexsoft.com/blog/acceptance-criteria-purposes-formats-and-best-practices/
- Monday.com — *Sprint Planning: The Complete Guide for 2025* · https://monday.com/blog/rnd/sprint-planning/
- Zenhub — *Sprint planning: Best practices in 2024* · https://blog.zenhub.com/the-ultimate-guide-to-agile-sprint-planning/

---

← [Anterior: Definição do Produto](../product/product-brief.md) · [Voltar ao índice](../README.md) · [Ver Sprints →](./sprints/)
