# Development Handover — 2026-09-07 (B)

**Supersedes:** `DEVELOPMENT_HANDOVER_2026-09-07.md`. That document remains in the repository as a historical record of the point where Event Builder Productivity & Training Only Event Audience Eligibility (`1c97ebb`) had just landed, with no Welfare work yet started. This document carries the resume point forward.

**Naming note:** the established convention in this repository is one immutable, dated handover file per docs-reconciliation session (`git log` shows every prior handover file was touched by exactly one commit — its creation — and never edited afterward). This checkpoint falls on the same calendar day as the existing `DEVELOPMENT_HANDOVER_2026-09-07.md`, so rather than edit that file in place (which would violate the immutable-checkpoint convention) or silently reuse its filename, this second same-day checkpoint is suffixed `B`. `DEVELOPMENT_HANDOVER_2026-09-07.md` is left completely untouched and remains an accurate record of state as of plugin `main` `1c97ebb`.

---

## DO NOT START NEW FEATURE DEVELOPMENT WITHOUT READING THIS

One further commit has landed and been accepted since the previous handover: **Welfare Workspace Workflows** (`5348403`) — a Welfare Concern Directory mobile/filter repair plus a new short operational Welfare Update capability. **Do not restart or re-scope this work.** See "Recently Completed" below and `SPRINTS.md`'s "Welfare Workspace Workflows" section for full delivery detail.

There is currently **no new confirmed Pre-MVP product decision** to start next. See "Recommended Next Starting Point" at the end of this document — it names a specific next controlled task, but that task is a **source audit / architecture step**, not authorisation to begin implementing Staff Compliance or a restricted Welfare Person profile.

---

## Current Git Baseline

- Plugin `main`: `5348403b36665e4960e3c6b4ac41f502d80d7a7a` ("feat: improve welfare workspace workflows")
- Plugin status: **clean after push** — verified via `git status --short` returning nothing and `git rev-parse HEAD` matching the commit above; `origin/main` confirmed at the same commit
- Docs baseline immediately before this reconciliation: `main` at `1449322f426e091331854c4811c558c590a3d983` ("docs: reconcile event builder and release readiness state"), clean — this reconciliation's own docs commit is not yet made; the Product Owner/lead developer will review before it is committed
- Prior plugin baseline (`DEVELOPMENT_HANDOVER_2026-09-07.md`): `1c97ebbd55854ccc7343419acf498ec0fca8cfdf`

## Current Phase

**Operational MVP / Internal Club Testing / Release Readiness** — unchanged. See `MASTER_DEVELOPER_GUIDE.md`'s "Current Priority": Final Release Readiness / Club OS v1.0 sign-off remains the overall priority; this Welfare batch is a completed piece of ongoing MVP-polish/functional-gap work within that phase, not a phase change.

---

## Recently Completed (since the 2026-09-07 handover)

### Welfare Workspace Workflows — `5348403`

Two accepted deliverables, reached across a controlled multi-round process (source audit → implementation → manual acceptance → a manually-rejected interim dashboard action → a final security/polish pass), all before this single commit:

1. **Welfare Concern Directory / mobile-filter presentation repair.** The Search/Status/Priority/Assigned Welfare Officer filters now reuse the existing, already-responsive `.iexel-experience-form-grid`/`.iexel-experience-field` component instead of a read-only stat-display component — fixing the ~320px Assigned Welfare Officer overhang and the browser-native appearance with **zero new CSS**.
2. **Welfare Updates — a short operational handover log**, deliberately separate from the generic Activity History. Dedicated append-only persistence (`welfare_concern_updates`, registered through the existing `DatabaseManager`/`UpgradeRunner` canonical schema convention — no invented migration mechanism); no edit/delete/attachments/rich-text/visibility model in this MVP; server-derived author and timestamp (never request-trusted); 1,000-character plain-text cap with no silent truncation; newest-first deterministic ordering (`created_at DESC, id DESC`); and — the core guarantee — **the operational text is never duplicated into the generic `activity_log` table's message or metadata**, which instead records only a fixed "Added a Welfare update." event with the Concern reference and update id.

**Rejected and removed before commit — do not treat as delivered:** a temporary dashboard action linking Emergency Contacts/Players Requiring Attention rows to "View concerns" was manually identified as semantically wrong (a Player can need attention with zero Concerns) and fully removed, including all of its supporting plumbing, which was audited first and confirmed to have no other legitimate caller.

Full, precise, source-verified delivery detail — including exact security findings, live database verification evidence, and the full validator list — is in `SPRINTS.md`'s "Welfare Workspace Workflows" section, and in `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s Welfare Workspace direction section (which also carries the precise approved future shape of Staff Compliance and the restricted Welfare Person projection — see below).

---

## Known Current Welfare State

- ✅ Welfare Updates (short operational handover log) — **implemented**, `5348403`.
- ❌ Detailed safeguarding case notes / allegation or evidence records — **not implemented**, and not the same thing as a Welfare Update. Do not conflate the two.
- ❌ Attachments — **not implemented**.
- ❌ Restricted Welfare Person profile/projection — **not implemented**. No Welfare-scoped Person read route exists; the Welfare dashboard's Emergency Contacts and Players Requiring Attention rows remain informative-only pending this.
- ❌ Staff Compliance (DBS/safeguarding/first-aid/qualifications) — **not implemented**. Approved future product direction only (see below) — not scaffolded, scheduled or begun.

---

## Known Technical Debt / Validator Caveats

Carried forward unchanged from `DEVELOPMENT_HANDOVER_2026-09-07.md` (none of the items below were touched by the Welfare batch):

- **Dev-fixture drift, not a product defect:** several DB-integrated Match Mode validators assume Person 19 is a genuine current Team-1 Player; on this dev database Person 19 is a Team-6 Player. Blocks `tools/validate-match-goal-live-eligibility.php` from running end-to-end. **Do not change production behaviour or seed data to silence this.**
- **`tools/validate-team-events-badge-mobile-repair.php`** has a separate, pre-existing, unrelated breakpoint assertion failure (`.iexel-team-event-past-meta` at 480px).
- **`tools/validate-visual-foundation.php`** — pre-existing, unrelated `"Public stylesheet dependency order changed."` failure, re-confirmed via `git stash` during the Welfare batch's own final validation pass to reproduce identically at the clean `1c97ebb` baseline. Not caused by, and not repaired by, the Welfare batch.
- **Person 176 orphaned Team Assignment** — an active `team_assignments` row referencing a `person_id` with no corresponding `people` row. Genuinely open; needs a dev-database data-integrity fix, not a code change.
- **Secretary late-add `EventAudienceBuilder::add_attendee()`/`add_attendees_batch()`** perform no eligibility validation of their own.
- **Raw Team `age_group` string normalisation** — regular-player same-age-group Team matching still does an exact string match, unlike Training Only matching.
- **Secretary's separate Event-creation architecture** (`PortalSecretaryEventAddPage.php`) — Cross-Team Duplicate was deliberately not built into it.
- Pre-existing, explicitly untouched: the `venue_mode` PHP warning; duplicated `public.css` rule blocks; the unused `EventRepository::duplicate()` method.

---

## Deferred Work (unchanged, do not restart without approval)

- Historical Match Participation Evidence opportunities — unchanged.
- The Release Readiness work described in `DEVELOPMENT_HANDOVER_2026-08-29.md` ("Remaining Release Checklist Work") remains outstanding.
- FIN-031 and OS-011 remain open MVP-scope roadmap items, neither promoted as the next batch — unchanged.
- The data-integrity items above (Person 176, raw `age_group` normalisation, Secretary late-add eligibility audit) are genuinely open data/validator hygiene items, not product features.
- **Restricted Welfare Person projection** and **Staff Compliance** — both approved future direction, both genuinely unimplemented (see "Known Current Welfare State" above and the next section).

---

## Recommended Next Starting Point

No new confirmed Pre-MVP product decision beyond the Welfare batch above is currently open. There is no already-authorised implementation batch — **the next task should be selected from the priorities below, not invented.**

The next controlled Welfare/shared-architecture task, per current confirmed product direction, is:

**Welfare People + Staff Compliance — source audit / architecture (not implementation).**

Current approved product direction to inform that audit:

- A single canonical, **shared** Person/staff credential record — explicitly not two duplicated Secretary/Welfare credential systems — with role-appropriate Secretary and Welfare projections.
- Covers DBS, safeguarding, first aid, and FA/custom qualifications; the credential type list must remain extensible, not a brittle hard-coded enum.
- Each credential: type/name, issue/award date, optional expiry/renewal date, optional reference/registration number where appropriate, a short administrative note, auditability, and a derived status.
- Likely semantic states: `Valid`, `Expiring soon`, `Expired`, `No expiry`/equivalent, `Missing/Incomplete` where appropriate.
- Semantic colour only for severity — expired = red, expiring soon = amber/warning, valid = the normal success/neutral treatment. **Never the club accent colour** for compliance severity.
- Advance expiry attention should eventually surface in the appropriate Welfare/Secretary priority areas.
- Separately, a restricted Welfare Person projection — reusing existing authorised read services under the existing `can_view_welfare()` capability, never the Secretary Person Profile wholesale — remains a smaller, independently-schedulable piece of the same general direction; it must never leak Finance, Registration administration, Team Assignment controls or unrelated Secretary operations.

1. Re-read `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s Welfare Workspace direction section and "Recommended next implementation batch" section for the precise current wording before scoping any implementation.
2. Consider whether Release Readiness sign-off work (per `MASTER_DEVELOPER_GUIDE.md`'s "Current Priority") should take precedence over this or any other polish/feature work.
3. Consider whether the Person 176 data-integrity item warrants a small, separate, explicitly-scoped fix before it is forgotten.
4. Prefer a small source-first verification step before implementing anything — the same approach that has repeatedly revealed items were already further along (or already complete) than the roadmap recorded.

**Important "do not restart" notes:**
- Do not re-implement the Welfare Concern Directory mobile/filter repair, or the Welfare Update capability (persistence, validation, authorization, activity-log separation, UI placement) — complete.
- Do not reintroduce the "View concerns" dashboard action on Emergency Contacts/Players Requiring Attention — manually rejected and removed.
- Do not begin Staff Compliance or the restricted Welfare Person projection as implementation — both remain a future controlled task, starting with a source audit, not a feature build.
- Do not re-implement any item listed as complete in `DEVELOPMENT_HANDOVER_2026-09-07.md` — that document's "do not restart" notes remain in force unchanged.
