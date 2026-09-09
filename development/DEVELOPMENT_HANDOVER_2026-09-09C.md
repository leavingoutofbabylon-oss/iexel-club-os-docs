# Development Handover — 2026-09-09 (C)

**Supersedes:** `DEVELOPMENT_HANDOVER_2026-09-09B.md`. That document remains in the repository as a historical record of the point where the MVP Release Candidate validation cycle had just completed with Product Owner sign-off, and Post-RC Guardian Link Alignment Batch 1 had just landed. This document carries the resume point forward through a second, separate post-RC follow-up batch: Treasurer Premium Workspace Alignment Batch 1, completed and Product Owner visually accepted.

---

## DO NOT START NEW FEATURE DEVELOPMENT WITHOUT READING THIS

Since the previous handover, one further commit has landed — a **post-RC follow-up batch**, not new feature work and not a reopening of RC validation:

- `840369102b5b1d24f7701c7d2af3b325971fa824` — "fix: align treasurer finance workspace" (Post-RC Treasurer Premium Workspace Alignment Batch 1)

**The MVP Release Candidate remains technically validated with Product Owner manual sign-off PASSED — this handover does not change that status.** See "MVP Release Candidate — Status (unchanged)" below. **Do not restart or re-scope any of RC-01, RC-02A, RC-02A-R1, RC-02B, RC-03, RC-03-R1, RC-03-CLOSE, Guardian Link Alignment Batch 1, or Treasurer Premium Workspace Alignment Batch 1.** Do not invent an "RC-04." Do not treat this as production deployment — see "What this does and does not mean" below.

---

## Current Git Baseline

- Plugin `main`: `840369102b5b1d24f7701c7d2af3b325971fa824` ("fix: align treasurer finance workspace")
- Plugin status: **clean** — verified via `git status --short` returning nothing, `git rev-parse HEAD` matching the commit above, and local `main` confirmed identical to `origin/main`
- Docs starting baseline for this reconciliation: `main` at `a82e8f0eef2505c7d747da1262190c324fc3e117` ("docs: record guardian link alignment"), clean — this reconciliation's own docs commit is not yet made; the Product Owner/lead developer will review before it is committed
- Prior plugin baseline (`DEVELOPMENT_HANDOVER_2026-09-09B.md`): `29220cc0d6be03085c5096bf6bbe3af044d01741`
- Post-RC checkpoints: Guardian Link Alignment Batch 1 (`29220cc0d6be03085c5096bf6bbe3af044d01741`), Treasurer Premium Workspace Alignment Batch 1 (`840369102b5b1d24f7701c7d2af3b325971fa824`)

## Current Phase

**MVP Release Candidate technically validated; Product Owner manually signed off; two post-RC follow-up batches (Guardian Link Alignment Batch 1, Treasurer Premium Workspace Alignment Batch 1) also complete, the second with its own dedicated Product Owner visual acceptance.** See "What this does and does not mean" below for the precise, non-speculative reading of that statement.

---

## MVP Release Candidate — Status (unchanged)

Nothing about the RC validation cycle's outcome has changed since the previous handover. The current build (plugin `840369102b5b1d24f7701c7d2af3b325971fa824`) has:

- **ZERO evidenced P0 release blockers**
- **ZERO evidenced unresolved P1 release blockers**
- **Product Owner manual sign-off: PASSED** (against `3ee4c92`, still valid — Guardian Link Alignment Batch 1 and Treasurer Premium Workspace Alignment Batch 1 are subsequent, separately-completed post-RC follow-ups, not changes requiring re-sign-off of the RC itself)

### What this does and does not mean

This means: **the MVP Release Candidate is technically validated and Product Owner accepted, and two further post-RC follow-up batches have since been implemented, validated, committed and pushed** — the second of which (Treasurer Premium Workspace Alignment Batch 1) also carries its own dedicated Product Owner **visual** acceptance, separate from the RC's own sign-off. It does **not** mean Club OS has been deployed to production, that a release tag/branch has been cut, or that any of the `RELEASE_CHECKLIST.md` "Release"/"Post-Release" steps have occurred — those remain a distinct, separate project step and no evidence in this cycle claims otherwise. `RELEASE_CHECKLIST.md` itself was not modified by either post-RC batch — both are post-RC follow-up work, not part of the RC evidence/history the checklist records.

**For the full RC-01 → RC-03-CLOSE narrative, see `DEVELOPMENT_HANDOVER_2026-09-09.md` and `SPRINTS.md`'s "MVP Release Candidate Validation Cycle (RC-01 → RC-03-CLOSE)" section — it is not reproduced again here, and nothing in it has changed. For the full Guardian Link Alignment Batch 1 narrative, see `DEVELOPMENT_HANDOVER_2026-09-09B.md` and `SPRINTS.md`'s "Post-RC Guardian Link Alignment Batch 1" section — also unchanged.**

---

## Post-RC Treasurer Premium Workspace Alignment Batch 1 (this handover's subject)

**Status: Complete. Product Owner visual acceptance PASSED.** Plugin `main` `840369102b5b1d24f7701c7d2af3b325971fa824`. Full delivery detail is recorded in `SPRINTS.md`'s "Treasurer Premium Workspace Alignment Batch 1" section and `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s section of the same name; summarised here for resume-point purposes.

### Origin

A read-only Treasurer/Finance workspace UX audit found Finance's own `.iexel-os-card`/`.iexel-finance-metrics` visual system read as pale and generic against the shared premium `.iexel-experience-hero`/`.iexel-experience-section`/`.iexel-experience-metrics` vocabulary already used elsewhere in Club OS (Secretary, Welfare, Treasurer's own People/Team/Registration pages). The audit proposed exactly one controlled implementation batch.

### Final behaviour

- **Finance's page framing, KPI strips and the great majority of its sections** now use the canonical `.iexel-experience-hero`/`.iexel-experience-section`/`.iexel-experience-metrics`/`.iexel-experience-metric` vocabulary. The legacy `.iexel-finance-workspace-header` and page-local `.iexel-finance-metrics` components are retired (confirmed unused first).
- **Invoice Detail's primary invoice record is the one deliberate exception, added by Product Owner direction after the initial migration was reviewed.** The primary invoice summary keeps the existing dark `.iexel-os-card` treatment (reused, not modified); its four supporting sections (Itemised Charges & Discounts, Payment Allocations, Invoice Timeline, Invoice Notes) use the light register. The resulting rhythm: light page identity → dark authoritative invoice record → light supporting detail sections. **Do not describe this as "every Finance card is dark" — Finance remains a premium light administrative workspace with one intentionally dark authoritative record.**
- **Two genuine mid-batch discoveries, both corrected in the same batch:** (1) `.iexel-os-card` actually resolves to a dark, gold-accented, white-text treatment via a second, later, more-specific rule in `public.css` — an earlier read-only audit had cited only the first, non-winning, plain-light rule; (2) `design-system.css` independently duplicated dark on-dark colour treatment for `.iexel-billing-schedule-card`/`.iexel-invoice-link` and their meta values, shared with several Team/Coach/Match dark-immersive components, silently overriding the first CSS fix. Both were found via live `getComputedStyle()` verification and corrected without touching the global `.iexel-os-card` rule or any Team/Coach/Match/Player entry.
- **Light-surface secondary-action readability fix:** the dark-native `.iexel-button-secondary` component was rendering white-on-near-white on four Finance actions that ended up on a light ancestor. Each now additionally carries the existing `iexel-fee-rule-back` component (already proven on the light Fee Rule/Discount Policy pages) — reuse, not a new treatment. See "Known debt / deferred items" below for the naming-debt disclosure this reuse carries.
- **Unchanged:** all Finance domain logic (`FinanceRepository`, `FinanceService`, invoice/payment/billing calculations, invoice lifecycle, payment allocation, `ResponsibleBillingContactResolver`), capabilities, routing, schema, migrations, exports and audit/activity behaviour. Every diff in `PortalFinanceWorkspacePage.php` is a markup/class-attribute change. The global `.iexel-os-card` and `.iexel-button-secondary` rules are both byte-unchanged. No other persona (Secretary/Welfare/Coach), Prospect styling, or wp-admin Finance surface was touched. Docs were not touched by the implementation work itself.

### Product Owner visual acceptance

**PASSED.** Accepted surfaces: Finance Overview, Invoices, Invoice Detail, Billing Schedules, Treasurer Dashboard, and 320px Invoice Detail.

### Validation evidence

| Validator | Result |
|---|---|
| `validate-parent-family-finance.php` | PASS — 44 |
| `validate-treasurer-billing-run-detail.php` | PASS — 93 |
| `validate-treasurer-directory-ux.php` | PASS — 34 |
| `validate-treasurer-finance-configuration.php` | PASS — 488 |
| `validate-treasurer-finance-relationships.php` | PASS — 264 |
| `validate-treasurer-invoice-detail.php` | PASS — 54 |
| `validate-treasurer-operational-read-access.php` | PASS — 45 |
| `validate-visual-foundation.php` | 1 confirmed baseline-only failure ("Public stylesheet dependency order changed", tied to untouched `PortalRouter.php` — not introduced by this batch) |

PHP lint passed on every touched PHP file throughout. `git diff --check` clean at every stage, including the final cumulative diff before commit.

### Known debt / deferred items introduced or reconfirmed by this batch

- **Finance Reports route defect (FIN-033, open)** — `finance-reports` is registered but not dispatched by the page's own `match($section)` handler and falls through to Finance Overview content. Deliberately not fixed (out of scope for a presentation-only batch). **Recommended next controlled development item** — see "Post-RC Next Development Position" below.
- **`iexel-fee-rule-back` naming debt** — the reused secondary-action component's name is narrower than its actual reuse (it originated on the Fee Rule page). Naming/architecture debt only; the visual treatment itself is accepted. Not fixed, deferred.
- **Premium Surface Colour Consistency Audit** — a broader future audit of Club OS's premium-surface colour consistency, identified as follow-on scope but not started by this batch. Must not be scoped as "make every pale card dark" or "make every Club OS page identical" — must distinguish intentionally light subordinate cards from surfaces genuinely inconsistent with the established hierarchy, and must preserve the immersive Team/Coach/Match Mode dark treatment where correct. Deferred, future/lower-priority unless newer evidence changes that.

---

## Known Technical Debt / Validator Caveats

Unchanged from `DEVELOPMENT_HANDOVER_2026-09-09B.md`, plus the three new items introduced/reconfirmed by Treasurer Premium Workspace Alignment Batch 1 above (Finance Reports route defect, `iexel-fee-rule-back` naming debt, Premium Surface Colour Consistency Audit). See that handover, and `SPRINTS.md`'s "Known Technical Debt / Validator Caveats" and "Treasurer Premium Workspace Alignment Batch 1" sections, for the full current list (the `CANONICAL_TABLES` 49-vs-51 gap, the `TeamStatisticsService.php:203` latent pattern, the CRLF validator-methodology note, the no-current-Season warning copy, the DevTools 404 observation, `validate-current-emergency-contact.php`, Person 19/Team 1 fixture drift, `validate-team-events-badge-mobile-repair.php`, `validate-visual-foundation.php`, `validate-team-workspace-overview-shell-polish.php`, Person 176 orphaned Team Assignment, Secretary late-add eligibility, raw `age_group` normalisation, and FIN-031).

**One item's status has changed:** the **Treasurer premium visual treatment** deferred candidate is no longer open — it completed as Treasurer Premium Workspace Alignment Batch 1, recorded above. Do not continue to list it as an open deferred candidate in any future document.

---

## Deferred / Post-MVP Work (unchanged unless noted, do not restart without approval)

Unchanged from `DEVELOPMENT_HANDOVER_2026-09-09B.md`, minus **Treasurer premium visual treatment** (now complete, see above), plus the three new deferred items from this batch: **Finance Reports route defect (FIN-033)**, **`iexel-fee-rule-back` naming debt**, and the **Premium Surface Colour Consistency Audit**. Remaining unchanged candidates: **Coach lineup formation-preservation enhancement**, **Generic custom formation labels**, **Same-context navigation friction**, **OS-011** (Welfare Concern Detail hierarchy polish), the data-integrity items (Person 176, raw `age_group` normalisation, Secretary late-add eligibility audit), **DevTools 404/status-code observation**, the RC-02A-introduced items, and Historical Match Participation Evidence opportunities (Post-v1).

Do not restart any completed workspace MVP sweep, RC-cycle repair, Guardian Link Alignment Batch 1, or Treasurer Premium Workspace Alignment Batch 1 — all remain complete as recorded here, in `MASTER_DEVELOPER_GUIDE.md`'s "Recently Completed"/"Current Priority", and in `SPRINTS.md`.

---

## Post-RC Next Development Position

We are still not in active Release Candidate defect closure, and Treasurer Premium Workspace Alignment Batch 1's completion does not itself mandate the next item without Product Owner/lead developer confirmation — but this handover does record a clear recommendation, unlike the previous handover's "no single dominant candidate" position.

**Recommended next controlled development item: the Finance Reports routing defect (FIN-033).** It is a small, well-scoped functional (not visual) Finance fix, directly identified during Batch 1 above. After that, retain the broader **Premium Surface Colour Consistency Audit** as future/deferred work unless newer evidence changes priority — it is a larger, less-scoped piece of work than Finance Reports and should not be started opportunistically.

Other genuinely open candidates, unchanged in status:

1. **OS-011** (Welfare Concern Detail hierarchy polish, Medium priority) — genuinely open, cosmetic/non-blocking.
2. **Person 176 orphaned Team Assignment** — a small, genuinely open dev-database data-integrity item, not a product feature.
3. The separate `RELEASE_CHECKLIST.md` "Release"/"Post-Release" gate (tagging, deployment) — a distinct project step from the technical/product validation this handover records, and not itself a development task.
4. **`iexel-fee-rule-back` naming debt** — small, low-priority, cosmetic-to-code-quality only.

**The Guardian Link Role Synchronisation Audit and the Treasurer premium visual treatment are no longer candidates on this list — both are complete** (Guardian Link Alignment Batch 1 and Treasurer Premium Workspace Alignment Batch 1, above).

**Product Owner/lead developer confirmation is still needed** before starting Finance Reports or any other item — this handover recommends, it does not unilaterally authorise. **Do not invent or begin a new implementation batch, an "RC-04," a "Guardian Link Batch 2," a "Treasurer Batch 2," or the Premium Surface Colour Consistency Audit from this handover's description alone.**

**Important "do not restart" notes:**
- Do not re-implement or re-scope RC-01, RC-02A-R1, RC-03-R1, Guardian Link Alignment Batch 1, or Treasurer Premium Workspace Alignment Batch 1 — all complete and closed.
- Do not re-open RC-02A, RC-02B, or RC-03 as if their findings were still pending — they are recorded in `DEVELOPMENT_HANDOVER_2026-09-09.md`.
- Do not re-open the Guardian Link Role Synchronisation Audit as if it were still an undecided observation — it is complete, recorded in `DEVELOPMENT_HANDOVER_2026-09-09B.md` and `SPRINTS.md`.
- Do not re-open the Treasurer Premium Workspace Alignment as if it were still awaiting Product Owner acceptance — visual acceptance has PASSED, recorded above and in `SPRINTS.md`.
- Do not extend the Invoice Detail dark-record exception to any other Finance surface without a fresh, explicit Product Owner decision.
- Do not re-implement any item listed as complete in earlier handovers — those documents' "do not restart" notes remain in force unchanged.
