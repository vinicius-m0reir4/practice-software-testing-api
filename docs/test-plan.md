# Test Plan — Practice Software Testing API

## 1. Objetivo

Validar os principais comportamentos funcionais da Practice Software Testing API e demonstrar uma estratégia de QA baseada em análise, execução manual, assertions, chaining, persistência, integração e automação.

## 2. Sistema sob teste

- API: Practice Software Testing API
- Base URL: https://api.practicesoftwaretesting.com
- Documentação: https://api.practicesoftwaretesting.com/docs?api-docs
- OpenAPI: https://api.practicesoftwaretesting.com/docs?api-docs.json

## 3. Escopo

### Incluído

- Authentication / Users
- Products
- Cart
- fluxo integrado de carrinho
- validações estruturais de resposta
- cenários positivos e negativos
- criação e reutilização de dados dinâmicos
- execução com Newman
- execução no GitHub Actions

### Fora de escopo

Não foram priorizados neste projeto:

- Payment
- Invoice
- Report
- Stream
- TOTP
- Favorite
- Contact
- Product Spec
- outros módulos não necessários para o objetivo principal do portfólio

## 4. Estratégia

A estratégia foi construída em etapas:

1. analisar a documentação;
2. validar requests manualmente;
3. criar assertions;
4. capturar IDs e tokens;
5. validar persistência;
6. criar o fluxo integrado;
7. executar via Newman;
8. executar no GitHub Actions.

A automação de CI foi concentrada no fluxo integrado principal.

## 5. Tipos de testes

- Funcional
- Positivo
- Negativo
- Estrutural / contrato por assertions
- Persistência
- Integração
- Regressão do fluxo integrado

## 6. Massa de testes

Foram utilizados dados dinâmicos sempre que possível.

Exemplos:

- e-mail de cadastro gerado com timestamp;
- token capturado do login;
- IDs de usuário, produto, categoria, marca, imagem e carrinho capturados durante a execução.

## 7. Riscos considerados

- ambiente público e compartilhado;
- alterações de dados entre execuções;
- dependência de IDs e estados prévios;
- restrições de autorização;
- diferenças entre documentação e comportamento observado;
- instabilidade ocasional da API pública.

## 8. Critérios de entrada

- API disponível;
- Collection configurada;
- credenciais de teste disponíveis localmente;
- dependências instaladas para execução via Newman.

## 9. Critérios de saída

O projeto é considerado pronto para portfólio quando:

- o fluxo de integração principal é executado com sucesso;
- as assertions críticas passam;
- o Newman retorna execução sem falhas;
- o GitHub Actions executa o fluxo;
- credenciais não são versionadas;
- README e documentação estão atualizados.

## 10. Resultado atual

Última execução validada do fluxo de CI:

```text
10 requests
38 assertions
0 failures
```
