# Production architecture overview: unified assets + ERC-4337

- **Release train**: `R2026.08-UA-AA`
- **Status**: Production
- **Effective date**: 2026-08-03

## System ownership boundaries

| Repository | Production version pin | Ownership boundary | Upstream dependencies | Downstream consumers |
| --- | --- | --- | --- | --- |
| [protocol-core](https://github.com/ryvra-protocol/protocol-core) | `v1.8.0` | Canonical contract set, contract version registry, and chain deployment manifest authority | Governance approvals | accounts, markets, pay, ledger-settlement |
| [accounts](https://github.com/ryvra-protocol/accounts) | `v1.8.0` | ERC-4337 runtime (EntryPoint wiring, Smart Account policy adapters, UserOperation verification) | protocol-core contract registry | markets, pay |
| [markets](https://github.com/ryvra-protocol/markets) | `v1.6.0` | Intent orchestration and policy-gated execution routing | accounts runtime + policy outcomes | ledger-settlement, pay |
| [asset-registry](https://github.com/ryvra-protocol/asset-registry) | `v1.5.0` | Canonical asset metadata authority (identity, decimals, normalization profile) | protocol-core version registry | markets, pay, ledger-settlement |
| [ledger-settlement](https://github.com/ryvra-protocol/ledger-settlement) | `v1.4.0` | Reconciliation, settlement finalization, and mismatch escalation | markets events + asset-registry metadata | finance ops |
| [pay](https://github.com/ryvra-protocol/pay) | `v1.3.0` | Payment execution boundary, paymaster-facing integration, and fallback rail triggers | accounts + markets + asset-registry | external payment processors |

## Production interaction model

1. `asset-registry@v1.5.0` resolves canonical asset identity and decimals profile.
2. `accounts@v1.8.0` validates and signs UserOperations against `protocol-core@v1.8.0` contract registry.
3. `markets@v1.6.0` executes only policy-ALLOW actions and emits execution outcomes.
4. `pay@v1.3.0` performs payment settlement path selection:
   - primary path: UserOperation sponsorship + preferred rail;
   - fallback path A: direct user-funded gas payment;
   - fallback path B: deferred settlement ticket for manual retry.
5. `ledger-settlement@v1.4.0` reconciles on-chain and internal ledgers, then finalizes settlement.

## Production invariants

- Canonical contract addresses **MUST** be resolved via `protocol-core@v1.8.0` registry snapshots.
- Asset decimals **MUST** be interpreted only from `asset-registry@v1.5.0` metadata.
- markets execution **MUST** enforce ALLOW-only dispatch; DENY/REVIEW outcomes MUST NOT execute side effects.
- pay fallback activation **MUST** preserve idempotency key semantics for settlement replay safety.

## Rollback boundary summary

- Contract rollback authority: protocol-core maintainers with governance approval.
- Runtime rollback authority: accounts and markets maintainers with incident commander approval.
- Settlement rollback authority: ledger-settlement owner and finance ops approver.
- Payment rail rollback authority: pay owner and operations commander.
