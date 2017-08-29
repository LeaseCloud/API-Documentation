---
title: Montly API Reference

language_tabs:
toc_footers:
  - <a href='https://www.montly.com'>Montly AB</a>

includes:
  - orders
  - tariffs
  - webhooks

search: false
---

# Introduction

<div class="move-right">
  <h3>Required http header</h3>
</div>

```yaml
Authorization: Bearer [bearer token]
```

Welcome to Montly API reference site. Please feel free to contact us if you have any questions or feedback.

Here you will find everything you need to develop Montly LeaseCloud modules for different e-commerce plattforms or to integrate Montly LeaseCloud in your checkout.

Use this [contact form](https://www.montly.com/#gen-contact-section) to get a API key or give us a call at +46844688110.

Until we have a signed partner agreement you will use a sandbox API key that is fully functional but doesn’t create live orders.

# SDK
* [PHP SDK](https://github.com/MontlyAB/montly-php-sdk)
* [.NET SDK](https://github.com/MontlyAB/montly-dotnet-sdk)

# Plugins
* Woocommerce
* Magento

# Data formats

### Amount
All amounts will be in the smallest currency amount. E.g. 1 SEK = 100 ören, 1 USD = 100 cent

### Strings
The maximum length of a string may be 255 characters.

### Currency
All currencies is in ISO 4217 standard. E.g. SEK, EUR

### Country
All Countries are is in ISO 3166 alpha-2. E.g. se = Sweden, no = Norway.
