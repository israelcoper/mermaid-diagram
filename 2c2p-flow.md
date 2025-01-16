# 2C2P Payment Flow
```mermaid
---
title:
---
flowchart TB;
    style A0 fill:#ee82ee
    style A1 fill:#3cb371
    style C fill:#ee82ee
    style D0 fill:#ee82ee
    style D1 fill:#3cb371
    A0[PUT /api/v1/customer-profiles/:id/find-or-create-2c2p-customer]-->A1[POST //sandbox-pgw.2c2p.com/customertoken/3.0/CustomerToken/add];
    C[POST /checkouts]-->D0[POST /2c2p/transactions/make-payment];
    D0-->D1[POST //sandbox-pgw.2c2p.com/payment/4.3/paymentToken];
```
