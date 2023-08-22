# Webhooks

## Inserir tracking

Esse webhook envia as informações de tracking após as etiquetas de uma remessa de pedidos serem geradas.

### TrackingInfo

| Propriedade       | Tipo                  | Descrição                                                   |
| ---               | ---                   | ---                                                         |
| token             | `string`              | identificador único da venda, como na plataforma de origem  |
| shipping_company  | `ShippingCompany`     | identificador da transportadora responsável pelo frete      |
| tracking_code     | `string`              | código de rastreio                                          |

### ShipppingCompany

```typescript
type ShippingCompany =
  | 'correios'
  | 'jadlog'
  | 'totalexpress'
  | 'loggi'
  | 'carriers'
```

### Exemplo

```json
[
  {
    "token": "123123",
    "shipping_provider": "correios",
    "tracking_code": "PQ..."
  }
]
```

