# Cross-repository alignment checklist

Use this checklist for changes that may affect implementation repositories.

## Organization repositories

- [ ] [protocol-core](https://github.com/ryvra-protocol/protocol-core)
- [ ] [accounts](https://github.com/ryvra-protocol/accounts)
- [ ] [asset-registry](https://github.com/ryvra-protocol/asset-registry)
- [ ] [ledger-settlement](https://github.com/ryvra-protocol/ledger-settlement)
- [ ] [policy-risk](https://github.com/ryvra-protocol/policy-risk)
- [ ] [pay](https://github.com/ryvra-protocol/pay)
- [ ] [markets](https://github.com/ryvra-protocol/markets)
- [ ] [agent-identity](TBD)
- [ ] [agent-gateway](TBD)
- [ ] [agent-runtime](TBD)
- [ ] [confidential-execution](TBD)
- [ ] [autonomous-finance](TBD)
- [ ] [website](https://github.com/ryvra-protocol/website)

## Canonical docs mapping for downstream references

| Common downstream reference | Canonical docs path |
| --- | --- |
| `docs/rfc-0001-aa-unified-assets.md` | `/docs/rfc/rfc-0001-aa-unified-assets.md` |
| `docs/rfc-0002-accounts-interfaces.md` | `/docs/rfc/rfc-0002-accounts-interfaces.md` |
| `docs/rfc-0003-asset-schema-and-valuation.md` | `/docs/rfc/rfc-0003-asset-schema-and-valuation.md` |
| `docs/rfc-0004-ledger-and-settlement-state-machine.md` | `/docs/rfc/rfc-0004-ledger-and-settlement-state-machine.md` |
| `docs/rfc-0005-programmable-financial-authority.md` | `/docs/rfc/rfc-0005-programmable-financial-authority.md` |
| `docs/rfc-0006-agent-identity-mandates-capabilities.md` | `/docs/rfc/rfc-0006-agent-identity-mandates-capabilities.md` |
| `docs/rfc-0007-agent-gateway-and-tool-security.md` | `/docs/rfc/rfc-0007-agent-gateway-and-tool-security.md` |
| `docs/rfc-0008-financial-intent-and-execution-provenance.md` | `/docs/rfc/rfc-0008-financial-intent-and-execution-provenance.md` |
| `docs/rfc-0009-risk-engine-and-policy-dsl.md` | `/docs/rfc/rfc-0009-risk-engine-and-policy-dsl.md` |
| `docs/rfc-0010-agent-runtime-architecture.md` | `/docs/rfc/rfc-0010-agent-runtime-architecture.md` |
| `docs/rfc-0011-confidential-execution-abstraction.md` | `/docs/rfc/rfc-0011-confidential-execution-abstraction.md` |
| `docs/rfc-0012-confidential-perpetual-markets.md` | `/docs/rfc/rfc-0012-confidential-perpetual-markets.md` |
| `docs/rfc-0013-private-liquidation-and-solvency-proofs.md` | `/docs/rfc/rfc-0013-private-liquidation-and-solvency-proofs.md` |
| `docs/rfc-0014-agentic-payments.md` | `/docs/rfc/rfc-0014-agentic-payments.md` |
| `docs/rfc-0015-agentic-markets.md` | `/docs/rfc/rfc-0015-agentic-markets.md` |
| `docs/rfc-0016-autonomous-treasury-and-finance-agents.md` | `/docs/rfc/rfc-0016-autonomous-treasury-and-finance-agents.md` |
| `docs/rfc-0017-autonomous-finance-threat-model.md` | `/docs/rfc/rfc-0017-autonomous-finance-threat-model.md` |
| `docs/rfc-0018-database-and-data-ownership-model.md` | `/docs/rfc/rfc-0018-database-and-data-ownership-model.md` |
| `docs/implementation-matrix.md` | `/docs/IMPLEMENTATION_MATRIX.md` |
| `docs/architecture-principles.md` | `/docs/ARCHITECTURE_PRINCIPLES.md` |
| `docs/authorization-pipeline.md` | `/docs/AUTHORIZATION_PIPELINE.md` |
| `docs/threat-model.md` | `/docs/THREAT_MODEL.md` |
| `docs/data-ownership-model.md` | `/docs/DATA_OWNERSHIP_MODEL.md` |
| `docs/go-live-checklist.md` | `/docs/GO_LIVE_CHECKLIST.md` |
| `docs/production-architecture-unified-assets-aa.md` | `/docs/architecture/production-unified-assets-aa-overview.md` |
| `docs/compatibility-unified-assets-aa.md` | `/docs/reference/api-contract-compatibility-matrix.md` |
| `docs/runbook-unified-assets-aa.md` | `/docs/operations/runbooks/unified-assets-aa-incident-response.md` |
| `docs/release-notes-unified-assets-aa.md` | `/docs/changelog/2026-08-03-release-unified-assets-aa.md` |
| `docs/tokenomics-proof-of-transaction.md` | `/docs/tokenomics/proof-of-transaction.md` |
| `docs/tokenomics-faq.md` | `/docs/tokenomics/tokenomics-faq.md` |
| `docs/brand-narrative.md` | `/docs/architecture/brand-narrative.md` |

For each impacted repo, include linked implementation issue or PR, expected compatibility notes, and readiness evidence before release signoff.
