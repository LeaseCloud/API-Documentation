# Webhooks

```http
POST https://example.com/montly/callback/ HTTP/1.1
X-Montly-Version: 1.0.0

JWT_PAYLOAD
```

Define a url endpoint where we will make post requests to with updates.

We will make a `POST` request to the endpoint and the body is a [JSON Web Token (JWT)](https://jwt.io/)

The JWT secret will be your API-key

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
