
# Tariff

## Get current tariff

```http
GET /v1/tariffs HTTP/1.1
Authorization: Bearer [bearer token]
```

<div class="move-right">
  <h3>Response body</h3>
</div>

```json
{
  "tariffs": [  
    {  
      "months": 24,
      "tariff": 1.47
    },
    {  
      "months": 36,
      "tariff": 1.04
    }
  ]
}
```
