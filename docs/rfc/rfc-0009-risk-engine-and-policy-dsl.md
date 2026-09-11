# RFC-0009: Risk Engine & Policy DSL

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-09-11
- **Updated**: 2026-09-11

## Context and motivation
A deterministic policy and risk layer is required so autonomous finance decisions are explainable, reviewable, and independent of model improvisation.

## Scope
### In scope
- Policy DSL shape, evaluation order, deterministic execution, and verdict semantics.
- Risk checks for limits, concentration, liquidity, solvency, and escalation.
- Versioning and rollout controls for policies and scoring inputs.

### Out of scope
- Machine-learning model training for predictive risk features.
- Manual exception workflows that never affect execution paths.

## Core specification
- Policy and risk evaluation **MUST** be deterministic for the same versioned inputs.
- The DSL **MUST** support deny, allow, reserve, review, and escalate outcomes with explicit reasons.
- Policy changes **MUST** be versioned, code-reviewed, and attributable to a named authority.
- Risk inputs **MUST** identify freshness, source system, and fallback behavior.
- Execution **MUST NOT** proceed when required policy or risk components are unavailable or non-deterministic.

## Security and risk considerations
- Change control and immutable evaluation traces limit covert policy manipulation.
- Fail-closed evaluation reduces exposure during provider or data outages.
- Dual control **SHOULD** be required for policy changes that expand authority or raise limits.

## Open questions
- Repository-specific rollout sequencing is tracked in the [implementation matrix](../IMPLEMENTATION_MATRIX.md).

## Backward compatibility and versioning
- Breaking changes **MUST** update the RFC revision, identify affected repositories, and include migration guidance.
- Additive clarifications **SHOULD** preserve existing identifiers and normative references when behavior is unchanged.

## Related RFCs and references
- [RFC-0005](./rfc-0005-programmable-financial-authority.md)
- [RFC-0008](./rfc-0008-financial-intent-and-execution-provenance.md)
- [RFC-0017](./rfc-0017-autonomous-finance-threat-model.md)
- [Threat model](../THREAT_MODEL.md)
