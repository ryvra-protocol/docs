# Ryvra Docs

Ryvra Docs is the canonical source of truth for Ryvra Protocol specifications, governance, and operational guidance.

## Canonical navigation

- [RFC index](./docs/rfc/README.md)
- [Implementation matrix](./docs/IMPLEMENTATION_MATRIX.md)
- [Architecture principles](./docs/ARCHITECTURE_PRINCIPLES.md)
- [Authorization pipeline](./docs/AUTHORIZATION_PIPELINE.md)
- [Threat model](./docs/THREAT_MODEL.md)
- [Data ownership model](./docs/DATA_OWNERSHIP_MODEL.md)
- [Go-live checklist](./docs/GO_LIVE_CHECKLIST.md)
- [Operations runbooks](./docs/operations/README.md)
- [Governance docs](./docs/governance/README.md)
- [Tokenomics docs](./docs/tokenomics/README.md)

## RFC publication status

| Range | Scope | Status |
| --- | --- | --- |
| RFC-0001 to RFC-0002 | Foundational asset and account interfaces | Accepted |
| RFC-0003 to RFC-0004 | Asset, ledger, and settlement baselines | Draft |
| RFC-0005 to RFC-0018 | Programmable and autonomous finance canonical set | Accepted |

## RFC index

| RFC | Title | Status |
| --- | --- | --- |
| [RFC-0001](./docs/rfc/rfc-0001-aa-unified-assets.md) | AA Unified Assets | Accepted |
| [RFC-0002](./docs/rfc/rfc-0002-accounts-interfaces.md) | Accounts Interfaces | Accepted |
| [RFC-0003](./docs/rfc/rfc-0003-asset-schema-and-valuation.md) | Asset Schema and Valuation | Draft |
| [RFC-0004](./docs/rfc/rfc-0004-ledger-and-settlement-state-machine.md) | Ledger and Settlement State Machine | Draft |
| [RFC-0005](./docs/rfc/rfc-0005-programmable-financial-authority.md) | Programmable Financial Authority | Accepted |
| [RFC-0006](./docs/rfc/rfc-0006-agent-identity-mandates-capabilities.md) | Agent Identity, Mandates & Capabilities | Accepted |
| [RFC-0007](./docs/rfc/rfc-0007-agent-gateway-and-tool-security.md) | Agent Gateway & Tool Security | Accepted |
| [RFC-0008](./docs/rfc/rfc-0008-financial-intent-and-execution-provenance.md) | Financial Intent & Execution Provenance | Accepted |
| [RFC-0009](./docs/rfc/rfc-0009-risk-engine-and-policy-dsl.md) | Risk Engine & Policy DSL | Accepted |
| [RFC-0010](./docs/rfc/rfc-0010-agent-runtime-architecture.md) | Agent Runtime Architecture | Accepted |
| [RFC-0011](./docs/rfc/rfc-0011-confidential-execution-abstraction.md) | Confidential Execution Abstraction | Accepted |
| [RFC-0012](./docs/rfc/rfc-0012-confidential-perpetual-markets.md) | Confidential Perpetual Markets | Accepted |
| [RFC-0013](./docs/rfc/rfc-0013-private-liquidation-and-solvency-proofs.md) | Private Liquidation & Solvency Proofs | Accepted |
| [RFC-0014](./docs/rfc/rfc-0014-agentic-payments.md) | Agentic Payments | Accepted |
| [RFC-0015](./docs/rfc/rfc-0015-agentic-markets.md) | Agentic Markets | Accepted |
| [RFC-0016](./docs/rfc/rfc-0016-autonomous-treasury-and-finance-agents.md) | Autonomous Treasury / Autonomous Finance Agents | Accepted |
| [RFC-0017](./docs/rfc/rfc-0017-autonomous-finance-threat-model.md) | Autonomous Finance Threat Model | Accepted |
| [RFC-0018](./docs/rfc/rfc-0018-database-and-data-ownership-model.md) | Database & Data Ownership Model | Accepted |

## Implementation and operations references

- [Implementation matrix](./docs/IMPLEMENTATION_MATRIX.md) for requirement-to-repo mapping, status, evidence, and next steps.
- [Authorization pipeline](./docs/AUTHORIZATION_PIPELINE.md) for end-to-end control flow, emergency controls, and human approvals.
- [Threat model](./docs/THREAT_MODEL.md) and [data ownership model](./docs/DATA_OWNERSHIP_MODEL.md) for security and boundary guidance.
- [Go-live checklist](./docs/GO_LIVE_CHECKLIST.md) and [operations runbooks](./docs/operations/README.md) for release readiness and incident handling.

## How to propose changes (quick flow)

1. Open an issue using a docs or RFC template.
2. Draft changes using repository templates and the style guide.
3. Run markdown and link quality checks with pnpm.
4. Submit a PR for code owner and domain review.
5. Update related readiness, governance, and changelog material when the change is normative.
