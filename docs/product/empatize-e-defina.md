# Fase 1 — Empatize e Defina
### Gestão Financeira Pessoal · Espaço de Problema

---

## 1. Delimitação do Espaço de Problema

O problema central que este projeto endereça é a **falta de controle consciente sobre a vida financeira pessoal** — um fenômeno que não é isolado nem circunstancial, mas estrutural. Pesquisas do Banco Central do Brasil indicam que 3 em cada 4 famílias brasileiras sentem alguma dificuldade para fechar o mês com seus rendimentos. Globalmente, dados do Ramsey Solutions (2025) mostram que metade dos americanos vive de salário em salário, com Gen Z (67%) e Millennials (63%) sendo os mais afetados.

O espaço de problema, portanto, abrange pelo menos três dimensões interdependentes: a **falta de visibilidade** sobre onde o dinheiro vai; a **fragmentação das fontes de receita e despesa** (múltiplas contas, cartões, carteiras digitais); e a **ausência de alertas proativos** que interrompam comportamentos de gasto antes que o dano esteja feito. Planilhas, a solução mais comum, até hoje atendem parte dessa necessidade — mas com custo alto de manutenção e visualizações que exigem esforço de interpretação, sem qualquer elemento de contexto ou alerta inteligente.

**Fontes:**
- Ramsey Solutions — *The State of Personal Finance in America Q4 2025* · https://www.ramseysolutions.com/budgeting/state-of-personal-finance
- Moneywise — *52% of Americans live paycheck to paycheck, says Ramsey Solutions* · https://moneywise.com/news/economy/52-of-americans-live-paycheck-to-paycheck-says-ramsey-solutions-and-they-dont-expect-relief-anytime-soon
- Banco Central do Brasil — *Relatório de Estabilidade Financeira / Pesquisa de Endividamento das Famílias* · https://www.bcb.gov.br

---

## 2. Revisão da Literatura sobre o Problema e Eventuais Soluções (Research Desk)

A literatura de UX em fintech aponta que a **falta de confiança e transparência** é a dor mais recorrente entre usuários de produtos financeiros digitais (Pixels & Sense, 2024). Além disso, a usabilidade precária é historicamente endêmica: produtos financeiros foram construídos para atender à empresa, não ao usuário. Uma pesquisa da NFCC (2024) revelou que apenas 42% dos americanos mantêm um orçamento e acompanham seus gastos ativamente — apesar da abundância de ferramentas disponíveis. Isso sugere que **o problema não é falta de ferramentas, mas falta de aderência às ferramentas existentes**.

No Brasil, o ecossistema de apps de finanças pessoais é relativamente maduro, com Organizze, Mobills, Minhas Economias e GuiaBolso como referências. Internacionalmente, o fechamento do Mint em março de 2024 desencadeou uma das maiores migrações de usuários que o setor já viu, revelando que nenhum sucessor natural ainda consolidou o mercado de forma definitiva. O estado da arte indica que a indústria avançou em categorização automática, previsões de fluxo de caixa e dashboards mais limpos — mas ainda falha em **mudança de comportamento real e personalização significativa**.

**Fontes:**
- Pixels and Sense — *Understand Your Fintech Customer Pains Without Spending $1,000s on UX Research* · https://www.pixelsandsense.com/insights/understand-your-fintech-customer-pains
- NFCC — *Survey: Financial Anxiety Soars as Americans Doubt Ability to Reach Goals* (2024) · https://www.nfcc.org/press_release/survey-financial-anxiety-soars-as-americans-doubt-ability-to-reach-goals/
- CNBC Select — *Mint is gone — here are the best alternative budget apps to consider* · https://www.cnbc.com/select/mint-budgeting-app-is-going-away-here-are-some-alternatives/
- TechFundingNews — *Personal finance app Monarch rises with $75M after Mint's meltdown* · https://techfundingnews.com/personal-finance-app-monarch-rises-with-75m-after-mints-meltdown-a-soonicorn-on-cards/

---

## 3. Análise do Problema em Contexto e Resultados

O problema de gestão financeira pessoal se manifesta de maneiras diferentes dependendo do perfil do usuário, mas há padrões consistentes. Dados do Ramsey Solutions (Q4 2025) mostram que 38% dos americanos gastaram mais do que planejavam no mês anterior — um número que se manteve estável por seis trimestres consecutivos, sugerindo que se trata de um padrão comportamental, não conjuntural. Entre jovens adultos (Millennials e Gen Z), 71% e 70% respectivamente reconhecem que lacunas de conhecimento financeiro já lhes custaram mais de US$ 1.000 em erros, segundo a Experian (2024).

No contexto brasileiro, o problema é agravado pela **multiplicidade de instituições financeiras** que os usuários utilizam simultaneamente — bancos tradicionais, fintechs como Nubank e Inter, carteiras digitais como PicPay — sem que haja uma visão unificada do fluxo. Isso torna a gestão por planilhas especialmente custosa: qualquer consolidação exige esforço manual repetitivo. O resultado identificado pela pesquisa é que usuários eventualmente **abandonam o controle** não por falta de intenção, mas por esgotamento do processo de manutenção.

**Fontes:**
- Experian — *Survey says: personal finance knowledge gaps are leading to costly mistakes* (2024) · https://www.experianplc.com/newsroom/press-releases/2024/survey-says--personal-finance-knowledge-gaps-are-leading-to-cost
- InvestmentNews — *What Americans don't know about finance is costing them dearly* · https://www.investmentnews.com/ria-news/what-americans-dont-know-about-finance-is-costing-them-dearly/252350
- Ramsey Solutions — *The State of Personal Finance in America Q4 2025* · https://www.ramseysolutions.com/budgeting/state-of-personal-finance

---

## 4. Síntese: Estado da Arte e da Técnica

O estado da arte em gestão financeira pessoal converge em torno de três capacidades técnicas centrais: **agregação de contas via Open Finance/Open Banking**, **categorização automática de transações por machine learning**, e **forecasting de fluxo de caixa**. A maioria dos players maduros (Monarch Money, Simplifi, Empower) já implementou as duas primeiras; o forecasting ainda é diferencial competitivo em 2025-2026. Tendências emergentes incluem assistentes de IA conversacionais para insights financeiros e personalização por comportamento de gasto — com 67% da Gen Z já utilizando IA para gestão financeira, segundo a Experian.

Do ponto de vista técnico, o padrão dominante é a integração via agregadores de dados financeiros (Plaid, nos EUA; Open Finance do Banco Central, no Brasil). A ausência de integração bancária nativa continua sendo o principal ponto de atrito no onboarding. Para projetos em fase de MVP, a estratégia mais adotada é o **lançamento manual de transações com categorização assistida**, evoluindo para integração automática em versões posteriores. Isso reduz a complexidade técnica inicial sem comprometer a proposta de valor central — visibilidade e controle.

**Fontes:**
- Experian — *Take a Look: Millennial and Gen Z Personal Finance Trends* · https://www.experian.com/blogs/news/2023/05/23/millennial-gen-z-personal-finance-trends/
- StanVision — *Fintech UX in 2026: what users expect from modern financial products* · https://www.stan.vision/journal/fintech-ux-in-2026-what-users-expect-from-modern-financial-products
- Eleken — *Fintech UX Best Practices 2026: Build Trust & Simplicity* · https://www.eleken.co/blog-posts/fintech-ux-best-practices
- Banco Central do Brasil — *Open Finance Brasil* · https://www.bcb.gov.br/estabilidadefinanceira/openfinance

---

## 5. Síntese: Stakeholders e Personas

Os stakeholders diretos deste produto são os **usuários finais** — pessoas físicas que buscam controle sobre suas finanças pessoais. Os stakeholders indiretos incluem instituições financeiras (cujos dados são fonte primária do produto) e potencialmente parceiros de educação financeira ou investimentos. Três personas representam bem o espectro de usuários relevantes para este produto:

**Persona 1 — O Estudante Universitário com Renda Variável**
Bruno, 22 anos, estudante de computação. Tem renda irregular entre bolsas, freelas e pequenos empregos. Possui conta no Nubank e no banco tradicional dos pais. Usa planilhas esporadicamente mas abandona em semanas. Sua maior dor é não saber se pode fazer uma compra grande sem comprometer o mês. Quer algo rápido de registrar, preferencialmente no celular logo após a compra.

**Persona 2 — O Jovem Profissional com Múltiplas Contas**
Camila, 28 anos, analista de marketing. Renda mensal fixa, mas com variáveis (comissões, freelas pontuais). Tem conta corrente no Itaú, cartão de crédito no Nubank, e investimentos na XP. Nunca conseguiu unificar a visão de tudo. Sua maior dor é descobrir no final do mês que gastou mais do que imaginou, sem saber em qual categoria. Quer relatórios comparativos por período e alertas antes de estourar o orçamento.

**Persona 3 — O Adulto Endividado em Processo de Reorganização**
Roberto, 38 anos, servidor público. Renda estável, mas acumulou dívidas em cartão de crédito. Quer entender quanto deve ao total, criar um plano de quitação e acompanhar o progresso. Sua maior dor é a falta de visibilidade sobre o total da dívida consolidada e a sensação de que o problema é maior do que consegue enxergar. Quer clareza e progresso visível.

**Fontes:**
- FINRA Foundation — *National Financial Capability Study 2024* · https://www.finra.org/investors/insights/finra-foundation-national-financial-capability-study
- Nasdaq / GOBankingRates — *Millennials vs. Gen Z: Who's More Financially Prepared for the Future?* · https://www.nasdaq.com/articles/millennials-vs-gen-z-whos-more-financially-prepared-future
- Bank of America — *Better Money Habits: Gen Z & Millennial Study 2025* · https://newsroom.bankofamerica.com/content/newsroom/press-releases/2025/07/confronted-with-higher-living-costs--72--of-young-adults-take-ac.html
- LIMRA — *Financial Literacy Month: Helping Gen Z and Millennial Consumers* (2024) · https://www.limra.com/en/newsroom/industry-trends/2024/financial-literacy-month-helping-gen-z-and-millennial-consumers-navigate-todays-financial-landscape/

---

## 6. Análise de Competidores

O mercado de gestão financeira pessoal pode ser segmentado em três categorias. Os **apps de orçamento estruturado** (YNAB, EveryDollar) pedem alto engajamento e têm curva de aprendizado íngreme — o YNAB custa US$ 14,99/mês e exige configuração intensa. Os **agregadores e dashboards** (Monarch Money, Rocket Money, Simplifi) oferecem visão consolidada com sincronização bancária automática, mas dependem de integrações que variam por região e instituição. Os **apps nacionais** (Organizze, Mobills, Minhas Economias) têm boa integração com o contexto brasileiro, mas interfaces que oscilam entre o excessivamente simples e o excessivamente denso.

As lacunas identificadas são consistentes: a maioria das ferramentas **falha em alertas proativos contextuais** (avisar antes do problema, não depois); poucos resolvem bem a **experiência de registro rápido no momento da compra**; e quase nenhum oferece comparações entre períodos de forma intuitiva sem exigir que o usuário navegue por múltiplas telas. O Mint, que era referência em usabilidade, foi descontinuado em 2024 sem um substituto natural de mesma simplicidade — deixando um espaço real para produtos que priorizem fluidez e leveza de uso.

**Fontes:**
- WalletHub — *What Happened to Mint? Explanation & Best Replacements* · https://wallethub.com/edu/b/what-happened-to-mint/151868
- Rocket Money — *Mint Closing: Alternatives, Timeline, And What It Means For Budgeters* · https://www.rocketmoney.com/learn/personal-finance/mint-app-shutting-down
- Abacus Wealth Partners — *Goodbye to Mint.com: 3 Alternative Budgeting Apps to Consider* · https://abacuswealth.com/goodbye-to-mint-com-3-alternative-budgeting-apps-to-consider/
- Aspyre Wealth Partners — *Mint Shut-Down: Other Options For Personal Budgeting Apps* · https://aspyrewealth.com/alternative-budgeting-app/

---

## 7. Identificação do que é ESSENCIAL para as Partes Envolvidas

Para o usuário, três capacidades são inegociáveis: **registrar uma transação com o menor atrito possível** (idealmente em menos de 10 segundos), **enxergar a situação financeira atual de relance** (saldo consolidado, gastos do mês, status do orçamento) e **receber alertas antes que os limites sejam ultrapassados**. Tudo que vai além disso é camada de valor adicional — útil, mas não bloqueante para adoção inicial. A aderência ao produto depende quase inteiramente da velocidade do registro e da clareza do dashboard — não da quantidade de funcionalidades.

Do ponto de vista do produto, o essencial é resolver o ciclo completo de visibilidade: receita → lançamento de despesa → categorização → saldo projetado → alerta contextual. Sem esse ciclo funcionando de forma fluida e confiável, features adicionais como relatórios históricos ou metas de longo prazo perdem valor porque o dado de entrada não é consistente. A confiabilidade dos dados e a velocidade de registro são, portanto, a fundação sobre a qual todas as outras funcionalidades são construídas.

**Fontes:**
- Pixels and Sense — *Why Should Fintechs Care About UX?* · https://www.pixelsandsense.com/insights/why-should-fintechs-care-about-ux
- Onething Design — *Top 10 Fintech UX Design Practices Every Team Needs in 2026* · https://www.onething.design/post/top-10-fintech-ux-design-practices-2026
- Eleken — *Fintech UX Best Practices 2026* · https://www.eleken.co/blog-posts/fintech-ux-best-practices

---

## 8. Síntese: Jornada dos Usuários

A jornada típica do usuário-alvo começa não no produto, mas em um momento de **desconforto financeiro** — a fatura do cartão que veio mais alta, a conta que não fecha, a sensação de que o dinheiro "some". Esse gatilho leva à busca por controle, que se manifesta na tentativa de adotar uma planilha ou um app. A jornada no produto segue quatro momentos críticos:

O primeiro é o **onboarding**: o usuário precisa ver valor antes de comprometer esforço. Se o setup inicial é complexo demais, o abandono acontece aqui. O segundo é o **primeiro registro de transação**: a velocidade e simplicidade desse momento define se o hábito vai se formar. O terceiro é o **primeiro insight gerado pelo produto** — um alerta, um gráfico, uma comparação — que responde à pergunta "isso está me ajudando?". O quarto é o **retorno ao produto no próximo ciclo financeiro** (semana ou mês seguinte), que marca a transição de usuário ocasional para usuário habitual. Produtos que não entregam valor visível antes do terceiro momento raramente chegam ao quarto.

**Fontes:**
- StanVision — *Fintech UX in 2026: what users expect from modern financial products* · https://www.stan.vision/journal/fintech-ux-in-2026-what-users-expect-from-modern-financial-products
- Pixels and Sense — *How Leading Fintech Transfer Apps Build Trust With Their Users* · https://www.pixelsandsense.com/insights/how-fintech-transfer-apps-build-trust
- Origin Financial — *Still Looking for a Replacement 1 Year After the Mint Shutdown?* · https://useorigin.com/resources/blog/mint-replacement-origin-financial-one-year-since-mint-shutdown

---

*Documento gerado na Fase 1 — Empatize e Defina · Próxima fase: Definição do Produto*
