# Contributing to Ryvra Docs

Thank you for improving Ryvra Protocol documentation.

## Scope
This repository is the canonical source for RFCs, tokenomics narratives, governance/process policy, architecture overviews, and release/reference docs.

## Quick contribution flow
1. Open an issue (Doc Change or RFC Proposal template).
2. Create a focused branch and update relevant docs.
3. Follow `/docs/reference/style-guide.md`.
4. Run:
   - `pnpm lint:md`
   - `pnpm check:links`
5. Open a PR and request review from code owners.

## Review standards
- Changes MUST be traceable, specific, and implementation-aware.
- Requirements language MUST use RFC 2119 keywords consistently (MUST/SHOULD/MAY).
- Tokenomics/compliance language MUST include disclaimers where applicable.
- RFC changes SHOULD include rationale, compatibility notes, and related references.

## Commit and PR guidance
- Keep changes small and purpose-specific.
- Reference affected section(s) and impacted repositories.
- Update changelog and decision log when policy or normative behavior changes.
