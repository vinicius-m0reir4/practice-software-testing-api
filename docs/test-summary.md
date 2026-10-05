# Test Summary

## Projeto

Practice Software Testing API — QA Portfolio

## Escopo automatizado no CI

Pasta:

```text
05 - Integration
```

## Última execução validada

```text
Requests:     10
Assertions:   38
Failures:     0
```

## Fluxo validado

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

## Evidências

### Newman local

Execução:

```powershell
npm run test:api
```

Resultado:

```text
10 requests
38 assertions
0 failures
```

### Newman com relatório JSON

Execução:

```powershell
npm run test:api -- --reporters cli,json --reporter-json-export reports/newman-report.json
```

O relatório é tratado como artefato local e não é versionado.

### GitHub Actions

Workflow:

```text
.github/workflows/api-tests.yml
```

Resultado validado:

```text
10 requests
38 assertions
0 failures
```

## Pontos fortes do projeto

- uso de API real/publicada;
- organização da Collection por domínio;
- assertions em JavaScript;
- captura e reutilização de IDs;
- dados dinâmicos;
- validação de persistência;
- cenários positivos e negativos;
- fluxo integrado com cleanup;
- Newman via CLI;
- execução automatizada em GitHub Actions;
- uso de Secrets;
- documentação de observações de QA.

## Limitações

- ambiente público e compartilhado;
- dados sujeitos a alterações externas;
- CI cobre especificamente o fluxo de integração principal;
- a Collection possui cenários adicionais fora do fluxo de CI.

## Conclusão

O projeto atende ao objetivo de demonstrar fundamentos de QA e API Testing com automação suficiente para um portfólio de nível júnior, sem depender de uma arquitetura excessivamente complexa.
