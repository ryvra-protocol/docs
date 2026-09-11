# Go-live checklist

Use this checklist for the first autonomous-finance production release.

## Mandatory release gates

- [ ] Capability-scoped agent creation is enforced for every production agent class.
- [ ] Versioned mandates are issued, reviewed, and revocable without redeploying agents.
- [ ] Deterministic policy and risk evaluation passes for all executable intent types.
- [ ] Reservation safety is validated under concurrency, retry, and failover scenarios.
- [ ] End-to-end provenance links intent, approvals, policy verdicts, reservations, executions, ledger entries, and settlement outcomes.
- [ ] Immediate suspension and kill switch validation has been exercised in a production-like drill.

## Authority and governance

- [ ] Mandate owners, policy owners, and runtime operators are named and approved.
- [ ] Approval thresholds are documented for payments, markets, treasury, and unwind actions.
- [ ] Emergency unwind authority is narrower than normal operating authority.
- [ ] RFC-0005 through RFC-0018 are published and linked from the docs README.

## Security and runtime controls

- [ ] Prompt injection and malicious tool output scenarios are tested.
- [ ] Credential rotation and secret-broker workflows are validated.
- [ ] Runaway agent limits, queue bounds, and rate limits are enforced.
- [ ] Provider compromise and confidential execution fallback policies are exercised.
- [ ] Data ownership anti-pattern checks confirm that private keys and sensitive state are stored only in approved boundaries.

## Execution, ledger, and settlement

- [ ] Reservation release behavior is verified for expiry, denial, and partial failure cases.
- [ ] Ledger reconciliation is required before settlement finality.
- [ ] Replay and double-spend protections are validated across retries and adapter restarts.
- [ ] Payment and market adapters preserve provenance references in their execution receipts.

## Operational readiness evidence

- [ ] Linked implementation PRs are captured in the [implementation matrix](./IMPLEMENTATION_MATRIX.md).
- [ ] Test evidence and drills are linked from the [production readiness evidence index](./operations/production-readiness-evidence-index.md).
- [ ] Incident response, suspension, and recovery runbooks are reviewed with operators.
- [ ] Open gaps have owners, target milestones, and compensating controls.
