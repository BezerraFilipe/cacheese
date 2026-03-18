← [Sprint 02](./sprint-02.md) · [Voltar ao Planejamento](../mvp-scope.md) · [Voltar ao índice](../../README.md)

# Sprint 3 — Alertas, Email e Qualidade


**[S3-01] Gerar alerta ao atingir 80% do orçamento** · Tamanho: M

*Como usuário, quero receber um alerta visual quando meu gasto em uma categoria atingir 80% do limite, para que eu ajuste meu comportamento antes de estourar o orçamento.*

- **Dado** que tenho orçamento de R$ 500,00 para Lazer e já gastei R$ 395,00, **quando** registro mais R$ 10,00 nessa categoria, **então** um alerta é gerado e aparece no dashboard
- **Dado** que o alerta de 80% foi gerado, **quando** acesso o dashboard, **então** vejo o alerta com a categoria, valor gasto e limite definido
- **Dado** que o alerta de 80% já foi gerado para uma categoria, **quando** registro outro gasto que não ultrapassa 100%, **então** nenhum alerta duplicado é gerado

---

**[S3-02] Gerar alerta ao atingir 100% do orçamento** · Tamanho: M

*Como usuário, quero receber um alerta quando meu gasto ultrapassar o limite de uma categoria, para que eu tenha consciência imediata do estouro.*

- **Dado** que tenho orçamento de R$ 200,00 para Transporte e já gastei R$ 195,00, **quando** registro mais R$ 10,00, **então** um alerta de estouro é gerado
- **Dado** que ocorre estouro, **quando** acesso o dashboard, **então** o indicador da categoria aparece em vermelho e o alerta mostra o valor excedido
- **Dado** que o alerta de 100% já foi gerado, **quando** registro mais gastos no mês na mesma categoria, **então** o valor excedido é atualizado sem criar alertas duplicados

---

**[S3-03] Notificação por email ao gerar alerta** · Tamanho: G

*Como usuário, quero receber um email quando um alerta é gerado, para que eu seja avisado mesmo sem estar com o app aberto.*

- **Dado** que um alerta de 80% é gerado, **quando** o sistema processa, **então** um email é enviado com nome da categoria, percentual atingido, valor gasto e limite definido
- **Dado** que um alerta de 100% é gerado, **quando** o sistema processa, **então** o email inclui o valor do estouro
- **Dado** que o email é aberto no celular, **quando** renderiza, **então** o template é responsivo e legível
- **Dado** que o serviço de email está fora do ar, **quando** o alerta é gerado, **então** o alerta visual no dashboard é criado normalmente e o envio é retentado via Active Job
- **Dado** que um alerta já gerou um email no mês, **quando** o mesmo limite é atingido novamente, **então** nenhum email duplicado é enviado

---

**[S3-04] Qualidade — cobertura de testes** · Tamanho: GG

*Como desenvolvedor, quero cobertura de testes ≥ 70% nas models e controllers críticos, para que o código seja confiável e refatorável com segurança.*

Itens técnicos que compõem o backlog desta história:
- Testes unitários para models: `User`, `Account`, `Transaction`, `Category`, `Budget`, `Alert`
- Testes de request spec para todos os fluxos CRUD
- Testes para o serviço de cálculo de orçamento e geração de alertas
- Testes para o Action Mailer de alertas
- Revisão de código com RuboCop e SimpleCov; refatoração dos pontos identificados

### Riscos identificados
- Lógica de deduplicação de alertas é mais complexa do que parece — modelar o estado do alerta com cuidado e cobrir com testes de borda (limite atingido, revertido e atingido novamente)
- Configuração do Active Job com backend de fila (Solid Queue ou Sidekiq) pode requerer infraestrutura adicional — definir na Sprint 0 e registrar no ADR de deploy


---

← [Sprint 02](./sprint-02.md) · [Voltar ao Planejamento](../mvp-scope.md) · [Voltar ao índice](../../README.md)
