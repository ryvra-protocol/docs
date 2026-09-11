# RFC-0006: Agent Identity, Mandates & Capabilities

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-09-11
- **Updated**: 2026-09-11

## Context and motivation
Autonomous finance depends on distinguishing who the agent is, what authority it has received, and which tools or actions it is capable of invoking at runtime.

## Scope
### In scope
- Agent identity primitives, attestation requirements, and capability descriptors.
- Versioned mandates that bind identity to authority and runtime restrictions.
- Capability scoping for models, tools, accounts, and confidential execution backends.

### Out of scope
- Model training data governance.
- User-interface level role management except where it maps into a mandate.

## Core specification
- Each agent instance **MUST** have a unique, attestable runtime identity and a stable principal binding.
- Capabilities **MUST** be explicitly enumerated and deny-by-default; absence of a capability is a hard execution stop.
- Mandates **MUST** bind permitted capabilities, account scopes, limits, approval thresholds, and expiry semantics.
- Capability grants **SHOULD** distinguish read, simulate, reserve, execute, and administer operations.
- Identity, mandate, and capability records **MUST** be included in provenance for every financial intent.

## Security and risk considerations
- Capability narrowing reduces blast radius for credential theft and malicious tool outputs.
- Attested identities **SHOULD** be rotated without changing mandate history or provenance references.
- Dormant or orphaned agents **MUST** be suspended automatically.

## Open questions
- Repository-specific rollout sequencing is tracked in the [implementation matrix](../IMPLEMENTATION_MATRIX.md).

## Backward compatibility and versioning
- Breaking changes **MUST** update the RFC revision, identify affected repositories, and include migration guidance.
- Additive clarifications **SHOULD** preserve existing identifiers and normative references when behavior is unchanged.

## Related RFCs and references
- [RFC-0005](./rfc-0005-programmable-financial-authority.md)
- [RFC-0007](./rfc-0007-agent-gateway-and-tool-security.md)
- [RFC-0010](./rfc-0010-agent-runtime-architecture.md)
- [Go-live checklist](../GO_LIVE_CHECKLIST.md)
