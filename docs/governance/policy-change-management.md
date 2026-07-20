# Policy Change Management

## Objective
Define how policy and risk parameter changes are proposed, reviewed, approved, and tracked.

## Change flow
1. Proposer submits policy change proposal with rationale and risk analysis.
2. Maintainers assess implementation impact across repositories.
3. Risk/policy reviewers evaluate controls and failure modes.
4. Governance authority approves/rejects and records decision.
5. Approved changes receive version update, changelog entry, and rollout plan.

## Policy/risk parameter controls
- Parameter changes MUST include old/new values, activation criteria, and rollback conditions.
- Emergency changes SHOULD be explicitly marked and post-reviewed.
- Unresolved items MUST be tagged as **TBD by governance/policy**.
