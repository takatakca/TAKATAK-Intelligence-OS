# TAKATAK-V1 ↔ Intelligence OS integration contract (draft)

This document is a **design contract**, not an assertion that endpoints exist.

## 1. Responsibility boundaries

- The runtime stays in `takatakca/takatak-v1` until a separately approved service is justified.
- Access checks must use the existing V1 server-resolved active client, authenticated session and permission model.
- An experiment's `siteId`, `clientId` and `goalId` must be validated against the same workspace; no caller-selectable tenant override.
- Use V1's TAKBOT/provider store and credit ledger, never parallel API keys or billing ledgers.

## 2. Proposed internal domain entities (not migrated)

```text
Experiment(id, clientId, verifiedSiteId, lifecycle, revision, goalId,
           allocationBps, approvedBy, approvedAt, pausedAt, createdAt)
ExperimentVariant(id, experimentId, revision, contentSurface, contentDigest,
                  weightBps, immutableApprovedContent)
ExperimentAssignment(experimentId, revision, pseudonymousVisitorId, variantId,
                     createdAt, expiryAt)
ExperimentEvent(id, experimentId, revision, variantId, eventType,
                validatedGoalId, occurredAt, idempotencyKey)
ExperimentAudit(id, clientId, actorId, action, revision, createdAt)
```

All storage requires reviewed workspace FK and database-level isolation, retention and deletion policy. Never apply migration without protected production backup + review.

## 3. Lifecycle invariants

- Only managers with authenticated permission may create/edit a draft.
- An approved immutable revision may be launched only on a verified client-controlled surface after explicit audited approval and consent.
- `running` can be killed/paused by a privileged manager or global operator, even when provider services are unavailable.
- Updating content creates a new approved revision; running content must not silently mutate.
- Credits or paid APIs require a distinct quote and permission at dispatch; missing provider price is **unknown**, not free.

## 4. Allocation contract (P0 source only)

Current policy: `takatak-v1/src/lib/intelligence/experiment-allocation.ts` on [PR #335](https://github.com/takatakca/takatak-v1/pull/335).

`assignExperiment(...)` needs: enabled flag, active client from signed server context, audited human approval, site ownership proof, visitor consent, opaque visitor UUID, 32+ char HMAC key and valid 2–5 variant weighting totaling 10000 basis points. Reject absent gates. The result is either `assigned: false` with a safe reason or an experiment/revision/variant identifier. P0 intentionally persists nothing.

**Before a live experiment:** add consent-aware sticky assignment persistence; re-evaluate revision rebucketing semantics; server-validated exposure/conversion goals, privacy guards, abuse prevention, A/B report, deployment adapter and audit.

## 5. Minimum acceptance and deployment

- Simulated two-client tests and real authorized smoke showing a user in client B cannot access/activate A's experiment.
- Default OFF for all unapproved clients. Explicit opt-in for one verified first-party site.
- Domain verification, separate manager approval, reversible adaptation, clear live monitoring.
- Event idempotency, consent enforcement, data retention, reliable baseline and statistical uncertainty.
- Green CI at exact head, reviewed merge, existing Coolify production deployed SHA verified; real client-visible behavior independently tested before calling **LIVE**.

No staging deployment. Disposable CI fixtures are permitted. Do not infer production readiness from PR merge alone.
