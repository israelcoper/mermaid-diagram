# Current Maya Payment Flow
```mermaid
---
title:
---
flowchart LR;
    A[POST /payments/v1/payment-token];
    B[GET /tokenized-transactions/cards]-- customer !exist -->C[Paymaya::Customer::Create];
    B-- customer exist -->D[Paymaya::Customer::Card::List];
    E[POST /checkouts];
    F[POST /tokenized-transactions/make-payment];
    F-- customer !exists -->G[Paymaya::Customer::Create];
    G-- customer !linkToCard -->I[Paymaya::Customer::Card::Link];
    I-->J;
    G-- customer linkToCard -->J[Paymaya::Payment::Create];
    F-- customer exists -->H[Paymaya::Customer::Show];
    H-- customer !linkToCard -->I;
    H-- customer linkToCard -->J;
```