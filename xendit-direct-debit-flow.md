# Checkout settlement operations (Maya)
```mermaid
---
title:
---
flowchart TB;
    A[Create Xendit Customer]-->B[Create Payment Method];
    B-- Select payment method -->C[List Active Payment Methods];
    C-- Hit Checkout button -->D[Create checkout record];
    D-- Make payment -->[Issue Payment request];
```
