# Procure-to-Pay (P2P) Process

## Business Objective
Standardize how the organization requests, approves, receives, and pays for goods and services, ensuring budget compliance, vendor accountability, and audit-ready financial records.

## Swimlanes (Roles)
- Requester (Business Unit)
- Procurement Team
- Approving Manager
- Vendor
- Finance / Accounts Payable

## BPMN-Style Flow

```mermaid
flowchart TD
    subgraph Requester
    A([Start: Need Identified]) --> B[Create Purchase Requisition]
    end

    subgraph Procurement
    B --> C{Value > Approval Threshold?}
    C -->|Yes| D[Route to Manager for Approval]
    C -->|No| E[Create Purchase Order]
    D --> F{Approved?}
    F -->|Yes| E
    F -->|No| Z([End: Requisition Rejected])
    E --> G[Send PO to Vendor]
    end

    subgraph Vendor
    G --> H[Deliver Goods / Perform Service]
    H --> I[Submit Invoice]
    end

    subgraph Finance
    I --> J[Three-Way Match: PO vs GRN vs Invoice]
    J --> K{Match Successful?}
    K -->|Yes| L[Process Payment]
    K -->|No| M[Raise Exception / Dispute with Vendor]
    M --> J
    L --> N([End: Payment Completed])
    end
```

## Key Decision Points
- Approval threshold check determines whether manager sign-off is required before a purchase order is issued.
- Three-way match (purchase order, goods receipt note, invoice) gates payment release and catches discrepancies early.

## Exception Handling
- Rejected requisitions are returned to the requester with reason codes.
- Invoice mismatches trigger a dispute sub-process with the vendor before payment is reprocessed.

## KPIs Tracked
- Requisition-to-PO cycle time
- Invoice match rate (first-pass yield)
- Days payable outstanding (DPO)

## Improvement Opportunities Identified
- Introduce auto-approval for low-value, pre-approved vendor categories to reduce cycle time.
- Automate three-way matching using OCR-based invoice capture to reduce manual exceptions.
