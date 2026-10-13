# IEXEL Club OS Experience Review and Roadmap

Role-based product review, MVP priorities, post-MVP roadmap and future club profiles

## Executive summary

Club OS has reached the stage where the core architecture is strong and the main remaining work is product refinement: role identity, workflow completeness, navigation, visual consistency, accessibility and selective pre-MVP engagement features.

## Workspace scores & UX walkthrough status

Walkthroughs have been completed by the Product Owner across all eight primary surfaces. Each workspace is formally recorded as **UX walkthrough complete / provisionally accepted**, with outstanding findings catalogued into Tier A/B/C/D and remaining open until implemented, validated, and accepted. Unresolved issues are strictly not marked as fixed or claimed as final release acceptance.

| Workspace | Score | Walkthrough Status | Summary |
|---|---:|---|---|
| Settings / Brand Studio | 9.5/10 | UX walkthrough complete / provisionally accepted | Premium, visual and approachable. Brand Studio intact; operational settings separating under SET-001. |
| Coach Workspace | 9/10 | UX walkthrough complete / provisionally accepted | Strongest operational experience. Matchday Hub, statistics, and lineup builder solid; fixture cards unified; bulk upcoming event responses open. |
| Welfare Workspace | 9/10 | UX walkthrough complete / provisionally accepted | Strong safeguarding workspace with concern management, medical overview, and emergency information. OS-011 card hierarchy refinement open. |
| Committee Workspace | 9/10 | UX walkthrough complete / provisionally accepted | Clear oversight experience. Communications approval gate and data minimisation (excluding welfare/finance/medical) open. |
| Treasurer Workspace | 9/10 | UX walkthrough complete / provisionally accepted | True finance workspace with invoices, payments, billing schedules, and Back My Game oversight. Core workflows validated. |
| Admin Experience | 8.5/10 | UX walkthrough complete / provisionally accepted | Navigation consolidated (ADM-001–003). Operational settings separation (SET-001) and blank Fundraising screen cleanup open; recovery access invariant preserved. |
| Parent Workspace | 8.5/10 | UX walkthrough complete / provisionally accepted | Solid family hub. Currency encoding (MOB-001), inline RSVP (MOB-008), Event Detail return (MOB-008A), and Priority Alerts 7-day RSVP window (PRN-002) resolved and accepted (`75c14aa`); RSVP wording distinction (PRN-001) open. |
| Player Workspace | 7.5/10 | UX walkthrough complete / provisionally accepted | Functionally stable. Youth Shop purchasing safeguards (YTH-001) resolved and accepted (`cdd9054`); YTH-002 and YTH-003 verified as existing safeguards by code audit; My Stats breakdown and My Progress match report deep links open for polish. |

## Role identity

- **Committee:** Run the club.
- **Welfare:** Protect people and keep the club safe and compliant.
- **Coach:** Manage and develop the team.
- **Treasurer:** Run and sustain the club’s finances.
- **Parent:** Stay informed and manage children.
- **Player:** Experience motivation, progress and belonging.
- **Administrator:** Maintain and configure the Club OS platform, not perform every sensitive operational role.

## MVP Priority Alert persona-scoping acceptance

**Status (updated 2026-08-14):** Implementation, source validation and LocalWP manual acceptance are complete. The implementation is merged to plugin `main`, the acceptance documentation is merged to docs `main`, and OS-032 is formally complete and closed for MVP.

### Accepted MVP policy

A Priority Alert shown in a workspace must represent something the **active persona** can legitimately understand and act upon. Canonical Person identity and Communication recipients remain shared, but each workspace applies persona relevance, capability checks and target authorization before rendering an alert. Committee membership alone does not imply Finance, Registration review, Match reporting, Event/team attendance or Welfare responsibility. Future read-only oversight belongs in Club Health, Team Health or governance reporting rather than as a misleading actionable Priority Alert.

The accepted projection uses `WorkspacePriorityAlertService`, recipient-aware Communication candidate retrieval, `MemberExperienceContext` filtering and final display limiting only after eligibility checks. `FinanceOperationalAlertsProvider` owns one shared Finance warning calculation. Notification delivery, recipient generation, unread/read and acknowledgement state, Event and Welfare permissions, Secretary Command Centre Priority Actions and existing persona-native alerts are unchanged. No schema, migration, CSS or JavaScript change was required.

### Accepted persona behaviour

- **Parent:** Priority Alerts remain family/child relevant; authorised Parent Event notifications remain available; selected-child and all-children scoping is preserved; operational Finance warnings do not leak into Parent.
- **Player:** Priority Alerts remain Player-relevant; unrelated Finance, Welfare, Secretary, Committee and Coach operational alerts are excluded.
- **Coach:** Priority Alerts remain Team, Matchday and attendance focused and scoped to legitimate Coach operational context; unrelated Committee, Finance and Welfare alerts are excluded.
- **Welfare:** Guardian Event notifications belonging to the same canonical Person do not appear while Viewing As Welfare. Welfare remains safeguarding-focused, Parent-only Event access remains restricted, and Welfare Event permissions were not broadened.
- **Ordinary Committee:** LocalWP acceptance with Louis Hall confirmed that Finance warnings, Incomplete Match Reports, Events awaiting attendance responses and Registrations requiring review are absent. With no genuine Committee priority, the dashboard correctly reports “Everything is running smoothly.” Committee remains a governance/oversight persona rather than an implicit Treasurer, Secretary, Coach or Welfare super-role.
- **Finance-authorised Committee:** LocalWP acceptance with Jess Test confirmed that the Finance warning appears when authorised, remains absent for ordinary Committee members and opens the canonical Outstanding Accounts surface instead of reloading Committee.
- **Treasurer:** A qualifying overdue invoice produces exactly one canonical Finance warning. Its action and the existing View Outstanding Accounts Quick Action both use `/club-os/finance/outstanding/`. The operational warning does not leak into Parent or Welfare.
- **Secretary:** Secretary Command Centre Priority Actions remain authoritative. No second generic Priority Alert feed was introduced and the existing Secretary workflow is unchanged.
- **Club Admin and multi-role users:** Broad capabilities do not override an active narrow Parent, Welfare, Player or Coach persona. Broader operational alerts return only in an appropriately broad persona with an authorised destination.

### Finance alert ownership and validation

Finance warnings are primarily Finance/Treasurer operational alerts. They may also appear in an authorised Committee/Admin context when canonical Finance and destination access permit it. The overdue-invoice calculation is shared through `FinanceOperationalAlertsProvider` rather than duplicated, and the canonical portal destination is `/club-os/finance/outstanding/`.

Final focused evidence: Workspace Priority Alert scoping 109 checks; Committee permissions 90; Treasurer operational read access 45; Treasurer Finance relationships 250; Treasurer directory UX 34; Parent Family Finance 44; Secretary Command Centre 95; Secretary Events 108; Event action leakage 27; Dashboard cancellations 54; Committee Communications 281. A pre-existing Treasurer Finance configuration validator baseline mismatch concerning the expected rewrite/schema version remains open. It predates this repair and is not resolved or caused by the Priority Alert work.

## MVP Release Readiness Integrity acceptance

**Status (updated 2026-08-15):** Batches 1, 2, 2.5 and 3 are implementation complete, source validation complete and LocalWP manually accepted. The plugin implementation is merged to plugin `main`, the documentation reconciliation is merged to docs `main`, and the MVP Release Readiness Integrity workstream is formally complete.

- **Batch 1 — Weather / Match Readiness Integrity:** Synthetic Weather was removed from active MVP Event Detail, Team Events, Matchday Hub, Match Mode, Match Report and Event Hub presentation where applicable, and Weather is no longer a readiness criterion or next action. Genuine preparation criteria determine readiness and a genuinely complete preparation reaches 100% / Match Ready. Weather was not implemented; dormant Weather integration scaffolding remains Post-MVP. LocalWP acceptance and the 110-check focused validator passed.
- **Batch 2 — Visible MVP Placeholder Cleanup:** Removed the accepted Player and Parent-preview Achievements placeholders, Matchday Travel Time and future Notes placeholders, Event Hub Rewards dead actions and stale Availability placeholder, synthetic/fixed-zero Event status or response presentation where applicable, Registration photo-upload placeholder, generic Admin Person/Team Profile menu entries, legacy Person/Team Coming Soon cards and the authenticated generic “Page coming soon” route fallback. Genuine Player Progress, Player-of-the-Match/statistics, Availability, Audience and ID-bound Person/Team routes remain; unknown authenticated generic portal routes now fail closed to HTTP 404 / Page not found. LocalWP acceptance passed and the focused validator reached 169 checks.
- **Batch 2.5 — Welfare Placeholder Repair:** Removed Timeline, Notes, Attachments, Communications, Activity History and misleading Next Steps placeholder cards from the remaining active legacy Admin Welfare Concern surface. The page still provides genuine concern data; status, priority and Welfare Officer assignment workflows, canonical portal detail, real portal Timeline and Activity History remain. Welfare authorization, sensitive response protection and unauthorized-access denial are unchanged. This does not claim deferred Notes, Attachments or concern Communications were implemented. LocalWP acceptance and the 193-check focused validator passed. (Reconciliation note, `5348403`: the short operational **Welfare Update** capability added later is a distinct, deliberately narrow concept — a one-line operational handover log, not the detailed safeguarding case-note/Attachments/Communications system this batch correctly still describes as unimplemented; see the Welfare Workspace Workflows bullet above.)
- **Batch 3 — Release Readiness Policy / Integrity:** Overall Ready is true only when there are zero unresolved risks with `required = true`. `required` is the deterministic blocking switch; severity describes classification and urgency. The previous Blocker/High/Medium-only test omitted Critical and could theoretically allow a required Critical risk to coexist with Ready. Critical is now canonical and any required Critical risk blocks release. The 244-check focused validator passed.

Required release categories are plugin activation, portal boot registration, authentication boundary, duplicate administrator routes, duplicate portal routes, duplicate scheduled hooks, missing database tables, Kernel service resolution, schema upgrade/lifecycle integrity, destructive-delete integrity, communication attachment validation and scheduled-hook deactivation cleanup.

LocalWP Release Readiness displayed **Ready**, zero required open risks, Blocker 0, Critical 0, High 0, Medium 4, Low 1 and Informational 2; controlled lifecycle evidence showed Pass. `medium.audit-coverage-inconsistent` was visible as **Required before 1.0: No** and remains Post-MVP/P2 debt for broader ActivityLogger/timeline completeness in some administrative domains, without removing or downgrading security-critical Welfare, Communications, Finance or Match audit boundaries. `medium.placeholder-experiences` was also visible as **Required before 1.0: No**: active audited MVP placeholder exposure is resolved, while dormant/deferred Post-MVP scaffolding remains. The inventory correctly distinguished resolved active MVP exposure from dormant Post-MVP scaffolding.

The full safely executable non-mutating release gate passed 68/68. Five controlled integration/mutating validators were excluded from that gate—not failed: `validate-parent-autosave-preservation.php`, `validate-parent-card-info-request.php`, `validate-person-first-team-assignment-routing.php`, `validate-secretary-registration-approval.php` and `validate-secretary-registration-lifecycle.php`.

Post-MVP scope remains explicit: real Weather integration, Rewards, Achievements/XP, Travel Time, richer Matchday Notes, broader audit completeness and dormant placeholder cleanup are not MVP release blockers.

## RC Clean-Install Blocker Repair acceptance

**Status (updated 2026-08-15):** Implementation, Gate 2C post-commit clean-install verification and pre-merge audit complete. Merged to plugin `main` at commit `e3f115dce90a04f3812036334317f691ba367b42`.

### Clean-install findings and blocker resolutions

A true fresh-install Release Candidate test on WordPress 7.0.4, PHP 8.2.29 and MySQL 8.4 established the clean-baseline foundation (48 Club OS-owned tables, schema/data version `2026.08.6`, complete upgrade status across 25/25 steps/results, 15 system formations and 129 slots) and resolved three genuine release-candidate blockers:

1. **AI Activity / dbDelta Schema Reconciliation (Blocker 1):**
   - **Defect:** Repeated schema reconciliation under WordPress 7.0.4 exposed a dbDelta parsing defect caused by intermediate blank lines inside `CreateAIActivityTable.php` multiline `CREATE TABLE` DDL. This produced `dbDelta` undefined-index warnings and malformed empty-index `ALTER TABLE` SQL.
   - **Repair:** DDL formatting was corrected without changing persistent schema semantics. Schema and data versions remain `2026.08.6`, no migration is required, and the 4 canonical indexes (`PRIMARY`, `user_id`, `provider`, `created_at`) remain intact. Repeated reconciliation passes 2/2 cleanly with 0 warnings and 0 malformed SQL.

2. **Member Experience Identity Boundary / Fail-Closed Enforcement (Blocker 2):**
   - **Defect:** An unlinked WordPress administrator with no canonical Club OS Person record previously resolved to a synthetic Welfare member experience with `person_id = 0`. This violated the core identity model.
   - **Repair:** Confirmed the canonical invariant: **Administrative authority does not create member identity**. Removed `synthetic_welfare_context` and synthetic identity fallback. Users without an active linked `Person` fail closed with `MemberExperienceOperationResult::fail()`. Legitimate linked Welfare, Committee, Coach, Parent, Player, Secretary and Treasurer persona resolution and switching are preserved, with zero capability broadening.

3. **Public Prospect Intake Feedback & Route Inventory (Blocker 3):**
   - **Defect:** Public prospect feedback-cookie consumption occurred inside `PublicProspectIntakePage::render_form()` after HTML output started, triggering headers-already-sent warnings. Additionally, public prospect route inventory rows had an incomplete tuple shape lacking the 4th boolean parameter.
   - **Repair:** Feedback-cookie consumption was moved to pre-output routing in `PublicProspectRouter.php`, ensuring zero header mutation during rendering. Public route inventory rows in `ReleaseRouteInventory::administrator()` were updated to the canonical 4-tuple element structure (`slug`, `title`, `capability`, `hidden = false`).
   - **Result:** Public enquiry GET returns HTTP 200, invalid submissions perform clean PRG redirect with one-time error notice rendering/clearing, valid submissions complete thank-you flow creating exactly 1 prospect record, zero duplicate records, zero header warnings, zero route inventory warnings and zero real emails sent.

4. **Billing Scheduler Contract on Clean Installation:**
   - On an empty installation with no billing schedules, `iexel_club_os_process_billing_schedules = 0`. This is the intentional canonical source behavior; zero billing hooks on an empty site is not a defect, and the scheduler contract was not altered.

### Validation & Release Candidate Status

- **Post-Commit Clean-Install Gate (Gate 2C):** Verified on a fresh WordPress 7.0.4 baseline copied with an exact deterministic 976-file SHA-256 manifest. Confirmed 48 tables, schema/data version `2026.08.6`, upgrade complete (25/25 steps/results), 15 formations, 129 slots, zero business fixtures, clean deactivation/reactivation, 2/2 repeated schema reconciliation passes, 0 dbDelta warnings, 0 malformed SQL, 0 duplicate hooks, and all identity/prospect flows.
- **Automated Validation:** Focused validators passed 3/3 (`validate-committee-permissions.php` 95 checks, `validate-event-lifecycle-participant-projections.php` 257 checks, `validate-public-prospect-intake-security.php` 124 checks). Full non-mutating validator gate passed 68/68. The previously accepted evidence that all 5 controlled mutating validators passed 5/5 is fully preserved. PHP lint passed 8/8.
- **Merge & Status:** Merged to plugin `main` (`e3f115dce90a04f3812036334317f691ba367b42`). Clean-install blocker repairs are formally complete.

## RC Controlled Upgrade Matrix Gate 2 acceptance

**Status (updated 2026-08-16):** Execution, architecture audit and formal acceptance complete.

### UpgradeRunner Reconciliation Architecture

`UpgradeRunner` was confirmed as a **full-registry idempotent reconciliation pipeline**:
- For any non-current baseline (`2026.07.1`, `2026.08.2`, `2026.08.5`), all 25 registered `UpgradeStep` contracts are evaluated sequentially.
- Each step checks its `is_valid()` predicate first: satisfied invariants execute as safe no-op checks (`ran = false`), while unfulfilled invariants execute `apply()` (`ran = true`) inside a database transaction and revalidate.
- Persisted `completed_steps` records all verified/satisfied invariants across the registry.
- `schema_version` and `data_version` do not filter the registry, and steps do not define from-version ranges.
- The pre-execution 18/9/2 assumption was a theoretical estimate of newly introduced migrations, not `UpgradeRunner` execution semantics.
- An already-current installation (`2026.08.6` with all 25 valid invariants) immediately returns `already_current` with 0 steps executed.

### Matrix Execution Evidence

1. **Row 1 (`906960b` / `2026.07.1` -> `2026.08.6`):** 41 -> 48 tables, 25 steps (18 mutating, 7 no-op) in 2.0803s. Normalized team reference to `TM-000001`, backfilled Secretary capabilities. **PASS**.
2. **Row 2 (`ddb784e` / `2026.08.2` -> `2026.08.6`):** 44 -> 48 tables, 25 steps (10 mutating, 15 no-op) in 1.4483s. Reconciled Coach team management capability. **PASS**.
3. **Row 3 (`0d62f56` / `2026.08.5` -> `2026.08.6`):** 47 -> 48 tables, 25 steps (3 mutating, 22 no-op) in 1.3500s. Reconciled Manager capability, backfilled Training participant player role. **PASS**.
4. **Row 4 (`e3f115d` / `2026.08.6` -> `2026.08.6` - Idempotence):** 48 tables, `code: already_current`, 0 steps executed in 0.3523s, 0 mutations. **PASS**.

### Interruption, Identity & Safety Guarantees

- **Controlled Interruption & Resume:** Simulated failure at step `2026_07_welfare_concerns`; verified `failed` status, non-ready blocking notice, smooth resumption to `complete` with `retry_count = 1`, and lock release. Harness/state simulation only; production plugin source was untouched.
- **Identity Invariant:** *Administrative authority does not create member identity*. Unlinked administrators fail closed across all upgraded baselines without synthetic `person_id = 0` personas.
- **Safety Audits:** Zero duplicate data, zero destructive reapplication, zero capability regression, zero event/match historical corruption, and zero formation/reference duplication.
- **Environment Isolation:** Executed entirely on disposable RC database (`127.0.0.1:10010`); development database (`127.0.0.1:10005`) and plugin source remained untouched.

Both Environment 1 (Clean Installation) and Environment 2 (Controlled Upgrade Matrix) have passed. Internal Club Testing and its subsequent remediation programme are now complete and merged to plugin `main` at `b2b51eb` (2026-08-29, pure fast-forward, GREEN pre-merge gate). Next milestone: Final Release Readiness / Club OS v1.0 sign-off — see `RELEASE_CHECKLIST.md` for the specific remaining gates. This is safe integration into `main`, not final Release Readiness sign-off or production deployment approval.

## MVP priorities

- **Global — complete:** Move Quick Actions directly below each workspace hero across all persona dashboards via `PortalDashboardLayout`.
- **Global — complete:** Fix blue-on-blue and other low-contrast text through shared design tokens (OS-029, FIN-028, PL-024) — delivered via the systemic dark-surface on-dark token treatment, commit `34cd5d4`, 2026-08-21; protected by `tools/validate-dark-surface-contrast.php` (6390 checks passing).
- **Global — complete:** Standardise displayed dates to DD/MM/YYYY and HH:mm consistently across Club OS via `DisplayDate` service (OS-027).
- **Committee — complete:** Remove duplicate Home / Club Overview navigation — Club Overview is the sole landing tab (OS-001).
- **Committee:** Registration summary metrics — executive Club Health overview delivered; operational registration review queues intentionally owned by Secretary Command Centre per OS-032 governance policy (OS-002).
- **Committee — complete:** Provide operational create/edit/archive flows for club events, communications and projects because committee users cannot use wp-admin (OS-004).
- **Coach — complete:** Capture opponent, competition and match location during match-event creation (OS-016).
- **Coach — complete:** Show authorised emergency contacts in Matchday Hub (OS-017).
- **Coach — complete:** Open Directions in a new tab without replacing Club OS via `target="_blank"` / `rel="noopener"` (OS-018).
- **Coach — complete:** Priority alerts dominance and scoping — resolved in `WorkspacePriorityAlertService` (OS-020).
- **Coach — complete:** Allow bench/substitute selection in Lineup Builder and persist it into Matchday Hub and substitution controls (OS-025).
- **Coach — complete:** Coach Team Event Scope Hardening & Football Event-Type Alignment (SEC-008) — restricted to Training, Fixture, Friendly, Tournament; Meet / Arrive Time intentionally supported for Training; Matchday Hub Match Location display repaired (`2370551`).
- **Coach — complete:** Completed Match Correction (CMC-001) — Correct Match Record (scorer/assist/minute correction, Normal ↔ Penalty), Remove Incorrect Goal and Add Missed Goal, built on canonical score reconciliation and Match incident `timeline_order`, with a combined end-to-end acceptance gate.
- **Coach — complete:** Verified Historical Scorer Attribution v1 (CMC-002) — exceptional, evidence-backed scorer recovery for a completed Match's active Club goal when reliable Tier-1 historical participation evidence is genuinely absent; Player-specific and provenance-specific, browser accepted and merged (`2f3dcee`).
- **Coach — complete:** Match Hero Goal-Scorer Presentation (CMC-003) — Club goal scorers present beneath the Match score in familiar football-result style, across both live Match Mode and completed-Match presentation, with a live-eligibility correction and responsive/half-width polish delivered in the same arc (`b37de1c`); see "Match Hero Goal-Scorer Presentation" below.
- **Parent — complete:** Fix selected-child context so an U8 child cannot see an U7 next event, and deliver Parent All-Children event identity + multi-child RSVP (OS-028).
- **Parent — complete:** Improve Team Hub text contrast (OS-029) — resolved by the systemic dark-surface contrast treatment, commit `34cd5d4`, 2026-08-21.
- **Parent — complete:** Provide a real Finance page with invoice detail and payment history — delivered in Parent Family Finance & Invoice Detail (OS-030).
- **Notifications:** Improve attachment/image viewing so users can close and return without relying on the browser Back button (OS-031 — Post-MVP).
- **Treasurer — complete:** Provide invoice view/edit/cancel/archive or void actions and a proper invoice detail route — delivered in Treasurer Finance MVP (FIN-027).
- **Treasurer — complete:** Allow Treasurer role to manage fee rules and discount policies inside Club OS — delivered in Treasurer Fee Rules & Discount Policies management (FIN-029, FIN-030).
- **Treasurer — complete:** Fix blue-on-blue text on billing pages (FIN-028) — resolved by the systemic dark-surface contrast treatment, commit `34cd5d4`, 2026-08-21; billing schedule cards, billing schedule metadata and finance invoice links now use appropriate on-dark foreground tokens.
- **Treasurer:** Fix static summary text showing caret as though editable (FIN-031). Low priority. A read-only source audit (2026-08-26) could not reproduce this in current Finance/Treasurer source — no static summary currently uses `cursor: text` or another confirmed input-like affordance, and the Treasurer/Finance surface has been substantially rebuilt since this finding was originally recorded. A second, independent, more targeted diagnostic (2026-09-08) investigated the same symptom reported against the analogous static Secretary Command Centre heading and directly proved the cause: plain non-`contenteditable` markup, `isContentEditable === false` at every ancestor, `document.designMode === "off"`, and zero `contenteditable`/`caret-color`/`designMode`/`execCommand` usage anywhere in plugin source. **Current classification: this is very likely browser caret browsing (e.g. F7-style caret navigation), not a Club OS implementation defect** — not merely "not reproducible," but positively evidenced as browser-side behaviour. No plugin change was made or is warranted. It remains formally open only pending Product Owner confirmation that this matches what they observed; it is not an unresolved implementation blocker.
- **Player — complete:** Create a real My Stats page based on the coach player-statistics experience, limited to the logged-in player (PL-022) — delivered in Batch IN3F16-PL1C at `/club-os/player/stats/`.
- **Player — complete:** Expand My Season with progress, attendance, milestones and next achievement (PL-021) — delivered in Batch IN3F17-PL2B2.
- **Player — complete:** Move Quick Actions near the top (PL-023) — delivered in `PortalDashboardLayout`.
- **Player — complete:** Fix blue-on-blue text (PL-024) — resolved by the systemic dark-surface contrast treatment, commit `34cd5d4`, 2026-08-21; Player Statistics dark surfaces now use appropriate on-dark foreground tokens.
- **Admin — complete:** Reorganise the Club OS sidebar into grouped sections and hide route-only detail pages — delivered as Admin Sidebar Navigation Consolidation & Route Cleanup (ADM-001 / ADM-002 / ADM-003), commit `c88eab9`, 2026-08-21.

## Consolidated review log

| ID | Area | Finding | Type | Priority | Release |
|---|---|---|---|---|---|
| OS-001 | Committee | Duplicate Home and Club Overview navigation — resolved; Club Overview is sole landing tab | Resolved UX | Complete | MVP |
| OS-002 | Committee | Registration panel operational metrics — executive Club Health overview delivered; operational queues intentionally owned by Secretary Command Centre per OS-032 | UX | Low | Post-MVP |
| OS-003 | Committee | Committee Quick Actions moved near the top; all five actions passed MVP acceptance | Resolved UX | Complete | MVP |
| OS-004 | Committee | Create/edit/archive club events, communications and projects — delivered in Secretary Events, Communications & Command Centre | Resolved workflow | Complete | Sprint 30/32 |
| OS-005 | Committee | Improve dashboard visual hierarchy — delivered in Secretary Command Centre & Portal Navigation | Visual | Complete | Sprint 30 |
| OS-006 | Committee | Projects card feels isolated | Visual | Low | Post-MVP |
| OS-008 | Welfare | Quick Actions moved directly below hero across all persona dashboards | Resolved UX | Complete | MVP |
| OS-009 | Welfare | Add edit/archive lifecycle for concerns; deletion heavily restricted | Workflow | Medium | Post-MVP |
| OS-010 | Welfare | Expand into broader compliance workspace — the canonical Staff Compliance credential foundation, Secretary management experience, the Welfare-facing restricted People/Person/Compliance projection, and proactive compliance expiry alerting are all now implemented (`b5f006a6`/`3352d300`/`cd871f3`/`2bdd62e`; DBS/safeguarding/first-aid/qualification categories, type-aware naming, target-Person eligibility, Welfare People directory + profile + compliance management, Expiring Soon/Expired alerts delivered to Secretary and Welfare with workspace-correct routing). See `SPRINTS.md`'s "Staff Compliance — Batch A, Batch B, Batch C & Batch D" section | Resolved gap | Complete | MVP |
| OS-011 | Welfare | Strengthen concern detail hierarchy — independently verified still present by a 2026-08-26 read-only audit (the portal Welfare Concern Detail page renders Summary/Information/Timeline/Activity History as undifferentiated equal-weight grid cards, with no safeguarding or capability impact). Confirmed real, cosmetic/non-blocking; not currently promoted ahead of Internal Club Testing | Visual/UX | Medium | Polish |
| OS-012 | Welfare | Make directory filters more compact | Visual | Low | Post-MVP |
| OS-016 | Coach | Capture match configuration during event creation — delivered in Portal Event Builder & Secretary Events Management | Resolved gap | Complete | Sprint 30 |
| OS-017 | Coach | Emergency contacts missing from Matchday Hub — exact-season authorised projection delivered | Resolved gap | Complete | MVP Experience Polish |
| OS-018 | Coach | Directions opens in same browser tab — resolved with `target="_blank"` / `rel="noopener"` across Matchday and Event venue cards | Resolved bug | Complete | MVP |
| OS-019 | Coach | Some pages use different visual language — dark immersive matchday/team styling is intentional and should not trigger homogenisation | Visual | Low | Post-MVP |
| OS-020 | Coach | Priority alerts dominate dashboard — persona scoping, capping and filtering delivered in `WorkspacePriorityAlertService` | Resolved UX | Complete | MVP |
| OS-025 | Coach | Bench players could not be selected or shown in Matchday Hub — saved substitute flow delivered | Resolved bug | Complete | MVP Experience Polish |
| OS-027 | Parent | Dates displayed in ISO format — standardised to DD/MM/YYYY and HH:mm via `DisplayDate` Batches 1 & 2 | Resolved consistency | Complete | MVP |
| OS-028 | Parent | Selected child sees event from wrong team — selected-child event scoping, Player Preview, and Parent All-Children multi-child RSVP delivered | Resolved bug | Complete | Sprint 31 |
| OS-029 | Parent | Team Hub had blue-on-blue text — resolved: `.iexel-team-workspace-hero` and related dark surfaces now use on-dark foreground tokens (`34cd5d4`, 2026-08-21); protected by `validate-dark-surface-contrast.php` | Resolved accessibility | Complete | MVP |
| OS-030 | Parent | Finance experience is too limited — Parent Family Finance workspace, invoice detail & payment history delivered | Resolved gap | Complete | Sprint 33 |
| OS-031 | Notifications | Image attachments lack an in-app close/viewer experience — direct link downloads are functional for MVP; lightbox viewer deferred | UX | Low | Post-MVP |
| OS-032 | Global | Priority Alerts could expose work unrelated to the active persona — persona/capability scoping accepted, merged to plugin `main`, and formally closed for MVP | Resolved security/UX | Complete | MVP |
| SEC-008 | Coach | Coach Team Event Scope Hardening & Football Event-Type Alignment — restricted to Training, Fixture, Friendly, Tournament; Meet/Arrive supported for Training; Matchday Hub Match Location repair delivered (`2370551`) | Resolved gap | Complete | MVP |
| CMC-001 | Coach | No safe way to correct a completed Match after Full Time — Correct Match Record, Remove Incorrect Goal and Add Missed Goal delivered on canonical score reconciliation and Match incident `timeline_order`, validated by a combined end-to-end acceptance gate | Resolved gap | Complete | MVP |
| CMC-002 | Coach | A completed Match's active Club goal can have no reliable Tier-1 historical participation evidence (no saved Selection, no legitimate live-bench admission), leaving the scorer unrecoverable and Data Quality showing a misleading generic outside-selection warning — exceptional, evidence-backed Verified Historical Scorer Attribution delivered (`2f3dcee`), Player-specific and provenance-specific throughout | Resolved gap | Complete | MVP |
| CMC-003 | Coach | Club OS did not present Club goal scorers beneath the Match score in familiar football-result style, in either live Match Mode or completed-Match presentation — delivered, with a live-eligibility correction and responsive polish in the same arc (`b37de1c`) | Resolved gap | Complete | Pre-MVP |
| PL-025 | Player | Player Progress navigation architecture undecided — confirmed canonical MVP journey is Player Home → Team Workspace → My Progress (embedded); Player global navigation stays Home/Team/Events/News with no fifth Progress item | Resolved decision | Complete | MVP |
| RR-001 | Release Readiness | Integrity Batches 1, 2, 2.5 and 3 implemented, validated and accepted; plugin implementation and documentation reconciliation merged to their respective `main` branches | Resolved release integrity | Complete | MVP |
| FIN-027 | Treasurer | Invoices cannot be viewed, edited, cancelled, archived or voided properly — Treasurer invoice lifecycle delivered | Resolved gap | Complete | Sprint 33 |
| FIN-028 | Treasurer | Blue-on-blue text on billing pages — resolved: billing schedule cards/metadata and finance invoice links now use on-dark foreground tokens (`34cd5d4`, 2026-08-21); protected by `validate-dark-surface-contrast.php` | Resolved accessibility | Complete | MVP |
| FIN-029 | Treasurer | Cannot create/edit/archive fee rules — Portal Fee Rules management delivered | Resolved gap | Complete | Sprint 33 |
| FIN-030 | Treasurer | Cannot create/edit/archive discount policies — Portal Discount Policies management delivered | Resolved gap | Complete | Sprint 33 |
| FIN-031 | Treasurer | Text shows caret as though editable (historical finding) — not reproducible in current source as of a 2026-08-26 read-only audit; no matching `cursor: text`/input-like affordance found on any current Finance/Treasurer static summary, and the surface has been substantially rebuilt since. Product Owner reproduction required before implementation | Visual bug | Low | MVP polish — awaiting reproduction |
| FIN-032 | Treasurer | Finance's own visual system felt pale/generic against the shared premium Club OS vocabulary — Treasurer Premium Workspace Alignment Batch 1 delivered, Product Owner visual acceptance PASSED (`8403691`) | Resolved gap | Complete | Post-RC |
| FIN-033 | Treasurer | `finance-reports` was an unfinished route/title scaffold present since the original Treasurer Finance implementation, with no dispatcher, renderer or service ever built — identified during FIN-032 and initially recorded as an open routing defect; a dedicated audit reclassified it as an unfinished scaffold rather than a fixable defect (never a regression, no product scope ever defined), and the phantom scaffold was removed (`fbfc032`) rather than completed. A genuine Finance Reports capability remains future product-definition work, not implemented | Resolved (removed) | Complete | Post-RC |
| PL-021 | Player | My Season has too much unused space and weak engagement — delivered with Season Journey, Milestones, Attendance rate, Next Milestone target in Batch IN3F17-PL2B2 | Resolved UX | Complete | MVP |
| PL-022 | Player | My Stats is only a minimal dashboard section — dedicated standalone experience with Appearances, Goals, Assists, POTM, Attendance, Clean Sheets, safeguarding delivered in Batch IN3F16-PL1C | Resolved gap | Complete | MVP |
| PL-023 | Player | Quick Actions moved directly below hero across all persona dashboards | Resolved UX | Complete | MVP |
| PL-024 | Player | Blue-on-blue text — resolved: Player Statistics dark surfaces now use on-dark foreground tokens (`34cd5d4`, 2026-08-21); protected by `validate-dark-surface-contrast.php` | Resolved accessibility | Complete | MVP |
| ADM-001 | Admin | Sidebar navigation was too long — over 30 items in wp-admin sidebar; consolidated to 19 visible items grouped into logical clusters, 36 route-only items hidden with routes preserved (`c88eab9`, 2026-08-21) | Resolved UX | Complete | MVP |
| ADM-002 | Admin | Route-only pages appeared as sidebar destinations — hidden with in-page contextual creation actions restored on People/Teams/Events/Venues and existing admin-navigation components elsewhere; 227-check focused validator passing | Resolved UX | Complete | MVP |
| ADM-003 | Admin | Operational dashboards (e.g. Committee Dashboard) appeared in admin navigation — hidden from the sidebar; portal remains the canonical home for those experiences | Resolved UX/Architecture | Complete | MVP |
| ADM-004 | Admin | Long-term sensitive-role approval workflow | Security/Governance | High | Post-MVP |
| ADM-005 | Admin | Blank Fundraising screen in `/wp-admin/` (`page=iexel-club-os-fundraising`) — investigate routing defect or retire redundant admin menu entry | Defect / Cleanup | Medium | MVP (Tier B) |
| ADM-006 | Admin | Technical support, database upgrades, and recovery diagnostics access invariant — permanently retained via `/wp-admin/` | Architecture | Critical | MVP Invariant (Tier A) |
| SET-001 | Settings | Separate operational configuration (season dates, age groups, club contacts) from Brand Studio for MVP | Information architecture | Medium | MVP (Tier B) |
| SET-002 | Settings | Add image positioning, zoom and focal-point controls | Visual tool | Medium | Post-MVP (Tier D) |
| SET-003 | Settings | Create separate Club, System and Experience Settings areas — broader modular architecture | Information architecture | High | Post-MVP (Tier D) |
| SET-004 | Settings | Add club-profile defaults: Grassroots, Academy, Semi-Pro, Professional and Custom | Platform feature | High | Post-MVP (Tier D) |
| MOB-001 | Parent | Invoice payment settlement currency encoding (£ symbol defect) — resolved and accepted (`bf6df68`) | Resolved bug | Complete | MVP |
| MOB-005 | Coach | Lineup Builder unsubmitted selections lost on navigation — draft persistence and player link resolved (`28264dc`) | Resolved UX | Complete | MVP |
| MOB-006 | Coach | Lineup Builder bulk attendance race conditions — reliable bulk attendance resolved (`bc5ab91`) | Resolved UX | Complete | MVP |
| MOB-007 | Coach | Lineup Builder match status display out of sync — status synchronization resolved (`bc5ab91`) | Resolved bug | Complete | MVP |
| MOB-008 | Parent | Upcoming fixture cards lacked inline RSVP and lost page position — inline per-child RSVP and scroll return resolved (`fa72493`) | Resolved UX | Complete | MVP |
| MOB-008A | Parent | Standalone Event Detail RSVP redirects to Team Hub instead of returning to Event Detail — resolved with per-child anchor continuity (`75c14aa`) | Resolved workflow | Complete | MVP |
| MOB-009 | Fixtures | Completed fixture card presentation inconsistent between Parent and Coach hubs — unified via `FixtureCardMatchup` (`4e259f9`) | Resolved UX | Complete | MVP |
| MOB-010 | Fixtures | Parent upcoming fixture card lacked unified matchup visual hierarchy — unified via `FixtureCardMatchup` (`4e259f9`) | Resolved UX | Complete | MVP |
| MOB-011 | Fixtures | Coach upcoming fixture card opponent name wrapped awkwardly across words — unified with boundary wrapping (`4e259f9`) | Resolved UX | Complete | MVP |
| SEC-009 | Secretary | Create Event "Specific People" selector modal horizontal overflow on narrow mobile screens (320px–390px) | Layout / Mobile | Medium | MVP (Tier B) |
| PRN-001 | Parent | RSVP action button copy ambiguity when responding for child vs self — differentiate "Available for [Child]" vs "I'm Available" (remains open) | UX / Clarity | Medium | MVP (Tier B) |
| PRN-002 | Parent | Unanswered event RSVP action requests in Priority Alerts not windowed or ordered chronologically — resolved with rolling 7-day window and ascending start-time sort (`75c14aa`) | Resolved UX | Complete | MVP |
| COM-001 | Committee | General committee members can broadcast club-wide messages without administrative sign-off — approval gate and mobile attachment workflow resolved and accepted (`6d7a3f4`) | Governance / Comms | Medium | Complete |
| COM-002 | Committee | Committee views must strictly exclude confidential Welfare safeguarding notes, individual debtor ledgers, and registration medical records | Security / Data minimisation | High | MVP (Tier A) |
| CCH-001 | Coach | Bulk availability response management for upcoming training/events in Coach Hub (distinct from lineup attendance) | Operational UX | Medium | MVP (Tier B) |
| BMG-001 | Parent | Back My Game linked child and team supporter visibility and pledge status in Parent Hub | Operational UX | Medium | MVP (Tier B) |
| PL-026 | Player | Expandable match-by-match statistics breakdown underneath aggregate season totals | Visual / UX | Low | Polish (Tier C) |
| PL-027 | Player | Direct contextual deep links from Player My Progress appearance/milestone records into completed Match Reports | Visual / UX | Low | Polish (Tier C) |
| YTH-001 | Player / Shop | Youth players (<18) must not execute direct online hosted card checkout, select bank transfer, or create Club Shop financial orders without adult guardian authentication — resolved and accepted (`cdd9054`) | Resolved safeguarding | Complete | MVP (Tier A) |
| YTH-002 | Player / F2 | Youth Spot the Ball entry safeguarding — adult guardian authorization and minor prize routing to verified adult guardians | Code audit verification | Complete (Existing) | MVP (Tier A) |
| YTH-003 | Player / F1 | Youth fundraising appeal link attribution restricted to authenticated adult guardians; zero public child seller profiles | Code audit verification | Complete (Existing) | MVP (Tier A) |
| FND-001 | Parent / Fundraising | Campaign-specific family/player and team appeal attribution with QR-code sharing, safeguarding, payment confirmation, refund handling, and avoidance of double-counting | Enhancement | Medium | Post-MVP (Tier D) |
| B4D | Release | Private encrypted backup vault end-to-end payload population, verification, and restore validation | Disaster Recovery | High | MVP Gate (Tier A) |

## Detailed workspace direction

### Committee Workspace

- **Committee Workspace & Native Operations (complete):** Club OS-native management of club events, Club Projects CRUD, Committee Communications, Audience Builder v2, and live executive dashboard metrics are fully delivered (`Sprint 30`).
- Keep the premium hero and core dashboard structure.
- Use Club Overview as the sole landing tab.
- **Committee Quick Actions (OS-003 — accepted):** All five Committee Quick Actions work and OS-003 remains PASS.
- **Committee Communications Approval Gate (COM-001 — MVP Tier B):** General committee members sending broadcast communications to all club members, parents, or multiple teams require an administrative approval gate (Secretary or Club Admin sign-off) to prevent unvetted mass messages. Resolved and accepted (`6d7a3f4`). Image attachments, draft saving, audience preview, mobile filename containment, and approval gate submission validated on physical Android device over LAN.
- **Committee Permission Boundaries & Data Minimisation (COM-002 — MVP Tier A):** Committee workspace is strictly governance and oversight. General Committee views must strictly exclude confidential Welfare safeguarding notes and case records, individual member debtor ledgers and itemised family invoices (aggregates only), and registration medical records.
- **Committee Team Oversight Without Unnecessary PII (MVP Tier B):** Committee team oversight should present squad counts, coaching coverage, and operational readiness indicators without exposing unnecessary player personal data or private family details.
- **Non-blocking MVP UX follow-up:** Review the current **Open Team Workspaces** wording and destination for the Committee persona. It correctly opens the shared Coach Team area and correctly shows **No assigned teams** when a Committee user has no Team assignment, so this is not a functional defect. Prefer clearer leadership-oriented wording such as **View Teams** or **Team Overview**, or a more suitable oversight destination. This follow-up does not create a new MVP implementation batch; release readiness remains the primary MVP priority.
- Add richer registration metrics.

#### Post-MVP concept — Committee / Executive Team Health Dashboard

**Status:** Explicitly deferred until Post-MVP. This is a leadership and oversight experience for Committee/Admin users, not an operational Coach management experience and not an MVP release blocker.

The Team Health Dashboard could provide a club-wide, read-mostly summary of Team health without sending oversight users into the Coach Team Workspace. Potential summary data includes:

- Player count.
- Coach and Manager count.
- Squad capacity and vacancies.
- Games played, wins, draws and losses.
- Goals for and goals against.
- Attendance rate.
- Availability rate.
- Current Registration/compliance completeness.

Future high-level status labels could include **Healthy**, **Needs Attention** and **Critical**. Their semantics and thresholds remain intentionally undefined until a later authorised product and data-design phase.

#### Post-MVP concept — Team Health Profile

Selecting a Team from the Team Health Dashboard could open a richer leadership drill-down covering:

- Squad composition and capacity.
- Coaching coverage.
- Match and results trends.
- Attendance and availability trends.
- Registration/compliance indicators.
- Football performance summaries.
- Alerts requiring Committee/Admin attention.

Future authorised extensions may include Finance or sponsorship indicators only where the user's permissions allow. The profile must not expose sensitive Welfare information.

The Team Health experience must remain a leadership oversight layer over canonical Club OS data. It must not replace the Coach Team Workspace, Welfare Workspace, Finance Workspace or Secretary operational Team administration. Any later implementation should:

- Reuse canonical Team and TeamSeason data.
- Reuse current active Team Assignment data.
- Reuse canonical Statistics data.
- Reuse Attendance and Availability data.
- Remain role-aware and read-mostly for Committee users.
- Avoid duplicating operational Team data or creating a second source of truth.
- Preserve Coach workspace boundaries and Finance and Welfare permission boundaries.
- Be mobile-friendly and allow later authorised drill-down.

- **Welfare Experience Foundation (complete):** Role-aware safeguarding workspace, concern dashboard, concern directory, concern detail, status/priority lifecycle, optimistic revision control, activity timeline, and access isolation delivered (`Sprint 29`).
- **Welfare Workspace Workflows (complete, `5348403`):** Two accepted deliverables in one commit. First, the Welfare Concern Directory's Search/Status/Priority/Assigned Welfare Officer filters now reuse the established `.iexel-experience-form-grid`/`.iexel-experience-field` component already used elsewhere in Club OS (no new Welfare-only design system), resolving the ~320px Assigned Welfare Officer overhang and the previous browser-native filter appearance. Second, a new **Welfare Update** capability lets an authorised Welfare Officer append a short operational handover note (e.g. "Awaiting response from league.") to a Concern via a dedicated, append-only `welfare_concern_updates` table — no edit or delete path exists in this MVP, and there are no attachments, rich text, visibility levels or a recipient system. Author and timestamp are always server-derived and never trusted from the request; body text is sanitised (`sanitize_textarea_field`, tags stripped, ordinary line breaks preserved) and escaped on output; empty/whitespace-only input is rejected and the body is capped at 1,000 characters server-side (not merely via the textarea's `maxlength`) with no silent truncation; updates render newest-first (`created_at DESC, id DESC`, not insertion order). **This is a data-minimisation boundary, not an oversight:** a Welfare Update is a short operational handover line for colleagues, never a detailed safeguarding case note, allegation record or evidence log — the generic Activity History records only that an update occurred (a fixed "Added a Welfare update." message plus the Concern reference and update id) and never duplicates the operational text into that shared, cross-domain audit surface. A manually-implemented interim dashboard action linking Emergency Contacts/Players Requiring Attention rows to "View concerns" was found to be semantically wrong (a Player can have zero concerns and still need attention) and was removed before this commit — **do not describe that action as delivered.** See `SPRINTS.md`'s "Welfare Workspace Workflows" section for full delivery detail and validator coverage.
- Keep the concern dashboard, concern directory, concern detail, medical overview and emergency contacts.
- Move Quick Actions higher.
- **Restricted Welfare Person projection + Welfare Staff Compliance experience — Staff Compliance Batch C, the recommended next controlled implementation batch, not yet implemented:** the Welfare dashboard's Emergency Contacts and Players Requiring Attention rows remain informative-only pending this. It must expose only appropriate safeguarding/welfare-relevant information (identity, club/player context, emergency contact, current Operational Medical & Safety, medical consent/completeness, legitimate Concern linkage) and must never reuse the Secretary Person Profile wholesale or leak Finance, Registration administration, Team Assignment controls or other unrelated Secretary operations. Its Staff Compliance read/write projection must reuse the now-implemented canonical `PersonCredentialService`/domain exactly as-is (see the Staff Compliance bullet below) — never a duplicated credential store or a parallel validator.
- **Staff Compliance — canonical foundation and Secretary management now IMPLEMENTED (Batch A `b5f006a66cdcd8df9e127c27da1a94b570b93514`, Batch B `3352d300ab8fde56d47d307deacdab4b1f35d64a`).** A single canonical, shared Person/staff credential record (`{prefix}iexel_os_person_credentials`, namespace `IEXEL\ClubOS\Core\StaffCompliance`) covers DBS, safeguarding, first aid and free-text qualifications — explicitly not a duplicated credential system, and reused as-is (not re-implemented) by any future Welfare projection. Each credential carries type, a name (canonical-only for DBS; optional specific name with canonical fallback for safeguarding/first aid; required free text for qualification — the type list remains a stable, reviewed set, not a hard-coded qualification catalogue), issue/award date, an optional expiry/renewal date, an optional reference/registration number, a short administrative note (explicitly not a safeguarding case-note field), auditability (changed-field-name-only audit, never reference/note content), and a derived-at-read-time status (`Valid` / `Expiring Soon` — 42-day domain constant, no Settings UI yet / `Expired` / `No Expiry`) using semantic colour only (expired = danger, expiring soon = warning, valid = success), never the club accent colour, for severity. The **Secretary Person Profile** shows this summary, gated on canonical target-Person eligibility (see "Target-Person eligibility" below), with a full management route at `/club-os/secretary/people/{PERSON_ID}/compliance/` (Add Credential, same-record Correction, Archive lifecycle, Compliance History; a renewal is always a new record via Add Credential and never archives the record it supersedes). See `SPRINTS.md`'s "Staff Compliance — Batch A & Batch B" section for full delivery detail, and `DEVELOPMENT_HANDOVER_2026-09-08.md` for the current resume point. **Still not implemented:** the restricted Welfare projection of this same domain (Staff Compliance Batch C, immediately below) and compliance expiry alerts (Staff Compliance Batch D — likely a `ComplianceExpiryAlertsProvider` on the established alert-provider architecture, warning/critical semantics only, never club-accent/`action_required` for compliance severity).
- **Target-Person eligibility — a durable Batch B product rule.** Staff Compliance is not presented or manageable for every Person — only one who currently holds at least one qualifying official/staff relationship: the club-wide operational roles `club_admin`, `secretary`, `treasurer`, `welfare_officer`, `committee_member`, or a team staff assignment (`coach`, `assistant_coach`, `manager`). An ordinary player-only or parent-only Person is not eligible, and eligibility never requires a linked WordPress user account. This is enforced identically wherever Staff Compliance is reachable (the Profile summary, the management route, and every write), so an authorised Secretary or Club Admin cannot manage Staff Compliance for an ineligible Person by visiting the URL directly — **target-Person eligibility is a separate concept from current-user authorization** (who may act) and does not bypass it in either direction: Admin authority does not bypass target-Person eligibility, and being an eligible target Person (e.g. a Coach or Treasurer) does not itself grant permission to manage anyone's Staff Compliance. Removing a Person's final qualifying role/assignment makes the UI/route unavailable immediately without deleting or archiving their existing credential history.
- Prefer archive over delete for safeguarding records; permanent deletion should be highly restricted and policy-controlled.

### Coach Workspace

- Preserve the Matchday Hub, Team Workspace, statistics and lineup builder design.
- **Coach Event Setup & Scope Hardening (SEC-008 — complete):** Coach team event creation is restricted to the four football event types `Training`, `Fixture`, `Friendly` and `Tournament`. Other generic event types are unavailable in the Coach workflow. Secretary retains the broader canonical event model. Meet / Arrive Time is intentionally supported for Training.
- **Matchday Hub Location & External Directions (complete):** Emergency-contact projection, bench/substitute selection, external Directions (`target="_blank"` / `rel="noopener"` via PR #123), and Match Location hero card derivation (`2370551`) are fully delivered and verified.
- **Completed Match Correction (CMC-001 — complete):** From a completed Event, Match correction and recovery → Correct Match Record supports score-neutral scorer/assist/minute correction and Normal ↔ Penalty without reopening the Match. Remove Incorrect Goal and Add Missed Goal are also delivered, built on canonical active-ledger score reconciliation and Match incident `timeline_order` (`sequence` stays the immutable creation/audit order; `timeline_order` owns effective chronological replay/display order). Historical Player eligibility always reflects the actual historical pitch state — saved selection, Event audience, Attendance and the on-pitch state at the chosen placement boundary — never merely all selected/bench Players, and an equal-minute tie always requires an explicit Coach Before/After choice rather than an arbitrary break. A combined end-to-end acceptance gate proved the full correction journey (correction, removal, addition, equal-minute placement, all goal semantics, statistics, participant privacy) on one disposable completed Match. The completed-match participant experience for Player/Parent/Parent Preview remains a privacy-minimised, scoring-focused Match Story that never exposes ratings, Coach Notes, correction reasons/audit metadata or unrelated Player identities.
- **Verified Historical Scorer Attribution v1 (CMC-002 — complete, `2f3dcee`):** For the rare case where a completed Match's active Club goal has no reliable Tier-1 historical evidence (no saved Selection, no legitimate live-bench admission via `effective_selection()`), an authorised Coach may use an exceptional, evidence-backed pathway (`CompletedMatchGoalCorrectionService::verify_historical_scorer()`) instead of the normal Correct Match Record form. Candidate discovery is narrowly exact Event Audience **or** exact Event Attendance for that exact Match — discovery only, never automatic proof — and the Coach must supply the verified scorer, a verification source (Match footage / Club records / First-hand knowledge), an evidence note and explicit confirmation. Reuses the established void+append correction architecture and writes a distinct, transactional `match_goal_verified_historical_attribution` audit record. A valid attribution is Player-specific and provenance-specific: it credits the verified goal, one appearance and Match-history inclusion for that exact Player only, never fabricates starting/substitute status, minutes, Attendance, rating, POTM or an assist, never rewrites saved Selection or broadens `effective_selection()`, and Data Quality recognises the exception only for the exact active incident's scorer role. A downstream Player-specific-crediting regression (a non-scoring Player's own Match card briefly showing another Player's verified goal) was found in browser acceptance and fixed before final sign-off. Two further correctness fixes landed in the same arc: `historically_eligible_players()` (Correct Match Record / Add Missed Goal) now replays the historical pitch state against `effective_selection()` (Selection **plus** legitimate live-bench admissions) rather than the raw saved Selection alone, so a Player legitimately admitted and substituted on live is no longer invisible to historical eligibility (`2cbae72`); and Data Quality's recovery-action routing (Team/Player Statistics "Fix" links) is now a positive allowlist — a warning code only routes to Correct Match Record, Event Attendance or Match Report when that destination can genuinely act on it, rather than defaulting unmatched codes to Match Report regardless (`7d3caa0`). See `MASTER_DEVELOPER_GUIDE.md`'s "Verified Historical Scorer Attribution — Historical Eligibility Direction" and `SPRINTS.md` for full delivery detail, and "Historical Match Participation Evidence — Deferred Opportunities" below for what remains out of v1 scope.
- **Match Hero Goal-Scorer Presentation (CMC-003 — complete, `b37de1c`):** Club goal scorers now present beneath the Match score in familiar football-result style on both live Match Mode and completed-Match presentation. See "Match Hero Goal-Scorer Presentation (CMC-003)" above for full detail, including the live-eligibility correction and focused-action/half-width responsive polish delivered in the same arc.
- **Primary immersive module accent-top consolidation (complete, `54edcb2`/`5616f8b`):** the restrained club-accent top-edge treatment already established on Team Events/Attendance/Statistics is now also used by Match Mode's own cards, Match Recovery/Match Details, the main Events header and the Matchday Hub hero, via one reusable `.iexel-accent-top-module` primitive. See `MASTER_DEVELOPER_GUIDE.md`'s "Primary Immersive Module Accent Treatment". This is a restrained, within-family accent addition, not a redesign — the next bullet's principle is unaffected by it.
- **Coach Workspace Batch B — Statistics chooser, inline availability editing & return-to-context (complete, `a9c5dc7`):** a dedicated Statistics landing page for a Coach/Manager who manages more than one Team; the former standalone "Update player availability" dropdown is replaced by an inline per-Player editor directly inside the existing Team Responses list (same canonical write path, same eligibility source); and Event lifecycle actions/inline availability writes now return the Coach to the specific section they just acted on rather than the top of the page. See `SPRINTS.md`'s "Coach Workspace Batch B" section for full delivery detail.
- **Lineup Builder Mobile Hardening (MOB-005/MOB-006/MOB-007 — complete):** Lineup Builder unsubmitted drafts now persist reliably across navigation; direct player profile view links restored; bulk attendance race conditions eliminated; match status synchronization verified (`28264dc`, `bc5ab91`).
- **Unified Fixture Card Presentation & Heading Boundary Wrapping (MOB-009/MOB-010/MOB-011 — complete, `4e259f9`):** Football fixture cards are unified across Parent and Coach Team Hubs using `FixtureCardMatchup`. Large mobile fixture card headings wrap strictly at team boundaries, keeping opponent club names visually grouped.
- **Coach Bulk Event Response Management (CCH-001 — MVP Tier B):** Introduce rapid bulk availability response tools for upcoming training sessions and events in Coach Hub, distinct from the completed lineup builder bulk attendance tool.
- **Premium Squad Availability Presentation Polish (MVP Tier C):** Visual hierarchy and styling refinement for squad availability summary cards and response badges in the Coach Team Workspace.
- **Live Match transient success notice auto-dismiss (complete, `22a18fd`):** a live Match Mode success notice (Goal added, Substitution made, etc.) now clears itself after ~5 seconds; persistent error/warning notices are never affected, and the page remains fully correct if the script does not run. See `SPRINTS.md`'s "Live Match Transient Success Notice Auto-Dismiss" section.
- **Event Builder Productivity & Training Only Event Audience Eligibility (complete, `1c97ebb`):** optional End Time, safe non-Match Duplicate Event (including cross-Team destination re-authorisation and audience re-derivation) and weekly independent recurring Events are now available in the Team Event Builder. Separately, and more significantly for product direction: **Training Only Players can now be deliberately included in appropriate Event audiences** — both "Current Team + Same Age Group Players" and "Selected Players" surface a clearly separated Training Only candidate group, sourced entirely from the canonical Training Membership record (never a Team Assignment, which Training Only Players continue to have none of). League/Fixture competitive eligibility protections are unchanged and unweakened — Training Only candidates are excluded from the Fixture audience/selection path specifically, while a Coach may deliberately admit a Training Only Player to an appropriate Friendly (with the full downstream Match Selection/lineup/Live Match lifecycle then working normally for that legitimately-admitted Player). See "Fixture / Friendly / Tournament participation distinction" in `SPRINTS.md`'s "Event Builder Productivity & Training Only Event Audience Eligibility" section for the full, precise rule — this is a genuinely new, deliberately narrow product rule and should not be summarised as either "Training Only can never play Matches" or "Training Only is eligible for all Matches."
- Use the Coach dashboard as the reference pattern for Quick Actions placement (delivered across all persona dashboards).
- Do not redesign the immersive dark team and match workspaces merely to make every page identical.

### Front-end Player Profile Workspace — Player Profile A

**Status (updated 2026-08-14):** Implementation and LocalWP manual acceptance complete; pending intentional commit. The existing partial route `/club-os/teams/{TEAM_ID}/players/{PERSON_ID}/` was hardened rather than replaced, preserving Team Hub → Squad → View Player. It remains read-only and private/no-store/noindex.

**Team Staff Operational Access Reconciliation prerequisite (source complete; core LocalWP manual acceptance passed):** Assignment-driven account provisioning gives a linked active Coach, Manager or Assistant Coach the narrow existing `iexel_manage_assigned_team` capability when the active Person has at least one active staff assignment on an active Team and active TeamSeason in the current active Season. LocalWP acceptance proved Manager access to U7 GOLD, Coach access to U8 GOLD and denial for an unrelated Team without broad all-Team access. The capability remains only Layer A.

- Player Profile authorization now proves linked active actor identity, Coach operational experience, `iexel_manage_assigned_team`, exact active route Team, exact active current TeamSeason and exactly one qualifying active `coach`, `manager` or `assistant_coach` assignment. A linked active Club Admin may use the established `iexel_manage_club_os` override. Preview and ordinary Secretary/Parent/Player/Treasurer/Welfare/Committee access are denied; Secretary continues at `/club-os/secretary/people/{PERSON_ID}/`.
- The target must be an active Person with active Player identity and exactly one active Player assignment on that exact Team/current TeamSeason. Training Only, former, inactive, missing, registered-but-unassigned, stale and duplicate/corrupt targets fail closed.
- One immutable authorized scope feeds a unified Player Profile snapshot. The minimum identity projection contains name, Club ID, avatar/initials, derived age, age group, Team and Season; exact DOB never enters rendered HTML, client state or URLs. Current assignment and current-Season Registration status are read-only and minimal.
- Guardian contact is shown only for positively known youth Players and is limited to name, neutral relationship ordering and telephone. Adult and age-unknown guardian cards are omitted. Emergency contact reuses `EmergencyContactService` for the exact current Season and remains visually separate.
- Current Operational Medical & Safety uses a dedicated non-Season Person-level singleton (`player_operational_medical_safety`) and never falls back to historical Registration. Admin and active Secretary users with `iexel_manage_registrations` own the protected current-state editor. Authorized current-Team Coach, Manager and Assistant Coach users receive only the four bounded current fields read-only. Registration stays immutable; only allergies and medication may seed prospectively on the first exact transition to `registered` when no current row exists. `medical_notes` and `emergency_information` never seed, existing Players are not bulk backfilled, and an explicit all-empty current row remains authoritative so historical declarations cannot reappear.
- Welfare concern existence/data and Finance data are absolutely excluded. No medical data is added to lists, directories, statistics, attendance, communications, client storage, analytics or activity logs. Attendance, statistics and Player Journey expansion remain deferred to Player Profile B.

**LocalWP acceptance update (2026-08-14):** Assigned Coach and Manager access, the Assistant Coach assignment architecture, exact assigned-Team authorization, cross-Team denial, Training Only isolation and the complete Player Profile A read model passed manual acceptance. The Secretary current Medical & Safety workflow, explicitly empty state and assigned-Team Coach read-only projection also passed. Registration testing proved seeding occurred only at the final `registered` transition: allergies and medication seeded where appropriate, historical medical notes and emergency information did not, and an existing current row was not overwritten. The persisted Training Member Registration type remained authoritative through successful submission. Responsive Player Workspace acceptance passed at 600px, 390px and 360px, and the intended private/no-store/no-cache/noindex response headers were verified. The final pre-commit audit found no functional MVP blocker. The accumulated batch remains pending intentional commit.

**Current Operational Medical & Safety status (updated 2026-08-14):** Schema, migration registration, canonical repository/service, Secretary Person Profile card, focused server-rendered edit route, prospective Registration seed hook and current-only Player Profile projection are implementation complete and have passed LocalWP manual acceptance. The entity is not Season-specific and stores one current row per Person. Emergency Contact remains separate as who to contact; Welfare/safeguarding and Finance remain separate domains. Sensitive routes are private/no-store/no-cache/noindex, and audit events record metadata/changed field names only. Intentional commit is still pending.

### Parent Workspace

- Keep dashboard, registrations, events and announcements.
- **Selected-Child & All-Children Event Scoping (complete):** Parent selected-child scoping (OS-028), Player Preview scoping, and All-Children event child identity (avatars/initials, per-child status) with independent multi-child RSVP on Event Detail are fully delivered.
- **Parent Family Finance (complete):** Family Finance workspace, invoice detail experience, child attribution, and payment allocation history are fully delivered.
- **Parent Invoice Payment Currency Encoding Repair (MOB-001 — complete, `bf6df68`):** Corrected currency symbol encoding across payment settlement receipts, confirmation screens, and invoice cards so the proper `£` sign renders consistently.
- **Parent Team Hub Inline RSVP & Position Restoration (MOB-008 — complete, `fa72493`):** Upcoming fixture cards now include inline per-child RSVP controls with fragment targeting and session flash scroll restoration returning the user directly to the acted-upon fixture card.
- **Parent Event Detail RSVP Return Navigation (MOB-008A — MVP Tier A):** Extends return continuity to standalone Event Detail views so RSVP submissions return to Event Detail rather than redirecting to Team Hub → Events. (Implementation complete in plugin working tree; awaiting Product Owner acceptance).
- **Parent Event RSVP Action Copy Differentiation (PRN-001 — MVP Tier B):** Refine RSVP button copy to distinguish between responding on behalf of a child ("Available for [Child Name]") versus responding for oneself ("I'm Available").
- **Back My Game Supporter Visibility (BMG-001 — MVP Tier B):** Ensure linked children and teams display clear supporter agreement status, pledge amounts, and contribution links directly within the Parent Hub.
- **Team Hub text contrast (OS-029 — complete):** Resolved by the systemic dark-surface contrast treatment (commit `34cd5d4`, 2026-08-21); protected by `tools/validate-dark-surface-contrast.php`.
- Improve notification attachments with an in-app viewer/lightbox (Post-MVP).
- Post-MVP, evolve communications into richer posts, galleries, match reports and generated club content.

### Treasurer Workspace

- Keep the dedicated finance identity, payment recording, bulk family invoicing and billing schedules.
- **Treasurer Finance MVP (complete):** Invoice lifecycle management (draft, issue, cancel), payment recording & allocations, Fee Rules, and Discount Policies are fully delivered inside Club OS.
- **Billing/invoice dark-surface contrast (FIN-028 — complete):** Resolved by the systemic dark-surface contrast treatment (commit `34cd5d4`, 2026-08-21); protected by `tools/validate-dark-surface-contrast.php`. FIN-031 (static caret-cursor visual bug) is a separate item — not addressed here; a 2026-09-08 diagnostic (see the Consolidated review log) now positively classifies it as browser caret browsing rather than a Club OS defect, so no plugin fix is expected to be needed.
- **Treasurer Premium Workspace Alignment Batch 1 (FIN-032 — complete, Product Owner visual acceptance PASSED):** Finance's own presentation migrated onto the shared premium `.iexel-experience-hero`/`.iexel-experience-section`/`.iexel-experience-metrics` vocabulary already used elsewhere in Club OS, resolving the pale/generic feel identified by a read-only UX audit. Invoice Detail's own primary invoice record is a single, Product-Owner-directed exception, keeping the existing dark `.iexel-os-card` treatment while its four supporting sections use the light register; a light-surface secondary-action readability defect this exposed was also corrected. See "Treasurer Premium Workspace Alignment Batch 1" below and `SPRINTS.md` for full delivery detail. **Finance remains a premium light administrative workspace — this is not an immersive-dark redesign.**
- **Finance Reports phantom-route cleanup (FIN-033 — complete):** `finance-reports` was an unfinished scaffold dating from the original Treasurer Finance implementation — route registration and title/intro metadata with no dispatcher case, renderer or service ever built, and never linked from Finance navigation. A dedicated read-only audit reclassified this as an unfinished scaffold rather than a fixable routing defect (not a regression, no product scope ever defined), and the phantom scaffold has been removed rather than completed (`fbfc032`). See "Finance Reports Phantom Route Cleanup Batch 1" below and `SPRINTS.md` for full delivery detail. **A genuine Finance Reports capability is not implemented and remains future product-definition work — do not describe it as an outstanding routing fix or a partially completed Reports page.**
- Post-MVP, add reporting, exports, reconciliation and payment integrations.

### Player Workspace

- Reframe the workspace around motivation, progress, achievement and belonging.
- **Player My Stats (PL-022 — complete):** Dedicated standalone `/club-os/player/stats/` page delivered in Batch IN3F16-PL1C with Appearances, Goals, Assists, Player of the Match, Attendance rate, Clean Sheets (GK), Season Story, and Recent Match Contributions, backed by child-safe privacy rules (excluding negative labels, match ratings, and starts/substitute breakdowns).
- **Player Match-by-Match Breakdown (PL-026 — MVP Tier C):** Expandable match-by-match breakdown under season aggregates, allowing players to review contributions per fixture.
- **Player My Progress Match Report Deep Links (PL-027 — MVP Tier C):** Direct links from milestones, appearances, and progress entries into completed Match Reports.
- **Youth Purchasing & Commercial Safeguarding (YTH-001/002/003 — MVP Tier A):**
  - Club Shop: Youth players under 18 must not execute direct hosted credit/debit card checkout without adult guardian authentication.
  - Spot the Ball: Youth entry requires adult guardian authorization; minor winnings route strictly to linked adult guardians.
  - Fundraising Appeals: Public sharing links attributing youth players require adult guardian issuance; no public child seller profiles or URLs.
- **Player My Season Journey & Milestones (PL-021 — complete):** Expanded `PlayerMySeasonCard` delivered in Batch IN3F17-PL2B2 with Season Journey progress, completed milestone badges, dynamic Next Milestone targets, and attendance rate context.
- **Player Quick Actions (PL-023 — complete):** Rendered directly below the hero card via `PortalDashboardLayout`.
- **Player Statistics dark-surface contrast (PL-024 — complete):** Resolved by the systemic dark-surface contrast treatment (commit `34cd5d4`, 2026-08-21); protected by `tools/validate-dark-surface-contrast.php`.
- **Player Progress canonical MVP journey (PL-025 — complete, confirmed Product Owner decision):** Player Progress remains an embedded Player-specific Team Workspace experience — Player Home → Team Workspace → My Progress. Player global navigation stays deliberately simplified (Home, Team, Events, News); Player Progress is **not** a fifth global navigation item, and the Player Home Progress card links through the authorised Team Workspace My Progress destination via the existing canonical Team/Member Experience projection. Player self-scope and Parent Preview exact-child scope remain authoritative. Standalone infrastructure (`/club-os/player/progress/`, `/club-os/parent/progress/`, `PlayerProgressUrl`) remains in the repository as unfinished/alternate infrastructure, not the primary journey; a future Post-MVP bounded decision will confirm whether to retain it as a documented alternate entry point or deprecate it.
- Post-MVP, add rewards, XP, coach pointers, league tables, development journeys and team challenges.
- **Player Communications & Safeguarding Roadmap:**
  - Player Messages / Club News is part of the intended Player Experience; activation is gated by safeguarding controls.
  - Youth players may receive appropriate Club OS communications with linked guardian visibility/oversight supported.
  - Adult/senior players receive normal player communications without inheriting youth guardian rules.
  - Retain one canonical `Player` role with age/safeguarding classification beneath it (`Known Youth`, `Known Adult`, `Age Unknown`).
  - `Age Unknown` receives safeguarding-restricted behaviour until DOB/classification is resolved.
  - Club OS Communications are recipient-neutral and reusable across authorized experiences.
  - Support for adult/senior players and grassroots/semi-pro adult clubs remains part of long-term product direction.

### Admin Experience

- Keep admin focused on platform maintenance, system configuration, database lifecycle, and technical recovery.
- **Admin Navigation Consolidation (ADM-001 / ADM-002 / ADM-003 — complete):** Delivered `c88eab9` (2026-08-21), "consolidate admin navigation and restore contextual creation actions". `AdminUI::register_menu()` now registers 19 visible sidebar destinations grouped into logical clusters (Platform/Dashboard; People & Football Operations; Seasons & Registrations; Finance, Communications & Projects; Welfare & Safeguarding; System & Settings) and 36 hidden route-only destinations (`add_submenu_page(null, ...)`), with every admin slug/route preserved. Route-only action and detail pages (`Add Person`, `Add Team`, `Add Event`, `Add Venue`, `Add Season`, `New Registration`, `Add Club Project`, etc.) remain reachable through in-page contextual creation actions restored on `PeoplePage`, `TeamsPage`, `EventsPage`, `VenuesPage` and pre-existing admin-navigation components elsewhere. The operational Committee Dashboard duplicate is hidden from the sidebar; the portal remains the canonical home for that experience. Zero schema or database changes. The focused validator `tools/validate-admin-navigation-consolidation.php` passes 227/227 checks.
- **WordPress Admin Fundraising Menu Cleanup (ADM-005 — MVP Tier B):** The `/wp-admin/admin.php?page=iexel-club-os-fundraising` menu entry currently renders a blank admin screen. Investigate whether this represents an incomplete admin dispatcher/view or a redundant menu entry that should be retired in favour of the canonical portal routes (`/club-os/fundraising/` and `/club-os/secretary/fundraising/`).
- **Permanent Technical Support & Recovery Access Invariant (ADM-006 — MVP Tier A):** While daily club operations progressively shift to the portal, `/wp-admin/` remains permanently accessible and supported for system administrators. Technical support, database upgrades (`UpgradeRunner`), diagnostic tools, recovery utilities, and plugin lifecycle management must never be removed or disabled from WordPress Admin.
- **Post-MVP Admin Evolution:** Separate WordPress administrator power from automatic access to sensitive operational data (ADM-004), and complete the progressive migration of club operations away from `/wp-admin/`.

### Settings and Brand Studio

- **Separate Operational Settings from Brand Studio for MVP (SET-001 — MVP Tier B):** The current settings screen is primarily Brand Studio (crests, colors, accent tokens, logos). Separate operational configuration (season dates, age group policies, official club contacts) into a dedicated, clean operational settings tab for MVP, keeping Brand Studio focused purely on visual identity.
- **Post-MVP Modular Settings Architecture (SET-003 / SET-004 — Post-MVP Tier D):** Broader modular multi-club profile architectures (Club, System, and Experience settings separation, with presets for Grassroots, Academy, Semi-Pro, Professional, and Custom) are explicitly preserved as Post-MVP.
- Post-MVP, add image movement, crop, zoom and focal-point controls (SET-002).

### Secretary Workspace Operational Review

- **Secretary Command Centre (complete):** People, Teams, Registrations, Venues, Events, Portal Accounts, and Shop Fulfilment console (`/club-os/secretary/shop/orders/`) are operational.
- **Create Event Specific People Modal Mobile Overflow (SEC-009 — MVP Tier B):** Resolve horizontal overflow and wrapping issues in the "Specific People" selector modal on narrow mobile screens (320px–390px), ensuring checkboxes and person labels remain fully accessible on mobile devices.
- **Recurring Events:** Weekly independent recurring events delivered in `1c97ebb`. Complex multi-week repeat planning and calendar synchronization remain Post-MVP.

### Registration Integrity — Secretary Operational Direction

**Guided Registration Conflict Resolution and Legacy Staff Registration Recovery: COMPLETE / ACCEPTED / MERGED ON MAIN (2026-09-29).** Current plugin baseline is `55ee697c796dbde93e481b45b5809422d7f3be0a`; conflict delivery is `e303ca96234c8c2530aae776ea55914d3a5dc02d`.

The two workflows address distinct fail-closed conditions within the Person-first architecture:

- **Duplicate active Person + Season + pathway journeys:** Secretary discovers and compares the conflict, deliberately selects a survivor, supplies a bounded reason and confirms. Transactional stale/locking/audit protection leaves the survivor unchanged and retains the duplicate as Withdrawn history; information and commercial snapshots are never merged. Desktop and mobile comparison/detail navigation and disposable resolution were accepted.
- **Historical unlinked Secretary Draft:** A narrowly eligible New Player Draft at Step 1 is deliberately linked to an existing active Player after legacy/canonical comparison, reason/confirmation and locked stale/collision revalidation. The same Registration resumes as Returning Player, identity normalized FROM Person, with mandatory audit and no Person/Finance/commercial mutation. Desktop and 320px search/comparison, centered heading, autogrow reason and successful browser recovery were accepted. Unsupported shapes fail closed; recovery cannot bypass duplicate-journey detection.

Staff name/DOB remain locked; identity correction belongs in authorized People. No alternate Person-creation or generic migration tool was introduced. Zayne #558 is protected historical evidence: at investigation no plausible canonical Player was found, and recovery is not claimed. Verify/create the genuine Player through People if genuinely absent before deliberate eligible recovery. Henry #304/#305 intentionally remain unresolved reference data. Canonical rules are in the Master Developer Guide; delivery/validation evidence is in `SPRINTS.md`.

### Training Membership pathway roadmap

**Batch 2C accepted status (updated 2026-08-14):** Implementation and LocalWP manual acceptance are complete. Secretary People surfaces derive current Training Only status from active current-Season TrainingMemberships; a dedicated Training Members directory/detail supports operational filters and lifecycle management; and youth creation routes immediately into the existing Guardian Links workflow. Acceptance covered the Registration lifecycle from Draft through Registered, with Training Only remaining competitively isolated until the explicit Registered-only handoff. The reciprocal transitions preserved the same Player Person, Registration and historical Team Assignment records; current People, Secretary Team roster and Coach squad projections changed only with active participation state. Duplicate active participation and Training Member Registration type changes remained blocked. Training Members mobile filters and focused closeout validation also passed. No Batch 2C MVP blocker remains. Coach/Manager Training Only visibility remains **NOT CURRENTLY VISIBLE** because authorised Coach surfaces are Team Assignment/Event-audience based. *(This was accurate as of 2026-08-14. It is now superseded — see "Event Builder Productivity & Training Only Event Audience Eligibility" in the Coach Workspace section below and `SPRINTS.md`: Event-audience surfaces are the mechanism by which Training Only Players are now made deliberately visible to authorised Coaches, not a limitation. Team Assignment remains, unchanged, not applicable to Training Only Players at all.)*

**Batch 2D-A accepted status (2026-08-12):** The atomic Match Player → Training Only transition and Match Event ownership repair are implemented and have passed LocalWP manual acceptance. The Secretary Person Profile uses one transaction to revalidate the active Person, retained Player role, current Season, every active competitive Player assignment, Team/TeamSeason chains, TrainingMembership state and saved Match selections; it then ends every target-Season assignment and starts the canonical TrainingMembership. The Player role, linked account, Registration, Guardian/family relationships, Finance, historical assignments and historical Match/statistics records remain unchanged. Saved not-started lineups block until the Player is removed, live Matches require a terminal state, and terminal history does not block. Fixture/Friendly ownership is canonical through Event `team_id`, `season_id` and `team_season_id`; malformed scheduled Matches are repairable through the Secretary UI only after Match-state and saved-lineup compatibility checks, with the audience rebuilt from the exact TeamSeason roster. Current self Player Experience ceases naturally when no active competitive assignment remains. Historical-only Player Experience and Parent Preview changes remain incomplete and explicitly deferred.

**Batch 2D-B1 accepted status (2026-08-13):** Final acceptance passed and the implementation is merged on `main`. The reciprocal Secretary-controlled participation transitions preserve canonical Player identity, enforce Training Only/competitive assignment exclusivity, and require exactly one current `registered` Registration for Training → Match Player. Current/historical roster and statistics presentation and the responsive Training Members mobile filters also passed acceptance.

**Batch 2D-B2 accepted status (2026-08-13):** Implementation and LocalWP happy-path manual acceptance are complete, and the batch is merged on `main`. Training Member detail resolves the canonical current-Season Registration state and starts, resumes or views the existing Registration lifecycle without creating a parallel form. New drafts reuse the existing Person and current TrainingMembership Season, preserve terminal history, fail closed on contradictory active rows and return to the Training Member for the B1 competitive handoff once Registered. Acceptance verified that one existing Person progressed through Draft, Submitted and Registered into one compatible current Team Assignment while retaining the Registration, family links and historical Training Membership, with one current Team Hub roster entry. No account, Finance or Event mutation is introduced.

Training Membership is the one canonical representation of Training Only participation. `Player` is the canonical football-participant Person identity, not competitive eligibility. Training Only is Player + active current TrainingMembership + no active competitive Player Team Assignment; Match Player requires a valid current competitive assignment and the applicable Registration state. Youth uses an explicit supported TeamSeason U-group, while DOB-classified adults use the schema-compatible `senior` key. Player role alone must not create account access, Registration, Team assignment, Event audience, lineup or Match eligibility.

- **2B — Prospect → Training Only:** Manual acceptance passed under the prior identity model. Batch 2D-B1 now ensures canonical Player identity during the same atomic conversion while retaining Training-only participation: no Team Assignment, Registration, account or Match eligibility is created.
- **2C — Training Membership Visibility & Secretary Management:** Implementation and LocalWP manual acceptance complete. Secretary visibility, direct Player-identity Training creation, re-entry and end/archive management use the canonical TrainingMembership domain. Registered-only reciprocal transitions preserve Person, Registration and historical assignment identity while current roster and squad projections follow active participation. Coach/Manager visibility remains assignment-based and was not broadened. No Batch 2C MVP blocker remains.
- **2D-A — Atomic Match Player → Training Only Transition:** Implemented; LocalWP manual acceptance passed; pending commit. All current-Season competitive Player assignments end with canonical history-preserving lifecycle semantics, one active TrainingMembership starts through the transaction-safe domain boundary, and non-terminal saved lineups fail closed. Player role, account and Registration are retained. The accepted Match Event ownership repair prevents Team-less Fixtures/Friendlies and safely repairs malformed scheduled Match ownership without rewriting completed history.
- **2D-B1 — Registered-only Training Only → Match Player:** Final acceptance passed; merged on `main`. The Secretary Training Member detail requires exactly one current Person-linked `registered` Registration and a compatible active current TeamSeason, defensively ensures Player identity, creates a new regular active Player assignment episode, ends the TrainingMembership and writes one safe orchestration event in one transaction. Registration, account, family, Finance, Event audiences and history remain unchanged.
- **2D-B2 — Secretary-native Registration setup:** Final acceptance passed; merged on `main`. The Training Member workspace owns the safe entry into the canonical Registration wizard for the existing Player/current Season, with state-based resume/view behavior and a Registered handoff back to B1. No duplicate Person, account, Finance or Event side effects; the accepted B1 handoff creates one canonical current Team Assignment and preserves Training Membership history.
- **Historical experience:** Not implemented. Historical-only former Player Experience, Parent Preview policy changes and a new Training Member portal remain separate future work.

The three Training Only entry paths—Prospect conversion, Secretary direct creation and an existing Match Player transition—must converge on the same TrainingMembership service/domain. Training Only is not a mandatory step before Match Player: a later bounded pathway may invite a Prospect directly into competitive registration and assignment.

Post-MVP planning retains Taster/Trial invitations, Secretary communications to the Prospect contact, configurable Secretary/reply-to addressing and eventual role-authorized club mailbox integration. These communication capabilities are not Operational MVP blockers and must continue to reuse the channel-neutral Communications architecture.

### Prospect Trial Period / Come and Try — completed

The public Come and Try enquiry and pre-membership Trialist journey are complete, Product Owner accepted and committed on plugin `main` at `e5426be1741e207cdc3ac56f86cf1fbaa55a49c3`. Public youth participation and responsible-adult authority are recorded at Prospect level. Secretary can schedule and review repeated dated sessions; assigned-Team Coaches/Managers see ready Trialists, relevant bounded safety information and can record attendance with a brief operational note. Session history remains with the Prospect through deliberate conversion to canonical Training Only membership. The conversion form recommends the natural football age group and offers only the existing service-permitted one-year-up alternative. See `SPRINTS.md` for acceptance and validation evidence.

Temporary Trialists are not canonical Players, Team Assignments or Event attendees. Conversion to Training Only does not itself grant competitive Registration, Finance or fixture eligibility, and Prospect-level trial permission is not unrestricted ongoing consent. The **integration of Prospect trial sessions with existing Team training sessions remains deferred**; no Event-attendance bridge was delivered. **Multi-club public-page branding remains future work**; the accepted public page uses the current club brand. The direct Prospect-to-competitive Match Registration invitation is also still a separate open seam.

## Newly confirmed product follow-ups

### Venue & Address Finder / Recent Grounds

**Status:** Future Product Candidate / Post-MVP Enhancement.

**Product Objective:** Make event and fixture creation significantly more convenient for club volunteers.

The intended experience is similar in convenience to Spond-style place/address search:
- As the user types a venue or ground address, Club OS offers structured real-place suggestions.
- Selecting a result automatically populates structured fields: Venue Name, Address, and Postcode.
- Manual text entry must always remain first-class and fully functional.

#### Recent and Frequently Used Venues
The design supports convenient reuse of:
- Recent Venues
- Frequently Used Grounds
- Repeat opposition/away grounds

**Architectural Principle:** Do *not* automatically promote every temporary or away ground into the canonical Club Venue directory. Maintain a clear distinction between:
1. **Club Venues:** Formally managed, reusable home/training/club facilities in `wp_iexel_os_venues`.
2. **Recent / Frequently Used Event Venues:** Lightweight convenience history for one-off, away, and neutral match locations.

#### Architecture Direction
Future implementation should use a reusable place-search provider boundary (`VenueSearchProvider` interface) rather than tightly coupling Event forms to a single mapping vendor:
- Provider abstraction for place lookups and geocoding.
- Structured result mapping into canonical event venue fields.
- Privacy and data minimisation for typed queries sent to external APIs.
- Graceful offline/network-failure fallback where manual entry remains seamlessly available.
- No maps provider is selected or integrated in MVP.

### Events Card Consistency

**Status:** Complete (`5616f8b`, building on already-delivered event-card work). The general `/club-os/events/` page (`EventsWorkspace`/`EventCard`) already carried the established Team Events midnight-blue visual language and club-accent top trim on its individual event cards before this reconciliation; a read-only design-system audit found the one remaining inconsistency was the page's own top-level header (`.iexel-events-workspace-header`), which still used a legacy accent left rail. The header now uses the same reusable primary-module accent-top treatment as the cards below it (see `MASTER_DEVELOPER_GUIDE.md`'s "Primary Immersive Module Accent Treatment"), without duplicating football-specific fields — the general Events page still serves club-wide non-football events (Meetings, Socials) unchanged. The main Events workspace is intentionally shared across every portal persona (Parent, Player, Coach, Secretary, Treasurer, Welfare, Committee), so this header treatment has deliberate multi-role reach, not a permissions/workspace leak.

### Venue Control Presentation

**Status:** Complete (`e796f19`, "fix: polish coach workspace release readiness").

The Event Builder venue-selection radio and control presentation appeared visually basic during SEC-008 browser acceptance. `TeamEventForm.php`'s Venue Type radios now use the same card-row visual language already established for the Audience Mode radios (`.iexel-team-venue-modes`/`.iexel-team-venue-mode`, mirroring `.iexel-team-audience-mode`) rather than bare unstyled labels. See `SPRINTS.md`'s "Coach Workspace Release-Readiness Polish" section.

### Training Meet / Arrive Time Policy

**Status:** Confirmed Product Decision.

Optional **Meet / Arrive Time is intentionally supported for Training** events. This supersedes any earlier handover statement suggesting Meet / Arrive Time should be hidden for training sessions. Grassroots clubs routinely require players to arrive before training commences for preparation, warmup, or administrative checks.

### Match Hero Goal-Scorer Presentation (CMC-003)

**Status:** Complete (`b37de1c`, plus responsive/eligibility follow-up below). Delivered on live Match Mode and completed-Match presentation alike, sourced from `MatchGoalScorersCard` against canonical active Match goal incidents only (no second scorer data store), reused unmodified by both the Coach-facing `MatchModeScoreCard` and the privacy-minimised participant Match Story. Ordinary Correct Match Record corrections and Verified Historical Scorer Attribution (CMC-002) both flow through automatically. Voided/superseded incidents are excluded; same-Player multiple goals consolidate naturally (`David Adel 12′, 48′`); opponent scorer identities are never invented; football terminology is used throughout. See `SPRINTS.md`'s "Match Hero Goal-Scorer Presentation (CMC-003)" section for full delivery detail.

**Product Objective (delivered):** Present Club goal scorers beneath the Match score in familiar football-result style, so a Match reads the way football fans naturally expect:

```
U7 GOLD 3–2 GURU NANAK

David Adel 12′, 48′
Jude Kane 37′
```

**Follow-on work completed in the same arc (see SPRINTS.md for commits):**
- **Live attribution eligibility correction:** browser acceptance surfaced that a legitimate on-pitch Player with no Attendance row was silently excluded from the Goal Scorer/Assist candidate list — not a CMC-003 regression, but a pre-existing rule that on-pitch state alone should govern live attribution. Fixed so a missing Attendance row no longer disqualifies an on-pitch Player, while an *explicit* negative Attendance status still does, and Available Bench Players remain ineligible until legitimately admitted/substituted on.
- **Focused-action and half-width responsive polish:** the Goal Attribution focused-action score card no longer stretches vertically merely to match a taller adjacent form; Team names now scale relative to the card/container's own width (a container-query-based resilient clamp) rather than the viewport, fixing character-by-character breaks in narrow half-width layouts; the scorer/minute list switches to one-entry-per-line below a safe card width so a Player name and minute never separate.
- Preserves the premium midnight-blue Club OS design system and the runtime club-accent token throughout (see `MASTER_DEVELOPER_GUIDE.md`'s "Primary Immersive Module Accent Treatment") — never a hardcoded colour.

### Guardian Link Role Synchronisation Audit

**Status: Complete.** The audit ran, its findings were confirmed, and the approved correction was implemented as **Post-RC Guardian Link Alignment Batch 1** (plugin `main` `29220cc0d6be03085c5096bf6bbe3af044d01741`, "fix: align guardian relationship role handling") — see `SPRINTS.md`'s "Post-RC Guardian Link Alignment Batch 1" section for full delivery detail and `development/DEVELOPMENT_HANDOVER_2026-09-09B.md` for the current resume point. This was post-RC follow-up work, completed after Product Owner manual sign-off on the MVP Release Candidate; it did not reopen or affect the RC-01 → RC-03-CLOSE validation cycle.

**Observed current/manual workflow (pre-Batch-1):** when manually linking a Person to a Player as Parent/Guardian via the Secretary's Guardian Links page, the operator needed to give that Person the Parent/Guardian role *first* before they became selectable in the workflow.

**Confirmed final behaviour:**
1. An otherwise-valid active adult Person can be selected in Secretary Guardian Links without first manually assigning a Parent/Guardian role.
2. Creating the `parent_of` relationship transactionally ensures an active `parent` role; creating `guardian_of` ensures active `guardian` — as a consequence of the already-authorised relationship write, in the same transaction, idempotently, preserving any unrelated existing roles.
3. **Treasurer is intentionally different.** A pure Treasurer does not hold the Secretary-specific `iexel_manage_person_roles` capability, so Treasurer's family/Finance relationship management must never grant or "top-up" a Parent/Guardian role. Under Treasurer policy, the adult must already hold the role matching the requested relationship type; a zero-role adult, and the pre-existing incidental cross-role top-up, are both now rejected server-side — enforced in the relationship service itself, not merely by candidate-picker filtering. Treasurer's candidate population remains role-filtered; only the eligibility probe's own relationship-type check was corrected, so already-valid parent-only/guardian-only candidates are no longer hidden by accident.
4. RELATIONSHIP and ROLE remain distinct domain concepts throughout — the relationship answers "which child/Player is this adult linked to?"; the role answers "which operational/persona identity does this Person hold?" A canonical family-link workflow may ensure the corresponding role as a consequence of relationship creation only where the originating policy is authorised to do so. See `development/MASTER_DEVELOPER_GUIDE.md`'s "Family Relationship Role Consequences" durable rule.
5. **Corrected characterisation of Registration and Prospect** (the original audit overstated both): normal current Registration matching/validation and Prospect guardian matching already prevent/require the role through their own existing gates in the supported workflow. The Batch-1 role-ensures added to both are defense-in-depth / canonical-invariant protection — not fixes for a currently user-reachable roleless-adult bypass, and for Prospect specifically, effectively a no-op for a currently matched existing guardian.

**Do not restart or re-scope this work.** Any further family/guardian enhancement (e.g. automatic role removal on unlink, which remains deliberately unchanged) is separately prioritised future work, not an open item from this audit.

### Treasurer Premium Workspace Alignment Batch 1

**Status: Complete. Product Owner visual acceptance PASSED.** A read-only Treasurer/Finance UX audit, then a single approved implementation batch (plugin `main` `840369102b5b1d24f7701c7d2af3b325971fa824`, "fix: align treasurer finance workspace") — see `SPRINTS.md`'s "Treasurer Premium Workspace Alignment Batch 1" section for full delivery detail and `development/DEVELOPMENT_HANDOVER_2026-09-09C.md` for the current resume point. This is post-RC follow-up work; it does not reopen the RC cycle or Guardian Link Alignment Batch 1 above.

**Accepted surfaces:** Finance Overview, Invoices, Invoice Detail, Billing Schedules, Treasurer Dashboard, and 320px Invoice Detail.

**Accepted design direction:**
1. Finance is a premium **light** administrative workspace — rich midnight/navy operational surfaces are used deliberately and sparingly, with a restrained runtime club-accent treatment (never a hardcoded literal colour), not as an immersive dark redesign.
2. Finance's page framing and its KPI/summary tiles use the same shared `.iexel-experience-hero`/`.iexel-experience-section`/`.iexel-experience-metrics`/`.iexel-experience-metric` vocabulary as Secretary, Welfare and Treasurer's own People/Team/Registration pages.
3. **Invoice Detail's own primary invoice record is the one deliberate exception:** it keeps the existing dark `.iexel-os-card` treatment as the workspace's single authoritative record, while its four supporting sections (Itemised Charges & Discounts, Payment Allocations, Invoice Timeline, Invoice Notes) use the light register. Light KPI cards remain intentionally subordinate financial summary tiles throughout, including nested inside that one dark record.
4. A light-surface secondary-action readability defect (`.iexel-button-secondary`, dark-native, rendering white-on-near-white on Finance's newly-light surfaces) was found and corrected by reusing the existing `iexel-fee-rule-back` component rather than a new treatment.
5. Narrow-screen (320px) responsive behaviour is accepted, with no page-level horizontal overflow introduced.

See `SPRINTS.md`'s "Treasurer Premium Workspace Alignment Batch 1" section for the full mid-batch discovery narrative (the `.iexel-os-card`/`design-system.css` cascade correction), the validation table, and the deferred items below.

**Deferred, not part of this batch:**
- **Finance Reports route defect (FIN-033) — status changed, see "Finance Reports Phantom Route Cleanup Batch 1" below.** At the time of this batch, `finance-reports` was registered but not dispatched, falling through to Finance Overview content, and was recorded here as the recommended next small functional Finance batch. **A subsequent dedicated audit reclassified this as an unfinished scaffold rather than a fixable routing defect, and the phantom scaffold has since been removed. Do not continue to describe this as open or as the recommended next Finance batch.**
- **`iexel-fee-rule-back` naming debt** — the reused secondary-action component's name is narrower than its actual reuse. Naming/architecture debt only; the visual treatment is accepted.
- **Premium Surface Colour Consistency Audit** — a broader future audit, not started. It must distinguish intentionally light subordinate cards from surfaces genuinely inconsistent with the established premium hierarchy, and must preserve immersive Team/Coach/Match Mode dark treatment where that is the correct, already-accepted design — it is not "make every pale card dark" or "make every Club OS page identical."

**Do not restart or re-scope this work.** Do not describe Finance as an immersive dark workspace, and do not extend the Invoice Detail dark-record exception to any other Finance surface without a fresh, explicit Product Owner decision.

### Finance Reports Phantom Route Cleanup Batch 1

**Status: Complete.** A dedicated read-only trace audit, then a single approved cleanup batch (plugin `main` `fbfc032fa286b2d227c085c369a02b8a9cd837f1`, "fix: remove phantom finance reports route") — see `SPRINTS.md`'s "Finance Reports Phantom Route Cleanup Batch 1" section for full delivery detail and `development/DEVELOPMENT_HANDOVER_2026-09-09D.md` for the current resume point. This is post-RC follow-up work; it does not reopen the RC cycle, Guardian Link Alignment Batch 1, or Treasurer Premium Workspace Alignment Batch 1 above.

**Corrected characterisation:** `finance-reports` was previously described (above, and in earlier documentation) as an open routing defect — registered, but missing a dispatcher case. The audit found this was incomplete: `finance-reports` had **never** had a dispatcher case, a Reports renderer, or a Reports service/read model, at any point since the original Treasurer Finance implementation — confirmed via git history on the introducing commit. It was an unfinished public-facing scaffold, not a regression, and no Finance Reports product scope had ever been defined anywhere in source or documentation.

**Product decision:** the phantom scaffold has been **removed**, not completed. Club OS should not expose a public route implying a Finance Reports feature that does not yet exist. `/club-os/finance/reports/` now returns the same established "unknown Club OS route" behaviour (HTTP 404) as any other nonexistent path — no Finance Reports hero, no Finance Overview masquerading as Reports, no invented redirect, no placeholder.

**A genuine Finance Reports capability is not implemented and is not scoped by this cleanup.** It is now future product-definition work: before any implementation, it needs an explicit Product Owner decision on what Treasurer questions/reports the feature should serve. Do not infer report types, filters or exports from the retired title/intro copy, and do not describe this cleanup as a partially completed Reports page or as an RC blocker.

**Do not restart or re-scope this work.** Do not reintroduce the `finance-reports` route/metadata without a genuine, product-defined Reports implementation behind it.

## Historical Match Participation Evidence — Deferred Opportunities

**Status:** Post-v1 / Deferred. None of the following are current v1 commitments; do not implement or scaffold any of them without a separate, dedicated approval.

Verified Historical Scorer Attribution v1 (CMC-002) deliberately keeps verified attribution Player-specific and provenance-specific rather than broadening `effective_selection()`. The following opportunities were identified during that work and are recorded here so they are not lost, not so they can be started:

### 1. Verified Historical Appearance

A future authorised-Coach pathway to verify that a Player genuinely participated in a historical Match even where Club OS has no saved Selection, no legitimate live-bench admission, no goal, no assist, and no POTM/rating — recovering a truthful historical appearance/Match-history record without inventing a Match incident. Likely future principles mirror CMC-002: explicit authorised verification, constrained historical candidate discovery, verification source, evidence note, explicit confirmation, auditable provenance, Player + Event specific, no current-roster fallback. Should eventually support appearance and Match history only — never a fabricated goal, assist, starter/substitute status, minutes, Attendance, rating or POTM.

### 2. Verified Historical Assist Attribution

CMC-002 is scorer-only. A corresponding verified historical assist pathway is deferred and should reuse appropriate safety/audit principles when eventually designed — its eligibility semantics should not be assumed identical to the scorer pathway without a future dedicated audit.

### 3. Historical Registration as candidate evidence

Season/age-group Registration history may eventually help identify historically plausible Players where exact Event Audience/Attendance evidence is unavailable. Registration must **not** be treated as reliable historical evidence until the repository/data model is audited for genuinely effective historical registration by Season, age group and relevant Match date. Even if later approved, Registration should initially be candidate-discovery evidence only, never automatic proof of participation.

### 4. Reliable effective-dated Team-assignment history

Current Team-assignment history is not sufficiently reliable for historical eligibility decisions. A read-only audit conducted during CMC-002 found `team_assignments.joined_on`/`left_on` unreliable in practice (three materially different write paths; a confirmed real-data counter-example of a `joined_on` date recorded 13 days after a Match the same Person is independently evidenced to have attended). Future work should establish a trustworthy effective-dated Team-membership history before Team assignments can be used as historical evidence. Do not imply that "ever assigned to this Team" proves Match-date eligibility.

### 5. Longer-term historical-participation evidence model

An architectural direction, not an immediate refactor: Club OS may eventually benefit from a coherent historical-participation evidence model that distinguishes the evidential strength of saved Match Selection, legitimate live-bench admission, explicitly verified scorer attribution, a future verified assist attribution, a future verified historical appearance, and potentially-reliable effective-dated Registration/Team membership once those are separately audited. Do not refactor toward this now — CMC-002's v1 architecture deliberately keeps verified attribution Player-specific and provenance-specific rather than broadening `effective_selection()`.

## Product principles

1. **Volunteer Administrative Efficiency:** Club OS must reduce repetitive administrative effort for club volunteers while preserving explicit user control.
2. **Purpose-Built Football Convenience:** Convenience features such as venue search, structured autofill, and recent ground reuse are commercially valuable because they make routine football administration fast and effortless, helping the product feel purpose-built for grassroots football rather than like generic management software.
3. **Canonical Identity & Boundaries:** Administrative authority never creates member identity; operational queues belong to their respective role workspaces (e.g. Secretary Command Centre owns registration review; Committee retains executive oversight).

## Recommended next implementation batch

**ADM-001 / ADM-002 / ADM-003 (Admin Sidebar Navigation Consolidation & Route Cleanup) is complete** — see the Admin Experience section above.

**OS-029, FIN-028 and PL-024 (blue-on-blue dark-surface text contrast) are also complete.** A read-only MVP / Release Readiness reconciliation audit confirmed all three were resolved by commit `34cd5d4` ("Fix dark-surface finance contrast and visual hierarchy", 2026-08-21) — the same day as the ADM commit — through a systemic on-dark foreground-token treatment covering Team Workspace/Team Hub, Finance/billing/invoice and Player Statistics dark surfaces. `tools/validate-dark-surface-contrast.php` currently passes 6390/6390 checks protecting this treatment. Both discoveries follow the same pattern: real, dated, validated work that this roadmap had not yet caught up to.

**No unresolved High/MVP implementation defect is currently known.** The same audit confirmed Release Readiness currently reports **Ready** (22 checks: 17 Pass, 1 Review, 4 External, 0 Fail, zero required-and-unresolved risks), and found no other open roadmap item at High priority within MVP scope. This does not mean Club OS is "finished" — it means no currently-known High/MVP blocker remains after source reconciliation, and **Club OS remains suitable for continued Internal Club Testing.**

The only items the roadmap still shows open within MVP scope are **FIN-031** and **OS-011**:

- **FIN-031** (Low priority, static caret-cursor visual bug) was first re-verified against current source by a read-only audit (2026-08-26) and **could not be reproduced in current source** — no Finance/Treasurer static summary currently uses `cursor: text` or another confirmed input-like affordance, and the Treasurer/Finance surface has been substantially rebuilt since this finding was originally recorded, with no specific fix commit identifiable. A second, independent, more targeted diagnostic (2026-09-08), investigating the same reported symptom against the analogous static Secretary Command Centre heading, went further and **positively confirmed the cause is browser caret browsing** — plain non-`contenteditable` markup, `isContentEditable === false` at every ancestor, `document.designMode === "off"`, and zero `contenteditable`/`caret-color`/`designMode`/`execCommand` usage anywhere in plugin source. This is no longer merely "not reproducible" — it is now classified as **not a Club OS implementation defect**, pending only a Product Owner confirmation that this matches what they observed. No plugin workaround (CSS/JS selection suppression) was applied or is warranted.
- **OS-011** (Medium priority/Polish, Welfare concern-detail hierarchy) **was independently confirmed still present**, with no safeguarding or capability impact — the portal Welfare Concern Detail page still renders its Summary, Information, Timeline and Activity History as undifferentiated equal-weight grid cards. It remains genuinely open and is a legitimate small future candidate, but is cosmetic/non-blocking and is not currently promoted ahead of Internal Club Testing.

**Neither is currently promoted as the next implementation batch.** No unresolved High/MVP implementation blocker is known, and Release Readiness currently reports Ready.

**Verified Historical Scorer Attribution v1 (CMC-002) is now complete** — see the Coach Workspace section above and `SPRINTS.md` for full delivery detail. Its downstream Data Quality exception, Player Statistics eligible-matches/crediting integration, and a browser-acceptance Player-specific-crediting regression were all implemented, validated and merged at `2f3dcee`.

**Match Hero Goal-Scorer Presentation (CMC-003) is now complete**, including its live-eligibility correction, responsive/half-width polish and the primary immersive module accent-top consolidation delivered in the same arc — see "Match Hero Goal-Scorer Presentation" and the Coach Workspace section above, and `SPRINTS.md` for full delivery detail. The deferred CMC-002 follow-on opportunities ("Historical Match Participation Evidence — Deferred Opportunities" above) remain Post-v1 and were not part of this arc.

**Team Events/Attendance and Shared Messages month-disclosure navigation, Coach Workspace Batch B (Statistics chooser, inline availability editing, return-to-context), Live Match transient success notice auto-dismiss, and Event Builder Productivity & Training Only Event Audience Eligibility are all now complete** (plugin `main` `082e418` through `1c97ebb`) — see the Coach Workspace section above and `SPRINTS.md` for full delivery detail on each. Training Only Players can now be deliberately included in appropriate Event audiences (Current Team + Same Age Group Players and Selected Players), with League/Fixture competitive eligibility unchanged and unweakened. **Do not restart or re-scope any of this work; do not re-implement Duplicate Event, cross-Team Duplicate, weekly recurrence, optional End Time, or Training Only Event-audience support.**

**Welfare Concern Directory/mobile-filter repair and short operational Welfare Updates are now complete** (plugin `main` `5348403`, "feat: improve welfare workspace workflows") — see the Welfare Workspace Workflows bullet above and `SPRINTS.md` for full delivery detail. **Do not restart or re-scope this work.** A temporary interim dashboard action linking Emergency Contacts/Players Requiring Attention to "View concerns" was manually rejected as semantically wrong and removed before this commit — do not reintroduce or document it as delivered.

**Staff Compliance — canonical foundation, Secretary management, the restricted Welfare People/Person/Compliance projection, and proactive compliance expiry alerting are all now complete** (plugin `main` `b5f006a6`, `3352d300`, `cd871f3`, then `2bdd62e`) — see the Staff Compliance bullets above and `SPRINTS.md`'s "Staff Compliance — Batch A, Batch B, Batch C & Batch D" section for full delivery detail. **Do not restart or re-scope this work; do not re-implement the credential domain, either workspace's route/workflow, target-Person eligibility, type-aware credential naming, the desktop layout repair, the Welfare People inclusion rule/directory/profile, or the compliance expiry alert provider/routing.** No further Staff Compliance batch is currently approved future direction — missing-compliance ("Not Recorded") alerting, a configurable expiry threshold, a broader qualification catalogue, and notification-channel delivery (email/SMS/push) were all explicitly out of scope for Batch D and remain uncommitted, speculative ideas rather than approved next steps; do not promote any of them to a "Batch E" without a fresh, explicit Product Owner decision.

**The MVP Release Candidate Validation Cycle (RC-01 through RC-03-CLOSE) is now complete, and Product Owner manual sign-off has PASSED** (plugin `main` `a197abd`, `73c5767`, `3ee4c92`) — see `SPRINTS.md`'s "MVP Release Candidate Validation Cycle (RC-01 → RC-03-CLOSE)" section for full delivery detail and `development/DEVELOPMENT_HANDOVER_2026-09-09B.md` for the current resume point. This closes out `MASTER_DEVELOPER_GUIDE.md`'s former "Current Priority" of Final Release Readiness / Club OS v1.0 sign-off as a *technical validation and product-acceptance* milestone — it is not itself a production deployment event; see `RELEASE_CHECKLIST.md`'s separate "Release"/"Post-Release" gate for that distinct step. **Do not restart or re-scope any RC-cycle work; do not invent an "RC-04."**

**The Guardian Link Role Synchronisation Audit and its approved correction (Post-RC Guardian Link Alignment Batch 1) are now also complete** (plugin `main` `29220cc`) — see "Guardian Link Role Synchronisation Audit" above and `SPRINTS.md`'s "Post-RC Guardian Link Alignment Batch 1" section for full delivery detail. This was post-RC follow-up work and does not reopen the RC cycle above. **Do not restart or re-scope this work.**

**Treasurer Premium Workspace Alignment Batch 1 is now also complete, with Product Owner visual acceptance PASSED** (plugin `main` `8403691`) — see "Treasurer Premium Workspace Alignment Batch 1" above and `SPRINTS.md`'s section of the same name for full delivery detail. This was post-RC follow-up work and does not reopen the RC cycle or Guardian Link Alignment Batch 1 above. **Do not restart or re-scope this work; do not extend the Invoice Detail dark-record exception to any other Finance surface without a fresh Product Owner decision.**

**The Finance Reports Phantom Route Cleanup (FIN-033) is now also complete** (plugin `main` `fbfc032`) — see "Finance Reports Phantom Route Cleanup Batch 1" above and `SPRINTS.md`'s section of the same name for full delivery detail. **The previous recommendation naming Finance Reports as the next controlled development item is withdrawn: it was based on the mistaken premise that Reports was an existing feature awaiting a routing fix, which the cleanup audit disproved — there was never a Reports implementation to reconnect, and completing one now would require an explicit Product Owner product definition that does not yet exist. Do not treat Finance Reports implementation as authorised or recommended by this or any prior roadmap entry.**

**Registration Packages Selection, Draft Ownership & Secretary Workflows (RP-B)**, **Registration Finance Handoff (RP-C)**, and **Post-Registration Package Arrangement Workflow (Post-RP)** are now complete (plugin `main` `4285091daecf24214575a1c06c8ea86f33bdb0e1`). RP-B delivered Step 5 Package Selection, immutable package snapshots, dual-context architecture, and attempt-token draft ownership. RP-C delivered the idempotent Finance Draft Invoice handoff, translating the commercial snapshot into a Treasurer Finance obligation, along with operational alerts and Treasurer directory finance statuses. Post-RP delivered the dedicated Treasurer post-registration commercial workflow (`/club-os/treasurer/registrations/{id}/arrange-package/`), establishing a distinct canonical domain (`registration_package_arrangements`), preserving the original registration's immutable "no package selected" audit history (`package_id = null`, `package_snapshot = null`), applying player pathway eligibility to packages and extra charges, and generating idempotent Draft Invoices (`INV-001583` on registration #303) with read-only Secretary visibility. Manual invoicing is explicitly not the solution for registrations completed without a package. See `SPRINTS.md` for full delivery detail.

**Current baseline: `cdd9054efe7394297b4047f1cd59ba1335266d52` on `main`, schema `2026.10.20`.**

The Prospect Trial Period milestone, Fundraising F1–F5, Hosted Payments, Club Shop Batches 1–4A, Admin Route Parity, Mobile UX Batches 1–5, accepted Parent fixes MOB-008A and PRN-002, and Club Shop Youth Purchasing Safeguarding (YTH-001) are complete and integrated on plugin `main`.

## Mobile Experience & WordPress Admin UX Walkthrough Closure

**Status: UX Walkthroughs Complete / Provisionally Accepted Across All 8 Workspaces.**

The Product Owner has conducted comprehensive mobile workspace and WordPress Admin UX walkthroughs across all eight primary operational surfaces:
1. **Parent / Guardian:** Core family workflows, registrations, and finance validated. Currency encoding (MOB-001), inline fixture RSVP (MOB-008), Event Detail return (MOB-008A), and Priority Alerts 7-day RSVP window (PRN-002) resolved and accepted (`75c14aa`). Open items: RSVP button copy distinction (PRN-001) and Back My Game supporter visibility.
2. **Secretary:** Command Centre, People, Teams, Registrations, Venues, and Shop Fulfilment validated. Open items: Create Event Specific People modal mobile overflow (SEC-009) and operational settings separation (SET-001).
3. **Treasurer:** Billing, invoicing, payment recording, fee rules, and Back My Game oversight validated. Open item: static caret browser artifact (FIN-031) awaiting PO confirmation to close.
4. **Committee:** Club overview, projects, and communications validated. Open items: data minimisation boundaries (excluding confidential welfare, individual invoices, and medical records) and club-wide communications approval gate.
5. **Coach / Manager:** Matchday Hub, lineup builder, match mode, completed match corrections, and training attendance validated. Lineup builder draft/bulk attendance fixes (MOB-005–007) and fixture cards unification (MOB-009–011) resolved and accepted. Open items: bulk upcoming event responses and squad availability polish.
6. **Player:** Player Hub, Matchday journey, My Stats, and My Progress validated. Youth Shop purchasing safeguards (YTH-001) resolved and accepted (`cdd9054`); YTH-002 and YTH-003 verified as existing safeguards by code audit (note: local youth persona lacked past orders, so historical youth-order visibility in My Orders was verified by automated tests rather than manual walkthrough); My Stats breakdown and My Progress deep links open for polish.
7. **Welfare:** Safeguarding dashboard, concern lifecycle, welfare updates, and staff compliance validated. Open item: OS-011 Concern Detail card visual hierarchy polish.
8. **WordPress Admin:** Route parity and consolidation validated. Open items: SET-001 operational settings separation, `/wp-admin/` blank Fundraising route cleanup, and permanent technical support/recovery access retention invariant.

**Governance Standard:** Each workspace is formally recorded as **UX walkthrough complete / provisionally accepted**. All outstanding findings remain open until individually implemented, validated, and accepted. Unresolved issues are strictly not marked as fixed or claimed as final release acceptance.

## Authoritative MVP Completion Plan: 4-Tier Delivery Classification

Every open finding is classified into a structured delivery tier to guide final live-deployment preparation:

### Tier A — Release-Critical (Security, Safeguarding, Essential Workflows, Release Controls)
- **Youth Safeguarding in Club Shop (YTH-001):** Resolved and accepted (`cdd9054`). Minor players (<18) and unverified-age users cannot place orders, select bank transfer, or initiate hosted card checkout; adult purchasing preserved; browsing with safeguarding guidance intact. Note: local youth persona lacked past orders, so historical youth-order visibility in My Orders was verified by automated tests rather than manual walkthrough.
- **Youth Safeguarding in Spot the Ball (YTH-002):** Existing safeguard verified by code audit. Minor entry requires adult guardian authorization; minor winnings route strictly to linked adult guardians.
- **Youth Fundraising Appeal Attribution (YTH-003):** Existing safeguard verified by code audit. Public appeal sharing links attributing youth players require adult guardian issuance (`FundraisingShareAttributionPolicy`); zero public child seller accounts or URLs.
- **Committee Data Minimisation (COM-002):** General Committee views must strictly exclude confidential Welfare notes, individual debtor ledgers, and registration medical records.
- **Private Encrypted Backup Vault End-to-End Validation (B4D):** Complete payload population, verification, and restore of `IEXEL_RC_VAULT` to validate DR readiness.
- **Parent Event Detail RSVP Return Navigation (MOB-008A):** Resolved and accepted (`75c14aa`). Event Detail RSVP submissions return to Event Detail with per-child anchor continuity rather than redirecting to Team Hub.
- **WordPress Admin Recovery Access Invariant (ADM-006):** `/wp-admin/` must remain permanently accessible for system administrators, technical support, database upgrades (`UpgradeRunner`), and recovery diagnostics.

### Tier B — MVP Usability & Operational Improvements
- **SET-001: Operational Settings Separation:** Separate operational configuration (season dates, age groups, club contacts) from Brand Studio into a dedicated settings tab for MVP.
- **ADM-005: WordPress Admin Fundraising Menu Cleanup:** Investigate blank screen on `/wp-admin/admin.php?page=iexel-club-os-fundraising` and clean up route/menu.
- **SEC-009: Secretary Create Event Selector Mobile Overflow:** Resolve mobile modal horizontal overflow in Create Event "Specific People" selector.
- **PRN-001: Parent RSVP Wording Distinction:** Differentiate button copy between "Available for [Child]" and "I'm Available". (Remains open; outstanding for implementation).
- **PRN-002: Parent Priority Alerts RSVP Window:** Resolved and accepted (`75c14aa`). Unanswered event RSVP action requests are limited to a rolling seven-day window using the club's configured timezone and sorted in ascending chronological order so imminent fixtures appear first; verified with 33 assertions in `tools/validate-parent-priority-alerts-rsvp-window.php`.
- **COM-001: Committee Communications Approval Gate:** Require administrative sign-off for general committee members broadcasting club-wide messages. Resolved and accepted (`6d7a3f4`). Enforces approval gate (`SUBMITTED_FOR_APPROVAL` / `PENDING_APPROVAL`) requiring Secretary or Club Admin sign-off prior to dispatch. Mobile attachment workflow hardened with fallback retention in `CommunicationAudienceRequestMapper` and CSS filename containment; database recipient-role schema expanded to `VARCHAR(191)` via `UpgradeRunner`. Validated on physical Android device over LAN; 564 automated assertions passed.
- **CCH-001: Coach Bulk Upcoming Event Responses:** Rapid bulk availability response tools for upcoming training/events in Coach Hub.
- **BMG-001: Parent Back My Game Supporter Visibility:** Clear supporter agreement and pledge status in Parent Hub.

### Tier C — North Star Visual Polish
- **OS-011: Welfare Concern Detail Hierarchy Polish:** Differentiate Summary, Information, Timeline, and Activity History card weights on Concern Detail.
- **Coach Premium Squad Availability Presentation:** Visual polish for squad availability cards and response badges.
- **PL-026: Player My Stats Match Breakdown:** Expandable match-by-match breakdown under season aggregates.
- **PL-027: Player My Progress Match Report Links:** Contextual deep links from appearance milestones into completed Match Reports.
- **FIN-031: Static Caret Visual Artifact:** Awaiting PO confirmation to formally close as browser caret browsing.

### Tier D — Post-MVP (Deferred Scope)
- Commercial Licensing Engine, signed updates, and Restricted Data Access Mode.
- Club OS Control Centre: commercial customer registry, licensing, support triage, coarse telemetry, strict data minimisation (no player/welfare/financial PII), and time-limited, audited support access.
- Optional Premium Club OS Website Theme (commercial add-on for clubs without websites).
- Universal Club OS App (included with every licence, regardless of theme purchase).
- Public Demonstration Environment with synthetic data, permission sandboxing, and automated wipe-and-reseed cycles.
- League OS Vision (~5-year horizon): federated league-to-club fixture syndication, tables, and referee assignment.
- Role-specific onboarding setup wizard and video training library.
- SET-003 / SET-004 modular multi-tier settings architecture (Grassroots, Academy, Semi-Pro, Pro, Custom).
- Full migration of operational CRUD away from WordPress Admin.
- Direct Prospect-to-competitive Match Registration invitation (`ProspectLifecycle::INVITED_MATCH_REGISTRATION`).
- General package amendments / upgrades post-registration.
- Club Draw (F6) statutory lottery engine.
- Notification attachment / image lightbox viewer (OS-031).
- Campaign-specific family/player and team fundraising appeal attribution tokens with downloadable and scannable QR-code sharing, safeguarding, payment confirmation, refund handling, and avoidance of double-counting (FND-001).

## Deployment Pipeline & Commercial Architecture

### Deployment Pipeline
1. **Local Development & Validation:** Engineering and validator passes executed on local environments.
2. **Pre-Production Rehearsal & Acceptance Site:** A dedicated operational website used for pre-production rehearsal, update testing, and PO acceptance. Must use isolated test data, safe payment/email credentials, access controls, and production-identical configurations. Versioned release tagging, backup gates, idempotent `UpgradeRunner` execution, rollback plans, and smoke tests are mandatory.
3. **IEXEL FC Production Live Operations:** The live operational deployment for IEXEL FC. **IEXEL FC is an independent football club and the first live deployment customer of Club OS; it is not the Club OS commercial entity.**

### Commercial Product Structure
- **WordPress Club OS Plugin:** The core operating system providing all operational club functionality.
- **Optional Premium Website Theme:** Commercial package distinction for clubs needing a public club website alongside the OS.
- **Universal Mobile App:** The future Club OS mobile application is included with every Club OS licence entitlement, whether or not the theme is purchased.
- **Scope Boundary:** Website theme and mobile app are Post-MVP initiatives; initial IEXEL FC deployment operates entirely on the core plugin in the responsive web portal.

## Operational Onboarding Workstream

A planned workstream for role-specific Club OS how-to guides is established covering 7 core roles: Secretary, Treasurer, Coach, Welfare Officer, Committee Member, Parent / Guardian, and Player.
- **Standards:** Verified real workflows tested step-by-step; synthetic sample test data only; strictly zero member PII.
- **Execution Boundary:** Guides are planned in this reconciliation; authoring and publication occur in a subsequent authorized batch. Setup wizard and video library are Post-MVP.


## Future club profiles

### Grassroots

- Parent, Player, Coach, Committee, Welfare and Treasurer workspaces
- Registrations, events, attendance, availability, finance and communications
- Simple defaults and fewer advanced fields

### Academy

- Everything in Grassroots
- Player development plans, assessments, coach feedback and training programmes
- Scouting notes, development milestones and richer analytics

### Semi-Professional

- Everything in Academy where required
- Squad numbers, contracts, match bonuses and staff hierarchies
- More advanced finance, compliance and performance reporting

### Professional

- Medical, analysis, recruitment, media and contract departments
- Transfers, agents, multi-team structures and advanced permissions
- Deeper performance data and operational governance

### Custom

- Feature-by-feature module control
- Custom role terminology and workspace naming
- Custom defaults, labels, workflows and visible modules

## Recommended document role

Use this as a living product review and roadmap document in the repository, for example:

`development/CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`

It should sit alongside `MASTER_DEVELOPER_GUIDE.md` and `SPRINTS.md`:

- `MASTER_DEVELOPER_GUIDE.md` remains the architecture and engineering source of truth.
- `SPRINTS.md` records implementation history and approved delivery phases.
- This document records product experience decisions, MVP gaps and future workspace direction.

## Product statement

> Committee runs the club. Welfare protects the club. Coaches develop the players. Treasurers sustain the club. Parents support the players. Players experience the journey. Administrators maintain the platform.
