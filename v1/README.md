# Rooster v1

## Autenticação

Para se autenticar na API deve-se enviar a chave obtida no cabeçalho HTTP `Authorization` juntamente com o prefixo "Bearer".

```sh
curl https://api-prod/api \
    -H 'Content-type: application/json' \
    -H 'Authorization: Bearer ey...'
```

## [Endpoints](/v1/endpoints)

### Pedidos

- [POST /api/order/insert/:id](): insere um pedido


## [Webhooks](/v1/webhooks)

- [inserção de tracking](/v1/webhhooks#)
