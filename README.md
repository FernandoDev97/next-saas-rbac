# Next.js SaaS + RBAC

Este projeto contém todos os padrões necessários para configurar um SaaS multilocatário com Next.js, incluindo autenticação e autorização RBAC.

## Características

### Autenticação

- [x] Deve ser possível autenticar usando e-mail e senha;
- [ ] Deve ser capaz de autenticar usando conta Github;
- [ ] Deverá ser possível recuperar a senha através do e-mail;
- [ ] Deverá ser possível criar uma conta (e-mail, nome e senha);

### Organizações

- [ ] Deve ser capaz de criar uma nova organização;
- [ ] Deve ser possível obter as organizações às quais o usuário pertence;
- [ ] Deve ser capaz de atualizar uma organização;
- [ ] Deve ser capaz de encerrar uma organização;
- [ ] Deve ser capaz de transferir a propriedade da organização;

### Convites

- [ ] Deverá ser possível convidar um novo membro (e-mail, função);
- [ ] Deve ser capaz de aceitar um convite;
- [ ] Deve ser possível revogar um convite pendente;

### Membros

- [ ] Deve ser capaz de consultar membros da organização;
- [ ] Deve ser capaz de atualizar uma função de membro;

### Projetos

- [ ] Deve ser capaz de conseguir projetos dentro de uma organização;
- [ ] Deverá ser possível criar um novo projeto (nome, url, descrição);
- [ ] Deve ser capaz de atualizar um projeto (nome, url, descrição);
- [ ] Deve ser possível excluir um projeto;

### Cobrança

- [ ] Deve ser possível obter detalhes de cobrança da organização (US$ 20 por projeto / US$ 10 por membro, excluindo a função de cobrança);

## RBAC

Roles & permissions.

### Roles

- Owner (count as administrator)
- Administrator
- Member
- Billing (one per organization)
- Anonymous

### Permissions table

|                        | Administrator | Member | Billing | Anonymous |
| ---------------------- | ------------- | ------ | ------- | --------- |
| Update organization    | ✅            | ❌     | ❌      | ❌        |
| Delete organization    | ✅            | ❌     | ❌      | ❌        |
| Invite a member        | ✅            | ❌     | ❌      | ❌        |
| Revoke an invite       | ✅            | ❌     | ❌      | ❌        |
| List members           | ✅            | ✅     | ✅      | ❌        |
| Transfer ownership     | ⚠️            | ❌     | ❌      | ❌        |
| Update member role     | ✅            | ❌     | ❌      | ❌        |
| Delete member          | ✅            | ⚠️     | ❌      | ❌        |
| List projects          | ✅            | ✅     | ✅      | ❌        |
| Create a new project   | ✅            | ✅     | ❌      | ❌        |
| Update a project       | ✅            | ⚠️     | ❌      | ❌        |
| Delete a project       | ✅            | ⚠️     | ❌      | ❌        |
| Get billing details    | ✅            | ❌     | ✅      | ❌        |
| Export billing details | ✅            | ❌     | ✅      | ❌        |

> ✅ = allowed
> ❌ = not allowed
> ⚠️ = allowed w/ conditions

#### Conditions

- Only owners may transfer organization ownership;
- Only administrators and project authors may update/delete the project;
- Members can leave their own organization;
