# Fase 2 — Definição do Produto
### Caixa Fácil · Gestão Financeira Pessoal · Do Problema à Solução

---

## 1. Geração de Ideias

Com o espaço de problema mapeado na Fase 1, esta etapa tem como objetivo expandir o horizonte de possibilidades antes de qualquer convergência. O exercício é deliberadamente divergente: nenhuma ideia é descartada prematuramente. A pergunta central é — *quais abordagens diferentes poderiam resolver as dores identificadas?*

A partir das personas e das dores mapeadas, seis direções foram geradas:

**Ideia A — Registro ultrarrápido de transações (micro-logging)**
Um produto centrado exclusivamente na velocidade de lançamento: o usuário registra uma transação em menos de 10 segundos, com categorização automática sugerida e confirmação por um toque. O foco é reduzir o atrito do hábito de registro, que é o ponto mais crítico de abandono identificado na Fase 1.

**Ideia B — Dashboard financeiro unificado com múltiplas contas**
Uma visão consolidada de todas as contas e cartões em um único lugar. O produto resolve o problema da fragmentação, agregando saldos e transações de diferentes instituições. O ponto de valor é a eliminação da necessidade de abrir múltiplos aplicativos bancários.

**Ideia C — Sistema de orçamento por categorias com alertas proativos**
Um produto baseado em envelopes digitais: o usuário define limites por categoria de gasto (alimentação, transporte, lazer) e recebe alertas ao se aproximar dos limites. O foco é o controle comportamental, não apenas o registro histórico.

**Ideia D — Comparação e análise histórica de gastos**
Um produto analítico que gera relatórios comparativos entre períodos — semana a semana, mês a mês, ano a ano — com visualizações claras. Resolve diretamente a dor de não conseguir identificar padrões de gasto ao longo do tempo.

**Ideia E — Assistente financeiro com metas e planejamento**
Um produto orientado a objetivos: o usuário define metas (viagem, reserva de emergência, quitação de dívida) e o sistema projeta prazos, sugere valores mensais e acompanha o progresso. Vai além do controle e entra no território de planejamento financeiro.

**Ideia F — Plataforma de educação financeira contextual**
Um produto que combina registro de transações com conteúdo educativo contextual — ao categorizar um gasto em "juros", o produto oferece um micro-conteúdo sobre como sair do rotativo do cartão. Resolve a lacuna de conhecimento financeiro identificada na pesquisa.

**Fontes:**
- SpaceO Technologies — *How to Build a Personal Finance App: Step-by-Step Guide 2025* · https://www.spaceotechnologies.com/blog/build-personal-finance-app/
- GeekyAnts — *Building an AI-Driven Personal Finance App: A Step-by-Step Guide* · https://geekyants.com/blog/building-an-ai-driven-personal-finance-app-a-step-by-step-guide
- FasterCapital — *How to calculate MVP cost for a personal finance app* · https://www.fastercapital.com/content/How-to-calculate-MVP-cost-for-a-personal-finance-app--A-user-research-and-monetization-model.html

---

## 2. Seleção de Ideias

A seleção foi guiada por três critérios objetivos: **impacto direto na dor central do usuário**, **viabilidade técnica para um MVP em Rails desenvolvido por um desenvolvedor iniciante no framework**, e **capacidade de gerar aprendizado sobre comportamento de usuário rapidamente**. Cada ideia foi avaliada nesses três eixos.

As Ideias A, B e C emergiram como as mais estratégicas — e não por acaso: elas respondem diretamente aos três problemas centrais identificados na pesquisa (atrito no registro, fragmentação das contas e ausência de controle proativo). As Ideias D, E e F têm valor real, mas dependem de dados acumulados ao longo do tempo (D) ou de complexidade técnica ou de conteúdo que ultrapassa o escopo de um MVP (E e F). A decisão foi **incorporar A, B e C como núcleo do produto**, tratando D como funcionalidade da v1.1 e E e F como visão de longo prazo. Isso cria um produto coerente que resolve o ciclo completo — registrar, visualizar, controlar — sem se dispersar.

**Fontes:**
- Aalpha — *How to Prioritize MVP Features in 2025 & Beyond* · https://www.aalpha.net/blog/how-to-prioritize-mvp-features/
- IPH Technologies — *10 MVP Features You Must Have (And 5 to Skip)* · https://iphtechnologies.com/mvp-features-startup-app-must-have/
- WEZOM — *MVP App Development in 2025* · https://wezom.com/blog/how-to-develop-an-mvp-app

---

## 3. Síntese

O produto que emerge da seleção é um **sistema de gestão financeira pessoal centrado no ciclo registro → visibilidade → controle**. Não é um super-app financeiro. Não é uma plataforma de investimentos. Não é uma ferramenta educacional. É um produto com escopo deliberadamente restrito que resolve um problema específico de forma completa e fluida: o usuário sabe, em qualquer momento, quanto tem, quanto gastou e quanto ainda pode gastar — sem precisar abrir planilhas ou alternar entre múltiplos aplicativos bancários.

A proposta de valor central pode ser enunciada em uma frase: **visibilidade financeira total com o menor atrito possível**. Isso posiciona o produto em contraste direto com planilhas (alta visibilidade, alto atrito) e com apps bancários (baixo atrito, visibilidade parcial e fragmentada). O nome do produto é **Caixa Fácil** — simples, direto e sem ambiguidade sobre o que faz.

**Fontes:**
- WildNetEdge — *Personal Finance Apps: What Users Expect in 2025* · https://www.wildnetedge.com/blogs/personal-finance-apps-what-users-expect-in-2025
- Bountisphere — *The State of Personal Finance Apps in 2025: A Complete Year-End Review* · https://bountisphere.com/blog/personal-finance-apps-2025-review

---

## 4. Funcionalidades Priorizadas

A priorização seguiu o método **MoSCoW** (Must Have / Should Have / Could Have / Won't Have), amplamente utilizado em engenharia de produto para forçar decisões explícitas de escopo e evitar a armadilha de tratar tudo como prioridade.

### Must Have — Sem isso, o produto não existe
- Cadastro e autenticação de usuário (email + senha, com sessão segura)
- Criação e gerenciamento de contas financeiras (conta corrente, poupança, cartão de crédito, carteira digital)
- Registro de transações (receitas e despesas) com data, valor, descrição e categoria
- Categorias de transação padrão (editáveis pelo usuário)
- Dashboard com saldo consolidado, total de receitas e despesas do período atual
- Definição de orçamento mensal por categoria
- Alertas visuais ao atingir 80% e 100% do limite de uma categoria
- **Notificação por email ao gerar novo alerta de orçamento** (via Action Mailer)
- **Bot do Telegram para registro de transações por texto ou voz em linguagem natural** (funcionalidade isolada — o app funciona normalmente se o bot estiver indisponível)

### Should Have — Aumenta significativamente o valor, mas não bloqueia o MVP
- Filtros e busca no histórico de transações
- Relatório comparativo entre períodos (mês atual vs. mês anterior)
- Gráfico de distribuição de gastos por categoria (pizza ou barras)
- Suporte a transações recorrentes (assinaturas, salário fixo)
- Exportação de dados em CSV

### Could Have — Desejável, entra se houver tempo
- Foto de comprovante anexada à transação
- Modo escuro
- Tags personalizadas em transações
- Resumo semanal por email (digest financeiro)

### Won't Have (nesta versão) — Explicitamente fora do escopo
- Integração automática com bancos (Open Finance / Plaid)
- Gestão de investimentos
- Score ou avaliação de saúde financeira
- Funcionalidades multiusuário (casal, família)
- App mobile nativo (iOS/Android)

**Fontes:**
- IPH Technologies — *10 MVP Features You Must Have (And 5 to Skip)* · https://iphtechnologies.com/mvp-features-startup-app-must-have/
- FasterCapital — *How to calculate MVP cost for a personal finance app* · https://www.fastercapital.com/content/How-to-calculate-MVP-cost-for-a-personal-finance-app--A-user-research-and-monetization-model.html
- Market Research Future — *Personal Finance Mobile App Market Size* · https://www.marketresearchfuture.com/reports/personal-finance-mobile-app-market-22409

---

## 5. Definição do MVP

O MVP do **Caixa Fácil** é a implementação completa de todas as funcionalidades **Must Have** listadas na seção anterior. O critério de seleção foi direto: o MVP precisa resolver o ciclo completo de visibilidade financeira — do registro ao alerta — sem deixar lacunas que tornem o produto inútil na prática. Um produto que registra transações mas não mostra saldo consolidado não gera valor. Um produto que exibe dashboard mas não alerta sobre estouros de orçamento não muda comportamento. As duas novas features — notificação por email e bot do Telegram — foram incorporadas ao MVP por expandirem os canais de registro e alerta sem alterar o núcleo da aplicação.

### Escopo do MVP

**Módulo 1 — Autenticação**
- Cadastro de novo usuário (nome, email, senha)
- Login e logout
- Gerenciamento de sessão com expiração por inatividade

**Módulo 2 — Contas Financeiras**
- Criação de conta com nome, tipo (corrente, poupança, cartão, carteira) e saldo inicial
- Listagem de contas com saldo atual calculado
- Edição e desativação de conta
- Saldo consolidado de todas as contas na tela inicial

**Módulo 3 — Transações**
- Registro de transação: tipo (receita/despesa), valor, data, descrição, categoria, conta vinculada
- Listagem de transações com filtro por período
- Edição e exclusão de transação
- Atualização automática do saldo da conta vinculada

**Módulo 4 — Categorias**
- Categorias padrão pré-configuradas (alimentação, transporte, moradia, saúde, lazer, educação, salário, outros)
- Criação de categorias personalizadas pelo usuário
- Associação de cor e ícone à categoria

**Módulo 5 — Dashboard**
- Saldo total consolidado (todas as contas)
- Total de receitas e despesas do mês atual
- Saldo do mês (receitas − despesas)
- Lista das últimas transações
- Indicadores visuais de orçamento por categoria (percentual utilizado)

**Módulo 6 — Orçamento e Alertas**
- Definição de limite mensal por categoria
- Cálculo automático do percentual consumido do orçamento
- Alerta visual no dashboard ao atingir 80% do limite
- Alerta visual ao atingir 100% do limite

**Módulo 7 — Notificações por Email**
- Envio automático de email ao gerar alerta de 80% de orçamento atingido
- Envio automático de email ao estourar 100% de orçamento de uma categoria
- Template de email responsivo com resumo da categoria, valor gasto e limite definido
- Implementado via Action Mailer (nativo do Rails) com fila de envio por Active Job

**Módulo 8 — Bot do Telegram (canal de registro alternativo)**
- Configuração de bot via BotFather e webhook apontando para a aplicação Rails
- Vinculação da conta Telegram ao usuário cadastrado no Caixa Fácil
- Registro de transação por texto em linguagem natural (ex: *"gastei 35 reais no almoço"*)
- Interpretação da mensagem via API de LLM (extração de valor, descrição e categoria sugerida)
- Confirmação da transação pelo usuário antes de persistir no banco
- Suporte a comando de voz via transcrição automática pelo Telegram
- **Princípio de isolamento:** falha no bot não afeta o funcionamento da aplicação web; as duas interfaces operam de forma completamente independente

### O que NÃO está no MVP e por quê
- **Relatórios comparativos entre períodos:** requer dados históricos acumulados; não gera valor imediato no primeiro mês de uso
- **Integração bancária automática:** complexidade técnica desproporcional para a fase atual; não é um bloqueador para o valor central do produto
- **App mobile nativo:** a web responsiva atende o caso de uso de registro no momento da compra; nativo entra no roadmap da v2.0

### Definition of Done (DoD) do MVP
O MVP estará completo quando:
- Um usuário conseguir criar conta, cadastrar suas contas financeiras, registrar uma transação e visualizar o saldo atualizado no dashboard em menos de 3 minutos de uso inicial
- O sistema calcular e exibir corretamente os alertas de orçamento no dashboard
- O email de alerta for enviado corretamente ao atingir 80% e 100% do limite de uma categoria
- O bot do Telegram conseguir interpretar uma mensagem em linguagem natural, extrair os dados da transação e persistir no banco após confirmação do usuário
- A aplicação web funcionar normalmente com o bot do Telegram indisponível
- A aplicação estiver deployada em ambiente de produção e acessível por URL pública
- Cobertura de testes automatizados de pelo menos 70% nas models e controllers críticos

**Fontes:**
- SpaceO Technologies — *How to Build a Personal Finance App: Step-by-Step Guide 2025* · https://www.spaceotechnologies.com/blog/build-personal-finance-app/
- WEZOM — *MVP App Development in 2025* · https://wezom.com/blog/how-to-develop-an-mvp-app
- WildNetEdge — *Personal Finance Apps: What Users Expect in 2025* · https://www.wildnetedge.com/blogs/personal-finance-apps-what-users-expect-in-2025

---

## 6. Métricas de Sucesso

As métricas foram definidas em duas camadas: **métricas de produto** (comportamento do usuário dentro da aplicação) e **métricas de engenharia** (qualidade técnica da entrega). Para um projeto de portfólio com usuário inicial sendo o próprio desenvolvedor, as métricas de produto funcionam como hipóteses a validar; as de engenharia são metas objetivas.

### Métricas de Produto

**North Star Metric — Transações registradas por usuário ativo por semana**
Esta é a métrica que melhor captura se o produto está cumprindo sua promessa. Um usuário que registra transações regularmente é um usuário que está usando o produto para gerenciar suas finanças de verdade. O benchmark inicial é ≥ 5 transações/semana por usuário ativo.

**Ativação — Tempo até o primeiro insight**
Mede o tempo entre o cadastro e o primeiro momento em que o usuário visualiza um indicador de orçamento no dashboard (ou seja, tem pelo menos uma conta, uma transação e um orçamento configurados). Meta: < 10 minutos.

**Retenção — D7 e D30**
Percentual de usuários que retornam ao produto no 7º e 30º dia após o cadastro. Benchmarks da indústria para apps financeiros: D7 ≥ 40%, D30 ≥ 25%. Para apps no top de retenção, D30 pode chegar a 43%.

**Engajamento — DAU/MAU (Stickiness)**
Razão entre usuários ativos diários e mensais. Para apps financeiros, o benchmark saudável situa-se entre 20% e 35%. Valores acima de 25% indicam formação de hábito consistente.

**Onboarding — Taxa de conclusão do setup inicial**
Percentual de usuários que completam o fluxo inicial (cadastro de conta financeira + primeira transação) após o registro. Meta: > 70%. Abaixo de 50% indica atrito crítico no onboarding.

**Alertas — Taxa de engajamento com alertas de orçamento**
Percentual de usuários que, ao receber um alerta de 80% de orçamento, tomam alguma ação (visualizam o dashboard ou registram uma nova transação nos 30 minutos seguintes). Esta métrica valida se os alertas estão gerando comportamento, não apenas notificação.

### Métricas de Engenharia

| Métrica | Meta |
|---|---|
| Cobertura de testes (models + controllers) | ≥ 70% |
| Tempo de resposta médio das páginas principais | < 300ms |
| Zero vulnerabilidades críticas (auditoria de segurança) | 100% |
| Uptime em produção | ≥ 99% |
| Commits semânticos no histórico | 100% |

**Fontes:**
- UXCam — *12 KPIs to Measure and Improve your FinTech App onboarding* · https://uxcam.com/blog/measure-fintech-app-onboarding-kpis/
- Plotline — *Mobile App Engagement Metrics: Essential KPIs to Track and Improve* · https://www.plotline.so/blog/mobile-app-engagement-metrics
- RevenueCat — *The complete guide to OKRs and KPIs for subscription apps* · https://www.revenuecat.com/blog/growth/okrs-kpis-subscription-apps/
- Finro — *Fintech KPIs: The Metrics That Define Success in Financial Technology* · https://www.finrofca.com/news/fintech-kpi-guide
- American Chase — *Mobile App KPI Metrics: Essential KPIs for App Success & Growth* · https://americanchase.com/mobile-app-kpi-metrics/

---

## 7. Ideias para Futuras Versões

O roadmap a seguir representa a visão de evolução do produto além do MVP. Cada versão tem um objetivo claro e um conjunto de funcionalidades que só fazem sentido após a validação da versão anterior.

### v1.1 — Análise e Contexto
*Objetivo: transformar dados acumulados em insights acionáveis*
- Relatório comparativo mensal (mês atual vs. anterior)
- Gráficos de tendência de gastos por categoria ao longo do tempo
- Exportação de dados em CSV e PDF
- Transações recorrentes automáticas (assinatura mensal, salário fixo)
- Busca e filtros avançados no histórico

### v1.2 — Experiência e Personalização
*Objetivo: reduzir ainda mais o atrito e aumentar a aderência*
- Modo escuro
- Tags personalizadas em transações
- Foto de comprovante anexada à transação
- Resumo semanal por email (digest financeiro)
- Atalho de registro rápido na tela inicial

### v2.0 — Planejamento Financeiro
*Objetivo: expandir de controle para planejamento*
- Metas financeiras (reserva de emergência, viagem, quitação de dívida)
- Projeção de saldo futuro com base em receitas e despesas recorrentes
- Plano de quitação de dívidas com simulação de juros
- Score de saúde financeira calculado com base no comportamento do usuário

### v3.0 — Integração e Automação
*Objetivo: eliminar o registro manual via integração bancária*
- Integração com Open Finance do Banco Central (importação automática de transações)
- Categorização automática de transações via machine learning
- Detecção automática de assinaturas e cobranças recorrentes
- Alertas de anomalia (cobrança duplicada, gasto fora do padrão)

### v4.0 — Colaboração e Expansão
*Objetivo: expandir para casos de uso multiusuário*
- Contas compartilhadas (casal, família, república)
- Divisão de despesas entre usuários
- App mobile nativo (React Native ou PWA avançado)
- API pública para integrações de terceiros

**Fontes:**
- Bountisphere — *The State of Personal Finance Apps in 2025: A Complete Year-End Review* · https://bountisphere.com/blog/personal-finance-apps-2025-review
- GeekyAnts — *Building an AI-Driven Personal Finance App: A Step-by-Step Guide* · https://geekyants.com/blog/building-an-ai-driven-personal-finance-app-a-step-by-step-guide
- WildNetEdge — *Personal Finance Apps: What Users Expect in 2025* · https://www.wildnetedge.com/blogs/personal-finance-apps-what-users-expect-in-2025
- Banco Central do Brasil — *Open Finance Brasil* · https://www.bcb.gov.br/estabilidadefinanceira/openfinance

---

*Documento gerado na Fase 2 — Definição do Produto · Próxima fase: Arquitetura e Decisões Técnicas*
