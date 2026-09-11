# RFC-0014: Agentic Payments

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-09-11
- **Updated**: 2026-09-11

## Context and motivation
Payment automation must allow agents to initiate, reserve, execute, and reconcile payouts without bypassing mandate, risk, or settlement controls.

## Scope
### In scope
- Payment intents, payee controls, approval paths, and settlement reconciliation.
- Rail selection, fallback handling, and idempotent retry requirements.
- Integration between smart accounts, pay rails, and ledger truth.

### Out of scope
- Consumer wallet user experience flows.
- Jurisdiction-specific payment licensing analysis.

## Core specification
- Payment requests **MUST** originate as canonical financial intents bound to a mandate and beneficiary policy.
- Reservation **MUST** precede payment execution so available balances and limits are locked before side effects occur.
- Rail adapters **MUST** enforce beneficiary verification, idempotency keys, and deterministic retry behavior.
- Payment execution **MUST** reconcile back into the ledger before final settlement is recorded.
- Fallback to an alternate rail **MUST** create a new provenance-linked execution attempt rather than mutating the original receipt.

## Security and risk considerations
- Beneficiary allowlists and mandate-scoped payout limits reduce credential theft impact.
- Out-of-band approvals **SHOULD** be required for first-time or unusually large beneficiaries.
- Stale reservations **MUST** expire automatically and release balances.

## Open questions
- Repository-specific rollout sequencing is tracked in the [implementation matrix](../IMPLEMENTATION_MATRIX.md).

## Backward compatibility and versioning
- Breaking changes **MUST** update the RFC revision, identify affected repositories, and include migration guidance.
- Additive clarifications **SHOULD** preserve existing identifiers and normative references when behavior is unchanged.

## Related RFCs and references
- [RFC-0008](./rfc-0008-financial-intent-and-execution-provenance.md)
- [RFC-0009](./rfc-0009-risk-engine-and-policy-dsl.md)
- [RFC-0015](./rfc-0015-agentic-markets.md)
- [Authorization pipeline](../AUTHORIZATION_PIPELINE.md)
