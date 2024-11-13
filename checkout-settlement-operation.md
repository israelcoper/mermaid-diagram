# Checkout settlement operations (Maya)
```mermaid
---
title:
---
flowchart TB;
    A[Update refunded amount]-->B[Issue refund];
    B-- Refund api return non 200 response -->C[Return 422]; 
    B-- Refund api return 200 response but status is not success -->C;
    B-- Refund api return 200 response and status is success -->D[Create transaction record];
    D-->E["Set settlement status to *settled*"];
    E-->F[Return 200];
```

# Checkout settlement operations (Gcash)
```mermaid
---
title:
---
flowchart TB;
    A[Update refunded amount]-->B[Issue refund];
    B-- Refund api return non 200 response -->X[Return 422];
    B-- Refund api return 200 response but status is not success -->D;
    B-- Refund api return 200 response and status is success -->D[Create transaction record];
    D-->E["Set settlement status to *settled*"];
    E-->F[Return 200];
```


# Checkout settlement operations (Xendit)
```mermaid
---
title:
---
flowchart TB;
    A[Update refunded amount]-->B[Issue refund];
    B-- Refund api return non 200 response -->C[Return 422]; 
    B-- Refund api return 200 response but status is not success -->C;
    B-- Refund api return 200 response and status is success -->D[Create transaction record];
    D-->E["Set settlement status to *settling*"];
    E-->F[Return 200];
    F-- Wait for Xendit webhook -->G[Webhook handler will set the terminal state of the settlement status];
```

# Checkout settlement operations (ideal behavior)
```mermaid
---
title:
---
flowchart TB;
    A-- Refund amount is greater than zero -->B[Issue refund];
    A[Calculate refund amount]-- Refund amount is zero -->Y["Set settlement status to *settled*"];
    Y-->H[Return 200];
    B-- Refund api return non 200 response -->D[Create transaction record]; 
    B-- Refund api return 200 response but status is not success -->D;
    B-- Refund api return 200 response and status is success -->D;
    D-- Refund status is not success -->X[Return 422];
    D-- Refund status is success -->Z[Update refunded amount];
    Z-->E["Set settlement status to *settling*"];
    E-->F[Return 200];
    F-- Wait for Payment gateway webhook -->G[Webhook handler will set the terminal state of the settlement status];
```
