# RFC-0001: AA unified assets (production final)

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-07-20
- **Updated**: 2026-08-03
- **Target release**: `R2026.08-UA-AA`

## Context and motivation

This RFC defines the production canonical asset model used by account abstraction and settlement workflows.

## Canonical asset identity

Each asset identity **MUST** be represented as:

- `asset_id`: immutable canonical identifier (`ASSET:<namespace>:<symbol>:<network>`)
- `chain_id`: execution domain identifier
- `contract_ref`: on-chain address or native sentinel
- `registry_version`: semantic version from `asset-registry`

Identity keys are immutable once published in a production registry version.

## Decimals semantics

- `decimals` is a canonical integer in range `[0, 38]`.
- Display conversions **MUST** be derived from canonical `decimals`.
- Arithmetic inputs **MUST** be normalized to integer atomic units before policy checks.
- Existing `asset_id` entries **MUST NOT** change decimals after production publication.

## Normalization rules

1. Parse input amount into decimal string form.
2. Validate precision does not exceed canonical `decimals`.
3. Convert to atomic units using deterministic round-down.
4. Reject negative or non-finite values.
5. Emit normalized payload with fields: `asset_id`, `atomic_amount`, `decimals`, `normalization_version`.

## Validation outcomes and error taxonomy

| Error code | Class | Trigger | Required outcome |
| --- | --- | --- | --- |
| `UA-VAL-001` | Identity | Unknown `asset_id` | Hard reject; do not enqueue execution |
| `UA-VAL-002` | Identity | Mismatched `chain_id` and `contract_ref` | Hard reject; emit audit event |
| `UA-VAL-003` | Amount | Precision exceeds canonical `decimals` | Hard reject; return validation detail |
| `UA-VAL-004` | Amount | Negative or non-finite amount | Hard reject |
| `UA-VAL-005` | Registry | Missing `registry_version` | Soft fail to REVIEW state, no execution |
| `UA-VAL-006` | Registry | Stale normalization version | Soft fail to REVIEW state, no execution |

## Backward compatibility and versioning

- Additive metadata fields are backward compatible.
- Any change to identity format or decimals semantics is breaking and requires a major version.
- Pre-PR7 integrations **MUST** migrate from symbol-only lookups to canonical `asset_id` + `registry_version` inputs.

## Related RFCs and references

- [RFC-0002](./rfc-0002-accounts-interfaces.md)
- [RFC-0003](./rfc-0003-asset-schema-and-valuation.md)
- [API and contract compatibility matrix](../reference/api-contract-compatibility-matrix.md)
