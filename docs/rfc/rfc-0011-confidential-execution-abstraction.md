# RFC-0011: Confidential Execution Abstraction

- **Status**: Accepted
- **Authors**: Ryvra RFC Editors
- **Created**: 2026-09-11
- **Updated**: 2026-09-11

## Context and motivation
Sensitive portfolio state, strategy parameters, and counterpart data require a portable abstraction for confidential execution that does not hard-code trust into any one provider.

## Scope
### In scope
- Portable confidential execution interface, attestation expectations, and workload lifecycle.
- Separation of plaintext control data from encrypted sensitive state.
- Fallback behavior when confidential execution is unavailable.

### Out of scope
- Cryptographic primitive selection beyond interface requirements.
- Vendor-specific enclave or MPC implementation details.

## Core specification
- Confidential execution **MUST** expose a provider-neutral interface for submit, attest, execute, and return-proof operations.
- Sensitive state **MUST** remain outside shared application databases in plaintext form.
- Attestation evidence **MUST** be captured in provenance before confidential results can influence settlement.
- The abstraction **SHOULD** support multiple backends without changing policy, ledger, or settlement semantics.
- Fallback to non-confidential execution **MUST** require an explicit policy path and human approval when confidentiality is mandatory.

## Security and risk considerations
- Provider neutrality limits lock-in and reduces single-provider compromise risk.
- Attestation freshness and measurement verification protect against fake confidential runtimes.
- Result minimization **SHOULD** expose only the outputs needed by downstream controls.

## Open questions
- Repository-specific rollout sequencing is tracked in the [implementation matrix](../IMPLEMENTATION_MATRIX.md).

## Backward compatibility and versioning
- Breaking changes **MUST** update the RFC revision, identify affected repositories, and include migration guidance.
- Additive clarifications **SHOULD** preserve existing identifiers and normative references when behavior is unchanged.

## Related RFCs and references
- [RFC-0010](./rfc-0010-agent-runtime-architecture.md)
- [RFC-0012](./rfc-0012-confidential-perpetual-markets.md)
- [RFC-0013](./rfc-0013-private-liquidation-and-solvency-proofs.md)
- [Data ownership model](../DATA_OWNERSHIP_MODEL.md)
