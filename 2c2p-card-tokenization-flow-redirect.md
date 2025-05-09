# 2C2P Card Tokenization Flow (Redirect)
```mermaid
---
title:
---
flowchart TB;
    style C fill:#3cb371
    C[POST /api/v2/two-c-two-p/payment-cards/tokenize-redirect];
    C-->E[Redirect to card input page];
    E-->G[2C2P will redirect customer back to merchant app];
```
