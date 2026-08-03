# RFC-0002: Accounts interfaces (ERC-4337 production final)

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-07-20
- **Updated**: 2026-08-03
- **Target release**: `R2026.08-UA-AA`

## Context and motivation

This RFC defines production ERC-4337 integration boundaries for Ryvra smart accounts.

## UserOperation lifecycle

1. Client assembles canonical payload and unified asset normalization output.
2. accounts runtime validates signatures, nonce, policy prerequisites, and gas constraints.
3. paymaster sponsorship eligibility is evaluated.
4. bundler receives signed UserOperation envelope.
5. EntryPoint execution result is propagated to markets and settlement consumers.

## Bundler and paymaster boundaries

- Bundler responsibility: mempool admission, simulation, bundle submission, and receipt relay.
- Paymaster responsibility: sponsorship policy, budget enforcement, and sponsorship attestation.
- accounts responsibility: canonical envelope creation, signature guarantees, nonce monotonicity.
- markets responsibility: ALLOW-only dispatch gate before execution request emission.

## Failure taxonomy

| Error code | Domain | Trigger | Outcome |
| --- | --- | --- | --- |
| `AA-UO-001` | Validation | Invalid signature or nonce | Reject before bundler submission |
| `AA-UO-002` | Paymaster | Sponsorship denied or depleted | Retry with user-funded mode |
| `AA-UO-003` | Bundler | Admission timeout | Mark pending incident and trigger runbook |
| `AA-UO-004` | Execution | EntryPoint revert | Emit terminal failure with revert class |
| `AA-UO-005` | Policy | Non-ALLOW verdict | No execution; persist DENY/REVIEW outcome |

## ALLOW-only execution invariant

- Only `ALLOW` verdicts may produce executable UserOperations.
- `DENY` verdicts **MUST NOT** trigger bundler submission or paymaster sponsorship.
- `REVIEW` verdicts **MUST NOT** trigger bundler submission or paymaster sponsorship.
- DENY/REVIEW outcomes **MUST** be persisted with trace identifiers for audit.

## Backward compatibility and versioning

- Envelope schema `v1` is backward compatible for additive optional fields.
- Any change to signed field ordering is a breaking change and requires major upgrade.
- Pre-PR8 consumers **MUST** migrate from direct transaction submission assumptions to UserOperation lifecycle events.

## Related RFCs and references

- [RFC-0001](./rfc-0001-aa-unified-assets.md)
- [RFC-0006](./rfc-0006-pay-rails-and-payment-intents.md)
- [RFC-0007](./rfc-0007-markets-intents-and-execution.md)
- [API and contract compatibility matrix](../reference/api-contract-compatibility-matrix.md)
