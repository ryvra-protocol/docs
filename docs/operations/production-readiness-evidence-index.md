# Production readiness and evidence index: unified assets + ERC-4337

- **Release train**: `R2026.08-UA-AA`
- **GO/NO-GO state**: Approved in protocol-core prior to this docs release PR.

## Stage check (pre-edit assessment)

- **Classification**: scaffold
- **Evidence**:
  - RFC-0001 and RFC-0002 were Draft stubs without production lifecycle or error taxonomy coverage.
  - No production architecture overview with explicit cross-repo ownership boundaries.
  - No version-pinned compatibility matrix for contract/interface adapters.
  - No incident runbooks for pending userops, bundler/paymaster degradation, settlement mismatch, or rollback.
  - No production evidence index linking hardening tracks, CI proof, drills, and signoffs.
  - No operator/integrator release notes for pre-PR7/PR8 migration.

## Hardening PR evidence (H1-H5)

| Track | Evidence link | Owner |
| --- | --- | --- |
| H1 contract hardening | [protocol-core H1 merged PRs](https://github.com/ryvra-protocol/protocol-core/pulls?q=is%3Apr+is%3Amerged+label%3AH1) | protocol-core maintainers |
| H2 accounts runtime hardening | [accounts H2 merged PRs](https://github.com/ryvra-protocol/accounts/pulls?q=is%3Apr+is%3Amerged+label%3AH2) | accounts maintainers |
| H3 orchestration/policy hardening | [markets H3 merged PRs](https://github.com/ryvra-protocol/markets/pulls?q=is%3Apr+is%3Amerged+label%3AH3) | markets maintainers |
| H4 asset + settlement hardening | [ledger-settlement H4 merged PRs](https://github.com/ryvra-protocol/ledger-settlement/pulls?q=is%3Apr+is%3Amerged+label%3AH4) | ledger-settlement maintainers |
| H5 payment reliability hardening | [pay H5 merged PRs](https://github.com/ryvra-protocol/pay/pulls?q=is%3Apr+is%3Amerged+label%3AH5) | pay maintainers |

## CI, drill, and signoff evidence

| Evidence type | Link |
| --- | --- |
| Docs CI (this repository) | [docs-ci workflow](https://github.com/ryvra-protocol/docs/actions/workflows/ci.yml) |
| protocol-core release workflow evidence | [protocol-core actions](https://github.com/ryvra-protocol/protocol-core/actions) |
| accounts release workflow evidence | [accounts actions](https://github.com/ryvra-protocol/accounts/actions) |
| Chaos drill records | [chaos-drill issues](https://github.com/ryvra-protocol/protocol-core/issues?q=is%3Aissue+label%3Achaos-drill) |
| Rollback drill records | [rollback-drill issues](https://github.com/ryvra-protocol/protocol-core/issues?q=is%3Aissue+label%3Arollback-drill) |
| GO/NO-GO signoff record | [approved go-no-go issues](https://github.com/ryvra-protocol/protocol-core/issues?q=is%3Aissue+label%3Ago-no-go+label%3Aapproved) |

## Residual known risks

| Risk | Mitigation | Owner |
| --- | --- | --- |
| Third-party bundler latency spikes | Multi-bundler failover + pending queue guardrails | accounts maintainers |
| Paymaster budget depletion during spikes | Auto-throttle and fallback path A | pay maintainers |
| Cross-chain metadata drift | Registry snapshot pinning and startup hash checks | asset-registry maintainers |
| Settlement event ordering delays | Reconciliation holdback window and manual dual-approval release | ledger-settlement maintainers |
