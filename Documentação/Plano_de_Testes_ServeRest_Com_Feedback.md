# Plano de Testes – ServeRest API (Revisado com Feedback)

## 1) Apresentação
Este plano descreve a estratégia de testes da API ServeRest, revisado após o feedback do Challenge 2.  
Foram aplicadas melhorias relacionadas a **testes de limite, mensagens de erro detalhadas e evidências mais claras**.

## 2) Pessoas Envolvidas
- Emanuel Felipe Avelino Silva  

## 3) Objetivo
Assegurar que as regras de negócio da API sejam atendidas com **confiabilidade, clareza e robustez**, validando não só o comportamento esperado mas também os limites e mensagens retornadas.

## 4) Escopo
- Rotas principais: `/usuarios`, `/login`, `/produtos` (e dependência de `/carrinhos`).  
- Verificação de operações CRUD (POST, GET, PUT, DELETE).  
- Regras de negócio essenciais.  
- **Inclusão de testes de limite** para reforçar a qualidade.  

---

## 5) Cenários de Teste (Revisados)

### Usuários
- CT-01: Cadastrar usuário válido → Esperado: **201 + mensagem 'Cadastro realizado com sucesso'**  
- CT-02: Cadastrar usuário duplicado → Esperado: **400 + mensagem 'Este email já está sendo usado'**  
- CT-03: Consultar usuário inexistente → Esperado: **404 + mensagem 'Usuário não encontrado'**  
- CT-04: Editar usuário inexistente → Esperado: **201 + novo usuário criado**  
- **CT-12 (Novo limite): Validar senha com 4 caracteres** → Esperado: **400 + mensagem 'Senha deve ter entre 5 e 10 caracteres'**  
- **CT-13 (Novo limite): Validar senha com 11 caracteres** → Esperado: **400 + mensagem 'Senha deve ter entre 5 e 10 caracteres'**

### Login
- CT-05: Login com sucesso → Esperado: **200 + token válido (Bearer)**  
- CT-06: Login com senha incorreta → Esperado: **401 + mensagem 'Email e/ou senha inválidos'**  
- CT-07: Login com usuário inexistente → Esperado: **401 + mensagem 'Email e/ou senha inválidos'**  
- **CT-17 (Novo limite): Login com token expirado** → Esperado: **401 + mensagem 'Token expirado'**

### Produtos
- CT-08: Cadastrar produto válido (com autenticação) → Esperado: **201 + mensagem 'Cadastro realizado com sucesso'**  
- CT-09: Cadastrar produto sem autenticação → Esperado: **401 + mensagem 'Token de acesso ausente, inválido, expirado ou usuário do token não existe mais'**  
- CT-10: Cadastrar produto duplicado → Esperado: **400 + mensagem 'Já existe produto com esse nome'**  
- CT-11: Editar produto inexistente → Esperado: **201 + novo produto criado**  
- **CT-15 (Novo limite): Cadastrar produto com preço negativo** → Esperado: **400 + mensagem 'Preço deve ser maior que 0'**  
- **CT-16 (Novo limite): Cadastrar produto com preço muito alto (ex.: 99999999)** → Esperado: **400 + mensagem 'Preço acima do permitido'**

---

## 6) Evidências
- **Execuções no Postman:** captura de tela da requisição e resposta (status code + body).  
- **Robot Framework (futuro):** log em HTML com resultado da execução e evidências automáticas.  
- **JSONs de retorno:** armazenados como prova do comportamento esperado.  

---

## 7) Priorização Revisada
- **Alta:** login, autenticação, cadastros e testes de limite.  
- **Média:** edições e listagens.  
- **Baixa:** consultas a registros inexistentes.  

---

## 8) Conclusão
Com os ajustes de **testes de limite, mensagens de erro detalhadas e evidências claras**, o plano se torna mais didático e confiável, cobrindo não apenas os fluxos principais, mas também situações críticas e de borda que reforçam a robustez da API.
