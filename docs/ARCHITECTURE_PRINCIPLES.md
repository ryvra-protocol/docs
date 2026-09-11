# Architecture principles

These principles are canonical for Ryvra programmable and autonomous finance.

## Canonical principles

1. model is intelligence
2. mandate is authority
3. policy is control
4. smart account is cryptographic boundary
5. ledger is economic truth
6. settlement is finality
7. provenance is accountability
8. confidential execution protects sensitive state

## Principle meaning

### model is intelligence
Models may reason, summarize, and propose actions, but they do not grant themselves authority or bypass deterministic controls.

### mandate is authority
A mandate is the source of executable authority. Every agent action must trace to a versioned mandate owned by an accountable principal.

### policy is control
Policy and risk engines convert broad authority into deterministic allow, deny, reserve, review, or escalate decisions.

### smart account is cryptographic boundary
Smart accounts enforce the final signing and execution boundary. They bind execution to the approved authority model instead of trusting application code alone.

### ledger is economic truth
The ledger is the canonical record of obligations, reservations, balances, and reconciled financial state.

### settlement is finality
Execution is not complete until settlement succeeds or fails through the canonical state machine and downstream reconciliations.

### provenance is accountability
Every step from intent through settlement must be explainable, attributable, and reviewable by operators, auditors, and governance.

### confidential execution protects sensitive state
Sensitive treasury, market, and counterparty state belongs inside a replaceable confidential execution boundary, not in prompts, frontends, or general-purpose databases.

## Design consequences

- Authority never originates from model output.
- Control points must fail closed when mandates, policies, reservations, or provenance are missing.
- Private execution capabilities must remain portable across providers.
- Human operators must be able to suspend or revoke execution independently of the active runtime.
