# Development Handover — 2026-09-08 (C)

**Supersedes:** `DEVELOPMENT_HANDOVER_2026-09-08B.md`. That document remains in the repository as a historical record of the point where Staff Compliance Batch C had just landed, with compliance expiry alerts (Staff Compliance Batch D) still unstarted product direction. This document carries the resume point forward.

---

## DO NOT START NEW FEATURE DEVELOPMENT WITHOUT READING THIS

One further commit has landed and been accepted since the previous handover — **Staff Compliance Batch D (Compliance Expiry Alerts)**. **Do not restart or re-scope it.** See "Recently Completed" below and `SPRINTS.md`'s "Staff Compliance Batch D" section for full delivery detail.

**Staff Compliance's entire approved arc (Batches A–D) is now complete.** No further Staff Compliance batch is currently approved future direction — see "Next Recommended Starting Point" below, which is deliberately **not** a "Batch E": the authoritative backlog does not currently make one implementation slice clearly dominant, and Product Owner/lead developer prioritisation is needed before starting anything new.

---

## Current Git Baseline

- Plugin `main`: `2bdd62e536beec27f0fec663db710efa93fb59e9` ("feat: add staff compliance expiry alerts")
- Plugin status: **clean** — verified via `git status --short` returning nothing and `git rev-parse HEAD` matching the commit above; `origin/main` confirmed at the same commit
- Docs baseline immediately before this reconciliation: `main` at `6bb83da533496a94661265e8e9e74b4007e626d4` ("docs: record welfare people and compliance workspace"), clean — this reconciliation's own docs commit is not yet made; the Product Owner/lead developer will review before it is committed
- Prior plugin baseline (`DEVELOPMENT_HANDOVER_2026-09-08B.md`): `cd871f38b17e1bee341b61e2b5bcba6c7e1f0357`
- Staff Compliance checkpoints, in order:
  - Batch A (canonical foundation): `b5f006a66cdcd8df9e127c27da1a94b570b93514` ("feat: add staff compliance foundation")
  - Batch B (Secretary Person Profile + Compliance Management UI): `3352d300ab8fde56d47d307deacdab4b1f35d64a` ("feat: add secretary staff compliance management")
  - Batch C (Restricted Welfare People Projection + Welfare Compliance Experience): `cd871f38b17e1bee341b61e2b5bcba6c7e1f0357` ("feat: add welfare people and compliance workspace")
  - Batch D (Compliance Expiry Alerts): `2bdd62e536beec27f0fec663db710efa93fb59e9` ("feat: add staff compliance expiry alerts")

## Current Phase

**Operational MVP / Internal Club Testing / Release Readiness** — unchanged. See `MASTER_DEVELOPER_GUIDE.md`'s "Current Priority": Final Release Readiness / Club OS v1.0 sign-off remains the overall priority; Staff Compliance was a deliberately pulled-forward piece of the previously Post-MVP Welfare/compliance direction, now complete end-to-end, not a phase change.

---

## Recently Completed (since the 2026-09-08B handover)

### Staff Compliance Batch D — Compliance Expiry Alerts — `2bdd62e`

Surfaces Staff Compliance expiry risk **proactively**, through the existing operational-alert architecture, so Secretary and Welfare can act on it directly from their own dashboards. Proactive visibility only — no credential lifecycle semantics changed, no new notification channel.

**Scope.** Alerts are generated only for the three core credential categories — DBS, Safeguarding, First Aid — and only for two states: Expiring Soon and Expired. Qualification-type credentials never generate a Batch D alert; a genuinely absent credential ("Not Recorded") never generates one either — this is an expiry-risk batch, not a missing-compliance assessment, and the two must not be conflated in future work.

**Canonical status/threshold rule.** The provider performs no date arithmetic of its own — every status is derived via the exact canonical `CredentialStatus::derive()` Secretary and Welfare already use, against the existing, unconfigurable 42-day `EXPIRING_SOON_WINDOW_DAYS` domain constant. Live-proven boundary behaviour: expired yesterday → Expired; expires today → Expiring Soon (inclusive lower bound); +1/+41/+42 days → Expiring Soon (inclusive upper bound at +42); +43 days → no alert (Valid); no expiry → no alert (No Expiry). Date-only semantics; no timezone off-by-one observed; the threshold remains a domain constant, not configurable.

**Current/relevant credential rule.** Only each Person's current/relevant core-type record — newest non-archived row by `issued_on DESC, id DESC`, identical to `current_core_for_person()`'s own single-Person selection — can drive an alert. A new, general-purpose bulk repository method, `PersonCredentialRepository::current_core_credentials_for_persons(array $person_ids)`, generalises this exact selection across a candidate set in one query (a portable `NOT EXISTS` self-join, not a window function). Historical superseded rows and archived rows never independently alert — live-proven with an older-expired-plus-newer-valid DBS pair (no alert) and an archived-expired First Aid row (no alert). No credential lifecycle semantics were changed.

**Alert provider architecture.** A dedicated `ComplianceExpiryAlertsProvider` (`app/core/Dashboard/`), modelled directly on `FinanceOperationalAlertsProvider`: same Kernel-constructor shape, same optional-nullable-context `alerts()` signature, same standard `DashboardAlert` output — no new alert DTO, no new alert framework, no new database table, no persisted alert state. Registered through the existing aggregation exactly like Finance: merged inside `CommitteeOperationalAlertsProvider::alerts()` (reaching Secretary, since the Secretary dashboard snapshot reuses this provider unchanged) and merged directly into `MemberExperienceService::welfare()` (since Welfare never goes through `CommitteeOperationalAlertsProvider`). Existing alert bridging (`dashboard_experience_alerts()`) and existing sorting/deduplication (`sort_alerts()`) are reused unchanged.

**Severity semantics.** Expiring Soon → `DashboardAlert` level `warning`. Expired → `DashboardAlert` level `critical`, presented by the existing bridge as the established `urgent` `ExperienceAlert` state. `action_required`/club-accent/gold are never used for compliance severity; risk meaning comes from the semantic warning/critical state plus explicit "Expiring Soon"/"Expired" labels, never colour alone.

**Secretary delivery/routing.** Reached through the existing operational-alert aggregation. Action routes to `home_url('/club-os/secretary/people/{PERSON_ID}/compliance/')` — the exact real Secretary Staff Compliance destination. No new Secretary dashboard, no duplicate compliance page. Delivery additionally requires the active Secretary workspace persona **and** the narrow `can_manage_staff_compliance()` capability.

**Welfare delivery/routing.** Merged directly into the existing Welfare dashboard alert flow. Action routes via `WelfareWorkspaceUrl::person_compliance($person_id)` to `/club-os/welfare/people/{PERSON_ID}/compliance/` — never through the Secretary route. Delivery additionally requires the active Welfare workspace persona, `can_view_welfare()`, and `can_manage_staff_compliance()`. The Batch C Welfare People entry point remains in place, unreplaced.

**Club Admin behaviour.** Club Admin receives compliance alerts when operating in an eligible portal persona/workspace context (Secretary or Welfare), via the existing capability-superset override. The `null`-context wp-admin Committee/Executive dashboard deliberately receives **no** Batch D alert, because no canonical wp-admin Staff Compliance destination exists (Batches A–C are portal-only) — an intentional decision, not a gap; no generic Club Admin compliance dashboard was added and no cross-persona routing was invented.

**Target-Person eligibility vs current-user authorization.** Alert generation still requires `StaffCompliancePersonEligibility` (bulk `eligible_person_ids()`, unchanged from Batch C), entirely separate from viewer authorization. Live-proven: removing a Person's final qualifying role immediately suppressed their alert while the credential row remained stored, untouched; restoring the role immediately restored the alert. An eligible Person needs no WP login for their state to alert (`wp_user_id = 0` proven live). Separately, expiry alerts are never broadcast merely because the target Person is eligible — the active viewer/workspace must independently be authorised: ordinary Committee, Coach/Manager, Treasurer, Parent and Player active-role contexts receive no alert regardless of target-Person eligibility (proven live for all five).

**Data minimisation.** Alert copy contains only Person display name, the established credential display name, Expiring Soon/Expired status, and the expiry date. No reference number, administrative note, safeguarding narrative, medical information, Emergency Contact information or Finance data is ever exposed; no sensitive value is embedded in a URL.

**Performance and deduplication.** No Person/type N+1 queries — one bulk `eligible_person_ids()` call, one bulk `current_core_credentials_for_persons()` call, one bulk `find_identity_summaries()` call per `alerts()` invocation, all SQL in the canonical repository. Exactly one logical alert per (Person, core credential type, active dashboard/persona context); no new dedup state — the existing `sort_alerts()` key-based dedup is reused unchanged.

**Validation:** `tools/validate-staff-compliance-expiry-alerts.php` (new) **69/69**. Regression unaffected: `validate-staff-compliance-foundation.php` (108/108), `validate-staff-compliance-secretary-ui.php` (98/98), `validate-welfare-people-compliance.php` (123/123), `validate-welfare-workspace-batch1.php` (118/118), `validate-secretary-people-foundation.php` (81/81), `validate-secretary-mobile-responsive.php` (138/138), `validate-committee-permissions.php` (105/105), `validate-plain-permalink-portal-routing.php` (55/55), `validate-team-staff-operational-access.php` (55/55), `validate-admin-person-role-sync.php` (54/54), `validate-admin-person-role-dependency-guards.php` (91/91), `validate-workspace-priority-alert-scoping.php` (**114/114**, after a narrow validator-harness `require_once` dependency fix — see below), `validate-welfare-dashboard-summary-sql.php` (28/28). All six changed/new PHP files lint-clean.

**Validator harness dependency fix (not a product change):** `tools/validate-workspace-priority-alert-scoping.php` is a static, no-bootstrap validator that manually `require_once`s each class it depends on. Adding the `ComplianceExpiryAlertsProvider` call inside `CommitteeOperationalAlertsProvider::alerts()` broke this validator's own dependency list. Fixed by adding two narrow `require_once` lines; confirmed this validator's Committee/Treasurer-only fixtures never reach a Secretary/Welfare active_role, so no further mocking was needed. No assertions removed or weakened — result unchanged in substance at 114/114.

**Live smoke-test results:** all eight required scenarios proven (DBS expired → critical; Safeguarding/First Aid expiring within threshold → warning; valid → no alert; no-expiry → no alert; older-expired-plus-newer-valid → no alert; archived expired → no alert; eligible Person without `wp_user_id` → alert; role removal/restoration → alert suppressed then restored, credential history untouched); the exact 42-day boundary sweep; real Secretary and Welfare dashboard snapshots (real WP logins) showing correct routing; denial for fabricated Committee/Coach/Treasurer/Parent/Player contexts and a `null` admin context, even while the acting user held admin capability; denial for a genuinely non-privileged real WordPress user forced into a Secretary/Welfare active role. All temporary test data fully restored afterward.

**Product Owner manually accepted** (conclusion: **"All checks passed."**): Secretary desktop (urgent alert for expired DBS, warning alert for expiring First Aid, existing Events/Registration alerts preserved, actions prominent); Welfare desktop (urgent and warning alerts visible, correct dashboard integration, action routes to the Welfare compliance destination); mobile (Secretary Priority Alerts at 320px, Welfare Priority Alerts at 320/390px, no horizontal overflow, no min-content/vertical-letter regression, action links readable and usable); and the compliance destination itself (Welfare compliance page at 390px, canonical state agreeing with the alert for both an expired DBS and an expiring First Aid). Visual severity was independently accepted as communicated through more than colour alone (explicit URGENT/WARNING labels, semantic left-border treatment, alert title/state copy) — no new icon system or dashboard redesign was required.

### DevTools 404 observation (deferred technical debt, not a Batch D failure)

During manual acceptance, the Welfare compliance destination page visibly rendered and worked correctly while the browser's DevTools Network panel showed a 404 status for the document request. This was **not treated as a Batch D blocker**: the route's content rendered successfully, the alert action landed on the correct Welfare compliance page, the functional routing validators (`validate-plain-permalink-portal-routing.php`, `validate-welfare-people-compliance.php`) both passed, and a similar development-environment status-code anomaly had been observed before in this project. The route is not believed to be broken, and this status-code behaviour is not claimed to be resolved — it was not investigated or fixed and remains a separate, deferred technical-debt observation (see "Known Technical Debt / Validator Caveats" below).

---

## Known Current Staff Compliance State

- ✅ Staff Compliance canonical domain (DBS/safeguarding/first-aid/qualification, status derivation, capabilities) — **implemented**, `b5f006a6`.
- ✅ Secretary Staff Compliance management (Profile summary, dedicated route, Add/Correct/Archive, target-Person eligibility, type-aware naming, desktop layout) — **implemented**, `3352d300`.
- ✅ Restricted Welfare People directory, Person profile (Identity/Concerns/read-only Medical & Safety/read-only Emergency Contact/eligible-only Staff Compliance), and Welfare Staff Compliance management — **implemented**, `cd871f3`.
- ✅ Secretary-vs-Welfare workspace mirror boundary — **implemented and proven live**, `cd871f3`.
- ✅ Compliance expiry alerts (Expiring Soon/Expired, core types only, Secretary + Welfare delivery, workspace-correct routing, semantic severity, bulk-query performance) — **implemented**, `2bdd62e`.
- **No further Staff Compliance batch is currently approved future direction.** The following were all explicitly out of scope for Batch D and remain uncommitted, speculative ideas rather than approved next steps — do not begin any of them without a fresh, explicit Product Owner decision:
  - ❌ Person-level missing-compliance ("Not Recorded") assessment/alerting.
  - ❌ Configurable compliance expiry threshold (the 42-day window remains a domain constant).
  - ❌ Hard-coded FA/other qualification catalogue.
  - ❌ Credential hard delete.
  - ❌ Detailed safeguarding case-note system.
  - ❌ Notification-channel delivery (email/SMS/push) for compliance alerts.
  - ❌ Scheduled/background alert jobs or persisted alert/dismissal state.
  - ❌ New Welfare Medical & Safety writer / new Welfare Emergency Contact writer.
  - ❌ Attachments (Welfare).

---

## Capability / Workspace Boundaries (Staff Compliance) — unchanged, carried forward

- **Club Admin:** authorised to manage Staff Compliance for any *eligible* target Person via either workspace's established override, and receives compliance expiry alerts wherever that override applies; does not bypass target-Person eligibility itself, and receives no alert in the wp-admin/null context (no canonical destination exists there).
- **Secretary:** `iexel_manage_staff_compliance` via the existing direct per-user capability architecture gates both the Secretary Compliance route and Secretary's compliance expiry alerts. Does not gain access to Welfare's People/Person/Compliance routes or alerts merely by holding this capability.
- **Welfare Officer:** the same shared capability pair, plus Welfare workspace authorization, gates Welfare's own restricted People/Person/Compliance routes and compliance expiry alerts. Does not gain access to the Secretary route or its alerts merely by holding the capability.
- **Ordinary Committee, Coach/Manager, Treasurer, Parent, Player:** none receive Staff Compliance expiry alerts through their own persona context, regardless of any target Person's eligibility.

---

## Known Technical Debt / Validator Caveats

Carried forward unchanged from `DEVELOPMENT_HANDOVER_2026-09-08B.md`, plus one new item from this batch:

- **DevTools 404 status-code observation on the Welfare compliance destination page** (new, Batch D) — content renders and functions correctly; the anomaly is confined to the DevTools Network panel's reported status for the document request; not investigated or fixed in Batch D; genuinely open, deferred.
- **`tools/validate-current-emergency-contact.php`** — a pre-existing, unrelated schema/data-version assertion failure, re-confirmed via `git stash` to reproduce identically at the clean Batch-C baseline with none of Batch D's work applied. **Not caused by, and not repaired by, Staff Compliance. Do not treat this as a Staff Compliance blocker.**
- Dev-fixture drift, not a product defect: several DB-integrated Match Mode validators assume Person 19 is a genuine current Team-1 Player; on this dev database Person 19 is a Team-6 Player. **Do not change production behaviour or seed data to silence this.**
- **`tools/validate-team-events-badge-mobile-repair.php`** has a separate, pre-existing, unrelated breakpoint assertion failure (`.iexel-team-event-past-meta` at 480px).
- **`tools/validate-visual-foundation.php`** — pre-existing, unrelated `"Public stylesheet dependency order changed."` failure.
- **Person 176 orphaned Team Assignment** — an active `team_assignments` row referencing a `person_id` with no corresponding `people` row. Genuinely open; needs a dev-database data-integrity fix, not a code change.
- Secretary late-add `EventAudienceBuilder::add_attendee()`/`add_attendees_batch()` perform no eligibility validation of their own.
- Raw Team `age_group` string normalisation; Secretary's separate Event-creation architecture (no Cross-Team Duplicate); the `venue_mode` PHP warning; duplicated `public.css` rule blocks; the unused `EventRepository::duplicate()` method — all pre-existing, explicitly untouched.
- **FIN-031 (Treasurer/Secretary static-caret finding)** — reconciled in a prior turn: positively classified as browser caret browsing, not a Club OS defect (see `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s FIN-031 entries). No plugin change is expected against it.

---

## Deferred Work (unchanged unless noted, do not restart without approval)

- **Treasurer premium visual treatment** — deferred, unchanged.
- **Coach lineup formation-preservation enhancement** — deferred, unchanged.
- Other deferred same-context Coach gaps recorded in `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` — unchanged.
- Existing validator/development-data debt (see above) — unchanged.
- Historical Match Participation Evidence opportunities — unchanged.
- The Release Readiness work described in `DEVELOPMENT_HANDOVER_2026-08-29.md` ("Remaining Release Checklist Work") remains outstanding.
- **OS-011** (Welfare Concern Detail hierarchy polish) remains an open, approved-but-unpromoted MVP-scope polish item.
- The data-integrity items above (Person 176, raw `age_group` normalisation, Secretary late-add eligibility audit) are genuinely open data/validator hygiene items, not product features.
- **DevTools 404/status-code observation** (new, Batch D) — deferred technical debt, not investigated.

Do not restart completed workspace MVP sweeps (Internal Club Testing, Completed Match Correction, Admin Navigation Consolidation, dark-surface contrast, Welfare Workspace Workflows, Staff Compliance Batches A/B/C/D) — all remain complete as recorded in `MASTER_DEVELOPER_GUIDE.md`'s "Recently Completed" and `SPRINTS.md`.

---

## Next Recommended Starting Point

**No single next implementation batch is currently dominant in the authoritative backlog.** With Staff Compliance A–D now complete, do **not** invent or begin a "Staff Compliance Batch E" — none of the ideas that could extend it (missing-compliance alerting, a configurable threshold, a qualification catalogue, notification-channel delivery) are approved future direction; they were explicitly out of scope for Batch D and remain speculative unless a fresh Product Owner decision commits one of them.

Reviewing `SPRINTS.md`, `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s "Recommended next implementation batch" section, and `MASTER_DEVELOPER_GUIDE.md`'s "Current Priority" together, the top candidates are:

1. **Final Release Readiness / Club OS v1.0 sign-off** — `MASTER_DEVELOPER_GUIDE.md`'s own stated "Current Priority." A checklist/gate review rather than a feature-coding batch — see `RELEASE_CHECKLIST.md` for its specific remaining gates.
2. **OS-011** (Welfare Concern Detail hierarchy polish, Medium priority) — genuinely open, cosmetic/non-blocking, independently re-confirmed still present (2026-08-26 audit); the roadmap explicitly notes it is "not currently promoted ahead of Internal Club Testing."
3. **Person 176 orphaned Team Assignment** — a small, genuinely open dev-database data-integrity item (an active Team Assignment with no corresponding `people` row), not a product feature.

**Product Owner/lead developer prioritisation is needed** to choose between these — none is clearly dominant per the authoritative docs, and this handover does not select one on its own authority.

**Important "do not restart" notes:**
- Do not re-implement the Staff Compliance canonical domain, either workspace's route/workflow, target-Person eligibility, type-aware credential naming, the desktop layout repair, the Welfare People inclusion rule/directory/profile, or the compliance expiry alert provider/routing — all complete (Batches A–D).
- Do not add missing-compliance alerts, qualification expiry alerts, a configurable threshold, alert persistence/dismissal, scheduled jobs, notification channels (email/SMS/push), or a new alerts table without a fresh, explicit Product Owner decision.
- Do not invent a generic wp-admin Staff Compliance destination or route Welfare through Secretary (or vice versa).
- Do not investigate or fix the DevTools 404/status-code observation as part of unrelated work without a dedicated, explicitly-scoped task.
- Do not re-implement any item listed as complete in `DEVELOPMENT_HANDOVER_2026-09-08B.md` or earlier handovers — those documents' "do not restart" notes remain in force unchanged.
