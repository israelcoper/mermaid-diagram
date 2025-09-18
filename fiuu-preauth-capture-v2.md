# Scenario 1: Normal pre-auth/capture
```mermaid
---
title:
---
flowchart TB;
    style B1 fill:#3cb371
    style C1 fill:#3cb371
    style D1 fill:#ee82ee

    style B2 fill:#3cb371
    style C2 fill:#ee82ee

    style B3 fill:#3cb371
    style C3 fill:#ee82ee

    A1["#1. Place order"]-->B1[POST /api/v2/checkouts];
    B1-->C1[POST /api/v2/fiuu/transactions/pre-auth];
    C1-->D1[POST /RMS/API/Direct/1.4.0/index.php];
    D1--Failure-->D11[Fail checkout];
    D1--Success-->D12[Activate checkout];
    D11-->D111[Webhook handler];
    D12-->D121[Webhook handler];

    A2["#2A. Complete Job order"]-->B2[POST /api/v1/job-orders/:id/complete];
    B2-->C2[POST /RMS/API/capstxn/index.php];
    C2--Failure-->D2[What to do?];
    C2--Success-->E2[Successful Capture and job order completion];
    D2-->D21[Webhook handler];
    E2-->E21[Webhook handler];

    A3["#2B. Cancel job order"]-->B3[POST /api/v1/job-orders/:id/cancel];
    B3-->C3[POST /RMS/API/refundAPI/refund.php];
    C3--Failure-->D3[What to do?];
    C3--Success-->E3[Successful Reversal of pre-auth and job order cancellation];
    D3-->D31[Webhook handler];
    E3-->E31[Webhook handler];
```

# Scenario 2: Pre-auth amount > Capture amount
```mermaid
---
title:
---
flowchart TB;
    style B1 fill:#3cb371
    style C1 fill:#3cb371
    style D1 fill:#ee82ee

    style B2 fill:#3cb371
    style C2 fill:#ee82ee

    style B3 fill:#3cb371
    style C3 fill:#ee82ee

    A1["#1. Place order"]-->B1[POST /api/v2/checkouts];
    B1-->C1[POST /api/v2/fiuu/transactions/pre-auth];
    C1-->D1[POST /RMS/API/Direct/1.4.0/index.php];
    D1--Failure-->D11[Fail checkout];
    D1--Success-->D12[Activate checkout];
    D11-->D111[Webhook handler];
    D12-->D121[Webhook handler];

    A2["#2A. Complete Job order"]-->B2[POST /api/v1/job-orders/:id/complete];
    B2-->C2[POST /RMS/API/capstxn/index.php];
    C2--Failure-->D2[What to do?];
    C2--Success-->E2[Successful Capture and job order completion];
    D2-->D21[Webhook handler];
    E2-->E21[Webhook handler];

    A3["#2B. Cancel job order"]-->B3[POST /api/v1/job-orders/:id/cancel];
    B3-->C3[POST /RMS/API/refundAPI/refund.php];
    C3--Failure-->D3[What to do?];
    C3--Success-->E3[Successful Reversal of pre-auth and job order cancellation];
    D3-->D31[Webhook handler];
    E3-->E31[Webhook handler];
```

# Scenario 3: Pre-auth amount < Capture amount (Exceeded amount)
```mermaid
---
title:
---
flowchart TB;
    style B1 fill:#3cb371
    style C1 fill:#3cb371
    style D1 fill:#ee82ee

    style B2 fill:#3cb371
    style C2 fill:#ee82ee
    style E22 fill:#ee82ee

    style B3 fill:#3cb371
    style C3 fill:#ee82ee

    style B4 fill:#3cb371
    style C4 fill:#ee82ee

    A1["#1. Place order"]-->B1[POST /api/v2/checkouts];
    B1-->C1[POST /api/v2/fiuu/transactions/pre-auth];
    C1-->D1[POST /RMS/API/Direct/1.4.0/index.php];
    D1--Failure-->D11[Fail checkout];
    D1--Success-->D12[Activate checkout];
    D11-->D111[Webhook handler];
    D12-->D121[Webhook handler];

    A2["#2. Shopping complete"]-->B2[PUT /api/v1/job-orders/:id];
    B2-->C2[POST /RMS/API/refundAPI/refund.php];
    C2--Failure-->D2[What to do?];
    C2--Success-->E2[Successful Reversal of previous pre-auth];
    D2-->D21[Webhook handler];
    E2-->E21[Webhook handler];
    E21-->E22[POST /RMS/API/Direct/1.4.0/index.php];
    E22--Failure-->E23[What to do?];
    E22--Success-->E24[Successful New pre-auth];
    E23-->E231[Webhook handler];
    E24-->E241[Webhook handler];

    A3["#3A. Complete Job order"]-->B3[POST /api/v1/job-orders/:id/complete];
    B3-->C3[POST /RMS/API/capstxn/index.php];
    C3--Failure-->D3[What to do?];
    C3--Success-->E3[Successful Capture and job order completion];
    D3-->D31[Webhook handler];
    E3-->E31[Webhook handler];

    A4["#3B. Cancel job order"]-->B4[POST /api/v1/job-orders/:id/cancel];
    B4-->C4[POST /RMS/API/refundAPI/refund.php];
    C4--Failure-->D4[What to do?];
    C4--Success-->E4[Successful Reversal of pre-auth and job order cancellation];
    D4-->D41[Webhook handler];
    E4-->E41[Webhook handler];
```
