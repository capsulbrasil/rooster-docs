# Webhooks

## Verificação de autenticidade

Os webhooks disparados pelo Rooster enviam o cabeçalho HTTP `X-Platform-Token` para comprovação de autenticidade. Para fazer a verificação compare o header recebido com o valor obtido na página Integrações.

## Atualização de tracking

Esse webhook envia as informações de tracking após as etiquetas de uma remessa de pedidos serem geradas.

### Tracking

| Propriedade      | Tipo                  | Descrição                        |
| ---------------- | --------------------- | -------------------------------- |
| event            | `'tracking:update'`   | constante representando o evento |
| integration_info | `IntegrationInfo`     | dados da integração              |
| result           | `Array<TrackingInfo>` | dados de rastreio                |

### IntegrationInfo

| Propriedade | Tipo      | Descrição                                                   |
| ----------- | --------- | ----------------------------------------------------------- |
| api_key     | `string?` | chave secreta da API                                        |
| partner_key | `string?` | chave do cliente (incluído para compatibilidade retroativa) |

### TrackingInfo

| Propriedade          | Tipo                | Descrição                                                  |
| -------------------- | ------------------- | ---------------------------------------------------------- |
| token                | `string`            | identificador único da venda, como na plataforma de origem |
| shipping_provider    | `ShippingProvider`  | identificador da transportadora responsável pelo frete     |
| tracking_code        | `string`            | código de rastreio                                         |
| in_route             | `boolean`           | em rota                                                    |
| was_received         | `boolean`           | foi recebido pelo cliente                                  |

### ShippingProvider

```typescript
type ShippingProvider =
  | 'correios'
  | 'jadlog'
  | 'totalexpress'
  | 'jtexpress'
  | 'loggi'
  | 'carriers'
```

### Exemplo

```json
{
  "event": "tracking:update",
  "integration_info": {
    "api_key": "bla...",
    "partner_key": "bla..."
  },
  "result": [
    {
      "token": "123123",
      "shipping_provider": "correios",
      "tracking_code": "PQ...",
      "in_route": false,
      "was_received": false
    }
  ]
}
```
