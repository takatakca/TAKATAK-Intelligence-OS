# Execution roadmap — TAKATAK Intelligence OS

Date: 2026-11-18. Product coordination issue: [#1](https://github.com/takatakca/TAKATAK-Intelligence-OS/issues/1).
All stages target V1's existing production application with feature flags OFF until their release gates are met.

| Phase | Deliverable | Acceptance evidence | Status |
|---|---|---|---|
| P0 | Safe first-party assignment policy + architecture | Source reviewed, tenant isolation tests, exact-head CI | V1 [draft PR #335](https://github.com/takatakca/takatak-v1/pull/335); [CI #44259072459](https://github.com/takatakca/takatak-v1/actions/runs/44259072459) passed; NOT LIVE |
| P1 | Manager experiments UI & approved lifecycle | FR/EN, access checks, workspace isolation, lifecycle audit | Not built/verified |
| P2 | Privacy-aware events, sticky assignment & conversion reporting | Server validation, idempotency, tests, credible uncertainty | Not built/verified |
| P3 | TAKBOT-powered SEO/conversion recommendations | Read-only evidence, cited source data, spending controls, human-reviewed drafts | Not built/verified |
| P4 | First controlled live website experiment | Owner-verified site, rollback, kill switch, Coolify exact served SHA and two-client smoke | Not built/verified |
| P5 | Repeatable approved optimization/personalization | Consent-aware targeting, accurate reporting and approval workflows | Not built/verified |

## Immediate next action

1. Review exact-green P0 draft PR #335; merge only reviewed source after checking current V1 main and coordination board.
2. Design P1 schema with FK/RLS, permission matrix, launch/kill audit and migration plan. **Before modifying a real DB**, verify protected backup and review affected data.
3. Implement P1 user interface and APIs in V1 behind server-only false-by-default flags; never expose arbitrary website scripts.
4. Add P2 events, conversion goals and consent-aware sticky assignment before any visitor experiment traffic.
5. Complete P3 & P4 progressively, with real production verification rather than presumed deployment.

## Work coordination

- Read V1 `AGENTS.md`, `WORKLOG.md`, `docs/AGENT_HANDOFF.md`, current GitHub CI and open PRs before touching V1 code.
- Multi-agent board: https://github.com/takatakca/foodhubca/issues/105.
- Separate this roadmap repository from the executable V1 source to avoid conflicting dashboard changes. Keep cross-repo issue links and explicit statuses.
- Status labels: `planned`, `source-only`, `CI-green`, `merged`, `runtime-verified`. Never label LIVE without last status.
