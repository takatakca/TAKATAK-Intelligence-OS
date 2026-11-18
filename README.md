# TAKATAK Intelligence OS

**Le moteur d'intelligence, d'expérimentation et d'optimisation de GROUPE TAKATAK.**

**Status / Statut (2026-11-18): Architecture & development foundation — NOT LIVE.**

This is the **product architecture, coordination and integration-contract repository** for TAKATAK Intelligence OS. The existing [TAKATAK-V1](https://github.com/takatakca/takatak-v1) application remains the deployable dashboard, authority for client accounts, billing and production releases. Do not create a second customer database, login or production environment here.

## Vision

A customer should be able to ask TAKATAK:

> « Pourquoi mon site ne convertit pas ? Analyse les résultats, propose deux variantes, demande mon approbation, lance un test sécurisé et explique quelle version fonctionne le mieux. »

**Human approval → verified site and permissions → experiment → measured conversions → AI recommendation → controlled improvement.**

Unlike a standalone content generator, this loop connects the existing website, analytics, SEO, Studio and Social tools. AI must distinguish observed data, hypotheses and tested outcomes.

## Existing TAKATAK integration

| Responsibility | Existing authority | Intelligence OS addition |
| --- | --- | --- |
| Customer identity & tenant | TAKATAK-V1 AUTH / access context | Reuse signed-in active client; never trust client IDs from a browser |
| AI and provider routing | Existing TAKBOT and provider store | Growth agent suggestions and reviewed drafts |
| Credits and billing | Existing AI credit ledger | Transparent metering, no surprise charges |
| Web / SEO / Social | Existing providers and dashboards | Read-only evidence and measured site changes |
| Studio and organizer | Existing project / approval model | Reusable content workflow patterns, not an alternate store |
| Deployment | TAKATAK-V1 main → existing Coolify production | Incremental feature flags, canary and rollback |

## Repositories and progress

- **This repository:** durable product decisions, technical contracts, rollout plan and cross-repository mission coordination.
- **Executable implementation:** [TAKATAK-V1](https://github.com/takatakca/takatak-v1), where the web UI, API, database schemas and runtime should live unless a separately justified service is approved.
- [V1 tracking issue #334](https://github.com/takatakca/takatak-v1/issues/334) describes the product.
- [V1 draft PR #335](https://github.com/takatakca/takatak-v1/pull/335) includes the first pure server-side A/B allocation policy, synthetic tests and CI; **not merged or deployed as of this checkpoint**. Its exact-head [GitHub CI #44259072459](https://github.com/takatakca/takatak-v1/actions/runs/44259072459) completed successfully.
- [Intelligence OS mission #1](https://github.com/takatakca/TAKATAK-Intelligence-OS/issues/1) is the cross-repository roadmap.

## Start here

1. [Architecture and boundaries](docs/ARCHITECTURE.md)
2. [Implementation roadmap and acceptance](docs/ROADMAP.md)
3. [Integration contract for V1](docs/INTEGRATION_CONTRACT.md)
4. [Instructions for collaborating agents](AGENTS.md)

## Non-negotiable guardrails

- **Production target only**: do not build or maintain unused staging infrastructure. CI can run isolated, disposable test databases; that is not a staging deployment.
- Production schema changes require a reviewed backup and migration plan. No experiment changes customer traffic until explicitly enabled, verified and reversible.
- Default OFF, isolated tenant data, domain-verified site, human approval, consent-aware analytics, accurate statistical reporting and full audit.
- **Never auto-publish, modify DNS, buy ads, charge customers, spend provider credits or activate external APIs** based on an AI recommendation alone.
- Keep protected credentials, customer files and personal information out of this public repository.
- Verify live Coolify-served revision and real client-specific results before claiming a feature is operational.

Inspired by the direction of modern digital experience platforms such as [Optimizely](https://www.optimizely.com/developers); independent first-party implementation, not copied proprietary code.
