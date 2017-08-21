# Webhooks

```http
POST https://example.com/montly/callback/ HTTP/1.1
Montly-Version: 1.0.0
Montly-Signature: t=1499785732,v1=[HMAC_SHA-256_PAYLOAD],v1=[HMAC_SHA-256_PAYLOAD_OLD]

{
  "id": "UNIQUE_EVENT_ID"
  "type": "NAME_OF_ACTION",
  "data": {
    "FIELDS": "FOR ACTION"
  }
}
```

```php
<?php hash_hmac("sha256", "${TIMESTAMP}.${PAYLOAD}", WEBHOOK_SECRET);
```

Define a url endpoint where we will make post requests to with updates.

We will make a `POST` request to the endpoint with a JSON body

The signature is with generated with the timestamp found in the `Montly-Signature` header combined with a `.` and the `payload`

We will make up 12 attempts to deliver the webhook with exponential delay up to 7 days from first try.
Returns 200 http status for success else we are assuming it failed.

### Events
 * order.accepted
 * order.declined
 * order.signed
 * order.deliveryApproved
 * tariff.updated

### Order accepted

```json
{
  "id": "evt:sdfgkjshdfg87oihsjdgfb",
  "type": "order.accepted",
  "data": {
    "orderId": 42
  }
}
```

When we have accepted an order and awaiting the customer to sign the agreement

### Order declined

```json
{
  "id": "evt:askjshdfg54fsjdgfb",
  "type": "order.declined",
  "data": {
    "orderId": 42,
    "reason": "Customer is not credit worthy"
  }
}
```

The order is declined

### Order signed

```json
{
  "id": "evt:sdfgkjshdfg87oihsjdgfb",
  "type": "order.signed",
  "data": {
    "orderId": 42
  }
}
```

The customer has signed and the shop can ship the products

### Order delivery has been approved

```json
{
  "id": "evt:sdfgkjshdfg87oihsjdgfb",
  "type": "order.deliveryApproved",
  "data": {
    "orderId": 42
  }
}
```

The customer has confirmed that the products has arrived

### Updated tariffs

```json
{
  "id": "evt:dsfsdf55ds3dgfb",
  "type": "tariff.updated",
  "data": {
    "tariffs": [  
      {  
        "months": 24,
        "tariff": 1.51
      },
      {  
        "months": 36,
        "tariff": 1.01
      }
    ]
  }
}
```

When the tariff changes
