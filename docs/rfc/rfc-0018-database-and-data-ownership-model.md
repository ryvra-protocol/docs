# RFC-0018: Database & Data Ownership Model

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-09-11
- **Updated**: 2026-09-11

## Context and motivation
A clear ownership model is required so autonomous finance data is written to the right authority boundary, stays auditable, and does not leak secret material into the wrong systems.

## Scope
### In scope
- System-of-record boundaries for mandates, policies, reservations, execution receipts, ledger entries, settlements, and confidential state.
- Write authority rules for repositories and operational services.
- Explicit anti-patterns that must be prohibited in all implementations.

### Out of scope
- Warehouse schemas for analytical experimentation.
- UI-local caching that does not create authority or truth.

## Core specification
- Each canonical data object **MUST** have a single system of record and a named owning repository or service boundary.
- Private keys **MUST NOT** be stored in PostgreSQL or other general application databases.
- Frontends **MUST NOT** create authority, approve execution, or hold final ledger truth.
- AI runtimes **MUST NOT** execute directly on-chain or against payment rails without gateway, policy, reservation, and smart-account enforcement.
- Confidential execution backends **SHOULD** be replaceable without replatforming the private execution core or changing settlement truth.

## Security and risk considerations
- Single-writer authority limits race conditions and hidden state divergence.
- Secret segregation reduces credential theft and insider misuse risk.
- Provider-neutral abstractions reduce lock-in and recovery risk after provider compromise.

## Open questions
- Repository-specific rollout sequencing is tracked in the [implementation matrix](../IMPLEMENTATION_MATRIX.md).

## Backward compatibility and versioning
- Breaking changes **MUST** update the RFC revision, identify affected repositories, and include migration guidance.
- Additive clarifications **SHOULD** preserve existing identifiers and normative references when behavior is unchanged.

## Related RFCs and references
- [RFC-0008](./rfc-0008-financial-intent-and-execution-provenance.md)
- [RFC-0011](./rfc-0011-confidential-execution-abstraction.md)
- [RFC-0017](./rfc-0017-autonomous-finance-threat-model.md)
- [Data ownership model](../DATA_OWNERSHIP_MODEL.md)
