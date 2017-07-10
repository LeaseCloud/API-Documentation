# Webhooks

Define a url endpoint where we will make post requests to with updates

## Order accepted

```http
POST https://example.com/montly/callback/ HTTP/1.1
X-Montly-Version: 1.0.0

JWT_PAYLOAD
```

> Events

```json
{
  "action": "orderStatus",
  "orderId": 42,
  "status": "[ accepted | denied ]"
}
```
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

When we have accepted an order we will make a post to an defined endpoint
