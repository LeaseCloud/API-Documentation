---
title: Montly API Reference

language_tabs:
toc_footers:
  - <a href='https://www.montly.com'>Montly AB</a>

includes:
  - orders
  - tariffs
  - webhooks
  - errors

search: false
---

# Introduction

<div class="move-right">
  <h3>Required http header</h3>
</div>

```yaml
Authorization: Bearer [bearer token]
```

Welcome to Montly AB API


# Data formats

### Amount
All amounts will be in the smallest currency amount. E.g. 1 SEK = 100 ören, 1 USD = 100 cent

### Strings
The maximum length of a string may be 255 characters.

### Currency
All currencies is in ISO 4217 standard. E.g. SEK, EUR

### Country
All Countries are is in ISO 3166 alpha-2. E.g. se = Sweden, no = Norway.
