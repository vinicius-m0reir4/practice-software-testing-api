# Test Scenarios

## Cenários principais

| ID | Área | Cenário | Resultado esperado |
|---|---|---|---|
| TS-001 | Authentication | Realizar login com credenciais válidas | Token retornado |
| TS-002 | Users | Consultar usuário autenticado | Dados do usuário retornados |
| TS-003 | Users | Acessar recurso com token inválido | API rejeita a requisição |
| TS-004 | Users | Registrar usuário com dados válidos | Usuário criado |
| TS-005 | Users | Atualizar usuário | Alteração confirmada |
| TS-006 | Users | Consultar usuário após atualização | Dados persistidos |
| TS-007 | Users | Enviar dados inválidos para atualização | API rejeita/retorna resposta de validação |
| TS-008 | Products | Listar produtos | Lista paginada retornada |
| TS-009 | Products | Consultar produto por ID | Produto retornado |
| TS-010 | Products | Consultar produto inexistente | Recurso não encontrado |
| TS-011 | Products | Paginar resultados | Página solicitada retornada |
| TS-012 | Products | Ordenar produtos | Resultado retornado conforme parâmetro |
| TS-013 | Products | Filtrar por faixa de preço | Produtos dentro do filtro retornados |
| TS-014 | Products | Criar produto | Produto criado e identificador retornado |
| TS-015 | Products | Consultar produto criado | Dados persistidos |
| TS-016 | Products | Atualizar produto | Alteração confirmada |
| TS-017 | Products | Consultar produto após atualização | Alteração persistida |
| TS-018 | Products | Aplicar PATCH | Alteração parcial confirmada |
| TS-019 | Products | Consultar após PATCH | Campo alterado persistido |
| TS-020 | Products | Buscar produto | Estrutura de busca retornada |
| TS-021 | Products | Buscar item inexistente | Lista vazia |
| TS-022 | Products | Buscar sem parâmetro `q` | Comportamento observado documentado |
| TS-023 | Products | Criar produto com dados inválidos | Resposta de validação |
| TS-024 | Cart | Criar carrinho | ID do carrinho retornado |
| TS-025 | Cart | Adicionar produto ao carrinho | Item adicionado/atualizado |
| TS-026 | Cart | Consultar carrinho | Itens e dados do carrinho retornados |
| TS-027 | Cart | Atualizar quantidade | Quantidade alterada |
| TS-028 | Cart | Validar quantidade persistida | Nova quantidade confirmada |
| TS-029 | Cart | Remover produto | Produto removido |
| TS-030 | Cart | Confirmar remoção | Produto não está mais no carrinho |
| TS-031 | Cart | Excluir carrinho | Carrinho excluído |
| TS-032 | Cart | Consultar carrinho excluído | Recurso não encontrado |
| TS-033 | Integration | Executar fluxo completo Login → Produto → Carrinho → Cleanup | 10 requests e 38 assertions sem falhas |

## Fluxo automatizado de CI

```text
Login
→ Get Products
→ Create Cart
→ Add Product
→ Update Quantity
→ Verify Cart
→ Delete Product
→ Verify Product Removed
→ Delete Cart
→ Verify Cart Deleted
```

## Observação

Os detalhes completos dos requests e assertions ficam na Collection do Postman. Este documento resume os cenários para facilitar a leitura do projeto.
