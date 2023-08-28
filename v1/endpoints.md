# Endpoints

## Pedidos

- [POST /api/order/insert/:id](): insere um pedido

Parâmetros da rota:

- `id`: id da integração

Corpo da requisição:

```json
{
  "event": "order_paid",
  "order": {
    "token": "2000003508897196",
    "amount": "50",
    "effective_amount": "50",
    "status": "paid",
    "payment_type": "account_money",
    "date_created": "2022-04-08T17:01:32.000-04:00",
    "date_updated": "2022-04-08T17:01:32.000-04:00",
    "billet_link": "https://linkboleto.com.br/643d954ed8503e51cb71b965",
    "billet_code": "34191090652428600620016155530005193260000029700",
    "receiver_name": "Usuário Teste",
    "receiver_document": "99999999999",
    "products": [
      {
        "code": "KWRD94TB6",
        "name": "3 Frascos - MM",
        "plans": {
          "code": "KWRD94TB6",
          "name": "3 Frascos - MM",
          "quantity": 1
        }
      }
    ],
    "customer": {
      "document": "99999999999",
      "email": "user@gmail.com",
      "phone": "37999999999",
      "document_type": "m",
      "name": "Usuário Teste"
    },
    "shipping_address": {
      "complement": "Apartamento 401",
      "address": "Rua A",
      "city": "Arcos",
      "country": "BR",
      "district": "Bairro B",
      "number": "120",
      "state": "MG",
      "zipcode": "35588000"
    }
  }
}
```

### Payload
| Propriedade       | Tipo              | Descrição                                 |
| ---               | ---               | ---                                       |
| event             | `EventType`       | evento de atualização do pedido           |
| order             | `Order`           | conteúdo do pedido                        |

### EventType

```typescript
type EventType =
  | 'order_paid'
  | 'order_updated'
  | 'cart_reminder'
```


### Order

| Propriedade       | Tipo              | Descrição                                 |
| ---               | ---               | ---                                       |
| token             | `string`          | identificador único do pedido             |
| amount            | `number`          | valor total do pedido                     |
| effective_amount  | `number`          | valor efetivo do pedido                   |
| status            | `Status`          | status do pedido                          |
| payment_type      | `PaymentType`     | tipo de pagamento                         |
| date_created      | `string`          | data de criação do pedido                 |
| date_updated      | `string`          | data de atualização do pedido             |
| billet_link       | `string`          | link do boleto                            |
| billet_code       | `string`          | código do boleto                          |
| receiver_name     | `string`          | nome do recebedor (produto físico)        |
| receiver_document | `string`          | documento do recebedor (produto físico)   |
| products          | `Array<Product>`  | produtos                                  |
| customer          | `Customer`        | cliente                                   |
| shipping_address  | `ShippingAddress` | endereço de entrega (produto físico)      |

### Status

```typescript
type Status =
  | 'created'
  | 'authorized'
  | 'waiting_payment'
  | 'paid'
  | 'handling_products'
  | 'on_carriage'
  | 'delivered'
  | 'cancelled'
  | 'refused'
  | 'invoiced'
  | 'shipment_exception'
  | 'chargeback'
```

### PaymentType

```typescript
type PaymentType =
  | 'creditcard'
  | 'debitcard'
  | 'pix'
  | 'billet'
```

### Product

| Propriedade   | Tipo                  | Descrição                         |
| ---           | ---                   | ---                               |
| code          | `string`              | identificador único do pedido     |
| name          | `number`              | valor total do pedido             |
| plans         | `Array<ProductPlan>`  | valor efetivo do pedido           |

### ProductPlan

| Propriedade   | Tipo              | Descrição                         |
| ---           | ---               | ---                               |
| code          | `string`          | identificador único do pedido     |
| name          | `number`          | valor total do pedido             |
| quantity      | `number` (min: 0) | valor efetivo do pedido           |

### ShippingAddress

| Propriedade   | Tipo          | Descrição                         |
| ---           | ---           | ---                               |
| address       | `string`      | logradouro                        |
| city          | `string`      | cidade                            |
| country       | `string`      | país                              |
| district      | `string`      | bairro                            |
| number        | `string`      | número                            |
| state         | `string`      | UF do brasil (ex.: MG, SP, etc)   |
| zipcode       | `string`      | código postal (ex.: 35588000)     |
| complement    | `string`      | complemento                       |

### ShippingAddress

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

