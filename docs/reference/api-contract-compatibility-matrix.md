# API and contract compatibility matrix (production)

- **Release train**: `R2026.08-UA-AA`
- **Baseline**: unified assets PR7 final + ERC-4337 PR8 final

## Version-pinned interface matrix

| Interface domain | Canonical owner | Producer version | Consumer expectation | Adapter contract | Backward compatibility behavior | Known constraints |
| --- | --- | --- | --- | --- | --- | --- |
| Contract registry snapshot | protocol-core | `v1.8.0` | accounts/markets/pay fetch immutable release snapshot by semantic version | `RegistrySnapshotAdapter@1.0.0` | Additive fields are backward compatible; field removals are breaking | Snapshot hash mismatch blocks startup |
| Smart account execution | accounts | `v1.8.0` | markets/pay submit ERC-4337 UserOperation envelope `v1` | `UserOpEnvelopeAdapter@1.0.0` | Optional metadata keys are ignored by older consumers | Envelope size bounded by bundler policy |
| Policy verdict stream | markets | `v1.6.0` | ledger-settlement consumes verdict + execution receipt schema `v2` | `PolicyVerdictAdapter@2.1.0` | New verdict reason codes are backward compatible; verdict type changes are breaking | REVIEW events are non-executable only |
| Asset metadata feed | asset-registry | `v1.5.0` | accounts/markets/pay/ledger-settlement require canonical decimals + normalization profile | `CanonicalAssetAdapter@1.2.0` | Additional metadata fields are non-breaking | Decimals changes for existing asset IDs are prohibited |
| Settlement reconciliation feed | ledger-settlement | `v1.4.0` | markets/pay ingest reconciliation status events `v1` | `SettlementStatusAdapter@1.0.0` | New status detail fields are backward compatible | Event ordering is eventually consistent |
| Payment execution boundary | pay | `v1.3.0` | markets issues payment intents schema `v1`; pay returns execution token schema `v1` | `PaymentIntentAdapter@1.0.0` | New optional fallback hints are backward compatible | Fallback rail invocation requires idempotency key |

## Compatibility policy

- All cross-repo interfaces **MUST** carry an explicit semantic version.
- Minor-version upgrades **MUST** remain backward compatible for one full release train.
- Major-version upgrades **MUST** include migration notes and a dual-read transition period.
- If adapter and producer versions diverge, consumers **MUST** fail closed and emit an integration error.

## Known rollout constraints

1. `accounts@v1.8.0` requires EntryPoint `0.6.x` compatibility mode.
2. `markets@v1.6.0` only supports policy verdict schema `v2`.
3. `pay@v1.3.0` fallback rail B requires settlement ticket processor enabled.
4. `ledger-settlement@v1.4.0` does not support retroactive decimals corrections.
