# RFC-0005: Programmable Financial Authority

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-09-11
- **Updated**: 2026-09-11

## Context and motivation
Ryvra autonomous finance requires a canonical definition of what authority an agent can exercise, where that authority is rooted, and how it is constrained before any executable financial action occurs.

## Scope
### In scope
- Authority delegation from legal or operational principals into machine-enforceable mandates.
- Binding among mandate versions, smart accounts, policy identifiers, and execution domains.
- Authority lifecycle controls including issuance, review, suspension, revocation, and expiry.

### Out of scope
- Human resources identity proofing workflows.
- Jurisdiction-specific legal drafting beyond canonical protocol control requirements.

## Core specification
- Every autonomous finance action **MUST** execute under an explicit mandate bound to a principal, purpose, scope, and validity interval.
- Authority **MUST NOT** be inferred from model output, frontend state, or tool availability alone.
- A smart account **MUST** be the cryptographic boundary that enforces mandate-linked execution constraints.
- Mandates **MUST** reference the policy set and risk profile required for execution and **MUST** fail closed when those references are missing or stale.
- Authority changes **MUST** be versioned, auditable, and immediately enforceable through suspension or revocation controls.

## Security and risk considerations
- Separation of principal intent from model suggestion limits prompt-driven authority escalation.
- Revocation and expiry **MUST** propagate faster than execution retries and queued actions.
- Break-glass authorities **SHOULD** be narrowly scoped and dual-controlled.

## Open questions
- Repository-specific rollout sequencing is tracked in the [implementation matrix](../IMPLEMENTATION_MATRIX.md).

## Backward compatibility and versioning
- Breaking changes **MUST** update the RFC revision, identify affected repositories, and include migration guidance.
- Additive clarifications **SHOULD** preserve existing identifiers and normative references when behavior is unchanged.

## Related RFCs and references
- [RFC-0006](./rfc-0006-agent-identity-mandates-capabilities.md)
- [RFC-0008](./rfc-0008-financial-intent-and-execution-provenance.md)
- [Architecture principles](../ARCHITECTURE_PRINCIPLES.md)
- [Authorization pipeline](../AUTHORIZATION_PIPELINE.md)
