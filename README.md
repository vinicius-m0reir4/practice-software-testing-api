# Practice Software Testing API — QA Portfolio

[![API Tests](https://github.com/vinicius-m0reir4/practice-software-testing-api/actions/workflows/api-tests.yml/badge.svg)](https://github.com/vinicius-m0reir4/practice-software-testing-api/actions/workflows/api-tests.yml)

Projeto de QA focado em **testes de API** utilizando Postman, JavaScript, Newman e GitHub Actions, desenvolvido sobre a API pública do Practice Software Testing.

O projeto foi estruturado para demonstrar não apenas a criação de requests, mas também **planejamento, análise de comportamento, assertions, massa de dados, encadeamento entre endpoints, persistência, testes negativos, integração, execução via CLI e CI**.

## Objetivo

Construir uma suíte de testes de API com foco em cenários funcionais e integrados, validando:

- autenticação e uso de token;
- estrutura e conteúdo das respostas;
- status codes e Content-Type;
- dados dinâmicos e IDs capturados durante a execução;
- operações de consulta, criação, atualização e exclusão;
- persistência após alterações;
- cenários positivos e negativos;
- fluxo integrado de carrinho;
- execução automatizada com Newman;
- execução contínua no GitHub Actions.

## API testada

**Practice Software Testing API**

Base URL:

https://api.practicesoftwaretesting.com

Documentação:

https://api.practicesoftwaretesting.com/docs?api-docs

OpenAPI:

https://api.practicesoftwaretesting.com/docs?api-docs.json

## Tecnologias

- Postman
- JavaScript
- Newman
- Node.js
- Git
- GitHub
- GitHub Actions
- Visual Studio Code

## Escopo

### Authentication / Users

- Login
- Register
- Current User
- Get User by ID
- Update User
- Invalid token
- Invalid user data

### Products

- List Products
- Product by ID
- Invalid Product ID
- Pagination
- Sort
- Price filter
- Create Product
- Get created Product
- Update Product
- Partial Update (PATCH)
- Search
- Search without result
- Search without query
- Invalid product data
- Lookup of Category, Brand and Image data used by product creation

### Cart

- Create Cart
- Add Product
- Get Cart
- Update Quantity
- Verify persistence
- Remove Product
- Verify removal
- Delete Cart
- Verify deleted resource

### Integration

O principal fluxo automatizado de CI está na pasta `05 - Integration`:

```text
INTEGRATION-001  Login
        ↓
INTEGRATION-002  Get Products
        ↓
INTEGRATION-003  Create Cart
        ↓
INTEGRATION-004  Add Product
        ↓
INTEGRATION-005  Update Quantity
        ↓
INTEGRATION-006  Verify Cart
        ↓
INTEGRATION-007  Delete Product
        ↓
INTEGRATION-008  Verify Product Removed
        ↓
INTEGRATION-009  Delete Cart
        ↓
INTEGRATION-010  Verify Cart Deleted
```

Esse fluxo usa IDs capturados durante a execução, permitindo que um request alimente o próximo.

## Estratégia de testes

A estratégia adotada foi:

```text
Análise da API
      ↓
Validação manual no Postman
      ↓
Assertions
      ↓
Captura de dados / chaining
      ↓
Persistência
      ↓
Integração
      ↓
Newman
      ↓
GitHub Actions
```

A automação prioriza cenários repetitivos e críticos para o fluxo integrado, evitando automatizar indiscriminadamente todos os requests da Collection.

## Tipos de testes

### Testes funcionais

Validação do comportamento esperado de endpoints e respostas.

### Testes positivos

Exemplos:

- login válido;
- cadastro válido;
- consulta de produtos;
- criação de carrinho;
- adição de produto;
- atualização de quantidade.

### Testes negativos

Exemplos:

- token inválido;
- ID de produto inexistente;
- dados inválidos de usuário;
- dados inválidos de produto;
- busca sem resultado;
- busca sem parâmetro `q`.

### Testes de persistência

Exemplos:

```text
criar → consultar
atualizar → consultar novamente
excluir → consultar novamente
```

### Testes estruturais / de contrato

Foram usadas assertions para validar presença de campos, tipos, estrutura de objetos/arrays e campos relevantes da resposta.

> O projeto não utiliza JSON Schema formal. A validação contratual implementada é baseada em assertions de estrutura e tipos.

### Testes de integração

O fluxo de carrinho combina múltiplos endpoints e valida o resultado de uma operação nas etapas seguintes.

## Massa de testes e chaining

O projeto evita depender de IDs fixos sempre que possível.

Exemplos:

- e-mail de cadastro gerado dinamicamente;
- `token` capturado após login;
- `user_id` capturado da resposta do usuário;
- `product_id` capturado da listagem de produtos;
- `category_id`, `brand_id` e `product_image_id` obtidos da API;
- `cart_id` capturado após criação do carrinho.

Isso reduz dependências de valores previamente existentes no ambiente.

## Newman

Execução local da suíte de integração:

```powershell
npm run test:api
```

A execução validada apresentou:

```text
10 requests
38 assertions
0 failures
```

Também foi gerado um relatório JSON local em:

```text
reports/newman-report.json
```

Os relatórios gerados não são versionados no Git.

## GitHub Actions

O workflow:

```text
.github/workflows/api-tests.yml
```

executa automaticamente:

1. checkout do repositório;
2. configuração do Node.js;
3. instalação das dependências com `npm ci`;
4. execução do Newman;
5. uso de secrets para as credenciais de login.

A execução de CI validada apresentou:

```text
10 requests
38 assertions
0 failures
```

O CI executa especificamente a pasta:

```text
05 - Integration
```

A Collection possui outros cenários destinados à exploração e validações funcionais fora desse fluxo automatizado de CI.

## Segurança

Credenciais não devem ser versionadas.

O Environment local com valores de execução é ignorado pelo `.gitignore`, e o GitHub Actions utiliza:

```text
LOGIN_EMAIL
LOGIN_PASSWORD
```

como GitHub Secrets.

Para novos ambientes, utilize o arquivo:

```text
postman/practice-software-testing.postman_environment.example.json
```

como modelo.

## Como executar localmente

### 1. Clonar

```powershell
git clone https://github.com/vinicius-m0reir4/practice-software-testing-api.git
cd practice-software-testing-api
```

### 2. Instalar dependências

```powershell
npm ci
```

### 3. Preparar o Environment

Copie o arquivo de exemplo:

```powershell
Copy-Item postman\practice-software-testing.postman_environment.example.json postman\practice-software-testing.postman_environment.json
```

Abra:

```text
postman/practice-software-testing.postman_environment.json
```

e preencha somente os valores locais de:

```text
login_email
login_password
```

Não faça commit desse arquivo.

### 4. Executar os testes

```powershell
npm run test:api
```

## Estrutura do projeto

```text
practice-software-testing-api/
│
├── .github/
│   └── workflows/
│       └── api-tests.yml
│
├── docs/
│   ├── test-plan.md
│   ├── test-scenarios.md
│   ├── test-cases.md
│   ├── defects.md
│   └── test-summary.md
│
├── postman/
│   ├── practice-software-testing.postman_collection.json
│   └── practice-software-testing.postman_environment.example.json
│
├── reports/
│   └── .gitkeep
│
├── .gitignore
├── package.json
├── package-lock.json
└── README.md
```

## Resultados

### Última execução local validada

```text
10 requests
38 assertions
0 failures
```

### Última execução validada no GitHub Actions

```text
10 requests
38 assertions
0 failures
```

## Observações de QA

Durante a análise da API foram registradas algumas divergências entre documentação e comportamento observado.

Essas observações não foram classificadas automaticamente como bugs, pois exigem confirmação adicional do comportamento esperado pelo produto/API.

Exemplos:

- o endpoint de criação de produto foi observado retornando `201 Created`;
- a busca de produtos sem o parâmetro `q` foi observada retornando `200` com lista vazia;
- uma busca pelo nome do produto criado nem sempre retornou o produto no ambiente público utilizado.

As observações estão documentadas em [`docs/defects.md`](docs/defects.md).

## Aprendizados demonstrados

Este projeto demonstra prática em:

- leitura e análise de documentação de API;
- planejamento de cenários de teste;
- HTTP/REST/JSON;
- autenticação e token;
- assertions com JavaScript;
- chaining e massa dinâmica;
- testes negativos;
- persistência;
- testes de integração;
- execução via Newman;
- CI com GitHub Actions;
- organização de evidências e documentação.

## Status

**Concluído — projeto de portfólio.**

Melhorias futuras podem incluir novas áreas da API e ampliar a cobertura de automação, sem transformar o projeto em uma suíte excessivamente complexa.

## Licença

MIT
