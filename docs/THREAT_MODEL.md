# Threat model

This document maps the canonical autonomous finance threat set to required controls.

| Threat | Primary attack path | Required controls | Detection and response |
| --- | --- | --- | --- |
| Prompt injection | Malicious instructions enter model context and attempt to override authority or policy | Isolate authority from prompts, capability-scope agents, require gateway mediation, fail closed on missing mandate or policy references | Alert on policy override attempts, suspend affected agent, review provenance chain |
| Malicious tool outputs | Tool returns forged data, hidden instructions, or manipulated execution receipts | Treat tool output as untrusted, validate schemas, sign or hash critical responses, require cross-checks before execution and settlement | Quarantine adapter, invalidate receipts, replay from trusted source |
| Credential theft | Provider, adapter, or operator credentials are exfiltrated or replayed | Short-lived brokered secrets, per-tool credentials, hardware-backed keys where possible, strict secret segregation | Rotate credentials, revoke sessions, suspend mandates tied to exposed credentials |
| Mandate escalation | Agent or operator attempts to expand scope, accounts, or limits without approval | Versioned mandates, dual control for scope expansion, smart-account enforcement, provenance on all mandate changes | Diff mandate versions, revoke unauthorized versions, run post-incident review |
| Policy manipulation | Hidden changes alter verdict logic, limits, or scoring inputs | Deterministic DSL, code review, immutable versions, signed policy bundles, separate owners for policy and runtime deployment | Compare expected and deployed hashes, freeze execution, require rollback or reapproval |
| Replay or double-spend | Duplicate intents, receipts, or reservations execute multiple times | Canonical idempotency keys, reservation locking, nonce discipline, ledger reconciliation before settlement | Detect duplicate keys or reservation collisions, block settlement, unwind safely |
| Runaway agent | Agent loops, exceeds rate limits, or floods downstream systems | Capability scoping, rate limits, quotas, bounded queues, external kill switch, approval thresholds for repeated actions | Trigger throttles, suspend runtime, preserve in-flight evidence for review |
| Compromised model or provider | Model provider, enclave provider, or hosted runtime is malicious or unavailable | Provider-neutral interfaces, attestation, output minimization, confidential execution abstraction, operator override paths | Fail over or suspend, re-attest, invalidate provider-specific trust until recovery |

## Control expectations

- Every execution-capable repository must map these threats into implementation controls.
- Controls must be tested through drills before first production release.
- Exceptions must identify owner, expiry, and compensating controls.

## Required validation scenarios

1. Prompt injection attempts cannot create or expand authority.
2. Forged tool outputs cannot survive gateway validation and settlement reconciliation.
3. Credential rotation and mandate revocation propagate before queued retries execute.
4. Replay attempts are blocked at reservation and ledger layers.
5. Kill switch and suspension paths stop new actions immediately.
6. Provider compromise scenarios preserve operator control and safe recovery.
