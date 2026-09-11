# RFC-0015: Agentic Markets

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-09-11
- **Updated**: 2026-09-11

## Context and motivation
Market automation needs a canonical control framework for order generation, venue routing, execution, and post-trade accounting under autonomous operation.

## Scope
### In scope
- Order intent lifecycle, venue policy controls, position limits, and reconciliation.
- Shared control primitives between spot, derivatives, and hybrid market actions.
- Human approvals and emergency trading halts.

### Out of scope
- Exchange listing decisions.
- Alpha generation techniques not relevant to control boundaries.

## Core specification
- Market actions **MUST** use the same mandate, policy, reservation, provenance, ledger, and settlement pipeline as payments.
- Venue selection **MUST** be policy-constrained and recorded as part of the intent and execution evidence.
- Position, concentration, and exposure limits **MUST** be checked before and after execution acknowledgement.
- Order amendments and cancels **MUST** preserve linkage to the original intent and reservation state.
- Trading halt, suspend, and revoke controls **MUST** stop new order placement immediately while preserving unwind authority when explicitly granted.

## Security and risk considerations
- Pre-trade and post-trade checks reduce runaway strategy losses.
- Venue adapters **SHOULD** isolate API credentials per strategy or mandate domain.
- Market data or venue outages **MUST** degrade to review or suspend states.

## Open questions
- Repository-specific rollout sequencing is tracked in the [implementation matrix](../IMPLEMENTATION_MATRIX.md).

## Backward compatibility and versioning
- Breaking changes **MUST** update the RFC revision, identify affected repositories, and include migration guidance.
- Additive clarifications **SHOULD** preserve existing identifiers and normative references when behavior is unchanged.

## Related RFCs and references
- [RFC-0009](./rfc-0009-risk-engine-and-policy-dsl.md)
- [RFC-0012](./rfc-0012-confidential-perpetual-markets.md)
- [RFC-0014](./rfc-0014-agentic-payments.md)
- [Threat model](../THREAT_MODEL.md)
