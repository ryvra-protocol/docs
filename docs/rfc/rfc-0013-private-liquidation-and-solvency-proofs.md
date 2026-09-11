# RFC-0013: Private Liquidation & Solvency Proofs

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-09-11
- **Updated**: 2026-09-11

## Context and motivation
Autonomous finance needs to prove solvency and enforce liquidation controls without unnecessarily revealing sensitive balance-sheet and position state.

## Scope
### In scope
- Private solvency attestations, liquidation triggers, and disclosure thresholds.
- Interfaces from confidential risk checks into ledger and settlement controls.
- Operator escalation and emergency unwind requirements.

### Out of scope
- Bankruptcy, legal recovery, or off-platform claims processes.
- Retail disclosure regimes outside protocol operations.

## Core specification
- Solvency controls **MUST** prove that obligations remain covered before leveraged or credit-sensitive actions finalize.
- Liquidation paths **MUST** preserve confidentiality until disclosure is required for safe market execution or governance review.
- Private liquidation triggers **MUST** feed the same reservation, provenance, and settlement controls as normal execution.
- Incomplete proofs or inconsistent reconciliations **MUST** halt new risk-taking and raise an operator escalation.
- Emergency unwinds **SHOULD** support partial disclosure modes that reveal only what execution and audit require.

## Security and risk considerations
- Failing closed on proof gaps reduces hidden insolvency risk.
- Escalation thresholds **SHOULD** be governed separately from normal strategy limits.
- Proof verification code **MUST** be independently change-controlled from strategy logic.

## Open questions
- Repository-specific rollout sequencing is tracked in the [implementation matrix](../IMPLEMENTATION_MATRIX.md).

## Backward compatibility and versioning
- Breaking changes **MUST** update the RFC revision, identify affected repositories, and include migration guidance.
- Additive clarifications **SHOULD** preserve existing identifiers and normative references when behavior is unchanged.

## Related RFCs and references
- [RFC-0009](./rfc-0009-risk-engine-and-policy-dsl.md)
- [RFC-0011](./rfc-0011-confidential-execution-abstraction.md)
- [RFC-0012](./rfc-0012-confidential-perpetual-markets.md)
- [Go-live checklist](../GO_LIVE_CHECKLIST.md)
