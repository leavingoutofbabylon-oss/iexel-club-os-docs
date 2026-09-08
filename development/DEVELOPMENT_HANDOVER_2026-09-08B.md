# Development Handover — 2026-09-08 (B)

**Supersedes:** `DEVELOPMENT_HANDOVER_2026-09-08.md`. That document remains in the repository as a historical record of the point where Staff Compliance Batches A and B had just landed, with the restricted Welfare People projection and Welfare Compliance experience (Staff Compliance Batch C) still unstarted product direction. This document carries the resume point forward.

---

## DO NOT START NEW FEATURE DEVELOPMENT WITHOUT READING THIS

One further commit has landed and been accepted since the previous handover — **Staff Compliance Batch C (Restricted Welfare People Projection + Welfare Compliance Experience)**. **Do not restart or re-scope it.** See "Recently Completed" below and `SPRINTS.md`'s "Staff Compliance — Batch A, Batch B & Batch C" section for full delivery detail.

The next recommended implementation batch is named at the end of this document: **Staff Compliance Batch D — Compliance Expiry Alerts.** It has not been started. Nothing below authorises beginning it without a fresh confirmation from the Product Owner/lead developer.

A separate, non-feature diagnostic (Secretary/Treasurer caret-browsing investigation) was also carried out and is recorded below so it is not repeatedly rediscovered as product debt.

---

## Current Git Baseline

- Plugin `main`: `cd871f38b17e1bee341b61e2b5bcba6c7e1f0357` ("feat: add welfare people and compliance workspace")
- Plugin status: **clean** — verified via `git status --short` returning nothing and `git rev-parse HEAD` matching the commit above; `origin/main` confirmed at the same commit
- Docs baseline immediately before this reconciliation: `main` at `afa49f76f2f4eeb69951e49188d45949a065c950` ("docs: record staff compliance secretary management"), clean — this reconciliation's own docs commit is not yet made; the Product Owner/lead developer will review before it is committed
- Prior plugin baseline (`DEVELOPMENT_HANDOVER_2026-09-08.md`): `3352d300ab8fde56d47d307deacdab4b1f35d64a`
- Staff Compliance checkpoints, in order:
  - Batch A (canonical foundation): `b5f006a66cdcd8df9e127c27da1a94b570b93514` ("feat: add staff compliance foundation")
  - Batch B (Secretary Person Profile + Compliance Management UI, including the correction/repair and eligibility/layout rounds): `3352d300ab8fde56d47d307deacdab4b1f35d64a` ("feat: add secretary staff compliance management")
  - Batch C (Restricted Welfare People Projection + Welfare Compliance Experience): `cd871f38b17e1bee341b61e2b5bcba6c7e1f0357` ("feat: add welfare people and compliance workspace")

## Current Phase

**Operational MVP / Internal Club Testing / Release Readiness** — unchanged. See `MASTER_DEVELOPER_GUIDE.md`'s "Current Priority": Final Release Readiness / Club OS v1.0 sign-off remains the overall priority; Staff Compliance is a deliberately pulled-forward piece of the previously Post-MVP Welfare/compliance direction, not a phase change.

---

## Recently Completed (since the 2026-09-08 handover)

### Staff Compliance Batch C — Restricted Welfare People Projection + Welfare Compliance Experience — `cd871f3`

Gives Welfare Officers a restricted, purpose-built People experience — **not a duplicate of Secretary People**. Workflow: **Welfare Workspace → Welfare People → Welfare Person Profile → review appropriate Welfare information → manage Staff Compliance for eligible officials/staff.**

**Welfare People inclusion rule.** A single shared computation (`MemberExperienceService::welfare_relevant_person_reasons()`) unions four bounded existence/eligibility queries into one `person_id => reasons[]` map, reused identically by the directory and the profile. A Person appears when **at least one** is true: (A) an active Welfare concern; (B) a current Medical & Safety row; (C) a current Emergency Contact row; (D) `StaffCompliancePersonEligibility::is_eligible()`. Reasons are unioned so a Person matching multiple never appears twice. Deliberately narrower than the full club roster — no new membership table.

**Welfare People directory** — `/club-os/welfare/people/` (`PortalWelfarePeopleDirectoryPage`, `WelfarePersonDirectorySnapshot`, Welfare's own established snapshot/`MemberExperienceOperationResult` convention). Compact rows: Person name, concise relevance reasons, "Review Welfare Profile" link, and an in-memory name search over the already-bounded candidate set. Never exposes medical narrative, emergency-contact phone, credential reference/notes, concern narrative, Finance, home address, or Secretary/member-administration controls.

**Welfare Person profile** — `/club-os/welfare/people/{PERSON_ID}/` (`PortalWelfarePersonProfilePage`, `WelfarePersonProfileSnapshot`). Denied identically ("The Person could not be found.") for a Person with zero relevance reasons and for a genuinely non-existent Person. Hierarchy: Identity → Welfare Concerns (reuses `WelfareConcernService::list_authorised()`; reference/status/priority/date + "View Concern" link only — no new case-note system, Welfare Updates remain the existing short handover mechanism) → Medical & Safety (**READ-ONLY** projection of the canonical `PlayerOperationalMedicalSafetyRepository`; no new Welfare writer, no `iexel_manage_registrations` grant) → Emergency Contact (**READ-ONLY** projection of the canonical `CurrentEmergencyContactRepository`; no new Welfare writer; stays a separate domain from Medical & Safety/Staff Compliance/concerns) → Staff Compliance (eligible officials/staff only, below). No Finance, Registration administration, Team Assignment or Secretary role-management data appears anywhere on it — this is a restricted Welfare projection, never the canonical full Person administration profile.

**Staff Compliance on the Welfare profile** appears **only** when `StaffCompliancePersonEligibility::is_eligible()` is true — entirely absent (never a placeholder) otherwise. Data population is gated on the narrow `can_view_staff_compliance()` read capability; a separate `can_manage` flag (`can_manage_staff_compliance()`) gates only the "Manage Compliance" button — preserving Target-Person-Eligibility-vs-Current-User-Authorization. Shows DBS/Safeguarding/First Aid current status and qualification count via the exact same canonical `PersonCredentialRepository`/`PersonCredentialService`/`PersonCredentialValidator`/`CredentialStatus`/`StaffCompliancePersonEligibility` classes Secretary uses — no duplicate compliance logic.

**Welfare Staff Compliance management** — `/club-os/welfare/people/{PERSON_ID}/compliance/` (`PortalWelfarePersonCompliancePage`, `WelfarePersonCredentialRequestHandler`). Add/Correct/Archive with identical canonical semantics to Secretary (renewal = new row via Add Credential; correction = same-row update; archive = explicit lifecycle action; no hard delete). Authorization requires **both** an authorised Welfare workspace persona **and** the narrow `can_manage_staff_compliance()` capability, plus target-Person eligibility — the identical write-security architecture as Batch B (POST-only, per-action nonce, server-side resolution, credential-belongs-to-route-Person check, PRG, fixed non-sensitive notices; cross-Person/fabricated ids fail closed).

**Shared Secretary/Welfare architecture — small, reuse-oriented, not a broad refactor.** `PortalSecretaryPersonCompliancePage` and `SecretaryPersonCredentialRequestHandler` had `final` removed and ~5–6 small `protected` accessor methods extracted (URLs, copy, handler/feedback class references, required persona, redirect base, nonce prefix); the bulk of the original rendering/write orchestration remains `private`, unchanged, proven byte-identical for Secretary via live smoke tests. `PortalWelfarePersonCompliancePage extends PortalSecretaryPersonCompliancePage` and `WelfarePersonCredentialRequestHandler extends SecretaryPersonCredentialRequestHandler` override only the workspace-identity accessors. A separate `WelfarePersonCredentialFeedback` class (own transient namespace) follows the existing per-workspace-feedback-class precedent.

**Secretary vs Welfare workspace boundary — mirror image of Batch B.** Welfare compliance management requires both Welfare workspace authorization and Staff Compliance management authorization; neither implies the other. Proven live: a genuine Club Admin/Secretary-persona user holding `can_manage_staff_compliance()` was denied the Welfare compliance route because their active persona/workspace was Secretary, not Welfare — the direct mirror of Batch B's "Welfare capability alone doesn't unlock the Secretary route" finding.

**Response protection & dashboard entry point.** The directory, profile and compliance page all use the established private/no-store/no-cache/noindex protection (via the existing `WELFARE_SECTIONS` list); direct-route authorization fails closed server-side, never merely front-end hiding. One new Welfare dashboard action, "Welfare People", was added without redesigning the broader dashboard. The existing "Players Requiring Attention"/"Emergency Contacts" rows were deliberately **not** rewired to the new profile — those rows surface Persons with *missing* information, which can mean no canonical row exists at all, exactly the case the new inclusion rule would then exclude, risking a 404 for precisely the Persons the link would most often target. Documented inline in `MemberExperienceService.php`.

**Validation:** `tools/validate-welfare-people-compliance.php` (new) **123/123**. Regression unaffected: `validate-staff-compliance-foundation.php` (108/108), `validate-staff-compliance-secretary-ui.php` (**98/98**, +1 assertion for the new `store_feedback()` reuse accessor), `validate-welfare-workspace-batch1.php` (**118/118**, one guard re-scoped to also exclude `MemberExperienceService.php`, mirroring the existing router-exclusion precedent), `validate-secretary-people-foundation.php` (81/81), `validate-secretary-person-editing.php` (39/39), `validate-secretary-person-role-management.php` (262/262), `validate-committee-permissions.php` (105/105), `validate-plain-permalink-portal-routing.php` (55/55), `validate-secretary-team-assignments.php` (174/174), `validate-team-staff-operational-access.php` (55/55), `validate-admin-person-role-sync.php` (54/54), `validate-admin-person-role-dependency-guards.php` (91/91), `validate-player-medical-safety-current-state.php` (190/190), `validate-welfare-dashboard-summary-sql.php` (28/28), `validate-secretary-mobile-responsive.php` (138/138). All changed/new PHP files lint-clean.

Live, non-destructive database verification proved: Welfare-authorised directory access; Secretary-only/Committee/ordinary-member denial; each relevance-reason combination appearing exactly once; a `wp_user_id = 0` eligible coach fully discoverable and manageable; ineligible-Person denial of both the profile section and the direct compliance route; role removal/restoration immediately toggling both while credential history remained untouched throughout.

Product Owner manually accepted: the Welfare Workspace → Welfare People entry point; the directory at desktop and 320px; the profile at 320px with concern + Medical & Safety + Emergency Contact + eligible Staff Compliance; an ordinary player/member profile showing no Staff Compliance section; Medical & Safety presentation; Emergency Contact empty-state behaviour; Welfare compliance management at desktop and mobile; and Secretary-only direct Welfare-route denial. Responsive checks passed with no horizontal overflow and no recurrence of the prior Staff Compliance min-content vertical-letter defect at desktop/768px/390px/320px.

### Secretary/Treasurer Caret-Browsing Diagnostic (not a Batch C feature — a separate pre-commit UX check)

A Product Owner reported a flashing text-insertion caret when clicking ordinary static Secretary Command Centre hero copy, noting a similar apparent issue previously investigated in Treasurer (FIN-031). A formal diagnostic was performed **before** Batch C was committed:

- The rendered heading is plain, non-`contenteditable` markup: `<h1>Secretary Command Centre</h1>`, with no `contenteditable` attribute anywhere in it or any ancestor up to `<html>`.
- `element.isContentEditable === false` for the heading and every ancestor.
- `document.designMode === "off"`.
- Zero `contenteditable`/`caret-color`/`designMode`/`execCommand` occurrences anywhere in plugin source (`app/`, `assets/`, `tools/`).
- The only `cursor: text` CSS rule in the codebase targets `.iexel-search-multiselect__control`, a genuine text-input container used elsewhere (Finance/registration search), never any heading.
- This directly corroborates the existing FIN-031 (Treasurer) finding, which had already independently concluded (2026-08-26) that no reproducible input-like affordance exists in current Finance/Treasurer source.

**Conclusion: this is browser caret browsing (e.g. an F7-style caret-navigation mode), not a Club OS editable-state defect.** No plugin change was made — no global `user-select: none`, no CSS/JS selection or caret suppression. `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s FIN-031 entries have been reconciled to reflect this positive conclusion rather than the earlier, weaker "not reproducible" framing. It remains formally open only pending Product Owner confirmation that this matches what they observed — it is not an unresolved implementation blocker, and no further plugin work is expected against it.

---

## Known Current Staff Compliance / Welfare State

- ✅ Staff Compliance canonical domain (DBS/safeguarding/first-aid/qualification, status derivation, capabilities) — **implemented**, `b5f006a6`.
- ✅ Secretary Staff Compliance management (Profile summary, dedicated route, Add/Correct/Archive, target-Person eligibility, type-aware naming, desktop layout) — **implemented**, `3352d300`.
- ✅ Restricted Welfare People directory (`/club-os/welfare/people/`) — **implemented**, `cd871f3`.
- ✅ Restricted Welfare Person profile (`/club-os/welfare/people/{PERSON_ID}/`) — Identity, Welfare Concerns, read-only Medical & Safety, read-only Emergency Contact, eligible-only Staff Compliance — **implemented**, `cd871f3`.
- ✅ Welfare Staff Compliance management (`/club-os/welfare/people/{PERSON_ID}/compliance/`) — Add/Correct/Archive, reusing the canonical Batch A domain and the Batch B presentation via the small shared accessor-extraction pattern — **implemented**, `cd871f3`.
- ✅ Secretary-vs-Welfare workspace mirror boundary (neither workspace's authorization alone unlocks the other's compliance route) — **implemented and proven live**, `cd871f3`.
- ❌ Compliance expiry alerts / dashboard integration — **not implemented**. Approved future direction (Staff Compliance Batch D) only.
- ❌ Detailed safeguarding case notes / allegation or evidence records — **not implemented**, and not the same thing as either a Welfare Update or a Staff Compliance administrative note (both are short and non-case-note by design).
- ❌ Configurable compliance expiry threshold — **not implemented**; the 42-day "Expiring Soon" window is a domain constant with no Settings UI.
- ❌ Hard-coded FA/other qualification catalogue — deliberately **not implemented**; Qualification names remain free text.
- ❌ Credential hard delete — deliberately **not implemented**; Archive is the only retirement action.
- ❌ New Welfare Medical & Safety writer / new Welfare Emergency Contact writer — deliberately **not implemented**; both remain read-only Welfare projections of the canonical Secretary-owned entities.
- ❌ Attachments (Welfare) — **not implemented**, unchanged from previous handovers.

---

## Capability / Workspace Boundaries (Staff Compliance)

Recorded explicitly because target-Person eligibility and current-user authorization are easy to conflate, and because Batch C introduced the mirror-image workspace boundary to Batch B's:

- **Club Admin:** authorised to manage Staff Compliance for any *eligible* target Person via either workspace's established override; does **not** bypass target-Person eligibility itself.
- **Secretary:** receives `iexel_manage_staff_compliance` via the existing canonical direct per-user capability architecture; this, together with the active Secretary persona and target-Person eligibility, gates the Secretary Compliance route. Holding this capability does **not** grant access to the Welfare People/Person/Compliance routes — those additionally require Welfare workspace authorization (`has_role(WELFARE)` + `can_view_welfare()`).
- **Welfare Officer:** receives the same shared capability pair directly on the WP role, and now (since Batch C) has its own restricted People directory, Person profile and Compliance management route, gated independently by Welfare workspace authorization **and** the shared capability **and** target-Person eligibility. Holding the capability does **not** grant access to the *Secretary* Compliance route, because that route additionally requires the active Secretary/Admin persona.
- **Ordinary Committee:** does not inherit Staff Compliance capability — Committee has neither capability nor either workspace's People routes.
- **Coach / Manager / Treasurer (as target Persons):** being an *eligible target Person* for Staff Compliance does not itself grant *permission to manage* anyone's Staff Compliance — eligibility and authorization are independently checked, in both workspaces.
- **Parent / Player:** not authorised, and (being ineligible targets in the ordinary case) not presented with the feature either, in either workspace.

---

## Known Technical Debt / Validator Caveats

Carried forward unchanged from `DEVELOPMENT_HANDOVER_2026-09-08.md` (none of the items below were touched by Batch C), plus reconciliation of the caret item:

- **`tools/validate-current-emergency-contact.php`** — a pre-existing, unrelated schema/data-version assertion failure ("Schema version was not advanced for this batch." / "Data version changed despite no data migration in this batch."), re-confirmed via `git stash` to reproduce identically at the clean Batch-B baseline with none of Batch C's work applied. **Not caused by, and not repaired by, Staff Compliance. Do not treat this as a Staff Compliance blocker.**
- Dev-fixture drift, not a product defect: several DB-integrated Match Mode validators assume Person 19 is a genuine current Team-1 Player; on this dev database Person 19 is a Team-6 Player. Blocks `tools/validate-match-goal-live-eligibility.php` from running end-to-end. **Do not change production behaviour or seed data to silence this.**
- **`tools/validate-team-events-badge-mobile-repair.php`** has a separate, pre-existing, unrelated breakpoint assertion failure (`.iexel-team-event-past-meta` at 480px).
- **`tools/validate-visual-foundation.php`** — pre-existing, unrelated `"Public stylesheet dependency order changed."` failure.
- **Person 176 orphaned Team Assignment** — an active `team_assignments` row referencing a `person_id` with no corresponding `people` row. Genuinely open; needs a dev-database data-integrity fix, not a code change.
- Secretary late-add `EventAudienceBuilder::add_attendee()`/`add_attendees_batch()` perform no eligibility validation of their own.
- Raw Team `age_group` string normalisation — regular-player same-age-group Team matching still does an exact string match, unlike Training Only matching.
- Secretary's separate Event-creation architecture (`PortalSecretaryEventAddPage.php`) — Cross-Team Duplicate was deliberately not built into it.
- Pre-existing, explicitly untouched: the `venue_mode` PHP warning; duplicated `public.css` rule blocks; the unused `EventRepository::duplicate()` method.
- **FIN-031 (Treasurer static-caret finding)** — reconciled this handover: no longer an open "not reproducible" item awaiting investigation; positively classified as browser caret browsing, not a Club OS defect (see "Recently Completed" above). No plugin change is expected against it.

---

## Deferred Work (unchanged unless noted, do not restart without approval)

- **Treasurer premium visual treatment** — deferred, unchanged.
- **Coach lineup formation-preservation enhancement** — deferred, unchanged.
- Other deferred same-context Coach gaps recorded in `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` — unchanged.
- Existing validator/development-data debt (see above) — unchanged.
- Historical Match Participation Evidence opportunities — unchanged.
- The Release Readiness work described in `DEVELOPMENT_HANDOVER_2026-08-29.md` ("Remaining Release Checklist Work") remains outstanding.
- OS-011 remains an open MVP-scope polish item, not promoted as the next batch — unchanged.
- The data-integrity items above (Person 176, raw `age_group` normalisation, Secretary late-add eligibility audit) are genuinely open data/validator hygiene items, not product features.
- **Compliance expiry alerts (Staff Compliance Batch D)** — approved future direction, genuinely unimplemented. See "Recommended Next Starting Point" below.

Do not restart completed workspace MVP sweeps (Internal Club Testing, Completed Match Correction, Admin Navigation Consolidation, dark-surface contrast, Welfare Workspace Workflows, Staff Compliance Batches A/B/C) — all remain complete as recorded in `MASTER_DEVELOPER_GUIDE.md`'s "Recently Completed" and `SPRINTS.md`.

---

## Recommended Next Starting Point

**STAFF COMPLIANCE — BATCH D: COMPLIANCE EXPIRY ALERTS**

This is not authorisation to begin implementation from this handover alone — confirm scope with the Product Owner/lead developer first, and prefer a small source-first audit before writing code.

Current approved product direction to inform that work:

- A `ComplianceExpiryAlertsProvider`, modelled on the established operational alert-provider architecture (the same pattern already used for other persona-scoped priority alerts), surfacing credentials that are Expiring Soon or Expired.
- Semantic severity only: **warning** for expiring, **critical/danger** for expired — never club-accent/gold or `action_required` semantics for compliance severity.
- Expected audiences: Secretary, Welfare, and Club Admin where appropriate, through the existing persona/dashboard architecture — never a new alert-delivery mechanism.
- Dashboard actions should now be able to link to the real destinations Batch C created: the Secretary compliance route (`/club-os/secretary/people/{PERSON_ID}/compliance/`) where the active workspace is Secretary, and the Welfare Person/Compliance destination (`/club-os/welfare/people/{PERSON_ID}/compliance/`) where the active workspace is Welfare.
- Reuse the existing `CredentialStatus::derive()` and the 42-day `EXPIRING_SOON_WINDOW_DAYS` domain constant — do not introduce a configurable threshold or a Settings UI as part of this batch.

1. Re-read `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s Staff Compliance / Welfare Workspace entries for the precise current wording before scoping any implementation.
2. Consider whether Release Readiness sign-off work (per `MASTER_DEVELOPER_GUIDE.md`'s "Current Priority") should take precedence over this or any other polish/feature work.
3. Consider whether the Person 176 data-integrity item warrants a small, separate, explicitly-scoped fix before it is forgotten.
4. Prefer a small source-first verification step before implementing anything.

**Important "do not restart" notes:**
- Do not re-implement the Staff Compliance canonical domain, the Secretary management experience (Batch A/B), or the restricted Welfare People/Person/Compliance projection (Batch C) — all complete.
- Do not re-implement the Welfare Concern Directory mobile/filter repair or the Welfare Update capability — complete.
- Do not reintroduce the "View concerns" dashboard action on Emergency Contacts/Players Requiring Attention, and do not rewire those rows to the new Welfare Person profile — both were deliberately rejected/avoided; see `SPRINTS.md`'s Batch C section for the specific 404-risk reasoning.
- Do not duplicate the Staff Compliance credential domain, validator or service for any future alert work — reuse the canonical `IEXEL\ClubOS\Core\StaffCompliance` classes exactly as-is.
- Do not let a shared capability alone unlock the other workspace's compliance route in either direction — this mirror boundary is now proven in both directions and must be preserved by any future work touching either route.
- Do not add any caret-browsing workaround (CSS/JS selection or caret suppression) — the Secretary/Treasurer caret reports are browser-side behaviour, not a Club OS defect.
- Do not re-implement any item listed as complete in `DEVELOPMENT_HANDOVER_2026-09-08.md` or earlier handovers — those documents' "do not restart" notes remain in force unchanged.
