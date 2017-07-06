---
title: Montly API Reference

language_tabs:
toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to Montly AB API

# Orders


## Create a new order

```http
POST /v1/orders HTTPS/1.1
Content-Type: application/json
Authorization: Bearer [bearer token]
```

<div class="move-right">
  <h3>Request body structure</h3>
</div>

```json
{
  "data": {
    "type": "order",
    "attributes": "ORDER OBJECT",
    "relationships": {  
      "item": {  
        "data": [ "ITEM OBJECTS" ]
      }
    }
  }
}
```

<div class="move-right">
  <h3>Request body example</h3>
</div>

```json
{
  "data":  {  
    "type": "order",
    "attributes": {  
      "orderId": "c8e0bda3-dbe0-55ad-8de7-4b341fab49a3",
      "firstName": "Matthew",
      "lastName": "Hunter",
      "company": "Winnie Moran",
      "email": "uc@pokev.dk",
      "phone": "09 61 64 48 49",
      "itemsCount": 2,
      "totalPrice": 962768,
      "VAT": 24440,
      "shipping": 12979,
      "shippingVAT": 11146,
      "customerIp": "131.168.20.70",
      "currency": "SEK",
      "months": 24,
      "billingAddress": "Russell Maldonado",
      "billingCity": "Leona Lindsey",
      "billingState": "Gussie Washington",
      "billingPostcode": "Sally Dean",
      "billingCountry": "Sophia McDaniel",
      "sandboxMode": false,
      "monthlyPrice": 121042,
      "tariff": 2.1,
      "orgNumber": "559089-4308"
    },
    "relationships": {  
      "item": {  
        "data": [  
          {  
            "name": "no",
            "productId": "32832849-23cc-550c-9456-06ea2ff0b55c",
            "quantity": 2,
            "totalPrice": 813726,
            "VAT": 12345
          },
          {  
            "name": "wel",
            "productId": "88624a25-e7e8-5da4-a819-8af8f5079ce2",
            "quantity": 8,
            "totalPrice": 490920,
            "VAT": 5254
          }
        ]
      }
    }
  }
}
```

<div class="move-right">
  <h3>Response body</h3>
</div>

```json
{
  "id": 42
}
```

### HTTP Request

`POST /v1/orders`

### Order object

Parameter | Type        | Required | Description
--------- | ----------- | -------- | -----------
firstName | string | ✔︎
lastName | string | ✔︎
company | string | ✔︎
orgNumber | string | ✔︎ | 000000-0000
email | string | ✔︎
phone | string | ✔︎
itemsCount | integer | ✔︎
totalPrice | integer | ✔︎
VAT | integer | ✔︎
shipping | integer | ✔︎
shippingVAT | integer | ✔︎
currency | enum | ✔︎ | `SEK`
months | integer | ✔︎ |
tariff | decimal | ✔︎ |
customerIp | string | ✔︎ |
billingAddress | string | ✔︎ |
billingAddress2 | string |
billingCity | string | ✔︎ |
billingState | string |
billingPostcode | string | ✔︎ |
billingCountry | string |
shippingFirstName | string |
shippingLastName | string |
shippingCompany | string |
shippingAddress | string |
shippingAddress2 | string |
shippingCity | string |
shippingState | string |
shippingPostcode | string |
shippingCountry | string |
sandboxMode | boolean |
kickback | integer |
monthlyPrice | integer | ✔︎ |
customerMessage | string |

### Item object

Parameter | Type        | Required | Description
--------- | ----------- | -------- | -----------
name | string | ✔︎ |
productId | string | ✔︎ |
quantity | integer | ✔︎ |
totalPrice | integer | ✔︎ |
VAT | integer | ✔︎ |
sku | string | |
variationId | string | |
serialNumber | string | |
