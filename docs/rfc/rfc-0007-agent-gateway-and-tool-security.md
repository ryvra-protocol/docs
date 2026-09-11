# RFC-0007: Agent Gateway & Tool Security

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-09-11
- **Updated**: 2026-09-11

## Context and motivation
The gateway is the choke point between autonomous reasoning and financial side effects; it normalizes requests, authenticates agent identity, and isolates tool execution from direct authority.

## Scope
### In scope
- Gateway admission, tool invocation, response normalization, and policy hooks.
- Tool trust boundaries, output verification, and credential handling.
- Safe failure behavior for synchronous and asynchronous tool execution.

### Out of scope
- Business logic internal to each downstream execution service.
- End-user application routing outside the gateway boundary.

## Core specification
- All autonomous finance requests **MUST** transit through an authenticated gateway before reservation or execution.
- The gateway **MUST** treat model content and tool output as untrusted input until policy and validation checks pass.
- Tool adapters **MUST** declare required credentials, output schemas, retry policy, and side-effect class.
- Direct model-to-chain or model-to-provider execution **MUST NOT** be allowed.
- Gateway audit logs **MUST** bind request payloads, tool outputs, verdicts, and execution references into a single provenance chain.

## Security and risk considerations
- Schema validation and response signing reduce malicious tool output injection.
- Short-lived credentials and brokered secrets **MUST** replace long-lived shared keys.
- Provider-specific integrations **SHOULD** terminate behind adapter interfaces so controls survive vendor changes.

## Open questions
- Repository-specific rollout sequencing is tracked in the [implementation matrix](../IMPLEMENTATION_MATRIX.md).

## Backward compatibility and versioning
- Breaking changes **MUST** update the RFC revision, identify affected repositories, and include migration guidance.
- Additive clarifications **SHOULD** preserve existing identifiers and normative references when behavior is unchanged.

## Related RFCs and references
- [RFC-0006](./rfc-0006-agent-identity-mandates-capabilities.md)
- [RFC-0008](./rfc-0008-financial-intent-and-execution-provenance.md)
- [RFC-0017](./rfc-0017-autonomous-finance-threat-model.md)
- [Threat model](../THREAT_MODEL.md)
