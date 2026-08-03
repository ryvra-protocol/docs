# Release notes: production unified assets + ERC-4337 rollout

- **Release train**: `R2026.08-UA-AA`
- **Date**: 2026-08-03

## Operator-facing changes

- Production runbooks are now canonical for UserOperation pending, bundler/paymaster degradation, settlement mismatch, and rollback handling.
- Production readiness evidence index is published with hardening-track references and signoff pointers.
- Cross-repo architecture ownership boundaries and rollback authorities are explicitly documented.

## Integrator-facing changes

- Unified asset model now requires canonical `asset_id` and `registry_version` inputs.
- Asset normalization and decimals semantics are fully versioned and deterministic.
- ERC-4337 integration is now defined by a canonical UserOperation lifecycle and failure taxonomy.
- ALLOW-only execution invariant is now explicit: DENY/REVIEW outcomes do not execute.

## Migration guidance from pre-PR7/PR8 assumptions

1. Replace symbol-only asset addressing with canonical `asset_id` + `registry_version`.
2. Replace direct transaction submission assumptions with UserOperation lifecycle event handling.
3. Implement handling for DENY/REVIEW non-execution outcomes in orchestration code.
4. Ensure adapter-version checks fail closed when producer/consumer versions diverge.

## References

- [Production architecture overview](../architecture/production-unified-assets-aa-overview.md)
- [API and contract compatibility matrix](../reference/api-contract-compatibility-matrix.md)
- [RFC-0001 unified assets production final](../rfc/rfc-0001-aa-unified-assets.md)
- [RFC-0002 accounts interfaces production final](../rfc/rfc-0002-accounts-interfaces.md)
- [Incident runbook](../operations/runbooks/unified-assets-aa-incident-response.md)
- [Production readiness and evidence index](../operations/production-readiness-evidence-index.md)
