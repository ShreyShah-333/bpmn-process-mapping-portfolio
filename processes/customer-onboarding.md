# Customer Onboarding Process

## Business Objective
Move a new customer from signed agreement to fully active account with accurate records, correct system access, and a positive first-touch experience, while satisfying KYC/compliance checks.

## Swimlanes (Roles)
- Sales
- Onboarding Specialist
- Compliance / KYC
- IT / Systems
- Customer

## BPMN-Style Flow

```mermaid
flowchart TD
    subgraph Sales
    A([Start: Contract Signed]) --> B[Handoff Package to Onboarding]
    end

    subgraph Onboarding
    B --> C[Create Customer Record in CRM]
    C --> D[Collect KYC Documents]
    end

    subgraph Compliance
    D --> E{KYC Verification Passed?}
    E -->|No| F[Request Additional Documents]
    F --> D
    E -->|Yes| G[Approve Account Activation]
    end

    subgraph IT
    G --> H[Provision System Access / Credentials]
    H --> I[Configure Billing & Services]
    end

    subgraph Customer
    I --> J[Welcome Call / Orientation]
    J --> K([End: Account Active])
    end
```

## Key Decision Points
- KYC verification gateway ensures no account is activated without passing compliance checks.
- Escalation path exists for incomplete documentation, looping back to the customer without restarting the whole process.

## Exception Handling
- Failed KYC checks trigger a document request loop rather than process termination.
- Provisioning failures are logged and routed to IT support queue for same-day resolution.

## KPIs Tracked
- Time-to-activate (contract signature to active account)
- KYC first-pass approval rate
- Onboarding satisfaction score (post welcome call survey)

## Improvement Opportunities Identified
- Pre-populate KYC forms using data already captured during the sales stage to reduce customer effort.
- Parallelize IT provisioning with compliance review where policy allows, instead of running them sequentially.
