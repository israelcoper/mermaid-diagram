# 2C2P Card Tokenization Flow (Redirect)
```mermaid
---
title:
---
flowchart TB;
    style A fill:#3cb371
    style B fill:#ffc0cb
    A[POST /api/v2/two-c-two-p/transactions/payment-redirect];
    A-->B[POST https://sandbox-pgw.2c2p.com/payment/4.3/paymentToken]
    B-->C[Redirect to card input page];
    C-->D[Redirect to OTP page];
    D-->E[2C2P will redirect customer back to merchant app];
```
