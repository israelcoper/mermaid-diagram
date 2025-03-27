# Proposed Maya Payment Flow
```mermaid
---
title:
---
flowchart TB;
    style B fill:#3cb371
    style F1 fill:#ee82ee
    style F2 fill:#ee82ee
    style F3 fill:#ee82ee
    style Y fill:#3cb371
    style Z fill:#ee82ee
    style E fill:#3cb371
    style G fill:#3cb371
    style H fill:#ee82ee
    A["#1. Vault Card"]-->B[POST /maya/payment-cards];
    B-- customer !exist -->F1[POST /payments/v1/customers];
    B-- customer exists -->F2[POST /payments/v1/payment-tokens];
    F1-->F2;
    F2-->F3[POST /payments/v1/customers/:maya_customer_id/cards];
    X["#2. List Vaulted Cards"]-->Y[GET /maya/transactions/cards];
    Y-->Z[GET /payments/v1/customers/:maya_customer_id/cards];
    C["#3. Place Order"];
    C-->E[POST /checkouts];
    E-->G[POST /maya/transactions/make-payment];
    G-->H[POST /payments/v1/customers/:maya_customer_id/cards/:card_token/payments];
    H-->I["#4. Render verificationUrl"];
```
