# Authorization pipeline

This document defines the canonical autonomous finance control flow from agent reasoning to final settlement.

## Primary control flow

```mermaid
sequenceDiagram
    participant Agent as Agent runtime
    participant Gateway as Agent gateway
    participant Policy as Policy and risk engine
    participant Reserve as Reservation service
    participant Exec as Execution adapter
    participant Ledger as Ledger
    participant Settle as Settlement

    Agent->>Gateway: Submit financial intent + mandate reference
    Gateway->>Policy: Validate identity, capability, mandate, and policy inputs
    Policy-->>Gateway: ALLOW / DENY / REVIEW / RESERVE verdict
    Gateway->>Reserve: Create or confirm reservation
    Reserve-->>Gateway: Reservation token or rejection
    Gateway->>Exec: Execute within smart-account boundary
    Exec-->>Gateway: Execution receipt + external references
    Gateway->>Ledger: Post intent, verdict, reservation, and execution entries
    Ledger->>Settle: Reconcile and finalize settlement state
    Settle-->>Ledger: Final status and settlement evidence
    Ledger-->>Gateway: Canonical economic truth updated
    Gateway-->>Agent: Outcome + provenance reference
```

## Stage narrative

1. **Agent to gateway**: the agent submits a canonical intent, never a direct executable side effect.
2. **Gateway to policy and risk**: the gateway authenticates the agent, loads the versioned mandate, validates capabilities, and runs deterministic policy checks.
3. **Reservation**: available balances, limits, and concurrency-sensitive resources are reserved before execution starts.
4. **Execution**: side effects occur only through approved adapters and smart-account controls.
5. **Ledger**: all accepted attempts are recorded in the ledger, including denied or reviewed outcomes when they affect accountability.
6. **Settlement**: settlement completes the state transition and produces finality evidence.
7. **Provenance**: every stage emits identifiers that chain back to the original intent.

## Control invariants

- No direct AI-to-chain execution.
- No execution without a valid mandate and deterministic policy pass.
- No settlement finality without ledger reconciliation and provenance completeness.
- No silent fallback from confidential to non-confidential execution when confidentiality is required.

## Emergency flows

```mermaid
flowchart TD
    Detect[Alert or operator concern] --> Suspend[Suspend agent or mandate]
    Suspend --> QueueStop[Stop new reservations and executions]
    QueueStop --> Review[Review in-flight reservations and receipts]
    Review --> Revoke{Revoke authority?}
    Revoke -- Yes --> RevokeMandate[Revoke mandate or capability set]
    RevokeMandate --> Unwind[Allow only approved unwind actions]
    Revoke -- No --> ResumeCheck[Validate controls and evidence]
    Unwind --> ResumeCheck
    ResumeCheck --> Resume{Safe to resume?}
    Resume -- Yes --> Reinstate[Reinstate with new versioned mandate]
    Resume -- No --> KeepSuspended[Remain suspended and escalate]
```

### Emergency requirements

- Suspension must stop new reservations immediately.
- Revocation must invalidate queued or retryable executions that depend on the revoked authority.
- Kill switches must be reachable outside the active model provider and runtime session.
- Approved unwind authority must be narrower than normal operating authority.

## Human-in-the-loop approval path

```mermaid
sequenceDiagram
    participant Agent as Agent runtime
    participant Gateway as Agent gateway
    participant Policy as Policy and risk engine
    participant Approver as Human approver
    participant Reserve as Reservation service
    participant Exec as Execution adapter

    Agent->>Gateway: Submit intent
    Gateway->>Policy: Evaluate intent
    Policy-->>Gateway: REVIEW verdict
    Gateway->>Approver: Request approval with provenance package
    Approver-->>Gateway: Approve, deny, or modify threshold policy
    Gateway->>Policy: Re-evaluate with approval evidence
    Policy-->>Gateway: ALLOW or DENY
    Gateway->>Reserve: Create reservation if allowed
    Gateway->>Exec: Execute if reservation succeeds
```

### Approval requirements

- Human approval must be captured as provenance, not as an out-of-band message.
- Approval may narrow authority, but it must not broaden authority beyond the active mandate.
- Time-bounded approvals should expire automatically if execution does not begin within the approved window.
