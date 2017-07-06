# Webhooks

Define a url endpoint where we will make post requests to with updates

## Order accepted

```http
POST https://example.com/montly/callback/ HTTP/1.1
X-Montly-Version: 1.0.0

{
  "action": "orderUpdate",
  "orderId": 42,
  "event": "accepted"
}
```

When we have accepted an order we will make a post to an defined endpoint
