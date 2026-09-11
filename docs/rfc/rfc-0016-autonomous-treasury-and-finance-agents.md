# RFC-0016: Autonomous Treasury / Autonomous Finance Agents

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-09-11
- **Updated**: 2026-09-11

## Context and motivation
Treasury and finance agents coordinate cash, liquidity, hedging, funding, and operational workflows, so they require a consolidated operating model across payment and market domains.

## Scope
### In scope
- Agent classes for treasury, liquidity, hedging, rebalancing, collections, and operational finance workflows.
- Shared control objectives, human approval thresholds, and monitoring expectations.
- Interoperation with payments, markets, ledger, and settlement systems.

### Out of scope
- Corporate accounting policies outside autonomous execution.
- Non-financial agent use cases.

## Core specification
- Autonomous finance agents **MUST** be capability-scoped to their financial domain and prohibited from unbounded general authority.
- Each agent class **MUST** declare allowed intents, approval thresholds, operating hours, and emergency behavior.
- Treasury workflows **SHOULD** reuse canonical reservations to prevent double-spend across simultaneous agents.
- Cross-domain actions such as hedge-and-pay or rebalance-and-settle **MUST** compose through linked intents and provenance rather than opaque internal shortcuts.
- Operators **MUST** have immediate visibility into active agents, queued actions, and suspension state.

## Security and risk considerations
- Capability scoping and linked reservations reduce mandate escalation and double-spend risks.
- Queue visibility and rate limits limit runaway automation.
- Cross-domain orchestration **SHOULD** require stronger approval for first-release production use.

## Open questions
- Repository-specific rollout sequencing is tracked in the [implementation matrix](../IMPLEMENTATION_MATRIX.md).

## Backward compatibility and versioning
- Breaking changes **MUST** update the RFC revision, identify affected repositories, and include migration guidance.
- Additive clarifications **SHOULD** preserve existing identifiers and normative references when behavior is unchanged.

## Related RFCs and references
- [RFC-0005](./rfc-0005-programmable-financial-authority.md)
- [RFC-0010](./rfc-0010-agent-runtime-architecture.md)
- [RFC-0014](./rfc-0014-agentic-payments.md)
- [RFC-0015](./rfc-0015-agentic-markets.md)
