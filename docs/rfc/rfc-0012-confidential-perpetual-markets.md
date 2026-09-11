# RFC-0012: Confidential Perpetual Markets

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-09-11
- **Updated**: 2026-09-11

## Context and motivation
Perpetual markets require confidential handling of strategy state, position intent, and hedging logic while preserving deterministic policy checks and settlement truth.

## Scope
### In scope
- Confidential intent formation for perpetual positions, hedges, and roll operations.
- Interfaces between confidential strategy execution, market gateways, and settlement systems.
- Proof and disclosure requirements for risk, accounting, and operator review.

### Out of scope
- Specific exchange integrations and venue fee schedules.
- Public market-making strategy optimization.

## Core specification
- Perpetual market strategies with sensitive state **MUST** execute through the confidential execution abstraction when policy marks them as private.
- Margin, leverage, and liquidation checks **MUST** remain deterministic even when strategy inputs are confidential.
- Execution venues **MUST** receive only the minimum information required to place and reconcile orders.
- Confidential strategy results **MUST** emit proofs or attestations sufficient for ledger and settlement acceptance.
- Venue outages or proof failures **MUST** degrade to suspend-or-review rather than silent fallback.

## Security and risk considerations
- Information minimization protects strategy alpha and counterparty-sensitive state.
- Cross-checks between confidential outputs and public reconciliations reduce hidden loss accumulation.
- Venue adapters **SHOULD** enforce anti-replay and nonce discipline.

## Open questions
- Repository-specific rollout sequencing is tracked in the [implementation matrix](../IMPLEMENTATION_MATRIX.md).

## Backward compatibility and versioning
- Breaking changes **MUST** update the RFC revision, identify affected repositories, and include migration guidance.
- Additive clarifications **SHOULD** preserve existing identifiers and normative references when behavior is unchanged.

## Related RFCs and references
- [RFC-0011](./rfc-0011-confidential-execution-abstraction.md)
- [RFC-0013](./rfc-0013-private-liquidation-and-solvency-proofs.md)
- [RFC-0015](./rfc-0015-agentic-markets.md)
- [Threat model](../THREAT_MODEL.md)
