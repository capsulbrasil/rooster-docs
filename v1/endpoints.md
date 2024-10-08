# Endpoints

## Pedidos

- `POST /api/platform-postback/system/:id`: insere um pedido

Parâmetros da rota:

- `id`: id da integração

Corpo da requisição:

> [!WARNING]
> Cada plano com quantidade diferente deve possuir um código único (ABCD-3, ABCD-5, etc).

> [!WARNING]
> Os valores dos campos "amount", "effective_ammount" e "products.plans.price" devem ser enviados em reais (12.50), não em centavos (1250).

```json
{
  "event": "order:created",
  "order": {
    "token": "2000003508897196",
    "amount": 50,
    "effective_amount": 50,
    "status": "paid",
    "payment_type": "account_money",
    "date_created": "2022-04-08T17:01:32.000-04:00",
    "date_updated": "2022-04-08T17:01:32.000-04:00",
    "billet_link": "https://linkboleto.com.br/643d954ed8503e51cb71b965",
    "billet_code": "34191090652428617393016155530005193260000029700",
    "receiver_name": "Usuário Teste",
    "receiver_document": "99999999999",
    "products": [
      {
        "code": "KWRD94TB6",
        "name": "Produto Teste",
        "plans": {
          "code": "KW1239TB6-3",
          "name": "3 Frascos",
          "price": 12.50,
          "quantity": 3
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
    },
    "commissions": [
      {
        "type": "Co-Produtor",
        "percentage": 35,
        "value": 50,
        "name": "Empresa XXX",
        "email": "empresaxxx@gmail.com",
        "document": "4582361435333345"
      }
    ]
  }
}
```

### Payload

| Propriedade | Tipo        | Descrição                       |
| ----------- | ----------- | ------------------------------- |
| event       | `EventType` | evento de atualização do pedido |
| order       | `Order`     | conteúdo do pedido              |

### EventType

```typescript
type EventType = 
  | 'order:created' 
  | 'order:updated' 
  | 'cart:reminder'
```

### Order

| Propriedade       | Tipo              | Descrição                               |
| ----------------- | ----------------- | --------------------------------------- |
| token             | `string`          | identificador único do pedido           |
| amount            | `number`          | valor total do pedido                   |
| effective_amount  | `number`          | valor efetivo do pedido                 |
| status            | `Status`          | status do pedido                        |
| payment_type      | `PaymentType`     | tipo de pagamento                       |
| date_created      | `string`          | data de criação do pedido               |
| date_updated      | `string`          | data de atualização do pedido           |
| billet_link       | `string`          | link do boleto                          |
| billet_code       | `string`          | código do boleto                        |
| receiver_name     | `string`          | nome do recebedor (produto físico)      |
| receiver_document | `string`          | documento do recebedor (produto físico) |
| products          | `Array<Product>`  | produtos                                |
| customer          | `Customer`        | cliente                                 |
| shipping_address  | `ShippingAddress` | endereço de entrega (produto físico)    |

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

| Propriedade | Tipo                 | Descrição                      |
| ----------- | -------------------- | ------------------------------ |
| name        | `string`             | nome do produto                |
| code        | `string`             | identificador único do produto |
| plans       | `ProductPlan`        | planos do produto              |

### ProductPlan

| Propriedade | Tipo              | Descrição                    |
| ----------- | ----------------- | ---------------------------- |
| name        | `string`          | nome do plano                |
| code        | `string`          | identificador único do plano |
| quantity    | `number` (min: 0) | valor efetivo do pedido      |

### ShippingAddress

| Propriedade | Tipo     | Descrição                       |
| ----------- | -------- | ------------------------------- |
| address     | `string` | logradouro                      |
| city        | `string` | cidade                          |
| country     | `string` | país                            |
| district    | `string` | bairro                          |
| number      | `string` | número                          |
| state       | `string` | UF do brasil (ex.: MG, SP, etc) |
| zipcode     | `string` | código postal (ex.: 35588000)   |

### Commissions

| Propriedade | Tipo              | Descrição                       |
| ----------- | ----------------- | ------------------------------- |
| type        | `string`          | tipo do recebedor               |
| percentage  | `number` (min: 0) | porcentagem recebida            |
| value       | `number` (min: 0) | valor recebido                  |
| name        | `string`          | nome do recebedor               |
| email       | `string`          | email do recebedor              |
| document    | `string`          | documento do recebedor          |
