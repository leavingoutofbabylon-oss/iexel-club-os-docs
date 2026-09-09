# Development Handover — 2026-09-09 (B)

**Supersedes:** `DEVELOPMENT_HANDOVER_2026-09-09.md`. That document remains in the repository as a historical record of the point where the MVP Release Candidate validation cycle (RC-01 → RC-03-CLOSE) had just completed with Product Owner sign-off, and the "Guardian Link Role Synchronisation Audit" had just been recorded as a Product Owner observation/audit candidate — not yet run, not yet decided. This document carries the resume point forward through that audit's completion and its approved implementation.

---

## DO NOT START NEW FEATURE DEVELOPMENT WITHOUT READING THIS

Since the previous handover, one further commit has landed — a **post-RC follow-up batch**, not new feature work and not a reopening of RC validation:

- `29220cc0d6be03085c5096bf6bbe3af044d01741` — "fix: align guardian relationship role handling" (Post-RC Guardian Link Alignment Batch 1)

**The MVP Release Candidate remains technically validated with Product Owner manual sign-off PASSED — this handover does not change that status.** See "MVP Release Candidate — Status (unchanged)" below. **Do not restart or re-scope any of RC-01, RC-02A, RC-02A-R1, RC-02B, RC-03, RC-03-R1, RC-03-CLOSE, or Guardian Link Alignment Batch 1.** Do not invent an "RC-04." Do not treat this as production deployment — see "What this does and does not mean" below.

---

## Current Git Baseline

- Plugin `main`: `29220cc0d6be03085c5096bf6bbe3af044d01741` ("fix: align guardian relationship role handling")
- Plugin status: **clean** — verified via `git status --short` returning nothing, `git rev-parse HEAD` matching the commit above, and local `main` confirmed identical to `origin/main`
- Docs starting baseline for this reconciliation: `main` at `76e09bd54a8b78e5dab4ab053c5b1081a7b34d00` ("docs: close MVP release candidate validation"), clean — this reconciliation's own docs commit is not yet made; the Product Owner/lead developer will review before it is committed
- Prior plugin baseline (`DEVELOPMENT_HANDOVER_2026-09-09.md`): `3ee4c92963e8721b5562aa3a64e3706f81a346dc`
- Post-RC checkpoint: Guardian Link Alignment Batch 1 (`29220cc0d6be03085c5096bf6bbe3af044d01741`)

## Current Phase

**MVP Release Candidate technically validated; Product Owner manually signed off; one post-RC follow-up batch (Guardian Link Alignment Batch 1) also complete.** See "What this does and does not mean" below for the precise, non-speculative reading of that statement.

---

## MVP Release Candidate — Status (unchanged)

Nothing about the RC validation cycle's outcome has changed since the previous handover. The current build (plugin `29220cc0d6be03085c5096bf6bbe3af044d01741`) has:

- **ZERO evidenced P0 release blockers**
- **ZERO evidenced unresolved P1 release blockers**
- **Product Owner manual sign-off: PASSED** (against `3ee4c92`, still valid — Guardian Link Alignment Batch 1 is a subsequent, separately-completed post-RC follow-up, not a change requiring re-sign-off of the RC itself)

### What this does and does not mean

This means: **the MVP Release Candidate is technically validated and Product Owner accepted, and one further post-RC follow-up batch has since been implemented, validated, committed and pushed.** It does **not** mean Club OS has been deployed to production, that a release tag/branch has been cut, or that any of the `RELEASE_CHECKLIST.md` "Release"/"Post-Release" steps have occurred — those remain a distinct, separate project step and no evidence in this cycle claims otherwise. `RELEASE_CHECKLIST.md` itself was not modified by Guardian Link Alignment Batch 1 — it is post-RC follow-up work, not part of the RC evidence/history the checklist records.

**For the full RC-01 → RC-03-CLOSE narrative, see the previous handover (`DEVELOPMENT_HANDOVER_2026-09-09.md`) and `SPRINTS.md`'s "MVP Release Candidate Validation Cycle (RC-01 → RC-03-CLOSE)" section — it is not reproduced again here, and nothing in it has changed.**

---

## Post-RC Guardian Link Alignment Batch 1 (this handover's subject)

**Status: Complete.** Plugin `main` `29220cc0d6be03085c5096bf6bbe3af044d01741`. Full delivery detail is recorded in `SPRINTS.md`'s "Post-RC Guardian Link Alignment Batch 1" section; summarised here for resume-point purposes.

### Origin

The previous handover recorded a Product Owner workflow observation as an audit candidate: manually linking a Person to a Player as Parent/Guardian via Secretary's Guardian Links appeared to require pre-assigning the Parent role first. A read-only audit ran, confirmed this was accurate for the Secretary workflow, and surfaced a related Treasurer-authorization question that was resolved in the same batch.

### Final behaviour

- **Secretary:** an otherwise-valid active adult Person can now be selected in Guardian Links without a pre-existing Parent/Guardian role. `PersonRelationshipManagementService::link_existing_adult()` (under `POLICY_SECRETARY`) transactionally ensures the corresponding role (`parent_of` → `parent`, `guardian_of` → `guardian`) as a consequence of the relationship write — idempotent, preserving unrelated existing roles, enforced server-side (a direct/crafted POST behaves identically to the UI).
- **Treasurer:** confirmed intentionally different. A pure Treasurer does not hold `iexel_manage_person_roles` (Secretary-specific, explicitly withheld by `ClubRoleCapabilityRegistrar`). Under `POLICY_TREASURER`, the adult must already hold the role matching the *requested* relationship type; a zero-role adult is rejected server-side with no role/relationship side effects, and the pre-existing incidental cross-role top-up (traced to pristine code and confirmed policy-blind, not an authorised Treasurer capability) is now also rejected. Treasurer's candidate picker remains role-filtered; only its per-candidate eligibility probe was corrected (checking both relationship types instead of a hardcoded one) so already-valid candidates are not accidentally hidden.
- **Architecture preserved:** RELATIONSHIP and ROLE remain distinct domain concepts; a canonical family-link workflow may ensure a role only where its policy is authorised to do so. See `MASTER_DEVELOPER_GUIDE.md`'s new "Family Relationship Role Consequences" durable rule.
- **Registration/Prospect — corrected characterisation:** the original audit overstated both. Normal current Registration matching/validation and Prospect guardian matching already prevent/require the role through their own existing gates in the supported workflow. The role-ensures added to both in this batch are defense-in-depth / canonical-invariant protection, not fixes for a currently reachable bypass — and for Prospect, effectively a no-op for a currently matched existing guardian. **Do not describe Registration or Prospect as currently permitting a roleless matched adult through normal flows.**
- **Unchanged:** removing a relationship does not auto-remove the role (multi-child guardians keep their role when one child link is removed); `MemberExperienceResolver`'s Parent-persona tolerance is unchanged; no backfill/migration; no schema change; no capability added, removed, or reassigned.

### Validation evidence

| Validator | Result |
|---|---|
| `validate-treasurer-finance-relationships.php` | PASS — 264 |
| `validate-secretary-guardian-linking.php` | PASS — 70 |
| `validate-secretary-person-role-management.php` | PASS — 262 |
| `validate-admin-person-role-dependency-guards.php` | PASS — 91 |
| `validate-admin-person-role-sync.php` | PASS — 54 |
| `validate-treasurer-operational-read-access.php` | PASS — 45 |
| `validate-registration-existing-player-link.php` | PASS — 75 |
| `validate-family-relationship-integrity.php` | 70 passed / 1 confirmed baseline-only failure |
| `validate-prospect-training-conversion.php` | 1 confirmed baseline-only failure |

Both baseline-only failures pre-date this batch, were reproduced identically against the pristine pre-batch source, and are unrelated to this work — not regressions. Runtime security proof (Treasurer roleless/cross-role rejection; Secretary roleless success) was independently confirmed live on disposable RC Upgrade, fixtures fully cleaned up, environment restored.

### Known debt / deferred items introduced by this batch

None. This batch introduced no new deferred debt.

---

## Known Technical Debt / Validator Caveats

Unchanged from `DEVELOPMENT_HANDOVER_2026-09-09.md` — carried forward verbatim, since Guardian Link Alignment Batch 1 introduced no new debt. See that handover, and `SPRINTS.md`'s "Known Technical Debt / Validator Caveats" and "Post-RC Guardian Link Alignment Batch 1" sections, for the full current list (the `CANONICAL_TABLES` 49-vs-51 gap, the `TeamStatisticsService.php:203` latent pattern, the CRLF validator-methodology note, the no-current-Season warning copy, the DevTools 404 observation, `validate-current-emergency-contact.php`, Person 19/Team 1 fixture drift, `validate-team-events-badge-mobile-repair.php`, `validate-visual-foundation.php`, `validate-team-workspace-overview-shell-polish.php`, Person 176 orphaned Team Assignment, Secretary late-add eligibility, raw `age_group` normalisation, and FIN-031).

**One item's status has changed:** the **Guardian Link Role Synchronisation Audit** is no longer open — it completed and its approved correction is Guardian Link Alignment Batch 1, recorded above. Do not continue to list it as an open audit candidate in any future document.

---

## Deferred / Post-MVP Work (unchanged unless noted, do not restart without approval)

Unchanged from `DEVELOPMENT_HANDOVER_2026-09-09.md`, minus the Guardian Link Role Synchronisation Audit (now complete, see above). Remaining candidates: **Treasurer premium visual treatment**, **Coach lineup formation-preservation enhancement**, **Generic custom formation labels**, **Same-context navigation friction**, **OS-011** (Welfare Concern Detail hierarchy polish), the data-integrity items (Person 176, raw `age_group` normalisation, Secretary late-add eligibility audit), **DevTools 404/status-code observation**, the RC-02A-introduced items, and Historical Match Participation Evidence opportunities (Post-v1).

Do not restart any completed workspace MVP sweep, RC-cycle repair, or Guardian Link Alignment Batch 1 — all remain complete as recorded here, in `MASTER_DEVELOPER_GUIDE.md`'s "Recently Completed", and in `SPRINTS.md`.

---

## Post-RC Next Development Position

We are still not in active Release Candidate defect closure, and Guardian Link Alignment Batch 1's completion does not itself select the next item. The next development work should be selected deliberately from the approved post-RC backlog / Product Owner priorities — this handover does not select one on its own authority.

Reviewing `SPRINTS.md`, `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s "Recommended next implementation batch" section, and this handover together, the candidates are:

1. **OS-011** (Welfare Concern Detail hierarchy polish, Medium priority) — genuinely open, cosmetic/non-blocking.
2. **Person 176 orphaned Team Assignment** — a small, genuinely open dev-database data-integrity item, not a product feature.
3. The separate `RELEASE_CHECKLIST.md` "Release"/"Post-Release" gate (tagging, deployment) — a distinct project step from the technical/product validation this handover records, and not itself a development task.

**The Guardian Link Role Synchronisation Audit is no longer a candidate on this list — it is complete** (Batch 1, above). Any further family/guardian enhancement (e.g. automatic role removal on unlink, deliberately left unchanged by Batch 1) would be new, separately-prioritised work, not a continuation of this audit.

**Product Owner/lead developer prioritisation is needed** to choose between the remaining candidates — none is unambiguously dominant per the authoritative docs. **Do not invent or begin a new implementation batch, an "RC-04," a Staff Compliance "Batch E," or a "Guardian Link Batch 2" from this handover's description alone.**

**Important "do not restart" notes:**
- Do not re-implement or re-scope RC-01, RC-02A-R1, RC-03-R1, or Guardian Link Alignment Batch 1 — all complete and closed.
- Do not re-open RC-02A, RC-02B, or RC-03 as if their findings were still pending — they are recorded in the previous handover.
- Do not re-open the Guardian Link Role Synchronisation Audit as if it were still an undecided observation — it is complete, and its findings are recorded above and in `SPRINTS.md`.
- Do not re-implement any item listed as complete in earlier handovers — those documents' "do not restart" notes remain in force unchanged.
