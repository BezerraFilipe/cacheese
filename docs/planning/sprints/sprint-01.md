← [Voltar ao Planejamento](../mvp-scope.md) · [Voltar ao índice](../../README.md) · [Sprint 02 →](./sprint-02.md)

# Sprint 01 — Autenticação, Contas e Transações



**[S1-01] Cadastro de usuário** · Tamanho: M

*Como visitante, quero criar uma conta com nome, email e senha, para que eu possa acessar o Cacheese.*

- **Dado** que estou na página de cadastro, **quando** preencho nome, email e senha válidos e submeto, **então** minha conta é criada e sou redirecionado ao dashboard com mensagem de boas-vindas
- **Dado** que estou na página de cadastro, **quando** submeto com um email já cadastrado, **então** vejo erro informando que o email já está em uso
- **Dado** que estou na página de cadastro, **quando** submeto com senha com menos de 8 caracteres, **então** vejo mensagem de validação
- **Dado** que submeto o formulário com campos em branco, **quando** o sistema valida, **então** os campos obrigatórios são destacados com erro

---

**[S1-02] Login e logout** · Tamanho: P

*Como usuário cadastrado, quero fazer login e encerrar minha sessão, para que meus dados fiquem protegidos.*

- **Dado** que estou na página de login, **quando** insiro credenciais corretas, **então** sou autenticado e redirecionado ao dashboard
- **Dado** que estou na página de login, **quando** insiro credenciais incorretas, **então** vejo mensagem de erro genérica (sem indicar qual campo está errado)
- **Dado** que estou logado, **quando** clico em "Sair", **então** minha sessão é encerrada e sou redirecionado ao login
- **Dado** que não estou logado, **quando** tento acessar qualquer página autenticada, **então** sou redirecionado ao login

---

**[S1-03] Criar e gerenciar contas financeiras** · Tamanho: M

*Como usuário, quero cadastrar minhas contas financeiras com nome, tipo e saldo inicial, para que o Cacheese saiba de onde parte meu controle financeiro.*

- **Dado** que estou na área de contas, **quando** preencho nome, tipo (corrente, poupança, cartão ou carteira) e saldo inicial e salvo, **então** a conta aparece na listagem com o saldo informado
- **Dado** que tenho contas cadastradas, **quando** acesso a listagem, **então** vejo cada conta com nome, tipo e saldo atual
- **Dado** que estou editando uma conta, **quando** altero o nome e salvo, **então** a alteração é refletida na listagem
- **Dado** que clico em desativar uma conta, **quando** confirmo, **então** a conta sai da listagem ativa mas seus dados são preservados

---

**[S1-04] Registrar transação** · Tamanho: G

*Como usuário, quero registrar uma receita ou despesa informando valor, data, descrição, categoria e conta, para que meu saldo seja atualizado automaticamente.*

- **Dado** que preencho todos os campos e salvo, **quando** a transação é confirmada, **então** ela aparece no histórico e o saldo da conta vinculada é atualizado
- **Dado** que registro uma despesa de R$ 50,00 em uma conta com R$ 200,00, **quando** salvo, **então** o saldo passa a R$ 150,00
- **Dado** que registro uma receita de R$ 1.000,00, **quando** salvo, **então** o saldo da conta aumenta em R$ 1.000,00
- **Dado** que seleciono uma transação e edito seus dados, **quando** salvo, **então** o saldo da conta é recalculado corretamente
- **Dado** que excluo uma transação, **quando** confirmo, **então** ela é removida e o saldo da conta é restaurado

---

**[S1-05] Listar e filtrar transações** · Tamanho: M

*Como usuário, quero ver meu histórico de transações e filtrá-lo por período, para que eu consiga localizar lançamentos específicos.*

- **Dado** que acesso o histórico sem filtro, **quando** a página carrega, **então** vejo as transações do mês atual em ordem cronológica decrescente
- **Dado** que seleciono um período personalizado, **quando** o filtro é aplicado, **então** vejo apenas transações do período selecionado
- **Dado** que não há transações no período selecionado, **quando** o filtro é aplicado, **então** vejo mensagem de estado vazio

### Riscos identificados
- Lógica de recálculo de saldo ao editar ou excluir transações pode gerar inconsistências — cobrir com testes unitários específicos para esses fluxos
- Fuso horário: garantir que datas sejam salvas e exibidas corretamente (configurar `config.time_zone` no Rails desde a Sprint 0)

---
---

← [Voltar ao Planejamento](../mvp-scope.md) · [Voltar ao índice](../../README.md) · [Sprint 02 →](./sprint-02.md)
