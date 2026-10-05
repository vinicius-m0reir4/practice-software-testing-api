# Test Cases

Este documento reúne os casos mais representativos do projeto. A Collection do Postman permanece como fonte de execução dos requests e assertions.

## Authentication / Users

| ID | Método | Endpoint | Objetivo | Resultado esperado |
|---|---|---|---|---|
| AUTH-001 | POST | `/users/login` | Autenticar usuário | `200` e `access_token` |
| USER-001 | GET | `/users/me` | Consultar usuário autenticado | `200` e estrutura válida |
| USER-002 | GET | `/users/me` | Validar token inválido | `401` |
| USER-003 | POST | `/users/register` | Criar usuário com dados dinâmicos | `201` e ID |
| USER-005 | PUT | `/users/{userId}` | Atualizar usuário | `200` e `success=true` |
| USER-006 | GET | `/users/{userId}` | Validar persistência da atualização | `200` e campos persistidos |
| USER-007 | PUT | `/users/{userId}` | Validar dados inválidos | resposta de validação/rejeição |

## Products

| ID | Método | Endpoint | Objetivo | Resultado esperado |
|---|---|---|---|---|
| PRODUCT-001 | GET | `/products` | Validar listagem | `200` e `data[]` |
| PRODUCT-002 | GET | `/products/{productId}` | Validar produto por ID | `200` e estrutura válida |
| PRODUCT-003 | GET | `/products/{productId}` | Validar ID inexistente | `404` |
| PRODUCT-004 | GET | `/products?page=2` | Validar paginação | `200` e página 2 |
| PRODUCT-005 | GET | `/products?sort=name,asc` | Validar parâmetro de ordenação | `200` e lista |
| PRODUCT-006 | GET | `/products?between=10,30` | Validar filtro de preço | `200` e preços numéricos |
| PRODUCT-007 | POST | `/products` | Criar produto | criação validada conforme comportamento observado |
| PRODUCT-011 | GET | `/products/{productId}` | Validar persistência da criação | produto criado retornado |
| PRODUCT-012 | PUT | `/products/{productId}` | Atualizar produto | `success=true` |
| PRODUCT-013 | GET | `/products/{productId}` | Validar persistência do PUT | campos atualizados persistidos |
| PRODUCT-014 | PATCH | `/products/{productId}` | Aplicar atualização parcial | `success=true` |
| PRODUCT-015 | GET | `/products/{productId}` | Validar persistência do PATCH | campo alterado persistido |
| PRODUCT-016 | GET | `/products/search?q=...` | Validar busca | estrutura paginada retornada |
| PRODUCT-017 | GET | `/products/search?q=...` | Busca sem correspondência | `data=[]` e `total=0` |
| PRODUCT-018 | GET | `/products/search` | Observar comportamento sem `q` | comportamento documentado |
| PRODUCT-019 | POST | `/products` | Dados inválidos | resposta de validação |

## Cart

| ID | Método | Endpoint | Objetivo | Resultado esperado |
|---|---|---|---|---|
| CART-001 | POST | `/carts` | Criar carrinho | `201` e ID |
| CART-002 | POST | `/carts/{cartId}` | Adicionar produto | `200` e `result` |
| CART-003 | GET | `/carts/{cartId}` | Consultar carrinho | `200` e `cart_items[]` |
| CART-004 | PUT | `/carts/{cartId}/product/quantity` | Atualizar quantidade | `200` e `result` |
| CART-005 | GET | `/carts/{cartId}` | Validar quantidade persistida | quantidade atualizada |
| CART-006 | DELETE | `/carts/{cartId}/product/{productId}` | Remover produto | `204` |
| CART-007 | GET | `/carts/{cartId}` | Confirmar remoção | produto ausente |
| CART-008 | DELETE | `/carts/{cartId}` | Excluir carrinho | `204` |
| CART-009 | GET | `/carts/{cartId}` | Confirmar exclusão | `404` e mensagem |

## Integration

| ID | Objetivo |
|---|---|
| INTEGRATION-001 | Login e captura do token |
| INTEGRATION-002 | Consulta de produtos e captura do `product_id` |
| INTEGRATION-003 | Criação do carrinho e captura do `cart_id` |
| INTEGRATION-004 | Adição do produto |
| INTEGRATION-005 | Atualização da quantidade |
| INTEGRATION-006 | Validação do carrinho e persistência |
| INTEGRATION-007 | Remoção do produto |
| INTEGRATION-008 | Validação da remoção |
| INTEGRATION-009 | Exclusão do carrinho |
| INTEGRATION-010 | Validação de exclusão com `404` |

## Resultado do fluxo de Integration

```text
Requests: 10
Assertions: 38
Failures: 0
```
