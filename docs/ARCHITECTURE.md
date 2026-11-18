# Architecture — TAKATAK Intelligence OS

## Decision ADR-001 (2026-11-18): first-party intelligence inside existing TAKATAK-V1

**Decision:** This repository owns the product specification and cross-repository contracts. `takatak-v1` owns the executable APIs, dashboard, customer authorization, data model, billing, provider connections and its existing Coolify deployment. A separately deployed service must be justified by a concrete scaling/security bottleneck and approved explicitly; it must not duplicate client identity or payment authority.

### Target logical system

```text
Authenticated TAKATAK client / manager (FR/EN)
              |
       TAKATAK-V1 dashboard
              |
  Permission + active-client authority
              |
+-------------------------------+
| Intelligence control plane    |
| Experiment lifecycle/approval |
| Verified site & surface       |
| Signed assignment + events    |
| Reports and AI recommendations|
| Audit, budgets, kill switches |
+-------------------------------+
    |               |         |
  Website        TAKBOT /    Analytics /
  adapter        AI ledger   SEO / Social
    |               |         |
    +-------- trusted scoped data -----+
```

### Responsibilities and ownership

1. **Identity & access:** resolve active client ID, permissions and roles from V1 server session; never permit client-supplied identity, storage credentials or hidden cross-workspace queries.
2. **Experiments:** immutable/controlled revisions; explicit review approval; state machine `draft → approved → running → paused/completed` with a global server kill switch.
3. **Targeting:** first-party, owner-verified sites and only allowlisted editable content surfaces (e.g., headings, CTA copy); no arbitrary JavaScript, remote snippets, DNS writes or unrestricted CSS.
4. **Assignment:** server-defined flags, audience consent, pseudonymous IDs and sticky assignment persistence. The current P0 HMAC helper in [V1 PR #335](https://github.com/takatakca/takatak-v1/pull/335) is a *policy prototype*, not production visitor delivery.
5. **Measurement:** signed/idempotent exposure and conversion events, typed goals, safe attribution windows, consent/retention rules, traffic caps and explicit uncertainty. Never manufacture revenue or statistical certainty.
6. **AI:** use existing TAKBOT and central provider/credit store; suggestions remain proposals, each identifying underlying data and costs. Approvals for writing, publishing, ads and provider billing are separate.
7. **Operations:** exact-head CI, protected reviewed migrations, real production canary, metric checks, rollback and served-SHA verification. No staging infrastructure.

### What is NOT in scope initially

Full Optimizely feature parity, an independent customer CMS, omnichannel profile unification, multi-client benchmarking without licensing and consent, automatic advertising budget changes, automatic purchase, additional hosting panels or unsolicited customer tracking.

### Risk controls

- Client isolation must be tested with two distinct real/synthetic accounts across every API.
- Suppress experimentation on missing consent, role, verified domain, approved lifecycle, valid flag or secret.
- Customer-facing data collection needs transparent consent and privacy review before launch.
- Multi-variant assignment must not claim statistical conclusions from small sample sizes.
- Kill switch and rollback must be available even if AI systems/providers fail.
- Secrets and customer personal data never go into this public planning repository.

**Evidence status:** documents and V1 P0 code exist; dashboard, events, schema and production launch are not verified implemented.
