# RFC-0010: Agent Runtime Architecture

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-09-11
- **Updated**: 2026-09-11

## Context and motivation
The runtime architecture defines how models, tools, state, approvals, and execution services are composed so financial automation remains inspectable and controllable.

## Scope
### In scope
- Control-plane and data-plane boundaries for agent execution.
- Runtime lifecycle, sandboxing, observability, and approval interrupts.
- State handling between reasoning, planning, simulation, and execution stages.

### Out of scope
- Specific model vendor selection.
- Frontend rendering architecture except where it impacts authority boundaries.

## Core specification
- The runtime **MUST** separate intelligence orchestration from authority enforcement and settlement execution.
- Execution-capable stages **MUST** be resumable, observable, and externally interruptible.
- Runtime state **MUST** classify data by sensitivity and prohibit secret material from model context by default.
- Simulation and dry-run paths **SHOULD** share the same policy and reservation hooks as live execution paths.
- Runtime operators **MUST** have immediate suspension and kill-switch controls independent of the active model provider.

## Security and risk considerations
- Sandboxed tool execution reduces breakout and credential theft risk.
- Out-of-band operator controls limit runaway agent exposure.
- Provider substitution **SHOULD** be possible without breaking enforcement boundaries.

## Open questions
- Repository-specific rollout sequencing is tracked in the [implementation matrix](../IMPLEMENTATION_MATRIX.md).

## Backward compatibility and versioning
- Breaking changes **MUST** update the RFC revision, identify affected repositories, and include migration guidance.
- Additive clarifications **SHOULD** preserve existing identifiers and normative references when behavior is unchanged.

## Related RFCs and references
- [RFC-0006](./rfc-0006-agent-identity-mandates-capabilities.md)
- [RFC-0007](./rfc-0007-agent-gateway-and-tool-security.md)
- [RFC-0011](./rfc-0011-confidential-execution-abstraction.md)
- [Architecture principles](../ARCHITECTURE_PRINCIPLES.md)
