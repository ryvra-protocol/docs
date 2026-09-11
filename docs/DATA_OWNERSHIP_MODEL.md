# Data ownership model

This document defines canonical system-of-record boundaries for autonomous finance.

## Repo and data ownership matrix

| Domain object | System of record | Owning repo or service boundary | Allowed writers | Notes |
| --- | --- | --- | --- | --- |
| Mandates and authority grants | Mandate registry | `agent-identity` or equivalent control-plane service | Governance or delegated finance admins | Versioned, revocable, provenance-linked |
| Agent identity and capability descriptors | Identity registry | `agent-identity` | Runtime control plane | Capabilities are deny-by-default |
| Policy bundles and risk profiles | Policy registry | `policy-risk` | Policy maintainers under change control | Deterministic bundle hash required |
| Reservations | Reservation store | `ledger-settlement` | Reservation service only | Prevents double-spend across agents |
| Execution receipts | Execution journal | `agent-gateway`, `pay`, `markets` adapters | Approved execution adapters | Receipts are not final truth until ledgered |
| Ledger balances and obligations | Canonical ledger | `ledger-settlement` | Ledger service only | Economic truth for balances and obligations |
| Settlement outcomes | Settlement state machine | `ledger-settlement` | Settlement service only | Finality boundary |
| Smart-account configuration | Account policy registry | `accounts` and `protocol-core` | Account control plane | Cryptographic execution boundary |
| Confidential strategy state | Confidential state store | `confidential-execution` backend | Confidential workloads only | Plaintext does not belong in shared PostgreSQL |
| Documentation and normative mappings | Canonical docs | `docs` | RFC editors and maintainers | Cross-repo authority guidance |

## Boundary rules

- A single domain object must have one writable authority boundary.
- Read models and caches may copy data, but they do not become the system of record.
- Frontends may display status and collect requests, but they do not grant financial authority or own final truth.
- Provenance references must connect all replicated records back to their canonical owner.

## Explicit anti-patterns

- **No private keys in PostgreSQL**.
- **No frontend authority**.
- **No direct AI-to-chain execution**.
- **No provider lock-in in private execution core**.

## Additional prohibited patterns

- Storing approval decisions only in chat transcripts or ticket comments.
- Allowing tools to mutate ledger truth directly without settlement controls.
- Reconstructing balances from analytics pipelines instead of the ledger.
- Treating model memory or prompt context as durable authority state.
