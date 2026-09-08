# Development Handover — 2026-09-08

**Supersedes:** `DEVELOPMENT_HANDOVER_2026-09-07B.md`. That document remains in the repository as a historical record of the point where Welfare Workspace Workflows (`5348403`) had just landed, with Staff Compliance and the restricted Welfare Person projection both still unstarted product direction. This document carries the resume point forward.

---

## DO NOT START NEW FEATURE DEVELOPMENT WITHOUT READING THIS

Two further commits have landed and been accepted since the previous handover — **Staff Compliance Batch A (canonical foundation)** and **Staff Compliance Batch B (Secretary Person Profile + management route)**, the latter including a dedicated correction/repair round. **Do not restart or re-scope either.** See "Recently Completed" below and `SPRINTS.md`'s "Staff Compliance — Batch A & Batch B" section for full delivery detail.

The next recommended implementation batch is named at the end of this document: **Staff Compliance Batch C — Restricted Welfare People Projection + Welfare Compliance Experience.** It has not been started. Nothing below authorises beginning it without a fresh confirmation from the Product Owner/lead developer.

---

## Current Git Baseline

- Plugin `main`: `3352d300ab8fde56d47d307deacdab4b1f35d64a` ("feat: add secretary staff compliance management")
- Plugin status: **clean** — verified via `git status --short` returning nothing and `git rev-parse HEAD` matching the commit above; `origin/main` confirmed at the same commit
- Docs baseline immediately before this reconciliation: `main` at `1bcc3e71321e2b7838bed627a128885058a9348e` ("docs: reconcile welfare workspace workflows"), clean — this reconciliation's own docs commit is not yet made; the Product Owner/lead developer will review before it is committed
- Prior plugin baseline (`DEVELOPMENT_HANDOVER_2026-09-07B.md`): `5348403b36665e4960e3c6b4ac41f502d80d7a7a`
- Staff Compliance checkpoints, in order:
  - Batch A (canonical foundation): `b5f006a66cdcd8df9e127c27da1a94b570b93514` ("feat: add staff compliance foundation")
  - Batch B (Secretary Person Profile + Compliance Management UI, including the correction/repair and eligibility/layout rounds): `3352d300ab8fde56d47d307deacdab4b1f35d64a` ("feat: add secretary staff compliance management")

## Current Phase

**Operational MVP / Internal Club Testing / Release Readiness** — unchanged. See `MASTER_DEVELOPER_GUIDE.md`'s "Current Priority": Final Release Readiness / Club OS v1.0 sign-off remains the overall priority; Staff Compliance is a deliberately pulled-forward piece of the previously Post-MVP Welfare/compliance direction, not a phase change.

---

## Recently Completed (since the 2026-09-07B handover)

### Staff Compliance Batch A — Canonical Domain Foundation — `b5f006a6`

A new canonical, shared credential domain, entirely independent of any UI:

- **Storage:** `{prefix}iexel_os_person_credentials`, registered through the exact `DatabaseManager`/`UpgradeRunner` trio every other canonical table uses. A credential belongs to the canonical `Person`, never primarily to a WordPress user — `wp_user_id` is never required. No persisted derived-status column; status is always computed at read time.
- **Categories:** `dbs`, `safeguarding`, `first_aid`, `qualification` — a stable, reviewed list, not a hard-coded catalogue of specific qualifications (only the four *categories* are fixed; a `qualification` record's own name is free text).
- **Lifecycle:** `active` / `archived`. No hard-delete action exists anywhere in the domain.
- **Current/relevant record** for a core category (`dbs`/`safeguarding`/`first_aid`) is a read-time query — the newest non-archived record ordered `issued_on DESC, id DESC` — never a uniqueness constraint. Qualifications are never collapsed to one record.
- **Derived status:** `Valid` / `Expiring Soon` (42-day domain constant, no Settings UI) / `Expired` / `No Expiry`, via `CredentialStatus::derive()` — a pure function.
- **Capabilities:** narrow, standalone `iexel_view_staff_compliance` / `iexel_manage_staff_compliance` pair. Club Admin/administrator get every capability (self-healing). Welfare Officer gets the pair directly on its WP role. Secretary gets the pair as a **direct per-user capability grant**, re-synced whenever a Person's canonical roles change, with a one-off `StaffComplianceCapabilityBackfill` retroactively covering already-linked Secretaries. Ordinary Committee, Coach, Treasurer, Parent, Player inherit neither capability.
- **Domain classes:** `CredentialType`, `CredentialLifecycle`, `CredentialStatus`, `PersonCredential`, `PersonCredentialValidator`, `PersonCredentialRepository`, `PersonCredentialService` — namespace `IEXEL\ClubOS\Core\StaffCompliance`.

No UI existed in this batch. Focused validator `tools/validate-staff-compliance-foundation.php` (static, no WP bootstrap) was created at 99/99 at the time and later extended twice by Batch B (see below).

### Staff Compliance Batch B — Secretary Person Profile + Compliance Management — `3352d300`

Built across three controlled rounds (initial implementation → a targeted correction/repair for full-record editing → a final club-official-eligibility + responsive-UX repair), all landing in this one commit:

- **Secretary Person Profile summary:** DBS/Safeguarding/First Aid status + qualification count + Manage Compliance action, shown **only for an eligible Person** (see below) — absent entirely, never a placeholder, for an ineligible one.
- **Dedicated route:** `/club-os/secretary/people/{PERSON_ID}/compliance/` (`PortalSecretaryPersonCompliancePage`, POST dispatched from `PortalRouter` exactly like Medical & Safety/Emergency Contact — never `admin-post.php`). Requires an active Secretary/Admin persona **and** the narrow `can_manage_staff_compliance()` capability **and** target-Person eligibility, all three independently. A genuine Welfare Officer holding the capability is still denied this route because their active persona is Welfare, not Secretary.
- **Workflow:** Current Compliance, Qualifications (never collapsed), Add Credential (a genuine renewal — always a new row, never archives the record it supersedes), Correction (`PersonCredentialService::correct()` — updates the SAME record's type/name/dates/reference/note in place, never a second row, never an archive), Archive (explicit lifecycle retirement only, never automatic on renewal, never a hard delete).
- **Type-aware credential naming (final shape):** DBS is canonical-name-only (no name field shown, any submission discarded); Safeguarding/First Aid take an *optional* specific course name with a canonical fallback when blank; Qualification requires a free-text name. `credential_type` remains canonical and drives current-record selection; `credential_name` is descriptive only. A small dedicated `assets/js/staff-compliance-form.js` progressively enhances the Add/Edit form's Credential Type → Name field behaviour, following the existing lightweight `data-*`/`change`-listener pattern already used by `team-assignments.js` — server-side resolution remains authoritative regardless of JavaScript.
- **Target-Person eligibility (`StaffCompliancePersonEligibility`)** — a durable Batch B product rule, not just an authorization detail: eligible only when the Person currently holds at least one of `club_admin`/`secretary`/`treasurer`/`welfare_officer`/`committee_member` (club-wide) or `coach`/`assistant_coach`/`manager` (team staff assignment), reusing the exact canonical `PeopleRepository::roles_for_person()` active-role set already relied on elsewhere — no second role computation, no `wp_user_id` requirement. Enforced identically in three places (Profile summary, the route, the request handler) so it can never drift; an ineligible-Person denial and a non-existent-Person denial are identical and non-disclosing. Removing a Person's final qualifying role makes the UI/route unavailable immediately (recomputed live) **without deleting or archiving any existing credential history**. See `MASTER_DEVELOPER_GUIDE.md`'s new "Target-Person Eligibility vs Current-User Authorization" engineering rule, generalised from this exact case.
- **Desktop layout repair:** a genuine Product-Owner-identified defect (populated rows collapsing to one character per line) was root-caused to the shared `.iexel-experience-item-actions{width:100%}` rule leaking from its intended `.has-actions` grid context into this page's plain flex layout, and fixed by adopting the same established `.has-actions`/`.iexel-experience-item-copy` convention already used by `PortalSection::action_item()` — no shared CSS changed for this, no fixed pixel widths introduced. A separate, small, genuinely necessary CSS fix (`.iexel-experience-field[hidden]{display:none}`) restores the browser's standard `[hidden]` behaviour, which an existing `display:grid` rule was silently overriding for every field in the design system.

**Validation:** `tools/validate-staff-compliance-foundation.php` **108/108**; new `tools/validate-staff-compliance-secretary-ui.php` **97/97**. Regression unaffected across Secretary People/editing/role-management/mobile-responsive, Welfare Workspace Batch 1 (one stale over-broad guard corrected — scoped to that batch's own files rather than the whole shared router — result unchanged at 118/118), Committee permissions, plain-permalink routing, Secretary Team Assignments, Team Staff operational access, and admin Person-role sync/dependency-guard validators. Full detail, exact live-database verification evidence and the complete validator list are in `SPRINTS.md`'s "Staff Compliance — Batch A & Batch B" section.

Product Owner manually accepted the overall Secretary Staff Compliance experience, the corrected populated desktop layout, and 320px responsive behaviour.

---

## Known Current Staff Compliance / Welfare State

- ✅ Staff Compliance canonical domain (DBS/safeguarding/first-aid/qualification, status derivation, capabilities) — **implemented**, `b5f006a6`.
- ✅ Secretary Staff Compliance management (Profile summary, dedicated route, Add/Correct/Archive, target-Person eligibility, type-aware naming, desktop layout) — **implemented**, `3352d300`.
- ❌ Restricted Welfare Person profile/projection — **not implemented**. No Welfare-scoped Person read route exists; the Welfare dashboard's Emergency Contacts and Players Requiring Attention rows remain informative-only pending this.
- ❌ Welfare Staff Compliance read/write projection — **not implemented**. Must reuse the now-canonical `PersonCredentialService`/domain exactly as-is; must never duplicate storage or validation.
- ❌ Compliance expiry alerts / dashboard integration — **not implemented**. Approved future direction (Staff Compliance Batch D) only.
- ❌ Detailed safeguarding case notes / allegation or evidence records — **not implemented**, and not the same thing as either a Welfare Update or a Staff Compliance administrative note (both are short and non-case-note by design).
- ❌ Configurable compliance expiry threshold — **not implemented**; the 42-day "Expiring Soon" window is a domain constant with no Settings UI.
- ❌ Hard-coded FA/other qualification catalogue — deliberately **not implemented**; Qualification names remain free text.
- ❌ Credential hard delete — deliberately **not implemented**; Archive is the only retirement action.
- ❌ Attachments (Welfare) — **not implemented**, unchanged from the previous handover.

---

## Capability / Workspace Boundaries (Staff Compliance)

Recorded explicitly because target-Person eligibility and current-user authorization are easy to conflate:

- **Club Admin:** authorised to manage Staff Compliance for any *eligible* target Person; does **not** bypass target-Person eligibility itself.
- **Secretary:** receives `iexel_manage_staff_compliance` via the existing canonical direct per-user capability architecture (`OperationalRoleAccessManager`); this is what actually gates the Secretary Compliance route, together with the active Secretary persona and target-Person eligibility.
- **Welfare Officer:** receives the same shared capability pair directly on the WP role — genuinely holds `can_manage_staff_compliance()` — but this does **not** grant access to the *Secretary* Compliance route, because that route additionally requires the active Secretary/Admin persona. Welfare gets its own restricted projection in Batch C, not this route.
- **Ordinary Committee:** does not inherit Staff Compliance capability merely because Secretary's own grant partly overlaps with committee-adjacent WP-role architecture elsewhere in the codebase — Committee has neither capability.
- **Coach / Manager / Treasurer (as target Persons):** being an *eligible target Person* for Staff Compliance does not itself grant *permission to manage* anyone's Staff Compliance — eligibility and authorization are independently checked.
- **Parent / Player:** not authorised, and (being ineligible targets in the ordinary case) not presented with the feature either.

---

## Known Technical Debt / Validator Caveats

Carried forward unchanged from `DEVELOPMENT_HANDOVER_2026-09-07B.md` (none of the items below were touched by Staff Compliance), plus one Staff-Compliance-specific item confirmed still present:

- **`tools/validate-current-emergency-contact.php`** — a pre-existing, unrelated schema/data-version assertion failure ("Schema version was not advanced for this batch." / "Data version changed despite no data migration in this batch."), re-confirmed via `git stash` to reproduce identically at the clean Batch-A baseline with none of the Staff Compliance work applied. **Not caused by, and not repaired by, Staff Compliance. Do not treat this as a Staff Compliance blocker.**
- Dev-fixture drift, not a product defect: several DB-integrated Match Mode validators assume Person 19 is a genuine current Team-1 Player; on this dev database Person 19 is a Team-6 Player. Blocks `tools/validate-match-goal-live-eligibility.php` from running end-to-end. **Do not change production behaviour or seed data to silence this.**
- **`tools/validate-team-events-badge-mobile-repair.php`** has a separate, pre-existing, unrelated breakpoint assertion failure (`.iexel-team-event-past-meta` at 480px).
- **`tools/validate-visual-foundation.php`** — pre-existing, unrelated `"Public stylesheet dependency order changed."` failure, previously re-confirmed via `git stash` during the Welfare batch's own final validation pass.
- **Person 176 orphaned Team Assignment** — an active `team_assignments` row referencing a `person_id` with no corresponding `people` row. Genuinely open; needs a dev-database data-integrity fix, not a code change.
- Secretary late-add `EventAudienceBuilder::add_attendee()`/`add_attendees_batch()` perform no eligibility validation of their own.
- Raw Team `age_group` string normalisation — regular-player same-age-group Team matching still does an exact string match, unlike Training Only matching.
- Secretary's separate Event-creation architecture (`PortalSecretaryEventAddPage.php`) — Cross-Team Duplicate was deliberately not built into it.
- Pre-existing, explicitly untouched: the `venue_mode` PHP warning; duplicated `public.css` rule blocks; the unused `EventRepository::duplicate()` method.

---

## Deferred Work (unchanged unless noted, do not restart without approval)

- **Treasurer premium visual treatment** — deferred, unchanged.
- **Coach lineup formation-preservation enhancement** — deferred, unchanged.
- Other deferred same-context Coach gaps recorded in `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` — unchanged.
- Existing validator/development-data debt (see above) — unchanged.
- Historical Match Participation Evidence opportunities — unchanged.
- The Release Readiness work described in `DEVELOPMENT_HANDOVER_2026-08-29.md` ("Remaining Release Checklist Work") remains outstanding.
- FIN-031 and OS-011 remain open MVP-scope roadmap items, neither promoted as the next batch — unchanged.
- The data-integrity items above (Person 176, raw `age_group` normalisation, Secretary late-add eligibility audit) are genuinely open data/validator hygiene items, not product features.
- **Restricted Welfare Person projection**, **Welfare Staff Compliance experience** (together, Staff Compliance Batch C — see below) and **compliance expiry alerts** (Staff Compliance Batch D) — all approved future direction, all genuinely unimplemented.

Do not restart completed workspace MVP sweeps (Internal Club Testing, Completed Match Correction, Admin Navigation Consolidation, dark-surface contrast, Welfare Workspace Workflows, Staff Compliance Batches A/B) — all remain complete as recorded in `MASTER_DEVELOPER_GUIDE.md`'s "Recently Completed" and `SPRINTS.md`.

---

## Recommended Next Starting Point

**STAFF COMPLIANCE — BATCH C: RESTRICTED WELFARE PEOPLE PROJECTION + WELFARE COMPLIANCE EXPERIENCE**

This is not authorisation to begin implementation from this handover alone — confirm scope with the Product Owner/lead developer first, and prefer a small source-first audit before writing code (the same approach that has repeatedly revealed items were already further along, or already complete, than the roadmap recorded).

Current approved product direction to inform that work:

- A restricted, Welfare-scoped Person read projection — reusing existing authorised read services under the existing `can_view_welfare()` capability, never the Secretary Person Profile wholesale. Must expose only safeguarding/welfare-relevant information (identity, club/player context, emergency contact, current Operational Medical & Safety, medical consent/completeness, legitimate Concern linkage) and must never leak Finance, Registration administration, Team Assignment controls or unrelated Secretary operations.
- Within that projection, a Welfare Staff Compliance read/write experience that reuses the now-canonical `PersonCredentialService`/`PersonCredentialValidator`/domain **exactly as-is** — never a duplicated credential store, never a parallel validator. Welfare's own authorization boundary is `can_view_staff_compliance()`/`can_manage_staff_compliance()`, the same capability pair Secretary uses, but Welfare's *route* must remain its own, restricted to the Welfare workspace — do not let holding the shared capability alone unlock the Secretary Compliance route, and do not let Welfare's own route expose anything beyond Staff Compliance plus the already-approved restricted Welfare Person fields above.
- Advance expiry attention should eventually surface in the appropriate Welfare/Secretary priority areas — that is Staff Compliance Batch D (`ComplianceExpiryAlertsProvider`, modelled on the established operational alert-provider architecture, warning/critical semantics only, never club-accent/`action_required` for compliance severity) and is a separate, later, independently-schedulable batch from Batch C.

1. Re-read `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s Welfare Workspace direction section for the precise current wording before scoping any implementation.
2. Consider whether Release Readiness sign-off work (per `MASTER_DEVELOPER_GUIDE.md`'s "Current Priority") should take precedence over this or any other polish/feature work.
3. Consider whether the Person 176 data-integrity item warrants a small, separate, explicitly-scoped fix before it is forgotten.
4. Prefer a small source-first verification step before implementing anything.

**Important "do not restart" notes:**
- Do not re-implement the Welfare Concern Directory mobile/filter repair, the Welfare Update capability, or the Staff Compliance canonical domain/Secretary management experience (Batches A and B) — all complete.
- Do not reintroduce the "View concerns" dashboard action on Emergency Contacts/Players Requiring Attention — manually rejected and removed.
- Do not duplicate the Staff Compliance credential domain, validator or service for Welfare — reuse the canonical `IEXEL\ClubOS\Core\StaffCompliance` classes exactly as-is.
- Do not let the shared `can_manage_staff_compliance()` capability alone unlock the Secretary Compliance route for a Welfare-only user, or vice versa for a Secretary on a future Welfare route — persona/workspace boundaries remain independent of the shared capability.
- Do not begin compliance expiry alerts (Batch D) as part of Batch C scope.
- Do not re-implement any item listed as complete in `DEVELOPMENT_HANDOVER_2026-09-07B.md` or `DEVELOPMENT_HANDOVER_2026-09-07.md` — those documents' "do not restart" notes remain in force unchanged.
