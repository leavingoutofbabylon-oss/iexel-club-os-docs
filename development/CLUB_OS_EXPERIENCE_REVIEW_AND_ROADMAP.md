# IEXEL Club OS Experience Review and Roadmap

Role-based product review, MVP priorities, post-MVP roadmap and future club profiles

## Executive summary

Club OS has reached the stage where the core architecture is strong and the main remaining work is product refinement: role identity, workflow completeness, navigation, visual consistency, accessibility and selective pre-MVP engagement features.

## Workspace scores

| Workspace | Score | Summary |
|---|---:|---|
| Settings / Brand Studio | 9.5/10 | Premium, visual and approachable. Best treated as Brand Studio, with separate operational and system settings. |
| Coach Workspace | 9/10 | The strongest operational experience. Matchday Hub, team workspace, statistics and lineup builder are standout features. |
| Welfare Workspace | 9/10 | Strong safeguarding workspace with concern management, medical overview and emergency information. |
| Committee Workspace | 9/10 | Clear oversight and decision-making experience. Needs fuller operational CRUD because committee users should not depend on wp-admin. |
| Treasurer Workspace | 8.5–9/10 | Feels like a real finance workspace with invoices, payments, billing schedules and bulk family billing. |
| Admin Experience | 8.5/10 | Powerful and comprehensive, but navigation is crowded and long-term role separation needs refinement. |
| Parent Workspace | 8/10 | Solid family hub with events, registrations and communications. Finance and selected-child context need improvement. |
| Player Workspace | 6/10 current | Functionally stable, but needs a stronger identity centred on motivation, progress, achievement and belonging. |

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
- **Batch 2.5 — Welfare Placeholder Repair:** Removed Timeline, Notes, Attachments, Communications, Activity History and misleading Next Steps placeholder cards from the remaining active legacy Admin Welfare Concern surface. The page still provides genuine concern data; status, priority and Welfare Officer assignment workflows, canonical portal detail, real portal Timeline and Activity History remain. Welfare authorization, sensitive response protection and unauthorized-access denial are unchanged. This does not claim deferred Notes, Attachments or concern Communications were implemented. LocalWP acceptance and the 193-check focused validator passed.
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

Both Environment 1 (Clean Installation) and Environment 2 (Controlled Upgrade Matrix) have passed. Next milestone: Internal Club Testing.

## MVP priorities

- **Global — complete:** Move Quick Actions directly below each workspace hero across all persona dashboards via `PortalDashboardLayout`.
- **Global:** Fix blue-on-blue and other low-contrast text through shared design tokens (OS-029, FIN-028, PL-024).
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
- **Parent — complete:** Fix selected-child context so an U8 child cannot see an U7 next event, and deliver Parent All-Children event identity + multi-child RSVP (OS-028).
- **Parent:** Improve Team Hub text contrast (OS-029).
- **Parent — complete:** Provide a real Finance page with invoice detail and payment history — delivered in Parent Family Finance & Invoice Detail (OS-030).
- **Notifications:** Improve attachment/image viewing so users can close and return without relying on the browser Back button (OS-031 — Post-MVP).
- **Treasurer — complete:** Provide invoice view/edit/cancel/archive or void actions and a proper invoice detail route — delivered in Treasurer Finance MVP (FIN-027).
- **Treasurer — complete:** Allow Treasurer role to manage fee rules and discount policies inside Club OS — delivered in Treasurer Fee Rules & Discount Policies management (FIN-029, FIN-030).
- **Treasurer:** Fix blue-on-blue text on billing pages (FIN-028).
- **Treasurer:** Fix static summary text showing caret as though editable (FIN-031).
- **Player — complete:** Create a real My Stats page based on the coach player-statistics experience, limited to the logged-in player (PL-022) — delivered in Batch IN3F16-PL1C at `/club-os/player/stats/`.
- **Player — complete:** Expand My Season with progress, attendance, milestones and next achievement (PL-021) — delivered in Batch IN3F17-PL2B2.
- **Player — complete:** Move Quick Actions near the top (PL-023) — delivered in `PortalDashboardLayout`.
- **Player:** Fix blue-on-blue text (PL-024).
- **Admin:** Reorganise the Club OS sidebar into grouped sections and hide route-only detail pages (ADM-001 / ADM-002 / ADM-003 — Recommended Next Implementation Batch).

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
| OS-010 | Welfare | Expand into broader compliance workspace | Future feature | Medium | Post-MVP |
| OS-011 | Welfare | Strengthen concern detail hierarchy | Visual/UX | Medium | Polish |
| OS-012 | Welfare | Make directory filters more compact | Visual | Low | Post-MVP |
| OS-016 | Coach | Capture match configuration during event creation — delivered in Portal Event Builder & Secretary Events Management | Resolved gap | Complete | Sprint 30 |
| OS-017 | Coach | Emergency contacts missing from Matchday Hub — exact-season authorised projection delivered | Resolved gap | Complete | MVP Experience Polish |
| OS-018 | Coach | Directions opens in same browser tab — resolved with `target="_blank"` / `rel="noopener"` across Matchday and Event venue cards | Resolved bug | Complete | MVP |
| OS-019 | Coach | Some pages use different visual language — dark immersive matchday/team styling is intentional and should not trigger homogenisation | Visual | Low | Post-MVP |
| OS-020 | Coach | Priority alerts dominate dashboard — persona scoping, capping and filtering delivered in `WorkspacePriorityAlertService` | Resolved UX | Complete | MVP |
| OS-025 | Coach | Bench players could not be selected or shown in Matchday Hub — saved substitute flow delivered | Resolved bug | Complete | MVP Experience Polish |
| OS-027 | Parent | Dates displayed in ISO format — standardised to DD/MM/YYYY and HH:mm via `DisplayDate` Batches 1 & 2 | Resolved consistency | Complete | MVP |
| OS-028 | Parent | Selected child sees event from wrong team — selected-child event scoping, Player Preview, and Parent All-Children multi-child RSVP delivered | Resolved bug | Complete | Sprint 31 |
| OS-029 | Parent | Team Hub has blue-on-blue text | Accessibility | High | MVP |
| OS-030 | Parent | Finance experience is too limited — Parent Family Finance workspace, invoice detail & payment history delivered | Resolved gap | Complete | Sprint 33 |
| OS-031 | Notifications | Image attachments lack an in-app close/viewer experience — direct link downloads are functional for MVP; lightbox viewer deferred | UX | Low | Post-MVP |
| OS-032 | Global | Priority Alerts could expose work unrelated to the active persona — persona/capability scoping accepted, merged to plugin `main`, and formally closed for MVP | Resolved security/UX | Complete | MVP |
| SEC-008 | Coach | Coach Team Event Scope Hardening & Football Event-Type Alignment — restricted to Training, Fixture, Friendly, Tournament; Meet/Arrive supported for Training; Matchday Hub Match Location repair delivered (`2370551`) | Resolved gap | Complete | MVP |
| RR-001 | Release Readiness | Integrity Batches 1, 2, 2.5 and 3 implemented, validated and accepted; plugin implementation and documentation reconciliation merged to their respective `main` branches | Resolved release integrity | Complete | MVP |
| FIN-027 | Treasurer | Invoices cannot be viewed, edited, cancelled, archived or voided properly — Treasurer invoice lifecycle delivered | Resolved gap | Complete | Sprint 33 |
| FIN-028 | Treasurer | Blue-on-blue text on billing pages | Accessibility | High | MVP |
| FIN-029 | Treasurer | Cannot create/edit/archive fee rules — Portal Fee Rules management delivered | Resolved gap | Complete | Sprint 33 |
| FIN-030 | Treasurer | Cannot create/edit/archive discount policies — Portal Discount Policies management delivered | Resolved gap | Complete | Sprint 33 |
| FIN-031 | Treasurer | Text shows caret as though editable | Visual bug | Low | MVP polish |
| PL-021 | Player | My Season has too much unused space and weak engagement — delivered with Season Journey, Milestones, Attendance rate, Next Milestone target in Batch IN3F17-PL2B2 | Resolved UX | Complete | MVP |
| PL-022 | Player | My Stats is only a minimal dashboard section — dedicated standalone experience with Appearances, Goals, Assists, POTM, Attendance, Clean Sheets, safeguarding delivered in Batch IN3F16-PL1C | Resolved gap | Complete | MVP |
| PL-023 | Player | Quick Actions moved directly below hero across all persona dashboards | Resolved UX | Complete | MVP |
| PL-024 | Player | Blue-on-blue text | Accessibility | High | MVP |
| ADM-001 | Admin | Sidebar navigation is too long — over 30 items in wp-admin sidebar | UX | High | MVP |
| ADM-002 | Admin | Route-only pages appear as sidebar destinations | UX | High | MVP |
| ADM-003 | Admin | Operational dashboards appear in admin navigation | UX/Architecture | Medium | MVP polish |
| ADM-004 | Admin | Long-term sensitive-role approval workflow | Security/Governance | High | Post-MVP |
| SET-001 | Settings | Current page is primarily a Brand Studio, not a full Settings area — modular settings evolution deferred to Post-MVP | Information architecture | Medium | Post-MVP |
| SET-002 | Settings | Add image positioning, zoom and focal-point controls | Visual tool | Medium | Post-MVP |
| SET-003 | Settings | Create separate Club, System and Experience Settings areas | Information architecture | High | Post-MVP |
| SET-004 | Settings | Add club-profile defaults: Grassroots, Academy, Semi-Pro, Professional and Custom | Platform feature | High | Post-MVP |

## Detailed workspace direction

### Committee Workspace

- **Committee Workspace & Native Operations (complete):** Club OS-native management of club events, Club Projects CRUD, Committee Communications, Audience Builder v2, and live executive dashboard metrics are fully delivered (`Sprint 30`).
- Keep the premium hero and core dashboard structure.
- Use Club Overview as the sole landing tab.
- **Committee Quick Actions (OS-003 — accepted):** All five Committee Quick Actions work and OS-003 remains PASS.
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
- Keep the concern dashboard, concern directory, concern detail, medical overview and emergency contacts.
- Move Quick Actions higher.
- Post-MVP, expand beyond concern management into DBS, safeguarding, first-aid and qualification compliance.
- Prefer archive over delete for safeguarding records; permanent deletion should be highly restricted and policy-controlled.

### Coach Workspace

- Preserve the Matchday Hub, Team Workspace, statistics and lineup builder design.
- **Coach Event Setup & Scope Hardening (SEC-008 — complete):** Coach team event creation is restricted to the four football event types `Training`, `Fixture`, `Friendly` and `Tournament`. Other generic event types are unavailable in the Coach workflow. Secretary retains the broader canonical event model. Meet / Arrive Time is intentionally supported for Training.
- **Matchday Hub Location & External Directions (complete):** Emergency-contact projection, bench/substitute selection, external Directions (`target="_blank"` / `rel="noopener"` via PR #123), and Match Location hero card derivation (`2370551`) are fully delivered and verified.
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
- Improve notification attachments with an in-app viewer/lightbox (Post-MVP).
- Post-MVP, evolve communications into richer posts, galleries, match reports and generated club content.

### Treasurer Workspace

- Keep the dedicated finance identity, payment recording, bulk family invoicing and billing schedules.
- **Treasurer Finance MVP (complete):** Invoice lifecycle management (draft, issue, cancel), payment recording & allocations, Fee Rules, and Discount Policies are fully delivered inside Club OS.
- Post-MVP, add reporting, exports, reconciliation and payment integrations.

### Player Workspace

- Reframe the workspace around motivation, progress, achievement and belonging.
- **Player My Stats (PL-022 — complete):** Dedicated standalone `/club-os/player/stats/` page delivered in Batch IN3F16-PL1C with Appearances, Goals, Assists, Player of the Match, Attendance rate, Clean Sheets (GK), Season Story, and Recent Match Contributions, backed by child-safe privacy rules (excluding negative labels, match ratings, and starts/substitute breakdowns).
- **Player My Season Journey & Milestones (PL-021 — complete):** Expanded `PlayerMySeasonCard` delivered in Batch IN3F17-PL2B2 with Season Journey progress, completed milestone badges, dynamic Next Milestone targets, and attendance rate context.
- **Player Quick Actions (PL-023 — complete):** Rendered directly below the hero card via `PortalDashboardLayout`.
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

- Keep admin focused on platform maintenance, system configuration and canonical records.
- **Admin Navigation Consolidation (ADM-001 / ADM-002 / ADM-003 — Recommended Next Implementation Batch):**
  - Reorganise the 30+ item wp-admin sidebar into clean logical sections (Platform, People, Football, Seasons, Registrations, Finance, Communications, Welfare, System).
  - Assign `null` parent slugs to route-only action and detail pages (e.g. `Add Season`, `New Registration`, `Add Club Project`) so they remain accessible via in-page workflows without cluttering the sidebar.
  - Remove operational portal dashboard duplicates (e.g. `Committee Dashboard`) from wp-admin navigation.
  - Preserve portal/admin boundaries with zero schema or database changes.
- Post-MVP, separate WordPress administrator power from automatic access to sensitive operational data (ADM-004).

### Settings and Brand Studio

- Rename or separate the current visual page as Brand Studio (SET-001).
- Create separate Club Settings, System Settings and Experience Settings over time (SET-003).
- Post-MVP, add image movement, crop, zoom and focal-point controls (SET-002).
- Add club-profile defaults for Grassroots, Academy, Semi-Professional, Professional and Custom (SET-004).

### Training Membership pathway roadmap

**Batch 2C accepted status (updated 2026-08-14):** Implementation and LocalWP manual acceptance are complete. Secretary People surfaces derive current Training Only status from active current-Season TrainingMemberships; a dedicated Training Members directory/detail supports operational filters and lifecycle management; and youth creation routes immediately into the existing Guardian Links workflow. Acceptance covered the Registration lifecycle from Draft through Registered, with Training Only remaining competitively isolated until the explicit Registered-only handoff. The reciprocal transitions preserved the same Player Person, Registration and historical Team Assignment records; current People, Secretary Team roster and Coach squad projections changed only with active participation state. Duplicate active participation and Training Member Registration type changes remained blocked. Training Members mobile filters and focused closeout validation also passed. No Batch 2C MVP blocker remains. Coach/Manager Training Only visibility remains **NOT CURRENTLY VISIBLE** because authorised Coach surfaces are Team Assignment/Event-audience based.

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

**Status:** Candidate UX Follow-up.

During browser acceptance, Product Owner review noted that the **Team Events** cards have a stronger, more polished Club OS visual identity than the generic `/club-os/events/` cards.
- Future UX work will evaluate adapting the established Team Events visual language (midnight-blue card treatment, gold/yellow accent hierarchy, football-specific badges, and clear operational hierarchy) onto the general Events page.
- Avoid blindly duplicating every football-specific field, as the general Events page serves club-wide non-football events (Meetings, Socials) as well.
- Prefer reusable component architecture over creating ad-hoc card variations.

### Venue Control Presentation

**Status:** Candidate UX Polish.

The Event Builder venue-selection radio and control presentation appeared visually basic during SEC-008 browser acceptance. This will be addressed as bounded visual polish unless a formal accessibility audit identifies a genuine compliance blocker.

### Training Meet / Arrive Time Policy

**Status:** Confirmed Product Decision.

Optional **Meet / Arrive Time is intentionally supported for Training** events. This supersedes any earlier handover statement suggesting Meet / Arrive Time should be hidden for training sessions. Grassroots clubs routinely require players to arrive before training commences for preparation, warmup, or administrative checks.

## Product principles

1. **Volunteer Administrative Efficiency:** Club OS must reduce repetitive administrative effort for club volunteers while preserving explicit user control.
2. **Purpose-Built Football Convenience:** Convenience features such as venue search, structured autofill, and recent ground reuse are commercially valuable because they make routine football administration fast and effortless, helping the product feel purpose-built for grassroots football rather than like generic management software.
3. **Canonical Identity & Boundaries:** Administrative authority never creates member identity; operational queues belong to their respective role workspaces (e.g. Secretary Command Centre owns registration review; Committee retains executive oversight).

## Recommended next implementation batch

### ADM-001 / ADM-002 / ADM-003 — Admin Sidebar Navigation Consolidation & Route Cleanup

**Recommended Priority:** High / MVP
**Scope:**
- Consolidate the 30+ item wp-admin sidebar into clean, logical grouped sections (Platform, People, Football, Seasons, Registrations, Finance, Communications, Welfare, System).
- Assign `null` parent slugs to route-only action and detail pages (`Add Season`, `New Registration`, `Add Club Project`, etc.) so they remain accessible via in-page buttons and direct URLs without cluttering the sidebar navigation.
- Remove operational portal dashboard duplicates (e.g. `Committee Dashboard`) from wp-admin navigation (portal remains canonical home).
- Pure UI/routing refactor in `AdminUI.php` and `ReleaseRouteInventory.php` with zero database, schema, migration, or portal-routing risk.

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
