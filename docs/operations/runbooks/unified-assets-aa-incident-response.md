# Production incident runbook: unified assets + ERC-4337

- **Release train**: `R2026.08-UA-AA`
- **Scope**: accounts, markets, pay, asset-registry, ledger-settlement

## Incident classes

| Incident | Primary owner | Severity trigger |
| --- | --- | --- |
| UserOperation stuck pending | accounts | Pending age exceeds SLO threshold |
| Paymaster/bundler degradation | accounts + pay | Submission success drops below SLO |
| Settlement mismatch | ledger-settlement | Ledger delta non-zero after reconciliation window |
| Rollback trigger | Incident commander | Safety invariant breach or sustained Sev1 |

## Triage decision tree

1. Confirm impact scope (single tenant, chain, or global).
2. Check ALLOW-only invariant status:
   - if violated, immediately trigger rollback gate;
   - if intact, continue targeted mitigation.
3. Route by incident class table below.
4. Escalate if mitigation does not recover within one incident window.

## Playbook: UserOperation stuck pending

1. Validate pending queue age and bundler ACK status.
2. Re-simulate impacted UserOperation with current registry snapshot.
3. If paymaster denied, switch to user-funded fallback path.
4. If bundler timeout persists, fail over to secondary bundler.
5. If still pending, move operation to REVIEW and notify incident commander.

Escalation path: On-call accounts engineer -> Incident commander -> Protocol leadership.

## Playbook: paymaster/bundler degradation

1. Compare sponsorship acceptance rate vs baseline.
2. Check paymaster budget and policy throttles.
3. Drain traffic from degraded bundler.
4. Enable fallback path A (user-funded) for impacted flows.
5. Open Sev2 if degraded > 15 minutes; Sev1 if global execution blocked.

Escalation path: On-call pay engineer -> accounts owner -> Incident commander.

## Playbook: settlement mismatch

1. Freeze automatic settlement finalization for affected partition.
2. Re-run reconciliation with immutable event snapshot.
3. Validate asset decimals/normalization version from asset-registry.
4. If mismatch remains, issue manual correction ticket and hold payout release.
5. Resume settlement only after dual approval (ledger owner + finance ops).

Escalation path: On-call ledger engineer -> finance ops approver -> Incident commander.

## Rollback triggers and procedures

### Triggers

- ALLOW-only invariant violation.
- Repeated EntryPoint terminal failures above risk threshold.
- Settlement mismatch unresolved beyond two reconciliation windows.

### Procedure

1. Declare rollback and timestamp the event.
2. Pin traffic to last known-good release train versions.
3. Disable paymaster sponsorship for affected route.
4. Reconcile in-flight operations into terminal or REVIEW states.
5. Publish incident summary with owner and next review date.
