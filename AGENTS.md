# Agent guidance — TAKATAK Intelligence OS

This is the independent planning/architecture repository, **not a separate client-auth or billing platform**.

Before action:
1. Read README, docs/ARCHITECTURE.md, docs/ROADMAP.md and docs/INTEGRATION_CONTRACT.md.
2. Consult linked V1 project issue #334, PR #335 (or successors), current V1 AGENTS.md, WORKLOG.md, latest main and open PRs.
3. Check TAKATAK shared agent board https://github.com/takatakca/foodhubca/issues/105 to prevent conflicts.
4. Record source-only vs CI-green vs merged vs verified-live honestly and link exact evidence.

Rules:
- Runtime/UI/DB changes belong in `takatakca/takatak-v1` unless explicitly approved otherwise.
- Preserve single TAKATAK AUTH, server-resolved tenant identity, provider credentials and AI credit ledger.
- No staging environment. Do not bypass verified production backups, migrations, exact-head CI, approval or rollback.
- No private customer data, access tokens, company secrets or personal files in this public repository.
- Never write or launch websites/advertisements/DNS, buy third-party services or charge clients without explicit authorized workflow.
- Changes to experimental content/assignments require human review, consent-aware handling, and immutable/audited lifecycle.
- Do not claim production deployment without actual served-SHA and tenant-level smoke evidence.
- Documentation can be added here, but do not copy full source trees from V1 into this repository.
