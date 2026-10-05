# Defect Management / Observações

## Defeitos confirmados

Nenhum defeito de produto foi registrado como confirmado durante a execução deste projeto.

As situações abaixo foram tratadas como **observações/divergências** e não como bugs confirmados sem validação adicional com o comportamento esperado do ambiente.

## OBS-001 — POST /products observado com 201

**Endpoint:** `POST /products`

**Documentação analisada:** o contrato consultado indicava `200` como resposta de sucesso.

**Comportamento observado:** a API pública retornou `201 Created` em uma execução válida.

**Classificação:** divergência de documentação/comportamento observado.

**Status:** observação.

**Por que não foi registrada automaticamente como bug:** é necessário confirmar qual é o contrato oficial esperado para a versão/deploy utilizado.

---

## OBS-002 — `/products/search` sem `q`

**Endpoint:** `GET /products/search`

**Documentação analisada:** o parâmetro `q` é descrito como requerido.

**Comportamento observado:** a API retornou `200` com lista vazia quando `q` não foi informado.

**Classificação:** divergência entre documentação e comportamento.

**Status:** observação.

---

## OBS-003 — Busca do produto criado sem correspondência

**Endpoint:** `GET /products/search?q=...`

**Comportamento observado:** uma busca pelo nome de produto criado durante os testes retornou resposta válida, porém sem o produto esperado.

**Classificação:** comportamento a investigar.

**Status:** observação.

**Hipóteses que não foram assumidas como causa:** indexação, estado do ambiente, regras de busca ou implementação do endpoint.

Não houve alteração artificial de assertions para fazer o teste passar.

## Estratégia de defeitos

Antes de registrar um bug, a análise considera:

1. request;
2. método;
3. URL;
4. headers;
5. body;
6. variáveis;
7. autenticação;
8. estado dos dados;
9. comportamento documentado;
10. resposta real.

Somente após eliminar causas relacionadas ao teste, massa ou ambiente o comportamento deve ser classificado como defeito confirmado.
