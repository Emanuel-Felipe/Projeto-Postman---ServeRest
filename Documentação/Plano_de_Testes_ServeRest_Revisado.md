# Plano de Testes – ServeRest API (Versão Revisada)

## 1) Apresentação
Este plano descreve a estratégia de testes da API ServeRest, revisada após o Challenge 2.  
Foram aplicadas melhorias relacionadas à **cobertura de cenários, priorização, detalhamento e preparação para automação com Robot Framework**.

## 2) Pessoas Envolvidas
- Emanuel Felipe Avelino Silva  

## 3) Objetivo
Assegurar que as regras de negócio e comportamentos descritos nas US sejam atendidos e que as rotas de **Usuários, Login e Produtos** funcionem com confiabilidade, segurança e consistência, contemplando **fluxos positivos, negativos e alternativos**, com foco em futura automação.

## 4) Escopo
**Dentro do escopo**  
- Rotas principais: `/usuarios`, `/login`, `/produtos` (dependência consultiva de `/carrinhos`).  
- Verificação de operações **CRUD** (POST, GET, PUT, DELETE).  
- Regras de negócio essenciais:  
  - Unicidade de email e produto.  
  - Restrições de provedores de email.  
  - Senha dentro do tamanho mínimo e máximo.  
  - Produtos em carrinho não podem ser excluídos.  
  - Autenticação obrigatória para operações restritas.  

**Fora do escopo**  
- Integrações externas.  
- Testes de performance/carga.  
- Testes de segurança avançados.  

## 5) Cenários de Teste Planejados

### Usuários
- CT-01: Cadastrar usuário válido → Esperado: 201  
- CT-02: Cadastrar usuário duplicado → Esperado: 400  
- CT-03: Consultar usuário inexistente → Esperado: 404  
- CT-04: Editar usuário inexistente → Esperado: 201  
- CT-12: Validar email com provedor proibido → Esperado: 400  
- CT-13: Validar senha com tamanho inválido → Esperado: 400  
- CT-14: Validar formato de email inválido → Esperado: 400  
- CT-18: Atualizar usuário com email duplicado → Esperado: 400  
- CT-19: Cadastrar usuário administrador → Esperado: 201  
- CT-20: Validar campos obrigatórios usuário → Esperado: 400  
- CT-22: Excluir usuário válido → Esperado: 200  
- CT-24: Listar todos os usuários → Esperado: 200  
- CT-25: Buscar usuário por ID válido → Esperado: 200  

### Login
- CT-05: Login com sucesso → Esperado: 200 + token  
- CT-06: Login com senha incorreta → Esperado: 401  
- CT-07: Login com usuário inexistente → Esperado: 401  
- CT-17: Validar token expirado → Esperado: 401  

### Produtos
- CT-08: Cadastrar produto válido (com autenticação) → Esperado: 201  
- CT-09: Cadastrar produto sem autenticação → Esperado: 401  
- CT-10: Cadastrar produto duplicado → Esperado: 400  
- CT-11: Editar produto inexistente → Esperado: 201  
- CT-15: Consultar produtos sem autenticação → Esperado: 200  
- CT-16: Excluir produto em carrinho → Esperado: 400  
- CT-21: Validar campos obrigatórios produto → Esperado: 400  
- CT-23: Excluir produto válido → Esperado: 200  

---

## 6) Priorização da Execução
- **Alta prioridade:** login, autenticação, CRUD de usuários e produtos.  
- **Média prioridade:** edições, listagens, consultas gerais.  
- **Baixa prioridade:** consultas a registros inexistentes e cenários exploratórios.  

---

## 7) Matriz de Risco
- **Críticos:** falha no login, ausência de autenticação, inconsistência em cadastro.  
- **Altos:** exclusão incorreta de produtos/usuários, token inválido ou expirado.  
- **Médios/Baixos:** consultas a registros inexistentes.  

---

## 8) Cobertura de Testes
- Operações **CRUD** completas de usuários e produtos.  
- Autenticação via login, incluindo token válido e expirado.  
- Validação de regras de negócio (unicidade, campos obrigatórios, restrições de formato).  
- Cenários de sucesso, erro e alternativos.  

---

## 9) Testes Candidatos à Automação (Robot Framework)
- Login (válido, inválido, inexistente, token expirado).  
- Cadastro de usuário (válido, duplicado, administrador, campos obrigatórios).  
- Cadastro de produto (válido, duplicado, sem autenticação).  
- Exclusão de produto (válido, em carrinho).  
- Validações de email e senha.  
- Consultas por ID e listagens.  

---

## 10) Melhorias Aplicadas
- Expansão da cobertura de testes com novos cenários de validação.  
- Inclusão de cenários negativos e alternativos.  
- Detalhamento dos casos com pré-condições e resultados claros.  
- Reorganização da priorização com base em impacto e risco.  
- Preparação do planejamento para futura automação em **Robot Framework**, com uso de tags (`smoke`, `regression`, `critical`) e estrutura pensada para CI/CD.  
- Organização do documento revisada para melhor leitura e manutenção.  
