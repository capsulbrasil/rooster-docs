# Rooster v1

## Autenticação

Para se autenticar na API deve-se enviar a chave obtida no cabeçalho HTTP `X-Platform-Token` juntamente com o prefixo "Bearer".

```sh
curl https://api-prod/api \
    -H 'Content-type: application/json' \
    -H 'X-Platform-Token: ey...'
```

## [Endpoints](/v1/endpoints.md)

### Pedidos

- `POST /api/platform-postback/system/:id`: insere um pedido

## [Webhooks](/v1/webhooks.md)

- [inserção de tracking](/v1/webhooks.md#atualização-de-tracking)
