# ADR 002 — Estratégia de Autenticação

← [ADR 001](./001-banco-de-dados.md) · [Próximo: ADR 003 →](./003-telegram-bot.md) · [Voltar ao índice](../../README.md)

**Status:** Aceito
**Data:** Sprint 0

---

## Contexto

O Caixa Fácil precisa de um sistema de autenticação que cubra: cadastro de usuário com email e senha, login, logout, gerenciamento de sessão com expiração por inatividade e recuperação de senha. Os dados financeiros são sensíveis por natureza — a autenticação precisa ser segura, mas também precisa ser compreensível para um desenvolvedor iniciante em Rails, que precisa entender o que acontece sob o capô para poder customizar e testar.

Três alternativas foram avaliadas no ecossistema Rails.

---

## Alternativas Consideradas

### Devise (gem)
A gem de autenticação mais popular do ecossistema Rails. Usada pela maioria das aplicações Rails em produção.

**Prós:**
- Solução completa e battle-tested: confirmação de email, bloqueio de conta, rastreamento de sessões, OAuth, entre outros módulos opcionais
- Enorme comunidade e documentação
- Geração de views, controllers e rotas com um comando

**Contras:**
- Caixa-preta: o código de autenticação fica encapsulado na gem — difícil de ler, entender e customizar para iniciantes
- Opinionado em suas convenções: customizações fora do padrão exigem subclassificação de controllers internos da gem, o que é complexo
- Sobrecarga desnecessária: para o escopo do MVP, a maioria dos módulos do Devise não será usada
- Não é ideal para aprendizado — o desenvolvedor não aprende como a autenticação funciona de fato

### Rails 8 Authentication Generator (nativo)
O Rails 8 introduziu um generator nativo (`rails generate authentication`) que cria o código de autenticação diretamente na aplicação — sem dependência externa.

**Prós:**
- Código gerado vive no projeto, totalmente legível e modificável
- Usa as APIs nativas do Rails: `has_secure_password`, `generates_token_for`, cookies assinados e o model `Session` dedicado
- Sem dependências externas — menos superfície de ataque e sem preocupação com versões de gem
- Ideal para aprendizado: o desenvolvedor vê exatamente o que acontece em cada etapa do fluxo
- Alinha-se com a filosofia "batteries included" do Rails 8
- Sessões são rastreadas por model dedicado (`Session`), permitindo histórico e revogação granular

**Contras:**
- Mais minimal que Devise: não gera cadastro (registration) automaticamente — precisa ser implementado manualmente
- Menos battle-tested que Devise em escala — é novo (Rails 8, lançado em 2024)
- Sem suporte nativo a OAuth/social login (não necessário para o MVP)

### Authentication Zero (gem-generator)
Um generator mais completo que o nativo, inspirado no Rails 8, que gera código com mais features prontas (2FA, passwordless, sudo mode).

**Prós:**
- Mais completo que o generator nativo mantendo a filosofia de código próprio
- Segue boas práticas e é bem documentado

**Contras:**
- Dependência externa adicional
- Complexidade superior ao necessário para o MVP
- Menos adequado para quem está aprendendo a base do Rails

---

## Decisão

**Rails 8 Authentication Generator.**

A escolha prioriza aprendizado e transparência sem abrir mão de segurança. Para um projeto de portfólio cujo objetivo central é documentar e entender cada decisão, usar uma gem que encapsula a lógica de autenticação contradiz a própria proposta do projeto. O generator nativo do Rails 8 produz código seguro, legível e completamente customizável — e esse código vive no repositório como parte do projeto, não escondido dentro de uma gem.

O único trabalho adicional necessário — implementar a tela de cadastro manualmente — é também um aprendizado valioso sobre o fluxo de criação de usuários no Rails.

---

## Consequências

- Executar `rails generate authentication` na Sprint 0 como parte do setup inicial
- Implementar manualmente o fluxo de registro (cadastro de novo usuário) sobre o scaffold gerado
- O model `User` usará `has_secure_password` para armazenamento seguro de senhas via BCrypt
- O model `Session` rastreará sessões ativas por usuário, permitindo expiração por inatividade
- Recuperação de senha via token assinado e com tempo de expiração (15 minutos por padrão)
- Sem suporte a OAuth no MVP — registrado como funcionalidade de versões futuras se necessário

---

## Fontes
- Saeloun Blog — *Rails 8 adds built-in authentication generator* · https://blog.saeloun.com/2025/05/12/rails-8-adds-built-in-authentication-generator/
- Andrii Furmanets — *Built-in Authentication in Rails 8.0: A Technical Deep Dive and Comparison* · https://andriifurmanets.com/blogs/built-in-authentication-in-rails
- Avo — *Rails 8 Authentication with the auth generator* · https://avohq.io/blog/rails-8-authentication
- James Hibbard — *Authentication with Devise and CanCanCan in Rails 8* · https://hibbard.eu/authentication-with-devise-and-cancancan-in-rails/
- Masilotti.com — *Rails Authentication: Gems vs. Recipes vs. Generators* · https://masilotti.com/rails-authentication/

---

← [ADR 001](./001-banco-de-dados.md) · [Próximo: ADR 003 →](./003-telegram-bot.md) · [Voltar ao índice](../../README.md)
