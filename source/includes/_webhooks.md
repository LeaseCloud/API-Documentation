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

### Events
 * order.accepted
 * order.denied
 * tariff.updated

### Order accepted

```json
{
  "id": "event_sdfgkjshdfg87oihsjdgfb",
  "type": "order.accepted",
  "data": {
    "orderId": 42
  }
}
```

When we have accepted an order we will make a post to an defined endpoint

### Updated tariffs

```json
{
  "id": "event_dsfsdf55ds3dgfb",
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
