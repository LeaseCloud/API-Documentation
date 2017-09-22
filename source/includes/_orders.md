# Orders

## Create a new order

```http
POST /v1/orders HTTP/1.1
Content-Type: application/json
Authorization: Bearer [bearer token]
```

<div class="move-right">
  <h3>Request body example</h3>
</div>

```json
{
  "orderId": "c8e0bda3-dbe0-55ad-8de7-4b341fab49a3",
  "firstName": "Matthew",
  "lastName": "Hunter",
  "company": "Montly AB",
  "orgNumber": "559089-4308",
  "email": "hello@montly.com",
  "authorizedSignatory": null,
  "phone": "09 61 64 48 49",
  "customerIp": "131.168.20.70",
  "totalAmount": 1010000,
  "VAT": 252500,
  "shippingAmount": 10000,
  "shippingVAT": 2500,
  "currency": "SEK",
  "months": 24,
  "tariff": 1.1,
  "billing": {
    "address": "Mystreet 121",
    "address2": null,
    "city": "Stockholm",
    "state": null,
    "postalCode": "12345",
    "country": "SE"
  },
  "shipping": {
    "firstName": null,
    "lastName": null,
    "company": null,
    "address": null,
    "address2": null,
    "city": null,
    "state": null,
    "postalCode": null,
    "country": null,
  },
  "customerMessage": "I like cookies!",
  "items": [
    {
      "name": "Shiny new phone",
      "productId": "32832849-23cc-550c-9456-06ea2ff0b55c",
      "quantity": 2,
      "unitAmount": 250000,
      "totalAmount": 500000,
      "VAT": 125000
    },
    {
      "name": "40\" TV",
      "productId": "88624a25-e7e8-5da4-a819-8af8f5079ce2",
      "quantity": 1,
      "unitAmount": 500000,
      "totalAmount": 500000,
      "VAT": 125000
    }
  ]
}
```

<div class="move-right">
  <h3>Response body</h3>
</div>

```json
{
  "orderId": "c8e0bda3-dbe0-55ad-8de7-4b341fab49a3",
  "monthlyAmount": 50500
}
```

<div class="move-right">
  <h3>Error response body</h3>
</div>

```json
{
  "error": {
    "code": "InvalidOrder",
    "message": "Validation error",
    "fields": [
      {
        "title": "notNull Violation",
        "message": "orderId cannot be null on orderId",
        "field": "orderId"
      },
      {
        "message": "A valid organisation number is required e.g. xxxxxx-xxxx on orgNumber",
        "field": "orgNumber"
      }
    ]
  }
}
```

### HTTP Request

`POST /v1/orders`

### Order object

Parameter | Type        | Required | Description
--------- | ----------- | -------- | -----------
orderId | string | ✔︎ | A unique ID for the order
firstName | string | ✔︎ | Given name
lastName | string | ✔︎ | Family name
company | string | ✔︎ | Name of the company
orgNumber | string | ✔︎ | Company organisation number 000000-0000
email | string | ✔︎ | Valid email address
authorizedSignatory | string | | Email of the person authorized to sign the contract
phone | string | ✔︎ | Phone number
customerIp | string | ✔︎ | IP of the customer (for extra fraud check)
totalAmount | integer | ✔︎ | Total amount the customer will pay Ex. VAT <br> Minimum 6000 * 100
VAT | integer | ✔︎ | Total VAT amount
shippingAmount | integer | ✔︎ | The shipping cost
shippingVAT | integer | ✔︎ | The shipping cost VAT
currency | enum | ✔︎ | In which currency is the amounts. We only support `SEK` at the moment
months | integer | ✔︎ | How many months the customer want to lease for
tariff | decimal | ✔︎ | What was the current tariff when the purchase
billing | object | ✔︎ | An object containing the billing fields below
 • address | string | ✔︎ | The street address
 • address2 | string | | Second street address line
 • city | string | ✔︎ | City
 • state | string | | State if applicable
 • postalCode | string | ✔︎ | Postal code
 • country | string | ✔︎ | Country 2 letter code e.g. SE
shipping | object | | An object containing the sipping fields below
 • firstName | string | | Given name
 • lastName | string | | Family name
 • company | string | | Company name
 • address | string | | Street address
 • address2 | string | | Street address line 2
 • city | string | | City
 • state | string | | State if applicable
 • postalCode | string | | Postal code
 • country | string | | Country 2 letter code e.g. SE
customerMessage | string | | If the user left a custom message
items | Item object | ✔︎ | See below

### Item object

Parameter | Type        | Required | Description
--------- | ----------- | -------- | -----------
name | string | ✔︎ | Name / title of the product
productId | string | ✔︎ | Product id
quantity | integer | ✔︎ | Quantity
unitAmount | integer | ✔︎ | Price for a single unit ex VAT
totalAmount | integer | ✔︎ | Total amount (quantity * unitAmount) ex VAT
VAT | integer | ✔︎ | VAT for the total amount
sku | string | | Stock Keeping Unit
variationId | string | | Variation id
serialNumber | string | | Serial number of the product

<!-- -->

## Cancel an order

```http
POST /v1/orders/{orderId}/cancel HTTP/1.1
Authorization: Bearer [bearer token]
```

To cancel an order make a `POST` request `/v1/orders/{orderId}/cancel`
which will respond with 200 and an empty body

An order can be canceled until the user has signed the order


## Order shipped

```http
POST /v1/orders/{orderId}/shipped HTTP/1.1
Authorization: Bearer [bearer token]
```

<div class="move-right">
  <h3>(Optional) Request body example</h3>
</div>

```json
{
  "shippedAt": "2017-07-20T13:37:00.000Z"
}
```

Make a `POST` request to `/v1/orders/{orderId}/shipped` when an order has been shipped.
When the request is received we will set the current time as the shipped date
and time but you can send the body `shippedAt` and ISO-8601 date to override the date.

We will then send a confirmation email where the customer sign that they
have received the package and the order is completed.


## Get order status

```http
GET /v1/orders/{orderId}/status HTTP/1.1
Authorization: Bearer [bearer token]
```

```json
{
  "status": "pending"
}
```

Get the current status for an order

Status | Description
------ | -----------
pending | The order has arrived and are being processed
declined | The order has been declined
accepted | The order has been accepted and are waiting for the customer to sign the agreement
signed | The customer has signed and the order can be shipped
deliveryApproved | The customer has signed that the order has arrived
cancelled | The order has been cancelled
