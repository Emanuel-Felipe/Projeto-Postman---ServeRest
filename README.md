# Plano de Testes – ServeRest API

Este repositório contém o plano de testes elaborado para a API **ServeRest**, desenvolvido como parte das atividades de QA.

O objetivo do plano é garantir a qualidade das rotas principais da API, assegurando que regras de negócio e comportamentos descritos nas **User Stories** sejam atendidos.

---

## 📌 Objetivo
Assegurar que as rotas de **Usuários, Login e Produtos** funcionem de forma confiável, consistente e segura, contemplando:
- Operações CRUD.
- Autenticação via login.
- Regras de negócio críticas (unicidade, campos obrigatórios, restrições de formato).
- Cenários positivos, negativos e alternativos.

---

## 📌 Escopo

### Dentro do escopo
- Rotas: `/usuarios`, `/login`, `/produtos` (dependência consultiva de `/carrinhos`).
- Operações: **POST, GET, PUT, DELETE**.
- Regras de negócio relevantes:
  - Não permitir e-mails repetidos ou de provedores proibidos (gmail, hotmail).
  - Senhas com tamanho mínimo e máximo.
  - Garantir nomes únicos de produtos.
  - Exigir autenticação para manipulação de produtos.

### Fora do escopo
- Integrações externas.
- Testes de performance e carga.
- Testes de segurança avançados.

---

## 📌 Cenários de Teste (Versão Inicial)

### Usuários
- CT-01: Cadastrar usuário válido → Esperado: 201
- CT-02: Cadastrar usuário duplicado → Esperado: 400
- CT-03: Consultar usuário inexistente → Esperado: 404
- CT-04: Editar usuário inexistente → Esperado: 201

### Login
- CT-05: Login com sucesso → Esperado: 200 + token
- CT-06: Login com senha incorreta → Esperado: 401
- CT-07: Login com usuário inexistente → Esperado: 401

### Produtos
- CT-08: Cadastrar produto válido (com autenticação) → Esperado: 201
- CT-09: Cadastrar produto sem autenticação → Esperado: 401
- CT-10: Cadastrar produto duplicado → Esperado: 400
- CT-11: Editar produto inexistente → Esperado: 201

---

## 📌 Priorização
- **Alta prioridade:** Login e cadastros de usuários/produtos.
- **Média prioridade:** Edição de dados.
- **Baixa prioridade:** Consultas a registros inexistentes.

---

## 📌 Técnicas Utilizadas
- Testes de API.
- Testes automatizados (Postman).

---

## 📌 Matriz de Risco (Resumo)
- **Crítico:** falha no login (sem acesso à API).  
- **Moderado:** cadastros duplicados de usuário/produto.  
- **Alto:** acesso a endpoint protegido sem autenticação.  
- **Baixo:** consultas ou edições em registros inexistentes.  

---

## 📌 Testes Candidatos à Automação
- Login (válido e inválido).  
- Cadastro de usuário (válido e duplicado).  
- Cadastro de produto (válido e duplicado).  
- Exclusão de produto válido e inexistente.  
- Criação de carrinho e manipulação de estoque.  
