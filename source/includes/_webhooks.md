# Webhooks

```http
POST https://example.com/montly/callback/ HTTP/1.1
Montly-Version: 1.0.0
Montly-Signature: HMAC SHA-256
Montly-Timestamp: 1499785732


{
  "action": "NAME_OF_ACTION",
  "FIELDS": "FOR ACTION"
}
```

Define a url endpoint where we will make post requests to with updates.

We will make a `POST` request to the endpoint with a JSON body

The signature is with generated with `Montly-Timestamp` and the payload combined with a `.`

### Order accepted

```json
{
  "action": "orderStatus",
  "orderId": 42,
  "status": "[ accepted | denied ]"
}
```

When we have accepted an order we will make a post to an defined endpoint

### Updated tariffs

```json
{
  "action": "tariffs",
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
```

When the tariff changes
