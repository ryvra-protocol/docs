# RFC-0008: Financial Intent & Execution Provenance

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-09-11
- **Updated**: 2026-09-11

## Context and motivation
Autonomous finance needs canonical records that explain what was requested, why it was allowed, what executed, and how settlement completed.

## Scope
### In scope
- Intent schemas, provenance identifiers, evidence capture, and replay protection.
- Binding among approvals, policy verdicts, reservations, execution receipts, and ledger events.
- Operator and auditor retrieval expectations.

### Out of scope
- Cold-storage archival systems.
- Analytics use cases that do not affect operational truth.

## Core specification
- Every financial action **MUST** begin with a canonical intent record before execution is attempted.
- Provenance **MUST** chain intent, mandate version, identity attestation, policy verdict, reservation token, execution receipt, ledger entry, and settlement result.
- Idempotency keys and replay windows **MUST** be enforced at the intent and execution layers.
- Human approvals **MUST** be captured as first-class provenance events rather than external notes.
- Missing provenance evidence **MUST** block final settlement acknowledgement.

## Security and risk considerations
- Complete provenance narrows dispute surfaces and supports replay detection.
- Execution references **SHOULD** include immutable hashes of critical decision inputs.
- Retention controls **MUST** preserve auditability without exposing unnecessary sensitive state.

## Open questions
- Repository-specific rollout sequencing is tracked in the [implementation matrix](../IMPLEMENTATION_MATRIX.md).

## Backward compatibility and versioning
- Breaking changes **MUST** update the RFC revision, identify affected repositories, and include migration guidance.
- Additive clarifications **SHOULD** preserve existing identifiers and normative references when behavior is unchanged.

## Related RFCs and references
- [RFC-0005](./rfc-0005-programmable-financial-authority.md)
- [RFC-0009](./rfc-0009-risk-engine-and-policy-dsl.md)
- [RFC-0018](./rfc-0018-database-and-data-ownership-model.md)
- [Authorization pipeline](../AUTHORIZATION_PIPELINE.md)
