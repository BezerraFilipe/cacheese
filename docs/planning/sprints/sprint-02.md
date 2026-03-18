← [Sprint 01](./sprint-01.md) · [Voltar ao Planejamento](../mvp-scope.md) · [Voltar ao índice](../../README.md)

# Sprint 02 — Categorias, Dashboard e Orçamento


**[S2-01] Gerenciar categorias** · Tamanho: M

*Como usuário, quero usar categorias padrão e criar minhas próprias categorias com cor, para que meus lançamentos reflitam minha realidade financeira.*

- **Dado** que crio uma nova conta, **quando** acesso o formulário de transações pela primeira vez, **então** as categorias padrão (alimentação, transporte, moradia, saúde, lazer, educação, salário, outros) já estão disponíveis
- **Dado** que crio uma categoria com nome e cor, **quando** salvo, **então** ela aparece disponível para seleção nos formulários de transação
- **Dado** que edito o nome de uma categoria personalizada, **quando** salvo, **então** a alteração é refletida em todas as transações já associadas
- **Dado** que tento excluir uma categoria com transações associadas, **quando** confirmo, **então** recebo aviso pedindo que migre as transações antes

---

**[S2-02] Dashboard principal** · Tamanho: G

*Como usuário, quero ver no dashboard meu saldo consolidado, receitas, despesas do mês e últimos lançamentos, para que eu entenda minha situação financeira de relance.*

- **Dado** que acesso o dashboard, **quando** carrega, **então** vejo o saldo total consolidado de todas as contas ativas
- **Dado** que acesso o dashboard, **quando** carrega, **então** vejo total de receitas e despesas do mês atual e saldo do mês (receitas − despesas)
- **Dado** que acesso o dashboard, **quando** carrega, **então** vejo as últimas 5 transações com data, descrição, categoria e valor
- **Dado** que não tenho transações, **quando** acesso o dashboard, **então** vejo estado vazio com chamada para registrar o primeiro lançamento
- **Dado** que o dashboard carrega em produção, **quando** meço o tempo de resposta, **então** a página renderiza em menos de 300ms

---

**[S2-03] Definir orçamento mensal por categoria** · Tamanho: M

*Como usuário, quero definir um limite de gasto mensal por categoria, para que eu tenha controle sobre quanto posso gastar em cada área.*

- **Dado** que seleciono uma categoria e defino um valor limite, **quando** salvo, **então** o orçamento é criado e o percentual utilizado começa a ser calculado
- **Dado** que tenho orçamento de R$ 500,00 para Alimentação e já gastei R$ 300,00, **quando** acesso o dashboard, **então** vejo indicador com 60% utilizado
- **Dado** que não defini orçamento para uma categoria, **quando** registro uma transação nela, **então** a transação é registrada normalmente, sem indicador de orçamento
- **Dado** que edito um orçamento já existente, **quando** salvo o novo valor, **então** o percentual é recalculado imediatamente

---

**[S2-04] Indicadores visuais de orçamento no dashboard** · Tamanho: M

*Como usuário, quero ver o status de cada orçamento com um indicador visual no dashboard, para que eu saiba quais categorias estão próximas do limite sem precisar navegar.*

- **Dado** que tenho orçamentos definidos, **quando** acesso o dashboard, **então** vejo uma barra de progresso para cada categoria com orçamento
- **Dado** que o consumo está abaixo de 80%, **quando** visualizo o indicador, **então** ele aparece em cor neutra (cinza ou verde)
- **Dado** que o consumo está entre 80% e 99%, **quando** visualizo, **então** o indicador aparece em laranja/amarelo
- **Dado** que o consumo atingiu 100%, **quando** visualizo, **então** o indicador aparece em vermelho

### Riscos identificados
- Performance do dashboard: agregar saldos e calcular percentuais em uma única requisição pode ser lento com muitos dados — usar consultas SQL otimizadas e considerar caching desde já

---

← [Sprint 01](./sprint-01.md) · [Voltar ao Planejamento](../mvp-scope.md) · [Voltar ao índice](../../README.md)
