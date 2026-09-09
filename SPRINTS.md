# IEXEL Club OS Sprint Releases

This document tracks the major development milestones of IEXEL Club OS. Completed entries describe stable feature sets merged into the plugin's main branch.

---

# Sprint Summary

| Sprint | Feature | Status |
|---|---|---|
| 17 | Matchday Portal and Global Navigation | ✅ Complete |
| 18 | Coach Hub Foundation | ✅ Complete |
| 19 | Team Workspace Foundation | ✅ Complete |
| 20 | Secure Portal Event Builder | ✅ Complete |
| 21 | Team Attendance Workspace | ✅ Complete |
| 22 | Matchday Hub | ✅ Complete |
| 23 | Match Mode Foundation | ✅ Complete |
| 24 | Match Lineup Builder | ✅ Complete |
| 25 | Live Match Controls | ✅ Complete |
| 26 | Goal Attribution | ✅ Complete |
| 27 | Rolling Match Substitutions | ✅ Complete |
| 29 | Welfare Experience Foundation | ✅ Complete |
| 30 | Secretary Command Centre & Operations | ✅ Complete |
| 31 | Parent Experience Scoping & Multi-Child RSVP | ✅ Complete |
| 32 | Secretary Operations, Person-First Team Assignments & Auto Team-Season Resolution | ✅ Complete |
| 33 | Treasurer Finance, Invoices & Fee Rules Management | ✅ Complete |
| RC | Release Candidate Verification (Clean Install Gate 2C & Upgrade Matrix Gate 2) | ✅ Complete |
| Internal | MVP Internal Club Testing: SEC-001 through SEC-008 & Event Suite Alignment | ✅ Complete |
| ADM | Admin Sidebar Navigation Consolidation & Route Cleanup (ADM-001 / ADM-002 / ADM-003) | ✅ Complete |
| A11Y | Dark-Surface Text Contrast (OS-029, FIN-028, PL-024) | ✅ Complete |
| CMC | Completed Match Correction Architecture (Batches 2A, 2B-1, 2B-2), Acceptance Gate & Player Progress MVP Decision | ✅ Complete |
| ICT-Fixes | Internal Club Testing Remediation — Secretary Safeguards, Current Emergency Contact, Password-Reset Completion Alerts & Final Pre-Merge Validator Hygiene (`b2b51eb`) | ✅ Complete |
| RC2 | MVP Release Candidate Validation Cycle (RC-01 portal-status fix, RC-02A/RC-02A-R1 clean-install + no-current-Season repair, RC-02B upgrade validation, RC-03/RC-03-R1 persona validation + forbidden-status fix, RC-03-CLOSE) — Product Owner sign-off PASSED | ✅ Complete |
| GLA1 | Post-RC Guardian Link Alignment Batch 1 (Secretary roleless-adult Guardian Links + transactional role ensure; Treasurer zero-role-grant and cross-role-top-up security closure) | ✅ Complete |

---

# Sprint 17

## Matchday Portal and Global Navigation

**Status:** Complete

**Goal:** Provide a portal-first attendance register within the shared Club OS shell.

### Delivered

- Global portal navigation, breadcrumbs and shared layouts.
- Matchday attendance register, progress, player cards, bulk actions and save bar.

### Security/Data Integrity

- Coach-only attendance access and persisted event audience records.

### Validation

- Attendance permissions, routing, persistence, responsive layout and event detail integration were exercised during delivery.

### Deferred

- Match statistics and richer live-match workflows.

---

# Sprint 18

## Coach Hub Foundation

**Status:** Complete

**Goal:** Give coaches a dedicated, role-aware Club OS workspace.

### Delivered

- Coach Hub, automatic coach routing, breadcrumbs, upcoming sessions, statistics and activity components.

### Security/Data Integrity

- Role-aware portal navigation and coach-specific workspace access.

### Validation

- Coach routing, upcoming event summaries and shared portal layouts were validated.

### Deferred

- Notifications and deeper team statistics.

---

# Sprint 19

## Team Workspace Foundation

**Status:** Complete

**Goal:** Provide a secure workspace for each team managed by a coach.

### Delivered

- Team overview, squad and availability summaries, season statistics, quick actions and upcoming events.

### Security/Data Integrity

- Active coach assignment checks and administrator override through `can_manage_team()`.

### Validation

- Assigned-team access, team summaries, navigation and responsive layouts were validated.

### Deferred

- Advanced team statistics and messaging.

---

# Sprint 20

## Secure Portal Event Builder

**Status:** Complete

**Goal:** Let authorised coaches create and manage team events without leaving Club OS.

### Delivered

- Portal event creation and editing for team events, venues, audience and match details.

### Security/Data Integrity

- Stored-team authorisation, team-scoped nonces, server-side validation and transactional event/audience updates.

### Validation

- Creation, editing, event type, venue, audience and direct-route access paths were validated.

### Deferred

- Messaging and automated event notifications.

---

# Sprint 21

## Team Attendance Workspace

**Status:** Complete

**Goal:** Consolidate RSVP, audience and attendance management for a team event.

### Delivered

- Team Attendance Workspace, audience management, RSVP summaries and attendance register integration.
- PRG submissions for RSVP and attendance.

### Security/Data Integrity

- Event visibility rules, audience eligibility, stored-event team checks and unique event/person records.

### Validation

- Coach and participant visibility, RSVP, attendance saves, redirects and repeated saves were validated.

### Deferred

- Attendance reports, exports and messaging.

---

# Sprint 22

## Matchday Hub

**Status:** Complete

**Goal:** Bring match preparation into one secure workspace.

### Delivered

- Matchday Hub with match details, attendance, availability and preparation actions.

### Security/Data Integrity

- Stored-event team authorisation and direct-ID route protection.

### Validation

- Fixture/friendly eligibility, team isolation, navigation and mobile rendering were validated.

### Deferred

- Match Reports, Player Ratings and PDF export.

---

# Sprint 23

## Match Mode Foundation

**Status:** Complete

**Goal:** Establish secure Match Mode routes, state and live-match presentation.

### Delivered

- Match Mode workspace, Match Details, state progression and transactional score projection.

### Security/Data Integrity

- Server-derived team identity, event/action-scoped nonces, row locking and authorised state transitions.

### Validation

- Supported state transitions, invalid transitions, terminal states and direct-route access were validated.

### Deferred

- Browser timer, extra time and penalty shootout.

---

# Sprint 24

## Match Lineup Builder

**Status:** Complete

**Goal:** Store a reliable pre-match lineup baseline.

### Delivered

- Starters and substitutes, captain and goalkeeper selection, positions, ordering and shirt-number snapshots.

### Security/Data Integrity

- Server-side eligible-player allowlist, unique event/person selection and post-kickoff mutation lock.

### Validation

- Duplicate players, audience membership, active assignments, captain/goalkeeper rules and read-only state were validated.

### Deferred

- Formations and tactical diagrams.

---

# Sprint 25

## Live Match Controls

**Status:** Complete

**Goal:** Support the core match lifecycle safely from a mobile-first interface.

### Delivered

- Kickoff, half-time, second half, full-time, reopen and supported terminal-state controls.
- Live score and match-state display.

### Security/Data Integrity

- Transactional transitions, locked event and match-detail rows, and audit metadata.

### Validation

- Transition order, repeat submissions, reopen behaviour and event-status synchronisation were validated.

### Deferred

- Match clock, extra time, penalty shootout, AJAX and WebSockets.

---

# Sprint 26

## Goal Attribution

**Status:** Complete

**Goal:** Record realistic goal events while preserving a consistent score projection.

### Delivered

- Club and opponent goals, both own-goal directions, penalties, assists, optional opponent names, timeline and Undo Last Goal.

### Security/Data Integrity

- Append-only incidents, idempotent request keys, stored-lineup allowlists, row locking and transactional score updates/undo.

### Validation

- Goal modes, score direction, scorer/assist eligibility, duplicate requests and repeated undo were validated.

### Deferred

- Cards, injuries and player statistics aggregation.

---

# Sprint 27

## Rolling Match Substitutions

**Status:** Complete

**Goal:** Support grassroots roll-on/roll-off substitutions and reliable player re-entry.

### Delivered

- Current On Pitch, Available Bench, substitution timeline, player re-entry and Undo Last Substitution.

### Security/Data Integrity

- Pitch state derived by replaying active incidents; action-request ledger and transactions protect substitutions and undo.

### Validation

- On-pitch/bench eligibility, replay order, re-entry, duplicate requests and repeated undo were validated.

### Deferred

- Formation-aware positions, AJAX/WebSockets and player statistics aggregation.

---

# Sprint 28

## Match Readiness Dashboard

**Status:** Complete

**Goal:** Make preparation and live status visible from Matchday Hub.

### Delivered

- Dynamic readiness from Match Details, lineup, availability, attendance and match state.
- Integrated preparation, live-match and completed-match actions.

### Security/Data Integrity

- Readiness uses the authorised stored event and existing authoritative repositories.

### Validation

- Empty, partial, ready, live and full-time states were validated across mobile and desktop layouts.

### Deferred

- Match Reports, Player Ratings, Player of the Match, PDF export and messaging.

---

# Sprint 29

## Welfare Experience Foundation

**Status:** Complete

**Goal delivered:** Authorised Welfare Officers and Club Administrators have a secure, role-aware safeguarding workspace within Club OS.

### Delivered

- Admin and front-end Welfare dashboards and navigation.
- Authorised concern directory, detail and create/edit workflows.
- Concern category, priority, assignment and controlled lifecycle status updates.
- Linked member, reporter and assignee records using existing People data.
- Activity-backed concern timeline and Welfare summary statistics.
- Responsive portal and WordPress admin presentation.

### Security/Data Integrity

- Welfare Officer and Administrator access only.
- Server-side permission validation.
- Direct-route protection.
- Record-level authorisation.
- Activity logging for concern creation and workflow changes.
- Nonce protection for all state-changing actions.
- Revision checks and transactional writes for concern workflow changes.
- Reuse existing People, Permissions and Activity Log systems.
- Prevent welfare data appearing within coach, player or parent experiences.

### Deferred

- Secure welfare notes.
- Follow-up actions and reminders.
- Secure document uploads.
- External safeguarding referrals.
- AI-assisted safeguarding summaries.
- Advanced welfare reporting.

---

# MVP Experience Polish

**Status:** Complete

### Delivered

- Lineup Builder substitute/bench interaction with saved starters and substitutes projected into Matchday Hub.
- An exact-season emergency-contact resolver limited to eligible `registered` or `approved` player registrations; ambiguity and invalid scope fail closed.
- An authorised Matchday provider limited to saved starters/substitutes that remain eligible and active.
- A presentation-only Emergency Contacts card with escaped output, mobile-safe wrapping and callable telephone links where normalization succeeds.
- Private, non-cacheable and non-indexable response protection for Matchday Hub.
- No schema change: the feature reuses the existing registration emergency-contact fields.
- No medical, Welfare, registration-status or internal-resolution data is exposed to Coaches.

---

# Communications Convergence & Safeguarding Sequence

**Status:** In Progress

### Batches

- **IN3F6-A4:** Communications Channel / Player Safeguarding / Adult Player Architecture Audit — ✅ Complete
- **IN3F6-A5:** Channel-Neutral Communications Terminology + Architecture Documentation — ✅ Complete
- **IN3F6-A6:** Youth / Adult Player Classification Foundation — ✅ Complete
- **IN3F6-A7:** Youth Communication Safeguarding Foundation — ✅ Complete
- **IN3F6-A8:** Player Messages / Club News Activation — ✅ Complete

---

# Sprint 30

## Secretary Command Centre & Operations

**Status:** Complete

**Goal:** Deliver operational governance, venue CRUD, club-wide registration directory, and member lifecycle management within Club OS.

### Delivered

- **Secretary Teams & Assignments Management:** Team creation/editing, permanent team references, and player/staff team assignment workflows (`IN3F12-STM1`, `IN3F12-STA1`).
- **Venue Management Workspace:** Operational venue directory, create/edit/archive CRUD flows, and postcode-aware location resolution (`IN3F12-SV1`).
- **Club OS Portal Account Management:** Secretary-managed portal account creation and member account linking (`IN3F12-SPA1`).
- **Events Management Workspace:** Operational event builder capturing opponent, competition, and match location during event creation (`IN3F12-SE1`, `IN3F12-SE2`).
- **Club-Wide Registration Coverage:** Authorised operational registration directory distinct from Parent "My Registrations", search/filtering by player/parent/status/season/team, season-aware Not Registered list, and pre-filled registration starting workflow (`IN3F12-REG1`, `IN3F12-REG2`).
- **Member Active / Inactive Lifecycle:** Operational Person Profile Make Inactive / Reactivate workflow, historical statistics preservation, and exclusion of inactive members from active squad/registration workflows (`IN3F12-M1`, `IN3F12-M2`).
- **Committee Workspace & Native Operations:** Executive dashboard with live club health & finance metrics, native Club Projects CRUD (create, edit, progress %, status, priority, category, owner, archiving, visibility, reordering), Committee Communications (compose, schedule, templates, delivery logs, Audience Builder v2 targeting, safeguarding checks), and activity logging (`IN3F23-COM1A`).

---

# Sprint 31

## Parent Experience Scoping & Multi-Child RSVP

**Status:** Complete

**Goal:** Resolve Parent selected-child event scoping (OS-028), Player Preview scoping, and deliver Parent All-Children event child identity and independent multi-child RSVP.

### Delivered

- **Parent Selected-Child & Player Scoping Repair (OS-028):** Parent selected-child context strictly scopes events to the chosen child; Player Preview and real Player contexts remain strictly single-player (`IN3F12-P1A`, `IN3F12-P1A2`).
- **Parent All-Children Event Identity:** Shared event cards identify relevant linked children with 36px circular profile photos or gradient initials fallbacks, child names, and per-child availability status badges (`IN3F12-P2`, `IN3F12-P2A`).
- **Multi-Child Event Detail RSVP:** Event Detail renders independent RSVP controls per eligible child when multiple linked children qualify for the same event, submitting `(event_id, person_id)` records without sibling response overwrites (`IN3F12-P2C`, `IN3F12-P2D`).
- **Server Security & Lifecycle:** Parent-child relationships, event eligibility, and active player status validated server-side; inactive members blocked; Coach and Player surfaces consume canonical availability records.

---

# Sprint 32

## Secretary Operations, Person-First Team Assignments & Auto Team-Season Resolution

**Status:** Complete

**Goal:** Deliver full Secretary Operations capability map, parent wizard autosave notes preservation, person-first team assignment routing, and canonical Team Season auto-resolution.

### Delivered

- **Secretary People Directory & Person Profiles:** Portal-native Secretary people directory, person profiles, person creation, and DOB management (`IN3F12-SEC1`, `IN3F12-SEC2`).
- **Secretary Registration Detail & Review Lifecycle:** Full registration review, information request parent round-trip, approval, and registered conversion (`IN3F12-REG1`).
- **Player Materialisation & Parent Linkage:** Materialises active Player person record and links parent/guardian relationship automatically upon registration approval (`IN3F12-REG2`).
- **Secretary Portal Accounts Management:** Secretary-managed Club OS portal account creation and member account linking (`IN3F12-SPA1`).
- **Secretary Teams & Venue Management:** Permanent team references, team CRUD, venue directory, postcode-aware location resolution, and venue profiles (`IN3F12-STM1`, `IN3F12-SV1`).
- **Secretary Events Management & Notifications:** Event builder capturing opponent, competition, and location with lifecycle notification dispatches (`IN3F12-SE1`).
- **Person-First Team Assignment Routing & Auto Team-Season Resolution:** Person-first routing (`/secretary/people/{person_id}/assignments/new/`), dynamic team selector rendering, and automatic resolution of canonical `Team Season` records when `team_season_id = 0` (`IN3F12-STA1`).
- **ActivityLogger Argument Order Repair:** Corrected `ActivityLogger::log()` argument ordering across team assignment creation workflows (`IN3F12-LOG1`).
- **Parent Wizard Autosave Notes Preservation Repair:** Fixed wizard autosave to preserve Secretary information request notes without wiping during parent edit/resubmission (`IN3F12-SR3C`).

### Real Browser Verification

- Complete operational lifecycle browser-validated:
  Parent registration (Registration #195)
  → Secretary review
  → Information request
  → Parent edit & resubmission
  → Secretary approval
  → Registered status
  → Person #175 / CLB-000140 materialisation
  → Jess Test guardian linkage
  → Sammy Player portal account creation
  → Person-first team assignment to U9 GOLD
  → Auto-resolution to Team Season #7 (U9 GOLD 2026/27)
  → Assignment #102 created
  → Player Experience / Team Workspace verified

---

# Sprint 33

## Parent Family Finance & Treasurer Finance MVP Lifecycle

**Status:** Complete

**Goal:** Deliver Parent Family Finance workspace, Parent Invoice Detail experience, and confirm Treasurer Finance MVP lifecycle capability.

### Delivered

- **Parent Family Finance Workspace (OS-030):** Parent-facing Family Finance page (`/club-os/parent/finance/`), household total outstanding / overdue / open invoice metrics, multi-child charge breakdown, household invoice history, and Parent Home CTA (`IN3F19-PAR1B1`, `IN3F19-PAR1B2`, `IN3F19-PAR1B2A`).
- **Parent Invoice Detail & Canonical Overdue Derivation:** Dedicated Parent Invoice Detail page (`/club-os/parent/invoices/{id}/`), line items with child attribution, payment allocation history, payment instructions, canonical overdue status derivation via `Invoice::is_overdue()`, and strict household authorization boundary (`IN3F20-PAR1B3`, `IN3F20-PAR1B3D`).
- **Mobile-Responsive Invoice Item Presentation:** Stacked card layout for invoice items on screens <=600px, eliminating horizontal table scrollbars on mobile viewports (`IN3F20-PAR1B3E`).
- **Treasurer Finance MVP Audit (FIN-027):** Confirmed full operational readiness of Treasurer Finance overview, manual invoice creation, bulk/family fee-rule generation, draft management, invoice issuing, cancellation, payment recording, multi-invoice allocations, recurring billing schedules, fee rules, and discount policies (`IN3F21-FIN1A`).

---

# MVP Priority Alert Persona-Scoping Repair

**Status (updated 2026-08-14):** Implementation, source validation and LocalWP manual acceptance complete; implementation merged to plugin `main`, acceptance documentation merged to docs `main`, and OS-032 formally complete and closed for MVP.

**Goal:** Ensure every actionable Priority Alert is relevant to the active persona and has a destination that persona is authorised to use, without changing canonical notification delivery or recipient state.

### Delivered

- Added recipient-aware, `MemberExperienceContext`-based workspace projection through `WorkspacePriorityAlertService`, with target authorization and final display limits applied after eligibility filtering.
- Refined Committee operational alerts so ordinary Committee membership does not imply Treasurer, Secretary, Coach, Event/team attendance, Registration review or Welfare responsibility.
- Added shared Finance warning ownership through `FinanceOperationalAlertsProvider`; Treasurer and authorised Committee contexts reuse one overdue-invoice calculation and the canonical `/club-os/finance/outstanding/` portal destination where authorised.
- Preserved notification delivery, recipient generation, unread/read and acknowledgement state, Event and Welfare permissions, Secretary Command Centre Priority Actions and persona-native alerts. No schema, migration, CSS or JavaScript change was required.

### LocalWP acceptance

- Parent selected-child/all-children scoping, Player own-person relevance and Coach Team/current-TeamSeason scoping remain intact.
- Welfare no longer receives guardian/Parent Event alerts merely because the same Person has both personas; Welfare permissions remain unchanged.
- Louis Hall as ordinary Committee receives none of the unrelated Finance, Match Report, Event-response or Registration-review alerts and sees the correct smooth-running empty state.
- Jess Test as Finance-authorised Committee receives the Finance warning, and its action opens the canonical Outstanding Accounts surface rather than reloading Committee.
- Treasurer receives exactly one equivalent Finance warning for qualifying overdue invoices; Parent and Welfare receive none.
- Secretary Command Centre Priority Actions remain the authoritative Secretary feed, and broad Club Admin capabilities remain narrowed by the active persona.

### Validation

- Workspace Priority Alert scoping: 109 checks passed.
- Committee permissions: 90 passed.
- Treasurer operational read access: 45 passed.
- Treasurer Finance relationships: 250 passed.
- Treasurer directory UX: 34 passed.
- Parent Family Finance: 44 passed.
- Secretary Command Centre: 95 passed.
- Secretary Events: 108 passed.
- Event action leakage: 27 passed.
- Dashboard cancellations: 54 passed.
- Committee Communications: 281 passed.

The pre-existing Treasurer Finance configuration validator baseline mismatch concerning the expected rewrite/schema version remains open. It predates this repair and is not a regression caused by it.

# MVP Release Readiness Integrity

**Status (2026-08-15):** Batches 1, 2, 2.5 and 3 are implementation complete, source validation complete and LocalWP manually accepted. The plugin implementation is merged to plugin `main`, the documentation reconciliation is merged to docs `main`, and the MVP Release Readiness Integrity workstream is formally complete.

## Batch 1 — Weather / Match Readiness Integrity

- Removed synthetic Weather from active MVP Event Detail, Team Events, Matchday Hub, Match Mode, Match Report and Event Hub presentation where applicable.
- Removed Weather as a Match Readiness criterion and next action. Genuine readiness criteria now determine status, and genuinely complete preparation reaches 100% / Match Ready.
- Weather was not implemented; dormant Weather integration scaffolding remains Post-MVP.
- LocalWP acceptance, the 110-check focused validator and the full 68/68 non-mutating release gate passed.

## Batch 2 — Visible MVP Placeholder Cleanup

- Removed accepted active MVP placeholders/dead actions for Player and Parent-preview Achievements, Matchday Travel Time and future Notes, Event Hub Rewards and stale Availability, synthetic/fixed-zero Event status or response presentation where applicable, Registration photo upload, generic Admin Person/Team Profile entries, legacy Person/Team Coming Soon cards and the generic authenticated “Page coming soon” fallback.
- Preserved genuine Player Progress, Player-of-the-Match/statistics, Availability, Audience and valid ID-bound Person/Team Profile routes. Unknown authenticated generic portal routes fail closed to HTTP 404 / Page not found.
- LocalWP acceptance passed; the focused validator evolved to 169 checks and the full non-mutating gate remained 68/68.

## Batch 2.5 — Welfare Placeholder Repair

- Removed Timeline, Notes, Attachments, Communications, Activity History and misleading Next Steps placeholder cards from the active legacy Admin Welfare Concern detail while retaining its genuine authorised read value.
- Preserved genuine concern data, status/priority/Welfare Officer assignment workflows, canonical portal Welfare detail, real portal Timeline and Activity History. Welfare authorization, sensitive response protection and unauthorized-access denial remain unchanged.
- Deferred Notes, Attachments and concern Communications were not implemented.
- LocalWP acceptance, the 193-check focused validator and the 68/68 non-mutating release gate passed.

## Batch 3 — Release Readiness Policy / Integrity

- Corrected the canonical policy: overall Ready requires zero unresolved risks with `required = true`. `required` is the deterministic blocking switch; severity classifies urgency and does not decide whether a required risk blocks.
- Corrected the prior Blocker/High/Medium-only defect that omitted Critical and could theoretically allow a required Critical risk alongside Ready. Critical is canonical and required Critical risks block release.
- Required categories: plugin activation; portal boot registration; authentication boundary; duplicate administrator routes; duplicate portal routes; duplicate scheduled hooks; missing database tables; Kernel service resolution; schema upgrade/lifecycle integrity; destructive-delete integrity; communication attachment validation; scheduled-hook deactivation cleanup.
- The focused validator passed 244 checks.

### LocalWP acceptance and release evidence

- Release Readiness showed Ready; required open risks 0; Blocker 0; Critical 0; High 0; Medium 4; Low 1; Informational 2. Controlled lifecycle evidence showed Pass.
- `medium.audit-coverage-inconsistent` showed **Required before 1.0: No**. It remains visible Post-MVP/P2 completeness debt for broader ActivityLogger/timeline coverage across some administrative domains; security-critical Welfare, Communications, Finance and Match audit boundaries were not removed or downgraded.
- `medium.placeholder-experiences` showed **Required before 1.0: No**. Active audited MVP placeholder exposure is resolved, but dormant/deferred Post-MVP scaffolding remains. The inventory distinguishes those two states.
- The full safely executable non-mutating release gate passed 68/68.
- Five controlled integration/mutating validators were excluded, not failed: `validate-parent-autosave-preservation.php`, `validate-parent-card-info-request.php`, `validate-person-first-team-assignment-routing.php`, `validate-secretary-registration-approval.php`, `validate-secretary-registration-lifecycle.php`.
- Real Weather integration, Rewards, Achievements/XP, Travel Time, richer Matchday Notes, broader audit completeness and dormant placeholder cleanup remain Post-MVP.

# Training Membership MVP Sequence

## 2B — Prospect → Training Only

**Status:** Manual acceptance passed; pending commit

### Accepted behaviour

- A continuing Prospect can be converted through the Secretary Prospect detail workspace.
- Ambiguity-aware identity resolution creates or reuses the canonical Person and, for youth, Parent/Guardian Person and relationship.
- The pathway starts the canonical TrainingMembership for a selected active Season and normalized active TeamSeason Age Group, then records the Prospect as `converted_training`.
- Existing `UNDER 7`, `Under 7`, `U7` and `U 7` representations normalize to the stable Training Membership comparison key without rewriting TeamSeason data.
- Batch 2D-B1 later normalises the converted football participant to Player identity while still creating no account, competitive Team Assignment, Match Registration or Matchday eligibility.
- Final LocalWP browser acceptance confirmed conversion, resulting People visibility and the absence of competitive-player side effects.

## 2C — Training Membership Visibility & Secretary Management

**Source completion update (updated 2026-08-13):** Implementation is complete. It includes batched current-Season visibility, distinct Training Only/Youth Match Player/Senior Match Player summaries, responsive People and Training Members directories, existing-Person re-entry, and guarded end/archive lifecycle actions. Batch 2D-B1 updates direct Training creation to ensure canonical Player identity through the transaction-safe role boundary while leaving Training participation separate: no account, Team Assignment, Registration, Match eligibility, Finance or Event audience is created. DOB remains the classifier; youth uses a supported TeamSeason U-group and adults use `senior`. Coach/Manager visibility remains assignment-based and was not broadened.

**LocalWP acceptance update (2026-08-14):** Final manual acceptance passed for the Training Members directory and mobile filters, Training Member detail, existing-Person Registration creation, and the Draft, Submitted, Under Review, Approved and Registered boundaries. Training Only remained competitively isolated until the explicit Registered-only handoff. Training Only → Match Player retained the same Person and Registration, ended the Training Membership and created one active compatible Team Assignment; Match Player → Training Only retained Player identity and Registration, preserved historical Team Assignment rows as inactive, started one active Training Membership and removed the Player from current Secretary roster and Coach squad projections. People Directory projection, duplicate active-participation prevention and immutable Training Member Registration type compatibility also passed. Focused closeout validation passed 11/11 validators with 1,083 checks/assertions, and PHP lint passed for 16/16 directly involved files. No Batch 2C MVP blocker remains.

**Status:** Implementation and LocalWP manual acceptance complete

### Expected scope

- Canonical Training Membership read model.
- Clear Training Only badges/status in the Secretary People Directory, Person Profile, relevant relationship/member views and Training Membership management surfaces.
- Authorized Coach/Manager visibility where the member is legitimately visible, including appropriate training or Age Group operational summaries.
- Secretary direct creation of a Person/member as Training Only, reusing the canonical TrainingMembership service and canonical youth relationship rules.
- Season and normalized operational classification: an explicit supported U-group for youth, or DOB-derived `senior` for adults.
- Appropriate end/archive Training Membership actions.
- No fake Player role, account, Team Assignment or Registration to make Training Only visible.

## 2D — Competitive Player ↔ Training Only Transition

**Batch 2D-A acceptance update (2026-08-12):** The Secretary Person Profile owns an explicit **Move to Training Only** action, and the complete browser flow has passed LocalWP manual acceptance. The atomic service reloads/locks canonical state, rejects cross-Season assignment conflicts and any non-terminal saved Match lineup, ends every current-Season competitive Player assignment with `status=inactive` and canonical `left_on`, starts exactly one TrainingMembership through `start_in_transaction()`, writes safe activity events, and invalidates existing Player/Guardian experience caches. The Player role, linked account and Registration are deliberately retained. Person, family, Finance, Team Assignment, Match and statistics history remain untouched. Current self Player Experience and competitive Coach/Matchday projections cease naturally when active competitive assignments end. Acceptance also proved the saved not-started lineup block, removal through the normal lineup UI, successful `Training Only · U7` transition and repeat idempotency.

**Status:** Batch 2D-A implemented and manually accepted; pending commit. Batch 2D-B1 and Batch 2D-B2 final acceptance passed and both are merged.

### Match Event ownership integrity repair

- Fixture/Friendly ownership is canonical through `events.team_id`, `events.season_id` and `events.team_season_id`; Team-less Match writes fail closed while legitimate Team-less Training, Meeting and club Events remain supported.
- Malformed scheduled/not-started Match Events remain readable and can be repaired through the Secretary UI using an active Team and deterministic TeamSeason resolution.
- Existing saved selections are checked against the exact target TeamSeason roster before ownership changes; compatible lineups are retained and incompatible lineups fail with actionable feedback.
- Event ownership, exact-TeamSeason audience, Match details and audit writes remain one transaction, and the repaired audience is installed before Event change-notification recipient resolution.
- Completed malformed historical Events remain readable; no broad rewrite, schema change or migration was introduced.

### Expected scope

- Controlled, explicit and auditable Match Player → Training Only transition.
- Preservation of historical Person identity, Player Registrations, Team Assignments, match participation, statistics, finance and activity history.
- Audit and safe handling of current Team Assignment, Player role/account access, active Match Registration, future Matchday eligibility, future event audiences, TrainingMembership, Season/Age Group and finance/billing relationships.
- Preserve a future return or invitation to the Match Player pathway.

### Batch 2D-B1 — Registered-only Training Only → Match Player

**Final acceptance update (2026-08-13):** Player is the football-participant identity for both Training Only and Match Player states. Prospect conversion, direct Training creation and a narrow idempotent active/current Training participant backfill ensure Player without creating accounts, Registrations, assignments or Event eligibility. Secretary-controlled reciprocal transitions enforce participation exclusivity; Training → Match Player requires exactly one current Person-linked `registered` Registration, zero active Player assignment conflicts and a compatible active current Team/TeamSeason. Success creates a new regular active Player assignment episode, ends (never deletes/archives) the TrainingMembership and writes one safe activity event atomically. Current/historical roster and statistics presentation and the responsive Training Members mobile filters passed final acceptance. Registration, account, family, Finance, existing Event audiences, historical assignments and Match/statistics history remain unchanged.

**Status:** Final acceptance passed; merged on `main`

### Batch 2D-B2 — Secretary-native Registration setup

**Final acceptance update (2026-08-13):** The Secretary Training Member detail resolves the canonical current-Season Registration for the existing Player and presents state-based Start, Continue or View actions. Starting creates one canonical draft through the existing Registration service and wizard, binds `existing_person_id` and the active TrainingMembership Season, uses `returning_player` by default or `trialist_conversion` for reliable Prospect-origin membership, and resumes active episodes idempotently. Contradictory active records fail closed; rejected/withdrawn history remains intact. Youth guardian links are reused without duplication, while adults use existing Player contact details without creating a guardian. Registration does not change TrainingMembership, create an account or Team Assignment, or mutate Finance, Events or Matchday. LocalWP happy-path acceptance verified one existing Person through Draft, Submitted and Registered, followed by the accepted B1 transition to one compatible current Team Assignment; the Person, Registration, family links and historical Training Membership were retained, and Team Hub showed one current roster entry.

**Status:** Final acceptance passed; merged on `main`

### Explicitly deferred to later work

- Historical-only former Player Experience.
- Parent Preview policy or workspace redesign.
- Training Member self portal, Event/Coach/Finance integration, historical-only former Player Experience and Parent Preview policy changes.

## Team Staff Operational Access Reconciliation

**Status:** Implementation and LocalWP manual acceptance complete; pending intentional commit

This bounded prerequisite for Player Profile A reconciles the existing `iexel_manage_assigned_team` capability directly on linked active accounts from canonical current active Team staff assignments. Qualifying assignment roles are `coach`, `manager` and `assistant_coach`, and the assignment must belong to an active Team and active TeamSeason in the current active Season. Person role alone, an inactive Person, an inactive or historical assignment, and a stale TeamSeason do not qualify.

- Manager and Assistant Coach identity remains canonical in Team Assignment data; neither is promoted to a Coach WordPress role.
- An account created or linked after the assignment is reconciled immediately; an assignment never auto-creates credentials.
- Multiple qualifying assignments retain the capability when one ends; ending the final qualifying assignment removes it.
- Reconciliation owns only this assigned-Team capability and preserves Treasurer, Welfare, Club Admin and unrelated account access.
- The capability is an account-level prerequisite only. Every Team or Player operation must still prove the exact active Team assignment and current Team/TeamSeason scope at request time; the capability never grants all-Team access.
- Core LocalWP acceptance proved one Manager-assigned Team and one Coach-assigned Team were accessible while an unrelated Team remained denied, with no broad all-Team access.

## Player Profile A — Security, Core Workspace and Current Operational Medical/Safety

**Status:** Implementation and LocalWP manual acceptance complete; pending intentional commit

The existing front-end route `/club-os/teams/{TEAM_ID}/players/{PERSON_ID}/` is retained and hardened. A linked active Coach, Manager or Assistant Coach must use the Coach experience, hold `iexel_manage_assigned_team`, and have exactly one active staff assignment on the exact active route Team and exact active current TeamSeason. A linked active Club Admin retains the `iexel_manage_club_os` override. Ordinary Secretary stays on the Secretary Person Profile; Parent, Player, Treasurer, Welfare, Committee and preview contexts are denied.

- The target must be an active Player Person with exactly one active Player assignment on the exact route Team/current TeamSeason. Training Only, former, inactive, registered-but-unassigned, stale and duplicate/corrupt contexts fail closed.
- One immutable authorized scope supplies a unified read model containing minimum identity, current assignment, current-Season Registration status, known-youth guardian telephone, exact-Season emergency contact and existing football navigation. Exact DOB, previous Teams and mutation controls are absent.
- Current Operational Medical & Safety is a dedicated non-Season Person-level singleton (`player_operational_medical_safety`) with a unique canonical `person_id`. Admin and active Secretary users with `iexel_manage_registrations` may replace or explicitly clear the four bounded current fields through the protected Secretary Person workflow. Authorized exact-current-Team Coach, Manager and Assistant Coach users receive those fields read-only through Player Profile A, without history, provenance or editor metadata.
- Completed Registration remains immutable historical evidence. On the first exact transition to `registered`, allergies and medication may seed only when no current row exists; `medical_notes` and `emergency_information` never seed, existing Players receive no bulk historical backfill, and later Registration changes never synchronize into current state. An explicit all-empty current row remains authoritative and never falls back to historical Registration.
- Emergency Contact remains the separate who-to-contact architecture. Welfare/safeguarding cases and Finance remain separate and are neither queried nor copied. Secretary Person Profile, the focused editor and Player Profile A use private/no-store/no-cache/noindex response protection; activity events contain metadata and changed-field names only, never medical content.
- Welfare and Finance are absolutely excluded. The profile does not expand attendance, statistics or Player Journey, does not log views or sensitive content, and uses the established private/no-store/noindex response protection.
- The focused static/in-memory validator covers exact actor/target authorization, persona denials, duplicate/corrupt data, minimal fields, medical leakage, Welfare/Finance separation, response protection, retained route and mobile structure.

**LocalWP acceptance update (2026-08-14):** Manual acceptance is complete for assigned Coach, Manager and Assistant Coach architecture; exact assigned-Team authorization; cross-Team denial; Training Only isolation; Player Profile A; the Secretary current Medical & Safety workflow; the Coach read-only four-field projection; and an explicitly empty current state that does not resurrect Registration history. Registration lifecycle testing confirmed no current Medical & Safety content before the final `registered` transition, then seeded allergies and medication only; historical medical notes and emergency information did not seed, and an existing current row remained protected. The persisted Training Member Registration type remained authoritative through successful submission. Responsive acceptance passed at 600px, 390px and 360px. The Player Workspace response was verified with `Cache-Control: private, no-store, no-cache, must-revalidate, max-age=0`, `Pragma: no-cache` and `X-Robots-Tag: noindex, nofollow`. The final pre-commit audit found no functional MVP blocker. The accumulated batch remains pending intentional commit.

**Current Operational Medical & Safety implementation update (2026-08-14):** Implementation and LocalWP manual acceptance are complete; intentional commit is still pending.

## Later pathways and communications

- Prospect → direct Match Player invitation/registration remains a separate future pathway; Training Only is not a mandatory stepping stone.
- Taster/Trial invitations and Secretary communications to a Parent/Guardian or adult applicant are retained as post-MVP planning.
- Configurable Secretary/reply-to email and eventual role-authorized IMAP/SMTP or equivalent mailbox integration remain post-MVP and are not MVP blockers.
- Prospect conversion, Secretary direct creation and Match Player transition must all converge on the one canonical TrainingMembership domain.

---

# Release Candidate Gate 2C

## RC Clean-Install Blocker Repair

**Status:** Implementation, Gate 2C post-commit clean-install verification and pre-merge audit complete; merged to plugin `main` (`e3f115dce90a04f3812036334317f691ba367b42`).

### Delivered

1. **AI Activity / dbDelta Schema Reconciliation:**
   - Corrected multiline `CREATE TABLE` DDL formatting in `CreateAIActivityTable.php` by removing intermediate blank lines misparsed by WordPress 7.0.4 `dbDelta`.
   - Preserved persistent schema semantics, column types and exact 4 indexes (`PRIMARY`, `user_id`, `provider`, `created_at`) with zero schema/data version change and no migration required.
   - Repeated schema reconciliation passes 2/2 cleanly with 0 warnings and 0 malformed SQL.

2. **Member Experience Identity Boundary / Fail-Closed Enforcement:**
   - Removed `synthetic_welfare_context` and confirmed the architectural invariant: *Administrative authority does not create member identity*.
   - Unlinked WordPress administrators and users without an active linked `Person` fail closed cleanly with `MemberExperienceOperationResult::fail()`.
   - Legitimate linked Welfare, Committee, Coach, Parent, Player, Secretary and Treasurer persona resolution and switching are preserved without capability broadening.

3. **Public Prospect Intake Feedback & Route Inventory:**
   - Moved feedback-cookie consumption to pre-output routing in `PublicProspectRouter.php`, eliminating headers-already-sent warnings during form rendering.
   - Restored canonical 4-tuple element structure (`slug`, `title`, `capability`, `hidden = false`) for public prospect routes in `ReleaseRouteInventory::administrator()`.
   - Verified valid PRG flow, one-time error notice rendering/clearing, thank-you confirmation, exactly 1 prospect creation and zero real emails sent.

4. **Billing Scheduler Contract on Fresh Installation:**
   - Confirmed canonical current source behavior: `iexel_club_os_process_billing_schedules = 0` on an empty site with no billing schedules.

### Validation

- Fresh-install baseline verified on WordPress 7.0.4 / PHP 8.2.29 / MySQL 8.4 with 48 owned tables, schema/data version `2026.08.6`, complete upgrade state (25/25 steps/results), 15 formations and 129 slots.
- Lifecycle verified: deactivation PASS, reactivation PASS, repeated reconciliation 2/2 PASS, 0 dbDelta warnings, 0 malformed SQL, 0 duplicate hooks.
- Identity & routes verified: unlinked admin fail-closed PASS, linked personas PASS, public enquiry flow PASS, 12/12 admin pages smoke PASS, 166 Kernel accessors PASS.
- Controlled Upgrade Matrix (Environment 2) passed across all 4 canonical baselines plus controlled interruption/resume scenario.

---

# Release Candidate Gate 2

## RC Environment 2 — Controlled Upgrade Matrix Execution

**Status:** Implementation, full 4-row matrix execution, controlled interruption test, architecture audit and formal acceptance complete.

### Delivered & Verified

1. **Full-Registry Idempotent Reconciliation Architecture:**
   - Proved that `UpgradeRunner` evaluates all 25 registered `UpgradeStep` contracts sequentially on non-current databases without version slicing.
   - Verified that `is_valid()` precedes each step: steps already satisfied execute as safe, non-mutating checks (`ran = false`), while unfulfilled invariants execute `apply()` (`ran = true`) inside a transaction and revalidate.
   - Corrected previous pre-execution theoretical assumption of 18/9/2 applicable steps: `completed_steps` accurately reflects all verified invariants in the registry.
   - Current installations (`2026.08.6` with all 25 valid invariants) return `already_current` with 0 steps executed.

2. **Controlled Matrix Execution (Rows 1–4):**
   - **Row 1 (`906960b` / `2026.07.1` -> `2026.08.6`):** 41 -> 48 tables, 25 steps (18 mutating, 7 no-op) in 2.0803s. Secretary capabilities and team references normalized to `TM-000001`. **PASS**.
   - **Row 2 (`ddb784e` / `2026.08.2` -> `2026.08.6`):** 44 -> 48 tables, 25 steps (10 mutating, 15 no-op) in 1.4483s. Coach team management capability reconciled. **PASS**.
   - **Row 3 (`0d62f56` / `2026.08.5` -> `2026.08.6`):** 47 -> 48 tables, 25 steps (3 mutating, 22 no-op) in 1.3500s. Manager capabilities reconciled, Training participant player role backfilled. **PASS**.
   - **Row 4 (`e3f115d` / `2026.08.6` -> `2026.08.6` - Idempotence):** 48 tables, `code: already_current`, 0 steps executed in 0.3523s, 0 mutations. **PASS**.

3. **Controlled Interruption & Resume Verification:**
   - Injected interrupted failure state at step `2026_07_welfare_concerns`.
   - Verified `UpgradeStatus::current()->state` reported `failed` and `ready = false` with blocking notice.
   - Resumed `UpgradeRunner->run()`; completed remaining steps to `complete` with `retry_count = 1` and lock released.
   - Confirmed harness/database-state simulation only with zero production source modification.

4. **Safety & Data Integrity Guarantees:**
   - Zero duplicate data, zero destructive reapplication, zero capability regression, zero event/match corruption, and zero formation/reference duplication.
   - Verified *Administrative authority does not create member identity*: unlinked administrators fail closed across all upgraded baselines.
   - Isolated disposable database (`127.0.0.1:10010`) used exclusively; development database (`127.0.0.1:10005`) and plugin source remained untouched.

---

# MVP Internal Club Testing

## SEC-008 — Coach Team Event Scope Hardening & Football Event-Type Alignment

**Status:** Implementation complete, automated validation complete, LocalWP browser acceptance complete, committed and pushed (`2370551`).

**Goal:** Align Coach/Manager team event creation and editing with canonical `EventAudiencePolicy`, restricting Coach events strictly to valid football event types (`Training`, `Fixture`, `Friendly`, `Tournament`), preserving full event edit fidelity, repairing Matchday Hub match location display, and keeping Secretary flexible club event workflows intact.

### Delivered & Verified

1. **Coach Event Builder Scope Hardening:**
   - Restricted `TeamEventForm::event_types()` to the four canonical football event types: `Training`, `Fixture`, `Friendly`, and `Tournament`. Other generic event types are unavailable in the Coach workflow.
   - Enforced server-side validation rejecting any unauthorized Coach attempts to create non-football events.
   - Secretary retains the broader canonical event model across all seven event types (`Training`, `Match / Fixture`, `Friendly`, `Tournament`, `Meeting`, `Social`, `Other`) with flexible audience targeting.

2. **Contextual Football Field Behaviour:**
   - **Training:** Presents clean session-only fields (Title, Date, Start/End Time, Venue, Team Audience). Match-specific fields (Opponent, Competition, Home/Away/Neutral selector) are hidden.
   - **Important Product Owner Decision:** Optional **Meet / Arrive Time remains supported for Training**. This is intentional and supersedes older statements; grassroots clubs legitimately ask players to arrive before training commences.
   - **Fixture:** Fully supports Opponent Name, Competition, Home/Away/Neutral Match Location radio controls, Meet / Arrive Time, Kick-off Time, End Time, existing Club Venue or one-off venue with structured address/postcode, team audience, and Event Hub/Team Events projections.
   - **Friendly:** Retains full match-specific behaviour with explicit Friendly labelling in Team Events.
   - **Tournament:** Represents the overall tournament event cleanly without single-match Opponent/Competition fields or Home/Away selectors, supporting Start/End times, optional Meet / Arrive, venue, and team audience.

3. **Edit Fidelity & Matchday Hub Location Presentation Repair:**
   - Verified 100% round-trip edit preservation of event type, opponent, competition, match location, venue/address/postcode, date, meet time, kick-off, end time, status, and audience.
   - Discovered and repaired a Matchday Hub presentation defect where the `MATCH LOCATION` card rendered blank despite canonical `home_away` data persisting accurately in `wp_iexel_os_event_match_details`.
   - Root cause: `MatchdayHeroCard::render()` referenced an undefined `$match_location` variable.
   - Fixed by deriving display state from canonical `match_details['home_away']` with fallback to `event['home_away']` and default `'Home'`.
   - Verified Home, Away, and Neutral rendering states; Event 227 browser acceptance confirmed `MATCH LOCATION → Away`.
   - Automated validation: focused validator `tools/validate-coach-fixture-builder-match-details.php` passed **68/68 assertions**; master regression passed **25/25 suites**.

4. **Secretary Regression Protection:**
   - Verified that Secretary retains the full flexible event suite. Created a real Secretary Meeting with whole-club/no-team scope, Committee Members audience, and 3 invited participants without leakage of Coach restrictions.

---

# ADM-001 / ADM-002 / ADM-003 — Admin Sidebar Navigation Consolidation & Route Cleanup

**Status:** Complete. Implemented, validated and committed to `feature/mvp-internal-testing-fixes` (`c88eab9`, 2026-08-21); not yet merged to plugin `main`.

**Goal:** Reorganise the wp-admin Club OS sidebar (previously 30+ items) into a clean, role-appropriate structure without cluttering navigation with route-only action/detail pages, while preserving every existing slug/route and restoring in-page discoverability for anything moved out of the sidebar.

### Delivered

- `AdminUI::register_menu()` now registers 19 visible sidebar destinations grouped into logical clusters (Platform/Dashboard; People & Football Operations; Seasons & Registrations; Finance, Communications & Projects; Welfare & Safeguarding; System & Settings), and 36 hidden route-only destinations (`add_submenu_page(null, ...)`) — every prior admin slug/route remains addressable.
- Route-only action and detail pages (`Add Person`, `Add Team`, `Add Event`, `Add Venue`, `Add Season`, `New Registration`, `Add Club Project`, etc.) were removed from the sidebar and given restored in-page contextual creation actions on `PeoplePage`, `TeamsPage`, `EventsPage` and `VenuesPage`; Seasons, Registrations, Finance, Communications, Club Projects and Welfare already had their own admin-navigation components.
- The operational Committee Dashboard duplicate is hidden from the sidebar; the portal remains the canonical home for that experience.
- Zero database, schema, migration or portal-routing changes.

### Validation

- The focused validator `tools/validate-admin-navigation-consolidation.php` passes **227/227 checks**: exact visible (19) and hidden (36) slug sets and ordering; every callback resolves on `AdminUI`; `ReleaseRouteInventory` hidden-flag accuracy for every route it covers; no duplicate slugs; in-page discoverability across 11 pages/components; `ReleaseReadinessService` "Duplicate administrator routes" and "Duplicate portal routes" both report Pass; Welfare and Finance capability boundaries intact.

### Non-blocking follow-up identified during a subsequent read-only audit (not part of ADM-001/002/003 itself)

- `ReleaseRouteInventory::administrator()` does not yet enumerate 10 of the 55 real `AdminUI` routes (Committee Dashboard, AI Workspace, Club Projects, Add/Edit Club Project, Welfare Dashboard, Welfare Concerns, Add/View Welfare Concern, Entity Lifecycle). Current duplicate-route checks still pass; this is an inventory-completeness gap, not a routing failure.
- `app/UI/AdminMenu.php` is a HIGH-confidence dead-code cleanup candidate: an early foundation-era scaffold class with zero runtime call sites, never hooked to `admin_menu`, fully superseded by `AdminUI.php`.
- Two hidden routes (Committee Dashboard; the full standalone AI Workspace page, whose assistant widget the Dashboard already embeds inline) currently have no in-app discoverability path. Whether to retain either as intentionally hidden, add discoverability, or formally deprecate is an open Product Owner decision.

---

# OS-029 / FIN-028 / PL-024 — Dark-Surface Text Contrast

**Implementation status:** Complete. Implemented and committed to `feature/mvp-internal-testing-fixes` (`34cd5d4`, "Fix dark-surface finance contrast and visual hierarchy", 2026-08-21); not yet merged to plugin `main`.

**Documentation/source reconciliation status:** Confirmed complete by a subsequent read-only MVP / Release Readiness reconciliation audit (2026-08-26), which found the roadmap still describing all three as open High/MVP defects a month after they were fixed.

**Goal:** Eliminate low-contrast "blue-on-blue" text — dark navy foreground tokens (`--iexel-ink`, `--iexel-midnight`) accidentally reused on dark midnight-blue surfaces — across Team Workspace/Team Hub, Finance/billing/invoice and Player Statistics.

### Delivered

- A systemic on-dark foreground-token treatment in `design-system.css`: dark-surface component classes (`.iexel-team-workspace-hero`, `.iexel-billing-schedule-card`, `.iexel-billing-schedule-meta`, `.iexel-billing-run-meta`, `.iexel-player-statistics-hero`/`-quality`/`-filters`/`-summary`/`-history-section`, and related Team/Coach/Match dark surfaces) now force `--iexel-text`/`--iexel-muted`/`color` to `var(--iexel-color-on-dark, #fff)` rather than inheriting a dark-on-dark default.
- Direct fixes in `public.css` (Team Workspace hero heading/body text) and `member-experience.css` (finance invoice links, billing schedule metadata).
- `tools/validate-dark-surface-contrast.php` was added in the same commit to guard the exact bad pattern going forward.

### Validation

- `tools/validate-dark-surface-contrast.php` passes **6390/6390** checks (re-confirmed 2026-08-26).
- Independently re-verified: `.iexel-team-workspace-hero` (OS-029, Team Hub — also the Parent-facing Team Hub destination) renders white/near-white text on a dark midnight-navy gradient background; the design-system.css on-dark token block explicitly covers billing/invoice classes (FIN-028) and Player Statistics classes (PL-024).

### Scope note

FIN-031 (static caret-cursor visual bug, Low priority) and OS-011 (Welfare concern-detail hierarchy, Medium/Polish) are separate items and remain open — not addressed by this fix and not implemented in this reconciliation.

### FIN-031 / OS-011 read-only reconciliation audit (2026-08-26)

A follow-up read-only source audit reconciled both remaining open items against current source. Neither was implemented. **FIN-031** could not be reproduced in current Finance/Treasurer source — no static summary uses `cursor: text` or another confirmed input-like affordance, and no specific fix commit was identifiable; it remains open, reclassified as *not reproducible in current source, Product Owner reproduction required before implementation* (not marked complete). **OS-011** was independently confirmed still present on the portal Welfare Concern Detail page (undifferentiated equal-weight grid cards for Summary/Information/Timeline/Activity History, no safeguarding impact) and remains genuinely open. Neither was promoted to the next implementation batch; continued Internal Club Testing was recommended.

---

# Completed Match Correction Architecture & Player Progress MVP Decision

**Status:** Complete. Implemented, source-validated, browser-accepted where applicable, committed and pushed to `feature/mvp-internal-testing-fixes` (`436ec5d` through `2844e7a`, 2026-08-24 to 2026-08-26); not yet merged to plugin `main`.

**Goal:** Give Coaches a safe, auditable way to correct a completed Match's record after Full Time — score-neutral goal correction, incorrect-goal removal and missed-goal addition — on top of a canonical timeline-ordering and score-reconciliation architecture, while keeping the completed-match participant experience privacy-minimised, and resolve the Player Progress MVP navigation architecture.

## Completed Match Participant and Coach Experience

**Status:** Complete (`436ec5d`, `95142f3`, `3392843`).

- Delivered the completed-match participant experience (`CompletedMatchExperienceService`) for Player, Parent and Parent Preview: a scoring-focused Match Story and appropriate completed-match information, intentionally privacy-minimised.
- Participant projections exclude substitutions involving unrelated Players, ratings, Coach Notes, correction reasons, correction audit metadata and unrelated Player identities. Player self-scope, Parent linked-child scope and Parent Preview exact-child scope remain canonical and were proved by dedicated privacy assertions.
- Delivered the Coach completed-Event experience: Final Score, WIN/DRAW/LOSS result badge, Match Summary, authoritative Match Timeline, completed Match Report, and correction/recovery actions.
- Improved Full Time match report continuity and mobile score layout, and moved responsive Coach timeline/summary presentation to container-aware CSS so it remains usable when the Club OS content column narrows independently of the browser viewport.

## Completed Match Correction v1

**Status:** Complete (`8e42364`).

- Delivered score-neutral correction of an existing active Club goal: scorer change, assist add/change/removal, chronology-safe minute correction, and Normal ↔ Penalty.
- The workflow is reached from Completed Event → Match correction and recovery → Correct Match Record and never reopens the Match.
- Corrections are auditable and transactional. Historical Player eligibility is derived from the actual historical pitch state, not merely all selected Players. The scorer and assister cannot be the same Player.

## Batch 2A — Canonical Score Reconciliation & Remove Incorrect Goal

**Status:** Complete (`d8d9607`).

Implemented the canonical score-reconciliation architecture that every subsequent correction workflow builds on:

1. Canonical active-ledger score derivation and a reusable score-reconciliation writer.
2. Live Goal writes migrated away from independent score-delta ownership onto the same reconciliation writer.
3. Live Undo Last Goal migrated to canonical reconciliation, and stale live Undo is blocked outside valid Match phases (a completed/Full Time Match must use Correct Match Record instead).
4. Completed/Full Time Remove Incorrect Goal, with a mandatory correction reason for score-changing removal.
5. Idempotency, structured audit and rollback/failure safety across the write path.
6. Match Report, statistics and participant projections update from canonical active data without reopening the Match.

Stored Match score and the active scoring ledger must reconcile; normal correction operations fail closed when the pre-operation score is already inconsistent. Arbitrary direct score editing is not part of the architecture.

## Batch 2B-1 — Canonical Match Incident Timeline Order

**Status:** Complete (`eebd849`).

Resolved the architecture blocker around historical insertion by introducing `timeline_order` as a first-class concept, deliberately separated from Add Missed Goal so the replay architecture could be validated independently:

- `sequence` remains the immutable creation/audit order; `timeline_order` owns effective chronological replay/display order.
- Existing incidents were backfilled through the controlled upgrade path (`UpgradeRunner`); live incidents append with new sequence/timeline positions.
- Historical corrections can retain/reuse their logical timeline position while receiving a fresh creation sequence.
- Chronological repositories, replay, statistics and presentation use the effective timeline order as required. Active chronological display rank is not the same thing as immutable creation sequence, and historical `sequence` values are never renumbered.

## Batch 2B-2 — Add Missed Goal

**Status:** Complete (`6bb435b`).

- The completed-match correction page supports Add Missed Goal for all canonical scoring directions/modes: Club goal, opponent goal, opponent own goal awarded to Club, Club Player own goal awarded to opponent, and Normal/Penalty where semantically valid. Historical placement uses `timeline_order`.
- Historical scorer/assist eligibility is derived from saved Event selection, Event audience, Attendance Present/Late and the historical on-pitch state at the chosen placement boundary — never merely all selected/bench Players.
- Equal-minute behaviour is deterministic: if an existing incident shares the same period/minute, the Coach must choose an explicit Before/After historical boundary. The system never breaks an equal-minute tie using database ID, submission time or arbitrary ordering — proved on the established Event 57 acceptance scenario (at 20′, after the 18′ substitution and before the 24′ substitution, the eligible pool is Public Enquiry, DECLAN ROGERS, Test Person, HENRY JAMES and JUDE KANE, with david adel correctly off the pitch; at exactly 18′, Before yields Public Enquiry, david adel, DECLAN ROGERS, Test Person and HENRY JAMES, while After yields Public Enquiry, DECLAN ROGERS, Test Person, HENRY JAMES and JUDE KANE).
- The scorer cannot also be the assister. Goal-mode field semantics are enforced server-side; browser behaviour is a UX enhancement, not the security boundary.
- **UX acceptance:** manual "Show eligible Players" fallback; automatic historical eligibility refresh when Period/Minute/placement changes; stale scorer/assist selections cleared when timing changes; explicit equal-minute Before/After selection; scorer dynamically excluded from Assist; incompatible fields cleared/hidden when scoring mode changes; responsive/even goal-mode cards on mobile; a semantic interaction-continuity anchor at the Match-time working area after server round-trips (no brittle fixed-pixel scroll offset); Reason remains required for the real save but does not block the eligibility preview action. The broader OS continues to use server-rendered round trips for this workflow; interaction continuity is a reusable UX principle for future server-rendered actions, not a global AJAX architecture.

## Completed Match Correction End-to-End Acceptance Gate

**Status:** Complete (`2cb13ef`).

A disposable completed Match proved the combined journey in one continuous run: score-neutral correction, incorrect-goal removal, missed-goal addition, equal-minute historical placement, all supported goal semantics, canonical score reconciliation, timeline ordering, idempotency, rollback/failure safety, Match Report retention, ratings/POTM retention, Team/Player statistics, participant privacy and completed/full-time lifecycle preservation throughout. The acceptance validator passed 169 checks when introduced.

## Validator Hygiene Reconciliation

**Status:** Complete (`2844e7a`).

- The live-goal eligibility validator no longer assumes Event 57 is an old live First-Half fixture; its live-workspace, goal-attribution-form and idempotency coverage now runs against an isolated disposable fixture (57 checks).
- The substitution/Attendance eligibility validator no longer depends on obsolete Event 57 live-state assumptions; its rolling-substitution, re-entry, form and Match Mode page-rendering coverage now runs against an isolated disposable fixture (96 checks).
- The Player Progress validator no longer expects the deliberately removed WordPress/Gravatar Player-photo fallback, and its navigation assertions were reconciled to the confirmed embedded Team Workspace architecture below (367 checks).
- **Current Player image contract:** uploaded Player photo → otherwise the canonical configured/default Club OS visual. A linked WordPress account alone must not introduce an external Gravatar/WP-derived Player image.
- Event 57 remains the stable completed-Match acceptance fixture (completed, full_time, 2–0, five active incidents) throughout and was proved read-only at every step.

## Player Progress — Canonical MVP Architecture Decision

**Status:** Confirmed Product Decision (2026-08-26).

For the Operational MVP, Player Progress remains an embedded Player-specific Team Workspace experience:

Player Home → Team Workspace → My Progress

- Player global navigation remains deliberately simplified: Home, Team, Events, News. Player Progress is **not** a fifth global navigation item.
- The Player Home Progress card continues to link through the authorised Team Workspace My Progress destination, sourced from the existing canonical Team/Member Experience projection rather than a hand-built URL.
- Team Workspace → My Progress renders the Player Progress experience (`PortalPlayerProgressPage`) in embedded mode. Player self-scope remains authoritative; Parent Preview remains exact-child scoped.
- Standalone infrastructure — the `/club-os/player/progress/` and `/club-os/parent/progress/` routes and the `PlayerProgressUrl` URL-builder class — remains in the repository. Source evidence (introduced together in one earlier feature commit, fully route-registered and security-hardened, but with zero current call sites for `PlayerProgressUrl` anywhere in production code) classifies it as unfinished/alternate standalone infrastructure rather than the primary Player journey. It was not removed or redesigned.
- **Deferred cleanup item (Post-MVP, not a blocker):** after MVP/Release Readiness, decide whether to (A) formally retain/document the standalone route as an alternate/bookmarkable direct entry point, or (B) deprecate/remove the unused standalone URL-builder/route infrastructure.

---

# Internal Club Testing Remediation & Final Pre-Merge Validator Hygiene

**Status:** Complete — merged to plugin `main` at `b2b51eb` (2026-08-29).

Closes out the Internal Club Testing remediation programme that followed the SEC-001–SEC-008 / Completed Match Correction work above, and integrates the accumulated `feature/mvp-internal-testing-fixes` branch into plugin `main`.

## Delivered

- Secretary member-maintenance safeguards and person-bound registration/training-member flow fixes.
- Canonical Current Emergency Contact management: a Person-level current-state record, authoritative even when explicitly empty, with an exact-current-Season Registration compatibility fallback and unavailable as the final state — never inferring a value the Secretary has not recorded.
- Secretary-assisted password-reset completion alerts: request/completion tracked via ordinary WordPress user meta (no schema, no password/token/URL ever stored or logged), completion attributed to the resetting WP user (never falsely attributed to the requesting Secretary), idempotent on WordPress's own canonical `after_password_reset` hook, one logical `DashboardAlert` per eligible completion, seven-day (`604800`s) self-expiring eligibility window, fail-closed re-check of the Person/WP-user link at both completion and read time.
- Final pre-merge validator/repository hygiene: removed a stray scratch helper (`scratch/web_run_validator.php`); replaced brittle exact-literal `DATA_VERSION`/`SCHEMA_VERSION`/`REWRITE_SCHEMA_VERSION`/preview-route-array validator assertions with structural proofs of the underlying invariant across 14 validator files; repaired bootstrap/fixture drift (missing `require_once`s, missing WordPress function stubs, a stale local `Season` fixture, a variable-name collision) uncovered in the process. Zero production files were touched by this hygiene work.

## Integration

- **Method:** audited, GREEN-gated, pure fast-forward (`git merge --ff-only`) — no merge commit, no rebase, no squash, no force push.
- **Divergence at integration:** `origin/main` 0 commits ahead, `feature/mvp-internal-testing-fixes` 57 commits ahead, merge-base == `origin/main`.
- **Final clean-branch pre-merge release gate:** GREEN (zero functional/security/schema/integration blocker; two harmless validator-drift items and one bare-CLI mysqli environmental limitation, all individually classified as non-blocking).
- **Post-integration sanity validation:** PASS (all 10 required validators green on the post-merge tree).
- **Result:** plugin `main` and `origin/main` both point to `b2b51eb`.

## Known non-blocking validator debt (unchanged by this integration; tracked, not defects)

- `validate-prospect-training-conversion.php` — harmless source-shape drift: an exact-literal assertion against `TeamSeasonService`'s `age_group` snapshot expression no longer matches after a legitimate `trim()`/`'Unspecified'`-default refactor; the eligibility-governing invariant remains independently proven by adjacent assertions in the same file.
- `validate-committee-club-projects.php` — a stale exact-literal assertion no longer matches after a legitimate, already-committed `log_important_lifecycle_activity()` call was added inside the same success-gated block it pins; the "cache refresh restricted to successful mutations" invariant still holds by direct inspection.
- `validate-visual-foundation.php` — a stale dependency-array assertion (expects `public.css` enqueued with an empty dependency array) no longer matches after `public.css` was given a genuine, deliberate `iexel-club-os-club-mark` load-order dependency, introduced by an already-committed branding-controls feature.
- `validate-secretary-portal-account-linking.php` — passes, but emits non-fatal `stdClass could not be converted to int` PHP warnings; cosmetic, does not affect the PASS result.
- A pre-existing, non-content whitespace nit: a trailing blank line at EOF in `app/core/Upgrade/ParentGuardianRelationshipReconciliation.php` (flagged by `git diff --check`; not a conflict marker).

---

# Verified Historical Scorer Attribution v1 (CMC-002)

**Status:** Complete. Implemented, source-validated, browser-accepted, committed and pushed to plugin `main` at `2f3dcee` ("feat: add verified historical scorer attribution").

**Goal:** Give Coaches a safe, auditable, evidence-backed way to recover a genuine historical scorer on a completed Match's active Club goal for the rare case where reliable Tier-1 historical participation evidence (saved Selection + legitimate live-bench admission) is genuinely absent, without weakening the normal Correct Match Record eligibility rule and without broadening historical eligibility for anyone else.

## Verified scorer write path

**Status:** Complete.

- `CompletedMatchGoalCorrectionService::verify_historical_scorer()` follows the established void+append correction architecture (`void_incident()` + `add_goal_at_timeline_order()`) — no new persistence primitive. It re-confirms, under lock, that Tier-1 eligibility is still empty before proceeding, and rejects even a direct/forged invocation once Tier-1 evidence exists.
- v1 Tier-2 candidate discovery is deliberately narrow: exact Event Audience **or** exact Event Attendance for the exact Match — discovery only, never automatic proof of participation, and never intersected with Team assignment.
- Required Coach input: verified scorer, verification source (`match_footage` / `club_records` / `first_hand_knowledge`, a closed vocabulary shared with the form), a mandatory evidence note, and explicit confirmation.
- A distinct `verify_historical_match_goal` idempotent-action string keeps retries from colliding with ordinary `correct_match_goal` requests. A distinct `match_goal_verified_historical_attribution` audit action (metadata-only: event/incident IDs, verified scorer, verification source, evidence note, request key, acting user — deliberately never a candidate-pool list) keeps it from ever being confused with a system-verified correction.
- `CompletedMatchRecordCorrectionPage` adds a "Verify scorer manually" pathway from an adapted "Insufficient historical evidence" state, reachable only when Tier-1 is empty and the Tier-2 candidate pool is non-empty (fails closed with no dead-end link otherwise); the ordinary Correct Match Record form is unchanged and the two pathways are mutually exclusive for a given goal.

## Downstream integration — Data Quality and Player Statistics

**Status:** Complete.

- `FootballStatisticsEngine` gained a shared, role-specific `outsideSelectionPersonIds()` helper (reused by both the Team-scope and Player-scope outside-selection warning paths) that exempts **only** the exact active incident's scorer role when a matching, currently-live verified-attribution audit record exists — never the whole incident, never assist/player-in/player-out, never a different incident or Match. A superseded (re-verified) attribution naturally stops qualifying because it points at an incident that is no longer active.
- `PlayerStatisticsRepository::eligibleMatchesForPlayerSeason()` additively merges in a Match where the exact verified scorer has no Selection row but does have currently-live verified-attribution provenance, deduplicated by Match. The Player's own "My Progress" self-service view is explicitly excluded from this merge, mirroring how `effective_selection()` itself already stays out of that surface.
- `FootballStatisticsEngine::buildPlayerStatistics()` credits the verified scorer with exactly one goal and one appearance for that Match, reusing the genuine `attendanceForPerson()` lookup — never fabricating starting/substitute status, minutes, Attendance, rating or POTM, and never granting participation to any other Event Audience/Attendance candidate.
- A new `ActivityLogger::verified_scorer_attributions_for_events()` / `verified_scorer_attributions_for_person()` pair provides this provenance as narrow, batched reads (never one query per Match/incident), reusing the existing `activity_log` `action`/`object_id` indexes.

## Browser-acceptance regression — Player-specific Match-card crediting

**Status:** Found and fixed before final sign-off.

Browser acceptance found that a non-scoring Player's own Player Statistics Match card could show another Player's verified goal (e.g. `Goals 1` on a Player who did not score) — the verified-scorer crediting block credited every verified scorer for a Match regardless of which specific Player's own statistics build was being rendered. Fixed with a single additional guard so a Player-scoped build (`person_id` set) credits only that exact verified scorer; a team-wide build (`person_id === 0`) is unaffected and still credits every verified scorer, exactly as intended for the Team Statistics player table. A dedicated regression fixture in `tools/validate-player-season-stats.php` reproduces the exact leak and is confirmed to fail without the guard.

## Validation

- `tools/validate-team-workspace-overview-shell-polish.php` — 326 checks (write-path, Data Quality exception and downstream-integration assertions).
- `tools/validate-player-season-stats.php` — 112 checks, including the dedicated Player-specific-crediting regression fixture (verified scorer's own build vs. a non-scoring Player's own build vs. team-wide scope).
- `tools/validate-team-statistics-current-player-scope.php`, `tools/validate-player-team-statistics-visibility.php`, `tools/validate-player-progress.php`, `tools/validate-dark-surface-contrast.php` all pass unaffected.
- Browser acceptance confirmed: verified scorer recovered through the exceptional pathway; score unchanged; active goal incident carries the verified scorer; the Player receives goal + appearance + Match history; no starter/substitute/minutes fabricated; the exact verified scorer no longer triggers the generic outside-selection Data Quality warning while the two genuine goalkeeper warnings remain; Player Match-card statistics remain Player-specific after the crediting-leak fix.

## Historical eligibility and Data Quality correctness fixes

**Status:** Complete (`2cbae72`, `7d3caa0`, 2026-09-03 — landed in this same arc, ahead of `2f3dcee`).

- `historically_eligible_players()` (`CompletedMatchGoalCorrectionService`, used by both Correct Match Record and Add Missed Goal) now replays the historical pitch state against `MatchLiveBenchAdmissionService::effective_selection()` (Selection **plus** legitimate live-bench admissions) rather than the raw saved Selection alone (`2cbae72`, files: `CompletedMatchGoalCorrectionService.php`, `FootballStatisticsEngine.php`, `Kernel.php`, `CompletedMatchGoalAdditionService.php`). Without this, a Player legitimately admitted to the live bench and later substituted on was invisible to historical eligibility, incorrectly reporting zero eligible historical scorer/assist candidates even though the Match's own incident history proved they played. Pitch-state replay itself is unchanged — an admission still only becomes "on pitch" via a genuine substitution incident, never automatically.
- Data Quality's recovery-action routing (`TeamStatisticsDataQualityCard`/`PlayerStatisticsDataQualityCard`) is now a positive allowlist per destination rather than a catch-all default (`7d3caa0`). `GOAL_CODES` (routed to Correct Match Record / Remove Goal) now also includes `unattributed_goal` and `unattributed_own_goal` (both genuinely correctable/removable, previously omitted); a new `MATCH_REPORT_CODES` allowlist replaces the old "everything else goes to Match Report" default, listing only codes Match Report can actually edit (ratings, Player of the Match, report text); every other code (selection/incident/goalkeeper/location integrity) now correctly receives no Match Report recovery link rather than a misleading one.
- Both fixes are validated by `tools/validate-team-workspace-overview-shell-polish.php` (part of the same 326-check total cited below).

## Deferred / out of v1 scope

Not implemented, not scaffolded: Verified Historical Appearance, Verified Historical Assist Attribution, Historical Registration as candidate evidence, reliable effective-dated Team-assignment history, and a longer-term unified historical-participation evidence model. See `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s "Historical Match Participation Evidence — Deferred Opportunities" section. (Match Hero Goal-Scorer Presentation, formerly tracked here as a required Pre-MVP item, is now complete — see "Match Hero Goal-Scorer Presentation (CMC-003)" below.)

---

# Match Hero Goal-Scorer Presentation (CMC-003)

**Status:** Complete. Implemented, source-validated, browser-accepted, committed and pushed to plugin `main` at `b37de1c` ("feat: add match goal scorers to result heroes"), with a live-eligibility correction (`ff73ae6`) and responsive/half-width polish (`0b8d21b`) landing in the same arc.

**Goal:** Present Club goal scorers beneath the Match score in familiar football-result style on both live Match Mode and completed-Match presentation, sourced from canonical active Match goal incidents only.

## Scorer hero component and integration

**Status:** Complete (`b37de1c`).

- `MatchGoalScorersCard` (new, `app/core/UI/Components/MatchMode/MatchGoalScorersCard.php`) is the sole owner of scorer grouping/formatting: same-Player multi-goal consolidation (`David Adel 12′, 48′`), penalty suffix, neutral `Own goal`/`Scorer not recorded` entries, exclusion of opponent goals and voided/superseded incidents, and correct 0′-vs-null-minute handling (a stored `0` renders `0′`; a genuinely missing minute renders nothing).
- Composed directly inside `MatchModeScoreCard`'s own scoreboard grid via an optional, backward-compatible 5th `$incidents` parameter (an output-buffer-and-wrap technique) — not as an external sibling — associated with whichever column the Club's own side occupies. Shared verbatim by live Match Mode, the Coach completed-Event hero and the three focused sub-action pages (which simply omit the parameter and are unaffected).
- The privacy-minimised participant Match Story (`CompletedParticipantMatchExperience`) renders the same component directly against `CompletedMatchExperienceService`'s own narrow, 7-field `club_goal_scorers` projection (active/incident_type/goal_mode/goal_type/scorer_person_id/scorer_name/minute only — never assist/void/audit/rating/Coach-note fields).
- Ordinary Correct Match Record corrections and Verified Historical Scorer Attribution (CMC-002) both flow through automatically — no separate wiring per correction pathway, since both write through the same canonical active-incident data `MatchGoalScorersCard` reads.

## Participant scorer-name fix

**Status:** Complete (part of `b37de1c`'s arc).

Browser acceptance found a Player/Parent completed-Match Story showing "Scorer not recorded" for a Match where the Coach view showed the correct name. Root cause: `CompletedMatchExperienceService::build()` sourced incidents via `MatchIncidentRepository::active_for_event()` (an unjoined query with no `scorer_name`), while Coach paths use the joined `for_event()`. Fixed by switching to `for_event()` plus an explicit PHP `array_filter()` on `$row['active']` to preserve the original active-only semantics.

## Live attribution eligibility correction

**Status:** Complete (`ff73ae6`, "fix: align live goal eligibility with on-pitch state").

Browser acceptance on a synthetic live Match found the Goal Scorer/Assist dropdowns missing Players who were shown as Current On Pitch — confirmed **not** a CMC-003 regression (zero diff on the relevant files at the time), but a pre-existing rule violation newly surfaced by testing. `MatchLivePlayerEligibilityService::project()` was double-filtering: the on-pitch set (from Selection/substitution replay) was correct, but a second pass then additionally required an Attendance row of Present/Late, silently dropping an on-pitch Player with **no** Attendance row at all.

Fixed narrowly: an on-pitch Player is now scorer/assist eligible unless they carry an **explicit** non-Present/Late Attendance status — a missing row no longer disqualifies, but an explicit Absent/Excused status still does (this distinction was deliberately preserved after it was found to be independently asserted by `tools/validate-match-substitution-attendance-eligibility.php`). Available Bench Players remain ineligible until legitimately admitted (`MatchLiveBenchAdmissionService::admit()`/`effective_selection()`, which still requires Present/Late) or substituted onto the pitch. `MatchGoalService`'s server-side write validation calls the same `project()` method, so this one fix corrects both the dropdown candidates and write-time enforcement together.

## Focused-action and half-width responsive polish

**Status:** Complete (`0b8d21b`, "fix: polish match score hero responsive layout").

- The focused Goal Attribution/Substitution/Change Goalkeeper score card no longer stretches vertically merely to match a taller adjacent form (`align-items: start` on the focused-action grids, matching normal Live Match Mode's own already-correct behaviour).
- Team names now scale relative to the score card's own container width (`container-type: inline-size` + a resilient `clamp()`), not the viewport — fixing character-by-character breaks (`U7 / GO / LD`) that occurred whenever the card was narrower than the viewport assumed (a two-column desktop split, a focused-action card, or an actually-narrow viewport).
- The scorer list switches to one entry per line (bullet suppressed) below a safe card width, guaranteeing a Player name and minute never separate onto different lines regardless of how many scorers there are.
- All CMC-003 scorer grouping/semantics (consolidation, penalty, own goal, unattributed, 0′/null-minute, opponent/voided exclusion) are unaffected — this batch never touched `MatchGoalScorersCard::build_lines()`.

## Validation

- `tools/validate-match-goal-scorers-hero.php` (new) — 94 checks (component grouping/formatting, privacy-minimised projection, call-site integration, responsive resilience).
- `tools/validate-match-goal-live-eligibility.php` — extended with the live-eligibility correction fixture.
- `tools/validate-event-detail-batch1-mobile-redesign.php`, `tools/validate-dark-surface-contrast.php` pass unaffected.
- Browser acceptance confirmed on both live Match Mode and completed-Match presentation, at desktop and 320px, including the Rochester City/U7 Gold long-name and multi-scorer half-width cases.

---

# Primary Immersive Module Accent-Top Consolidation

**Status:** Complete (`54edcb2`, `5616f8b`).

**Goal:** Establish one reusable primitive for the restrained club-accent top-edge treatment already used independently across Team Events/Attendance/Statistics, Match Report, Correct Match Record and Event Detail, and close the remaining gaps on Match Mode, Match Recovery/Match Details, the main Events header and the Matchday Hub hero — without redesigning any already-accepted surface.

## Match Mode gold-trim polish

**Status:** Complete (`54edcb2`).

- Match Mode's own cards (Live Score, Match State, Current On Pitch, Available/Unavailable Bench, Starting Lineup, Other Matchday Players, Match Incident Timeline, Available player audience, Staff) converted from a one-off gold left rail to the established gold top-edge treatment, scoped to `.iexel-match-mode .iexel-match-mode-card:not(.iexel-attendance-change-card)` so `EventAttendancePage.php`'s own, unrelated reuse of the same shared class is untouched.
- Match Recovery and Match Details (the same shared `<details>/<summary>` disclosure) now use the same 2px accent border as the page's premium navigation controls (`.iexel-workspace-back`, "Back to Matchday Hub") in their resting/collapsed state, not only once expanded. Expand/collapse behaviour, the disclosure arrow, focus treatment and Recovery's own Undo Last Goal/Substitution/Goalkeeper Change content are all unchanged — **Undo Last Goal was not removed or moved.**

## Reusable primitive + remaining header gaps

**Status:** Complete (`5616f8b`).

- Introduced `.iexel-accent-top-module` (`assets/css/public.css`) as the one reusable primitive, deliberately the smallest safe property footprint (`border-top` only). Because a bare single-class rule was found to lose the cascade to a consumer's own pre-existing `border` shorthand at equal specificity, real consumers are paired with the modifier class in a compound selector rather than relying on source order.
- **Main Events header** (`EventsWorkspace.php`, `.iexel-events-workspace-header`) now carries the primitive, its legacy left rail removed. `.iexel-event-card` (the cards below it) already had the top-accent treatment from earlier work and was not touched.
- **Matchday Hub hero** (`MatchdayHeroCard.php`, `.iexel-matchday-hero`) now carries the primitive — the one genuine gap an audit found (a dark, page-level primary module with no accent treatment at all, unlike `MatchReadinessCard` immediately below it). Matchday Hub's own light (`#fff`) operational grid cards (Quick Actions, Selected Squad, Attendance, Venue, Emergency Contacts, Timeline, Register Progress) are a deliberately different card language and remain untouched.
- **Team Availability** was audited and found **already correctly treated** by a later, more complete "Final MVP Polish" rule (`.iexel-team-availability-tab .iexel-team-attendance-hero`) that an earlier read-only audit had missed — no production change was needed or made.
- **TeamEventForm** remains deliberately excluded — an interactive task/form surface, not a primary information module.
- The main Events workspace is intentionally shared across every portal persona (Parent, Player, Coach, Secretary, Treasurer, Welfare, Committee) — the header treatment's multi-role reach is deliberate, not a permissions/workspace leak.

## Validation

- `tools/validate-match-mode-gold-trim.php` (new) — 10 checks.
- `tools/validate-accent-top-module-primitive.php` (new) — 17 checks (primitive existence/token, both new consumers, TeamEventForm/`.iexel-os-card`/nested-row/semantic-card exclusions, Match Mode's and main Events' pre-existing treatments unaffected).
- `tools/validate-event-detail-batch1-mobile-redesign.php`, `tools/validate-dark-surface-contrast.php`, `tools/validate-events-workspace.php`, `tools/validate-team-workspace-route-and-display.php` all pass unaffected.
- Browser acceptance confirmed at desktop and 320px across Main Events, Matchday Hub, Team Availability (regression) and Match Mode (regression).

## Known validator debt (unrelated to this work)

Several DB-integrated Match Mode validators (`validate-match-mode-attendance-live-squad.php`, `validate-match-mode-player-actions.php`, `validate-match-substitution-attendance-eligibility.php`, `validate-live-bench-admission.php`, `validate-match-goal-live-eligibility.php`) share a pre-existing dev-fixture assumption that Person 19 is a genuine current Team-1 Player, which does not hold on this dev database (Person 19 is currently a Team-6 Player there). This predates the CSS/eligibility batches above and produces the identical failure at the identical assertion count regardless of which of them is run — confirmed unrelated by direct comparison. Do not change production behaviour or seed data to silence it.

Separately, some older visual-polish validators (e.g. `tools/validate-team-attendance-final-polish.php`, `tools/validate-team-workspace-overview-shell-polish.php`) include an in-flight "changed set" self-check (`git status`/`git diff --stat` against a hardcoded expected file list) written for their own original batch. These fail whenever run against a clean, fully-committed tree, or during any later, unrelated batch — a structural mismatch between how they were authored (a pre-commit self-check for one specific batch) and how they get invoked later, not a product regression. Treat as validator technical debt.

---

# Team Events & Attendance Month-Disclosure Navigation

**Status:** Complete (`082e418`, "feat: add month navigation to season history").

**Goal:** Replace the earlier fixed-batch-size "Past Events" progressive disclosure (load 5 more at a time) with calendar-month grouping, so a Team's history reads as recognisable football seasons rather than an arbitrary reveal count, and extend the same pattern to Attendance history.

## Reusable primitive

- `MonthDisclosureGrouping` (new, `app/core/UI/Formatting/MonthDisclosureGrouping.php`) is a small, stateless grouping/labelling helper extracted from `PlayerStatisticsMatchHistoryCard`'s own already-working, responsive-validated month-disclosure pattern — that original component is left completely unchanged and was not migrated onto the helper in this batch. Callers must pre-sort records themselves; the helper only buckets in encounter order by calendar month (`F Y`), plus an explicit-plural record-count label (`count_label()`) rather than a naive `+ 's'` default.

## Consumers

- `TeamEventsList::renderPast()` — Team Past Events now use month-disclosure grouping in place of the old fixed-size "load more" batches (`PAST_EVENTS_BATCH_SIZE` removed). Upcoming Events is deliberately untouched (unconditional full render) — only historical navigation was the reported pain point.
- `TeamCompletedRegistersCard` — Completed Attendance registers gained the same month-disclosure treatment.
- `EventsWorkspace` (Portal) and `TeamAttendanceService` were extended in the same arc to support the new grouping at their respective call sites.
- Latest month opens by default; older months collapse — the same convention later reused verbatim for Shared Messages (see "Shared Messages Month-Disclosure Navigation" below).

## Validation

- `tools/validate-month-disclosure-navigation.php` (new) — 348 lines of checks covering the grouping helper and its consumers.
- `tools/validate-events-workspace.php`, `tools/validate-player-team-events-navigation.php` extended/re-passing.

---

# Coach Workspace Release-Readiness Polish

**Status:** Complete (`e796f19`, "fix: polish coach workspace release readiness").

**Goal:** Close a small set of visual-polish items surfaced during release-readiness review, without touching business logic.

## Changes

- **Venue Control Presentation — resolved.** The Event Builder's Venue Type radios (`Existing Club Venue` / `One-off Venue`) previously rendered as bare, unstyled radio labels — noted as visually basic during SEC-008 acceptance (see `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s former "Venue Control Presentation" entry, now updated to reflect this fix). `TeamEventForm.php` now wraps them in `.iexel-team-venue-modes`/`.iexel-team-venue-mode`, the same card-row visual language already established for `.iexel-team-audience-mode` — no new pattern invented.
- **Matchday Selection formation-code badge.** `MatchdaySelectionCard` gained an optional `$formation_code` parameter, rendered as a small badge beside the card heading (e.g. alongside "Starting XI") when a valid formation is set.
- Small, mechanical class/markup touch-ups across several Matchday/Attendance components (`AttendanceBulkActionsCard`, `AttendanceHeroCard`, `AttendanceProgressCard`, `ReadonlyLineupPitch`, `MatchRatingsCard`, `MatchdayAttendanceCard`, `MatchdayEmergencyContactsCard`, `MatchdayQuickActionsCard`, `MatchdayTimelineCard`, `MatchdayVenueCard`, `PortalSection`, `MatchdayHubPage`, `MemberExperienceService`) — presentation-only, no permission or data changes.

## Validation

- Existing Matchday/Attendance/Event Builder validators re-pass unaffected; no new dedicated validator was required for this polish-only batch.

---

# Coach Workspace Batch B — Statistics Navigation, Inline Availability Editing & Return-to-Context

**Status:** Complete (`a9c5dc7`, "fix: close out coach workspace release readiness").

**Goal:** Close out the remaining Coach Workspace release-readiness gaps: a dedicated Statistics landing for a multi-Team Coach, inline Player-response editing directly from Event Detail, and returning the Coach to the section they just acted on rather than the top of a long page.

## B1 — Statistics navigation / Team chooser

`PortalCoachStatisticsChooserPage` (new) is the "Statistics" top-nav landing for a Coach/Manager who manages more than one Team (the single-Team case is resolved directly by `MemberExperienceService::navigation()` with no chooser needed). It reuses `PortalTeamsPage.php`'s exact accessible-Team source (`Relationships::accessible_team_summaries()`, the same authorisation boundary already used by every other Team-selection surface) and its established `.iexel-my-teams`/`.iexel-my-team-card` markup verbatim — no new query, no new visual language, no new permission boundary. Wired into `PortalRouter.php`'s `statistics` portal section. The destination itself (`TeamWorkspacePage`'s Statistics tab) retains its own independent authorisation check; this page is a navigation aid only, not a second security boundary.

## B2 — Inline Coach Team Responses availability editing

The former standalone `CoachAvailabilityUpdateForm` dropdown (a separate control below the response lists) is replaced by an inline per-Player editor directly inside the existing `AvailabilityPanel` list: `AvailabilityPanel::render()` gained optional `$event_id`/`$editable_person_ids` parameters, and a Player's name becomes a `<details>` disclosure containing a small Response select + Save button only when both are supplied and that Player's id is in `$editable_person_ids` (which must already be the exact canonical eligible-Player set, `MemberPortalService::coach_availability_players_for_event()` — the same source the former standalone dropdown used). This is a new **presentation** entry point into the existing `update_player_availability_as_coach()` write path — there is still exactly one Availability writer, and its own independent authorisation check (`can_manage_player_availability()`) is the real enforcement boundary regardless of what the panel shows. The separate "Coaches Attending" panel (Coach/staff data, not Player Availability) is explicitly excluded from becoming editable here.

## B3 — Return-to-context on redirect

Event lifecycle actions (schedule/cancel/complete/archive, `EventLifecycleRequestHandler`) and the new inline availability write (`MemberPortalService::redirect_coach_availability_result()`) now redirect back to the specific section the Coach just acted on (`#event-responses` / `#team-responses` via the existing `ContextAnchor` primitive — the same mechanism the sibling RSVP-reminder redirect already used) instead of the top of a potentially long Event Detail page. The fragment is a server-chosen literal, never derived from request data.

## Validation

- `tools/validate-coach-workspace-batch-b.php` (new) — 380 checks.
- `tools/validate-event-detail-batch1-mobile-redesign.php` extended/re-passing.

---

# Live Match Transient Success Notice Auto-Dismiss

**Status:** Complete (`22a18fd`, "fix: auto-dismiss live match success notices").

**Goal:** A live Match Mode success notice (Goal added, Substitution made, Lineup saved, etc.) should clear itself after being read, rather than sitting on screen until the Coach's next action; error/warning notices must never be affected.

## Implementation

`MatchModePage::notice()` marks **only** success-type notices with `data-iexel-transient-notice="1"` — error notices never carry this attribute. A new, small progressive-enhancement script (`assets/js/match-mode-notice.js`) removes the marked notice from the DOM and clears its query-string parameters (`match_notice`, `match_notice_type`) via `history.replaceState()` after 5000ms. Every live Match action is a POST → canonical write → `wp_safe_redirect()` → fresh GET, so at most one notice can exist on a given page load — there is no client-side stacking case. If the script fails to run, the server-rendered notice simply remains visible (the pre-existing behaviour) — it never disappears instantly or depends on JS for correctness.

## Validation

- `tools/validate-live-match-transient-notice.php` (new) — 196 lines of checks.

---

# Shared Messages Month-Disclosure Navigation

**Status:** Complete (`fc9dc8a`, "feat: improve shared messages navigation and presentation").

**Goal:** Apply the same calendar-month disclosure grouping established for Team Events/Attendance (see "Team Events & Attendance Month-Disclosure Navigation" above) to the shared Messages/Club Announcements history, so a long announcement history reads as recognisable months rather than one long undifferentiated list.

## Changes

- `PortalAnnouncementsPage.php` reuses the same `MonthDisclosureGrouping` helper (no second grouping implementation) to bucket the recipient's visible announcement/communication history by month. The latest month opens by default; older months collapse — matching the Team Events/Attendance convention exactly.
- Individual conversation/announcement **detail** view was **not** month-grouped — only the list/history view. Announcement previews preserve meaningful text structure (not a naive character-truncated snippet).
- Presentation now uses the established premium midnight-navy/accent-top card language consistent with the rest of Club OS's immersive surfaces.
- One shared, recipient-based Messages experience remains canonical (see `MASTER_DEVELOPER_GUIDE.md`'s "Channel-Neutral Communications" rule) — this batch did not introduce a role-specific Messages store or a second Communications architecture.
- **Explicitly not introduced in this batch:** unread counts, filtering, search or pagination. Do not describe any of these as delivered.

## Validation

- `tools/validate-shared-messages-month-navigation.php` (new) — 449 lines of checks.

---

# Event Builder Productivity & Training Only Event Audience Eligibility

**Status:** Complete (`1c97ebb`, "feat: improve event builder productivity and audience eligibility"). Implemented across several acceptance rounds with the Product Owner, source-validated and committed/pushed to plugin `main`.

**Goal:** Reduce repetitive Coach Event Builder effort (optional End Time, Duplicate Event, weekly recurrence) and correct a genuine Training Only Event-audience gap the Product Owner found in real browser testing, without weakening League/Fixture competitive eligibility protections or requiring a fake Team Assignment for Training Only Players.

## 1. Optional Event End Time

`EventRepository::clean_data()` now stores a genuinely blank End Time as `null` (the `events.end_time` column was already nullable — no migration) rather than silently coercing an empty string into a fake `00:00:00`. `start_time` handling is unchanged. The end-before-start validation (create and edit) remains conditional on both times genuinely being present. `EventChangeNotificationService` renders the word "Not set" for a blank before/after change value instead of a dangling arrow with nothing after it.

## 2. Duplicate Event (safe, non-Match types only)

A "Duplicate Event" action opens the **existing** Create Event form pre-filled from the source Event — it never immediately clones/persists anything, and the new Event is created only once the Coach reviews and submits normally through the unmodified `handle_create_event_request()` writer. The source Event is completely unaffected; no `duplicate_from_event_id` or similar provenance field was added to the schema (`EventRepository::duplicate()` — a pre-existing, unused method — was left untouched, not repurposed). Restricted to non-Match types (Training/Tournament) — Fixture/Friendly keep their own Match/fixture-specific setup and are not reachable through this productivity shortcut. Lifecycle/cancellation state, RSVP responses, Attendance and Match data (selections/incidents/statistics) are never part of the prefilled values.

## 3. Cross-Team Duplicate Event

A Coach, Manager or `iexel_manage_club_os` holder who manages more than one Team can change the **destination Team** before creating the duplicated Event (a `<select>` with server-precomputed per-option destination URLs, since the destination Team is a URL path segment, not a query parameter). Both source and destination Teams are independently re-authorised server-side against the same canonical `Relationships::accessible_team_summaries()` source already used elsewhere (never trusting the request's `team_id`/`duplicate_from`) — a fabricated or unauthorised Team fails closed. The destination audience (including its Same-Age-Group/Training Only candidates, see below) is always re-derived fresh from the **destination** Team's own current context; source-Team Person IDs are never copied blindly across Teams. Same-Team Duplicate continues to work exactly as before. Venues are club-wide (not Team-scoped), so a prefilled venue remains valid across the destination change with no re-derivation needed.

## 4. Weekly Recurring Events

Available on the CREATE form only (never Edit), for non-Match types only. Each requested occurrence (weekly, 1–4 week interval, first occurrence included in the count, server-side hard cap of 12 regardless of client input) is created through the exact same `EventRepository::create()` call a single Event uses — there is deliberately **no** recurrence-series entity, no `parent_event_id`, and no "edit all occurrences" behaviour. Every generated occurrence is a fully normal, independent Event from the moment it is created. Multi-occurrence creation is wrapped in one transaction — a partial failure rolls back the whole submission rather than reporting false success. The Repeat control's weekly-configuration fields (interval, occurrence count, explanatory note) are hidden whenever "Does not repeat" is selected and shown only for "Weekly" — a genuine CSS cascade-origin bug (an author-stylesheet `display: grid` rule always beats the browser's own `[hidden]{display:none}` rule at equal specificity, regardless of source order) was found and fixed with a `:not([hidden])` scope, not a JavaScript change (the toggle script itself was already correct on both load and change). Monthly/advanced recurrence was **not** implemented — do not describe it as available.

## 5. Training Only Event Audience Eligibility

**Root cause of the reported gap:** `TeamEventAudienceOptions::for_team()` only ever queried `team_assignments` for a Team's player pool. A Training Only Player has **no** `team_assignments` row at all by design (`TeamAssignmentRepository::validate_training_only_conflict()` actively refuses to create one while an active Training Membership exists) — so they were structurally unreachable from any audience surface built on that query alone, regardless of Event type.

**The fix:** `TeamEventAudienceOptions::for_team()` gained an explicit, additional Training Only candidate pool sourced from `TrainingMembershipRepository::for_age_group()` — the same canonical Training Membership query the Secretary Training Members workspace already uses — scoped to the current active Season and the Team's own age group (normalised via the existing `AgeGroupKey`, which already reconciles Team `age_group`'s "U7"/"UNDER 7" spelling variants). **Training Membership remains the sole and canonical source of truth for Training Only participation — no Team Assignment is created, read, or required to make a Training Only Player visible in any Event audience surface.** The same active/current registration bar already applied to every other candidate applies identically here; inactive Persons, an ENDED (former) Training Membership, a Training Membership scoped to a different age group, and a fabricated/nonexistent Person ID are all excluded (the last one silently, via the same `array_intersect()` pattern that already drops any other ineligible submitted ID — no new validation-error path).

**Where Training Only Players now appear:**

- **"Current Team + Same Age Group Players"** — surfaces valid same-age-group Training Only Players in a clearly separated "Training Only" group, each row tagged with a `Training Only` badge. If no Training Only candidates exist, the section is omitted entirely (an explicit empty-state sentence covers the case where no same-age candidates of any kind exist — never a bare "Optionally add players from:" heading over nothing).
- **"Selected Players"** — additionally exposes a clearly separated Training Only group (the exact same reused markup/CSS, not a new visual treatment) alongside the plain current-Team Player list. This required the write-time computation (`TeamWorkspacePage::handle_create_event_request()`, `PortalEventEditPage::validated_audience()`) to merge in only the narrower `training_only_person_ids` subset — deliberately never the full same-age pool, which would also (incorrectly) admit other Teams' regular same-age Players into "Selected Players", a different, deliberately broader feature.

## 6. Fixture / Friendly / Tournament participation distinction — the critical safety rule

This is a deliberate, type-aware distinction, not a blanket rule in either direction:

- **Fixture (League/competitive):** normal competitive registration/eligibility protections are **unchanged**. Training Only membership does **not** create blanket Fixture eligibility — the candidate pool computed by `TeamEventAudienceOptions::for_team()` simply never contains Training Only Players when the Event type is `fixture`, enforced identically at render time and, authoritatively, at write time using the **actually submitted** type (so a hand-crafted `type=fixture` POST cannot smuggle a Training Only Person ID into a Fixture's audience — proven by a real crafted-request test).
- **Friendly:** an authorised Coach **may** deliberately admit/select an otherwise-valid Training Only Player — for both "Current Team + Same Age Group Players" and "Selected Players". This does not create a Team Assignment, does not change Training Membership status, and does not convert the Player to competitive registration. Once legitimately admitted and saved into Match Selection (the existing `MatchSelectionRepository::replace_for_event()` writer), the existing saved-selection state carries the Player through the normal lineup/Matchday Hub/Live Match lifecycle unchanged — Live Match's Goal Scorer/Assist eligibility (`MatchLivePlayerEligibilityService`) does not reject them for being Training Only, because it is scoped by the saved selection and Event audience, exactly as for any other Player. An unrelated Training Only Player (never added to that specific Event's audience) never becomes globally Match-eligible.
- **Tournament:** the current Team Event Builder's Tournament type remains a plain **Event** workflow, not the Fixture/Friendly Match Selection/lineup/Live Match workflow (confirmed by source inspection: `CoachActionsCard`'s Match-workflow gate — Match Mode / Configure Match — is scoped to `fixture`/`friendly` only). Training Only participation for Tournament is therefore governed entirely by ordinary Event-audience rules (point 5 above); there is no separate Match-lifecycle rule to state, and Tournament must not be described as having the full Match lifecycle.

**Registration/competitive eligibility and event-specific participation eligibility are two distinct concepts** — this batch broadens the latter (which Events a Training Only Player can be deliberately included in) without touching the former (which Matches count toward competitive registration/League eligibility) in any way.

## 7. RSVP and Attendance

A legitimately admitted Training Only Event recipient participates in the normal RSVP path — `AvailabilityRepository::responses_for_event()`/`summaries_for_events()` (previously gated on an active `team_assignments` 'player' row for football event types, which a Training Only Player structurally never has) now also accept an active Training Membership as equally valid evidence. Attendance eligibility already followed the saved Event audience directly (`EventAttendancePage` reads `event_audience` membership with no `team_assignments` gate) and needed no change. No separate/duplicate RSVP or Attendance system was introduced.

## 8. Write-time validation and known data-quality finding

While investigating a reported "Selected Players first row shows a blank checkbox with no name" bug (same batch, same commit), the cause was found to be unrelated to Training Only: an existing, real `team_assignments` row (Person 176) references a `person_id` with **no corresponding row in `people` at all** — a pre-existing data-integrity defect, not introduced by this batch. Because `active_for_team_role()`'s `LEFT JOIN` yields a genuinely `NULL` name for that row and its `ORDER BY p.display_name` sorts `NULL` first (MySQL's default), the orphaned row was always the *first* rendered option. Fixed using Club OS's own established fallback convention (`$player['person_name'] ?? 'Player'`, already used pervasively elsewhere — e.g. `MatchLineupForm`, `MatchModeService`, `PortalEventAudienceCard`) rather than inventing a new label; the underlying Person is never dropped or hidden, only its display text. **Person 176's missing `people` row itself remains an open data-integrity follow-up — not fixed by this batch, and not a blocker to it.**

## 9. Mobile (320px) layout

A genuine responsive bug was found and fixed: the Training Only row could overhang the card's right edge at 320px. Root-caused (not guessed) to a flex item's default `min-width: auto` (not `0`) combined with a `white-space: nowrap` badge forcing the row wider than its grid track, compounded by a mobile-only grid rule using a bare `1fr` column instead of the desktop rule's `minmax(0, 1fr)`. Fixed with `min-width: 0` + `flex-wrap: wrap` on the row, a corrected `minmax(0, 1fr)` mobile column rule, and a responsive badge-wrap treatment (badge drops to its own line, its own text never breaks mid-word) — no page-level `overflow-x: hidden` workaround, no hidden badge, no player-specific hard-coded width. Confirmed at 320px and desktop, including a long-name case.

## Validation

- `tools/validate-event-builder-productivity.php` (new) — 672 lines; static source/CSS proof for every item above (End Time, Duplicate/cross-Team Duplicate, recurrence, Training Only pool construction and type-aware Fixture exclusion, the Selected Players merge, the mobile CSS fix, and the Person-176 display fallback).
- `tools/validate-training-only-event-audience.php` (new) — 757 lines; DB-integrated, self-cleaning behavioural proof (a valid Training Only Player appears/saves/RSVPs/is Attendance-eligible in both audience modes; ended/wrong-age-group/fabricated candidates are excluded; the empty-state and cross-Team re-derivation behave correctly; no Team Assignment is ever created).
- `tools/validate-match-goal-live-eligibility.php` — extended (291 new lines) with League/Friendly Match-eligibility parity checks for both audience modes, including the Training Only Player's full downstream lineup/Live Match lifecycle once legitimately selected. **Verified in isolation only** — see Known Debt below.
- `tools/validate-dark-surface-contrast.php`, `tools/validate-event-audience-policy.php`, `tools/validate-flexible-event-rsvp.php`, `tools/validate-coach-team-event-scope.php`, `tools/validate-secretary-flexible-event-audience.php`, `tools/validate-secretary-events-management.php`, `tools/validate-event-attendee-management.php`, `tools/validate-events-workspace.php`, `tools/validate-event-lifecycle.php` all pass unaffected.
- Real browser acceptance across multiple rounds with the Product Owner, at desktop and 320px, using real dev-database Training Only Players (including the exact Player originally reported missing). All test Events/audience rows created during verification were deleted afterward; no Training Membership or Team Assignment record was ever modified during testing.

## Known debt / deferred items (not resolved by this batch)

- **Person 176 orphaned Team Assignment** — an active `team_assignments` row with no corresponding `people` row (see item 8 above). Needs a dev-database data-integrity fix, not a code change.
- **`validate-match-goal-live-eligibility.php` cannot currently be run end-to-end** — its own pre-existing baseline (an unrelated dev-fixture assumption that Person 19 is a genuine current Team-1 Player — see "Known validator debt" above) still fails identically with this batch's changes fully reverted, confirmed by direct `git stash` comparison. This batch's own new checks were verified correct in isolation (extracted and run standalone, self-cleaning, idempotent) but the full file itself remains blocked on the pre-existing Person-19 drift.
- **`validate-team-events-badge-mobile-repair.php`** has a separate, also pre-existing, unrelated breakpoint assertion failure (`.iexel-team-event-past-meta` at 480px) — confirmed via the same `git stash` technique to predate this batch entirely.
- **Secretary late-add `EventAudienceBuilder::add_attendee()`/`add_attendees_batch()`** perform no eligibility validation of their own (pre-existing characteristic, not introduced here) — worth a dedicated audit if that path is ever extended toward Training Only.
- **Raw Team `age_group` string normalisation** — Team-to-Team same-age-group matching (`active_for_age_group()`) still does an exact string match (not the normalised `AgeGroupKey` comparison Training Membership matching now correctly uses), so two Teams spelling the same age group differently (e.g. "U7" vs "UNDER 7") would not currently be matched as same-age for the *regular-player* pool. Training Only matching is unaffected (it normalises on read). Not addressed in this batch.
- **Secretary has a separate Event-creation architecture** (`PortalSecretaryEventAddPage.php` — its own ~498-line form/handler, sharing only the same `EventRepository::create()` writer). Cross-Team Duplicate was **not** built into that separate form in this batch — a genuinely separate second implementation was judged out of scope; any `iexel_manage_club_os` holder (including an admin-role Secretary in this dev environment) already gets full Cross-Team Duplicate support for free through the Coach/Team Workspace path if they reach it via that route.
- Pre-existing, unrelated items explicitly left untouched: the `venue_mode` PHP warning noted during SEC-008 acceptance; duplicated `public.css` rule blocks; the unused `EventRepository::duplicate()` method.

# Welfare Workspace Workflows

Delivered across a controlled multi-round batch (source audit → implementation → manual acceptance → a manually-rejected interim step → a final security/polish pass) and merged to plugin `main` at `5348403b36665e4960e3c6b4ac41f502d80d7a7a` ("feat: improve welfare workspace workflows"). Two accepted deliverables:

## 1. Welfare Concern Directory / mobile-filter repair

The concern directory's Search, Status, Priority and Assigned Welfare Officer filters previously used `.iexel-experience-metrics`/`.iexel-experience-metric` — a read-only stat-display component with no input/select styling of its own, which produced a browser-native appearance and a genuine ~320px overflow (the Assigned Welfare Officer select overhung its card). The fix was a pure markup change to the existing, already-responsive, already-premium `.iexel-experience-form-grid`/`.iexel-experience-field` component the adjacent Add Concern form already used successfully — **zero new CSS was introduced.** Apply Filters/Clear Filters gained the existing `.iexel-experience-form-actions` treatment. Filtering behaviour and query semantics (`search`, `status`, `priority`, `assigned_to_person_id`) are unchanged.

## 2. Welfare Updates — short operational handover log

**Purpose:** a concise way for authorised Welfare colleagues to leave an operational handover note against a Concern (e.g. "Awaiting response from league.", "Follow-up requested.", "Matter remains under review."). **This is deliberately not a detailed safeguarding case-note, allegation or evidence repository** — that distinction is a product/data-minimisation boundary, not an oversight, and must not be weakened in any future batch.

**Persistence:** a new, minimal, dedicated table registered through the existing `DatabaseManager`/`UpgradeRunner` canonical schema convention (same `table_sql()`/`install_*()`/`*_schema_valid()` trio and `UpgradeStep` registration every other canonical table uses — no separate/invented migration mechanism):

```
{prefix}iexel_os_welfare_concern_updates
  id                  BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY
  concern_id          BIGINT UNSIGNED NOT NULL
  body                TEXT NOT NULL
  created_by_user_id  BIGINT UNSIGNED NOT NULL
  created_at          DATETIME NOT NULL
  KEY concern_created (concern_id, created_at)
  KEY created_by_user (created_by_user_id)
```

No `revision` column exists on this table, and appending an update deliberately does **not** consult the parent Concern's own optimistic-concurrency `revision` — an update is an independent, additive row, not a mutation of the Concern's shared mutable fields, so two authorised Welfare Officers can each add an update without a false stale-record conflict.

**Product/MVP rules (all confirmed in source and, where practical, against a live database):**

- **Append-only.** No edit or delete capability exists anywhere in this MVP — confirmed by an explicit absence check in the focused validator.
- **No attachments, no rich text, no visibility/recipient model.** Plain text only.
- **Author is always server-derived** (`get_current_user_id()`), **timestamp is always server-derived** (`current_time('mysql')`) — neither is ever read from request input.
- **Body validation:** trimmed, rejected if empty/whitespace-only, capped at 1,000 characters (`mb_strlen`, correct for multibyte text — verified live with a 1,000/1,001-character multibyte boundary test) with **no silent truncation**; sanitised via `sanitize_textarea_field()` (the same convention the existing Concern `description` field already relies on — strips tags/rich content, preserves ordinary line breaks) and rendered via `nl2br(esc_html())`. A live XSS-payload test (`<script>alert('xss')</script>...`) confirmed the tag is stripped server-side before persistence, not merely escaped on render.
- **Ordering is newest-first, deterministically:** `ORDER BY created_at DESC, id DESC` — an explicit timestamp-plus-id sort, not accidental insertion order (the `id` tie-break matters for two updates landing in the same second).
- **Authorization is unchanged from the existing Concern model:** adding an update requires the existing `can_manage_welfare()` capability (the same gate every other Concern write action uses, including nonce/CSRF and POST-only enforcement via the shared `guard()`); reading updates follows the same `can_view_welfare()` gate as the rest of the Concern detail read. A fabricated/non-existent `concern_id` fails closed (verified live) before any row is written. A genuine non-Welfare user was confirmed live to have `can_manage_welfare()=false`/`can_view_welfare()=false`.
- **Activity History separation is the core data-minimisation guarantee:** a successful update triggers exactly one generic `ActivityLogger` entry — a fixed `"Added a Welfare update."` message plus `{reference, update_id}` metadata — and the operational text is never written into that shared, cross-domain `activity_log` table's `message` or `metadata` columns. Verified live against real Product Owner acceptance-test data: two genuine updates ("Awaiting response from league following initial review.", "League acknowledged report. Awaiting further guidance.") persisted correctly with the real author (`LOUIS HALL`) and real timestamps, while their corresponding `activity_log` rows contained only the generic message and reference/update-id metadata — no operational text leaked.
- **UI placement:** a new, clearly separate "Welfare Updates" section on the portal Concern detail page (`/club-os/welfare/concerns/{id}/#welfare-updates`), visually and structurally distinct from Timeline, Activity History and Manage Concern — reusing 100% existing `.iexel-experience-workflow`/`.iexel-experience-items`/`.iexel-experience-item`/`.iexel-experience-field`/`.iexel-experience-button` components, zero new CSS. A calm empty state ("No operational updates have been added yet.") is shown when none exist. Submission uses the existing POST/redirect/GET pattern and returns to the same Concern with the `#welfare-updates` anchor and an existing-pattern success notice.
- **Copy polish:** the section's strong introductory data-minimisation explanation was kept; a duplicated long-form restatement beneath the textarea was shortened to "Short operational updates only." without breaking its `aria-describedby` accessibility association.

**Rejected interim step — explicitly not part of the delivered state:** during this batch, "View concerns" action links were temporarily added to the Welfare dashboard's Emergency Contacts and Players Requiring Attention rows, intended to make those rows actionable by reusing the existing concern directory's `linked_person_id` filter. **Manual review correctly rejected this as semantically wrong** — a Player can have zero Welfare Concerns and still need attention for an unrelated reason (e.g. a missing emergency contact), so the link routinely led to a misleading "0 concerns found." This action, and all of its supporting plumbing (`WelfareWorkspaceUrl::concerns_for_person()`/`add_for_person()`, the directory's `person_id` filter, the Add Concern form's person pre-selection), was fully audited for other legitimate callers (none existed) and removed before commit. **Do not document this as delivered, and do not reintroduce it without a fresh product decision.** The dashboard rows remain informative-only pending a proper restricted Welfare Person experience (see "Known debt / deferred items" below).

## Validation

- `tools/validate-welfare-workspace-batch1.php` (new, 118 checks) — static source-analysis proof covering: the mobile filter-component swap and no-new-CSS guarantee; unchanged `can_view_welfare()`/`can_manage_welfare()` gates; the rejected dashboard action and its supporting plumbing being fully absent; the `welfare_concern_updates` schema/`UpgradeStep`/Kernel-wiring trio; append-only enforcement (no edit/delete anywhere); fail-closed behaviour for a fabricated `concern_id`; empty/whitespace/1,000-character-boundary body validation; server-derived author/timestamp; Activity History body-leakage prevention (checked structurally, not just by string absence); the parent Concern revision's non-involvement; the Welfare Updates section's structural separation from Timeline/Activity History/Manage Concern; the POST/redirect/GET pattern; and the copy-polish accessibility fix.
- `tools/validate-welfare-dashboard-summary-sql.php`, `tools/validate-dark-surface-contrast.php` (8,872 checks), `tools/validate-workspace-priority-alert-scoping.php`, `tools/validate-event-experience-action-leakage.php`, `tools/validate-plain-permalink-portal-routing.php`, `tools/validate-portal-header-viewing-mode.php`, `tools/validate-secretary-mobile-responsive.php`, `tools/validate-training-members-mobile-filters.php`, `tools/validate-dashboard-cancellation-notices.php`, `tools/validate-committee-permissions.php`, `tools/validate-committee-communications.php`, `tools/validate-committee-event-routing.php` all pass unaffected.
- Live, non-destructive database verification against the real dev database at multiple points in this batch: schema installation and `*_schema_valid()`, a fabricated-concern-id rejection, sequential multi-officer appends with no false revision conflict, newest-first ordering, an XSS-payload sanitisation test, a multibyte length-boundary test, and a live capability check against several real non-Welfare user accounts. All synthetic test rows created during verification were deleted afterward; the two genuine Product Owner acceptance-test updates were left in place.
- Release Readiness re-confirmed **Ready** (zero required-and-unresolved risks) with the new table present.

## Known debt / deferred items (not resolved by this batch)

- **Restricted Welfare Person projection** — not implemented at the time of this batch. No Welfare-scoped Person read route/service existed yet; the Secretary Person Profile was deliberately not exposed to Welfare. **Since implemented as Staff Compliance Batch C** (`cd871f3`) — see "Staff Compliance — Batch A, Batch B, Batch C & Batch D" below and `DEVELOPMENT_HANDOVER_2026-09-08C.md` for the current state.
- **Staff Compliance** — not implemented at the time of this batch; approved future product direction only. **Since implemented across Batches A, B, C and D** (`b5f006a6`, `3352d300`, `cd871f3`, `2bdd62e`) — see "Staff Compliance — Batch A, Batch B, Batch C & Batch D" below.
- **`validate-visual-foundation.php`** — pre-existing, unrelated `"Public stylesheet dependency order changed."` failure, confirmed via `git stash` to reproduce identically at the clean `1c97ebb` baseline with none of this batch's changes applied. Not caused by, and not repaired by, this batch.
- All items already carried forward from the Event Builder batch above (Person 176 orphaned Team Assignment, `validate-match-goal-live-eligibility.php` Person-19 drift, `validate-team-events-badge-mobile-repair.php` breakpoint assertion, Secretary late-add eligibility validation, raw Team `age_group` normalisation, Secretary's separate Event-creation architecture, the `venue_mode` warning, duplicated `public.css` blocks, the unused `EventRepository::duplicate()` method) remain unchanged and unresolved by this batch.

# Staff Compliance — Batch A, Batch B, Batch C & Batch D

Delivered across four controlled implementation batches (Batch B including one dedicated correction/repair round), merged to plugin `main` at `b5f006a66cdcd8df9e127c27da1a94b570b93514` ("feat: add staff compliance foundation"), `3352d300ab8fde56d47d307deacdab4b1f35d64a` ("feat: add secretary staff compliance management"), `cd871f38b17e1bee341b61e2b5bcba6c7e1f0357` ("feat: add welfare people and compliance workspace") and `2bdd62e536beec27f0fec663db710efa93fb59e9` ("feat: add staff compliance expiry alerts"). This is the full implementation of the Staff Compliance direction described in `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s Welfare Workspace direction section — **the canonical domain, the Secretary management slice, the restricted Welfare People/Person/Compliance projection, and proactive compliance expiry alerting are all now implemented** (see "Known debt / deferred items" below and `DEVELOPMENT_HANDOVER_2026-09-08C.md` for the current resume point and next recommended implementation position).

## 1. Canonical domain foundation (Batch A, `b5f006a6`)

**Storage:** one new canonical table, registered through the exact same `DatabaseManager`/`UpgradeRunner` trio (`table_sql()`/`install_*()`/`*_schema_valid()` + `UpgradeStep` registration) every other canonical table uses — no invented migration mechanism:

```
{prefix}iexel_os_person_credentials
  id                  BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY
  person_id           BIGINT UNSIGNED NOT NULL
  credential_type     VARCHAR(30)  NOT NULL
  credential_name     VARCHAR(191) NOT NULL
  issued_on           DATE NOT NULL
  expires_on          DATE NULL
  reference_number    VARCHAR(191) NULL
  note                VARCHAR(255) NULL
  status              VARCHAR(20)  NOT NULL DEFAULT 'active'
  created_by_user_id  BIGINT UNSIGNED NOT NULL
  created_at          DATETIME NOT NULL
  updated_at          DATETIME NOT NULL
  updated_by_user_id  BIGINT UNSIGNED NULL
  KEY person_status (person_id, status)
  KEY credential_type (credential_type)
  KEY expires_on (expires_on)
  KEY person_type_current (person_id, credential_type, status, issued_on)
```

A credential belongs to the canonical `Person`, never primarily to a WordPress user — `wp_user_id` is never required or referenced anywhere in the domain, proven live with a Person holding `wp_user_id = 0`. There is no persisted derived-status column; compliance status is always computed at read time.

**Domain (namespace `IEXEL\ClubOS\Core\StaffCompliance`):** `CredentialType` (the four approved categories `dbs` / `safeguarding` / `first_aid` / `qualification`, deliberately not an open enum but a stable, reviewed list), `CredentialLifecycle` (`active` / `archived`), `CredentialStatus::derive(?string $expires_on, ?string $as_of = null)` — a pure function mapping to `Valid` / `Expiring Soon` / `Expired` / `No Expiry` (`EXPIRING_SOON_WINDOW_DAYS = 42`, a domain constant — there is no Settings UI for this threshold), `PersonCredential` (readonly entity), `PersonCredentialValidator`, `PersonCredentialRepository`, `PersonCredentialService` (transactional writes, `ActivityLogger` integration). "Current/relevant" for a core category (`dbs`/`safeguarding`/`first_aid`) is a **read-time query concern**, never a uniqueness constraint: the newest non-archived record ordered `issued_on DESC, id DESC`. Qualifications are deliberately never collapsed to one record — a Person may hold multiple concurrent active qualifications.

**Capabilities:** a narrow, standalone pair — `iexel_view_staff_compliance` / `iexel_manage_staff_compliance` — registered in `ClubRoleCapabilityRegistrar::CAPABILITIES` (self-healing on every boot, Club Admin/administrator get every capability). Welfare Officer receives the pair directly on its WP role. Secretary receives the pair as a **direct per-user capability grant** via `OperationalRoleAccessManager::SECRETARY_STAFF_COMPLIANCE_CAPABILITIES`, re-synchronised whenever a Person's canonical roles change, with a dedicated one-off `StaffComplianceCapabilityBackfill` (`2026_09_staff_compliance_capabilities`) retroactively re-syncing already-linked Secretaries on upgrade. `SensitiveModuleAccess::can_view_staff_compliance()` / `can_manage_staff_compliance()` follow the exact existing `current_user_can('iexel_manage_club_os') || current_user_can('iexel_X')` shape used by every other sensitive-module gate. Ordinary Committee, Coach, Treasurer, Parent and Player do not inherit either capability.

**Validation (four approved categories only):** qualification-only free-text naming (Batch A shape; refined further in Batch B, see below); core-type canonical naming; issue date required, valid, not in the future; expiry optional, valid, not before the issue date; explicit field-length limits with no silent truncation; HTML/script sanitisation. Writes: `create()` / `update_administrative_fields()` (Batch A shape, superseded by `correct()` in the Batch B repair below) / `archive()` — no hard-delete action exists anywhere in the repository or service. Audit events (`staff_credential_added` / `_updated` / `_archived`) record only `person_id` + `credential_type` (+ changed field **names** on update) — reference number, note and other credential content are never written into the generic audit trail.

**Validation:** `tools/validate-staff-compliance-foundation.php` (new at the time, later extended twice — see Batch B below) — a static, standalone validator following the `validate-welfare-workspace-batch1.php` convention (no WP bootstrap, no live database; exercises pure domain classes directly, proves the rest via source-string assertions). A dedicated upgrade-path sub-task additionally proved the real `UpgradeRunner::run()` orchestration end-to-end (not just direct method calls) using a controlled, fully-reversible fixture manipulation.

## 2. Secretary Staff Compliance management (Batch B, `3352d300`)

**Person Profile integration.** The Secretary Person Profile now shows a Staff Compliance summary card for an **eligible** Person only (see "Target-Person eligibility" below) — current/relevant status per core category (semantic badge; a genuinely absent record shows a plain `Not Recorded` state and is never persisted as a fake credential row), a qualification count, and a **Manage Compliance** action. For an ineligible Person the entire block is absent — no "Not Applicable" placeholder, no three empty statuses.

**Dedicated route.** `/club-os/secretary/people/{PERSON_ID}/compliance/` (`PortalSecretaryPersonCompliancePage`, dispatched from `PortalRouter` exactly like Medical & Safety/Emergency Contact — POST goes directly back to the same route URL, never `admin-post.php`). Access requires **all three** of: an active Secretary/Admin workspace persona, the narrow `can_manage_staff_compliance()` capability (never the broader `iexel_manage_registrations` People permission alone), and the route's target Person satisfying `StaffCompliancePersonEligibility::is_eligible()`. A Welfare Officer who genuinely holds `can_manage_staff_compliance()` is still denied this route because their active persona is Welfare, not Secretary — proven live against a real Welfare Officer account. Registered in `ReleaseRouteInventory` (route + `people.secretary-staff-compliance` mutation entry) and the sensitive-response (`private`/`no-store`/`no-cache`/`noindex`) protection list.

**Page structure:** Current Compliance (DBS/Safeguarding/First Aid), Qualifications (every active qualification, never collapsed to one), Add Credential, Compliance History (previous non-archived core records plus archived records, kept structurally distinct from "current" but never automatically labelled "Archived" unless genuinely archived).

**Writes** (`SecretaryPersonCredentialRequestHandler`, orchestration only — every rule lives in the canonical `PersonCredentialValidator`/`PersonCredentialService`): `create` (Add Credential — always a new row; this is how a **renewal** is done, and it never archives the record it supersedes), `update` (a full **correction** of the same record — see below), `archive` (explicit lifecycle retirement of an erroneous/duplicate/deliberately-retired record; never used automatically on renewal, never a hard delete). Every write is POST-only, per-action-and-Person/credential nonce-protected, re-resolves the Person and the credential server-side, and re-verifies the credential belongs to the route Person before proceeding — a fabricated or cross-Person credential id fails closed with the identical, non-disclosing "could not be found" response used for a genuinely missing record.

**Correction is not renewal.** `PersonCredentialService::correct()` (renamed and deliberately broadened from Batch A's `update_administrative_fields()` during the repair round below) updates the **same** row in place — it can now correct `credential_type`, `credential_name` where applicable, `issued_on`, `expires_on`, `reference_number` and `note` — and never inserts a second row or archives any row. Correcting `issued_on` or `credential_type` can legitimately change which record the read-time "current" projection now selects for its (possibly new) category; that is an expected consequence of the query, not a lifecycle side effect performed by `correct()`. A genuine renewal remains `create()` via Add Credential, which always preserves the previous record as history.

**Credential-name behaviour is type-aware** (the final, corrected Batch B shape — Batch B's own initial round had instead forced a canonical name for all three core types; the final club-official-eligibility + responsive-UX repair round refined this to the rule below):
- **DBS** — canonical name only ("DBS Check"); the UI does not present a name field for DBS, and any submitted value is discarded server-side before it is even read.
- **Safeguarding / First Aid** — an *optional* specific "Course / Qualification Name" (e.g. "Safeguarding Children", "Emergency Paediatric First Aid"); left blank, the canonical fallback name is used.
- **Qualification** — a *required* free-text Qualification Name; deliberately no hard-coded FA/other qualification catalogue.

`credential_type` remains canonical and is what drives core-category current-record selection, status and (future) alerting; `credential_name` is descriptive only. Name resolution depends only on the *currently submitted* type, so correcting a record's type (e.g. Qualification → DBS) always re-resolves the name correctly for the new type — proven live for Qualification→DBS (arbitrary name discarded, canonical name applied) and DBS→Safeguarding (a supplied course name accepted). The Add/Edit form's Credential Type → Name field behaviour (hide for DBS; relabel "Course / Qualification Name" for Safeguarding/First Aid; relabel "Qualification Name" and mark required for Qualification) is progressively enhanced by a small, dedicated `assets/js/staff-compliance-form.js` — the same lightweight `data-*`-attribute/`change`-listener pattern already used by `assets/js/team-assignments.js`, no new JS framework — with the server remaining fully authoritative regardless of JavaScript.

**Target-Person eligibility** — a deliberate, final Batch B product rule, not merely an authorization detail: Staff Compliance is **not** presented or manageable for every Person. `StaffCompliancePersonEligibility::is_eligible()` (backed purely by the canonical, currently-active role set from `PeopleRepository::roles_for_person()` — no second role computation, no direct Team Assignment query, since Team Assignment staff roles already flow into that same active-role set) returns true only when the Person currently holds at least one of: `club_admin`, `secretary`, `treasurer`, `welfare_officer`, `committee_member` (club-wide operational roles) or `coach`, `assistant_coach`, `manager` (team staff assignments). An ordinary player-only, parent-only, or otherwise-unqualified Person is not eligible, and eligibility never requires `wp_user_id` — proven live for a Person with `wp_user_id = 0` holding only a `coach` assignment. **Target-Person eligibility is enforced identically and independently in three places** — the Profile summary card, the Compliance route's own render, and the request handler's own write path — so eligibility can never drift between "show the card" and "allow the route/write," and an authorised Secretary or Club Admin cannot manage Staff Compliance for an ineligible Person merely by visiting the URL directly or crafting a POST: both cases receive the identical "Person could not be found" 404, disclosing nothing about which case applied. **Removing a Person's final qualifying role/assignment makes the Staff Compliance UI/route unavailable immediately (recomputed live, no caching) without deleting or archiving any of their existing credential history** — proven live end-to-end (added a credential while eligible → removed the role → card/route unavailable, credential untouched and still active → restored the role → card/route available again, same historical record unchanged).

## 3. Desktop layout repair (part of the Batch B correction round)

A genuine, Product-Owner-identified desktop defect (populated Current Compliance rows collapsing to one character per line) was root-caused to a pre-existing, unscoped shared-component CSS rule (`.iexel-experience-item-actions { width: 100% }`, member-experience.css) designed for the established `.has-actions` grid layout (`PortalSection::action_item()`) but leaking into the plain flex `.iexel-experience-item` layout this page originally used, starving its content column to near-zero width and triggering `overflow-wrap: anywhere` character-level collapse. Fixed by adopting the same established `.has-actions`/`.iexel-experience-item-copy` convention already used elsewhere — **no shared CSS was changed for this part, no arbitrary fixed pixel width was introduced.** A second, genuinely necessary one-rule CSS addition was required separately: `.iexel-experience-field { display: grid }` (design-system.css) was silently overriding the browser's default `[hidden] { display: none }` behaviour for every field in the design system, so the new type-aware name field was not actually hiding despite the correct `hidden` attribute; `.iexel-experience-field[hidden] { display: none }` restores standard behaviour. Verified by rendering the real markup against the real stylesheets at desktop (1000–1440px), 768px, 390px and 320px, with computed-style measurements (not just screenshots) proving the content column returned to full width and single-line text.

## Validation

- `tools/validate-staff-compliance-foundation.php` — **108/108** (started at 99 for Batch A; +1 net after retiring one Batch-A-only "no UI exists yet" scope guard made obsolete by Batch B's own UI; +4 for the Batch B correction round's type-aware name-resolution rules; +6 for the `correct()` write-surface rename/extension — repository/service never insert a second row or archive on correction, scoped to a single id).
- `tools/validate-staff-compliance-secretary-ui.php` (new, Batch B) — **97/97** (started at 67; +7 after the correction round made every field editable; +23 for target-Person eligibility, type-aware name presentation and the desktop layout root-cause fix).
- Regression, unaffected: `validate-secretary-people-foundation.php`, `validate-secretary-person-editing.php`, `validate-secretary-person-role-management.php`, `validate-secretary-mobile-responsive.php`, `validate-welfare-workspace-batch1.php` (one stale, over-broad "no Staff Compliance term anywhere in the shared router" guard corrected to scope to that batch's own files, since the shared router is legitimately touched by many unrelated later batches — result unchanged at 118/118), `validate-committee-permissions.php`, `validate-plain-permalink-portal-routing.php`, `validate-secretary-team-assignments.php`, `validate-team-staff-operational-access.php`, `validate-admin-person-role-sync.php`, `validate-admin-person-role-dependency-guards.php`.
- Live, non-destructive database verification at multiple points across all three rounds: create/correct/archive/renewal end-to-end via the real request handler; Welfare-officer-denied-Secretary-route; cross-Person and fabricated-credential-id rejection; a Person with `wp_user_id = 0` fully holding and managing credentials; every target-Person eligibility scenario (player-only denied, club official allowed, team-only-coach allowed with no WP account, role removal/restoration with credential history preserved throughout); every credential-name rule (DBS forced-canonical, Safeguarding/First-Aid named-or-fallback, Qualification required, type-change re-resolution); the corrected desktop layout. All synthetic test data was created and fully deleted within each round; a genuine Product-Owner-created acceptance-test credential pair (Person 9) was identified during cleanup and correctly left untouched.
- Product Owner manually accepted the overall Secretary Staff Compliance experience, the corrected populated desktop layout, and 320px responsive behaviour.

## Known debt / deferred items (not resolved by this work)

- **Restricted Welfare Person projection and Welfare Staff Compliance experience** — not implemented as of Batch B; this was **Staff Compliance Batch C**, at the time the recommended next controlled implementation batch. **Since implemented** — see "Staff Compliance Batch C" immediately below.
- **Compliance expiry alerts** — not implemented as of Batch B; this was **Staff Compliance Batch D**, at the time the next recommended Staff Compliance batch. **Since implemented** (`2bdd62e`) — see "Staff Compliance Batch D" below.
- **Detailed safeguarding case-note system** — not implemented and not the same thing as the Staff Compliance administrative note, which is explicitly short and administrative-only.
- **Configurable compliance expiry threshold** — not implemented; the 42-day "Expiring Soon" window is currently a domain constant, with no Settings UI.
- **Hard-coded FA/other qualification catalogue** — deliberately not implemented; Qualification names remain free text by design.
- **Credential hard delete** — deliberately not implemented; Archive is the only retirement lifecycle action.
- **`validate-current-emergency-contact.php`** — a pre-existing, unrelated schema/data-version assertion failure, re-confirmed via `git stash` to reproduce identically at the clean Batch-A baseline with none of this work's changes applied. Not caused by, and not repaired by, Staff Compliance. Re-confirmed identical again during Batch C's own final validation pass.
- All items already carried forward from the Welfare Workspace Workflows batch above (`validate-visual-foundation.php` and the items it carried forward in turn) remain unchanged and unresolved by this work.

# Staff Compliance — Batch C (Restricted Welfare People Projection + Welfare Compliance Experience)

Merged to plugin `main` at `cd871f38b17e1bee341b61e2b5bcba6c7e1f0357` ("feat: add welfare people and compliance workspace"). Gives Welfare Officers a restricted, purpose-built People experience — **not** a duplicate of Secretary People — answering "who is this Person, what Welfare-relevant information exists, and can I maintain their Staff Compliance record" without becoming a general administration profile. Workflow: **Welfare Workspace → Welfare People → Welfare Person Profile → review appropriate Welfare information → manage Staff Compliance for eligible officials/staff.**

## 1. Welfare People inclusion rule

A single shared computation, `MemberExperienceService::welfare_relevant_person_reasons()`, unions four independent bounded existence/eligibility queries into one `person_id => reasons[]` map, reused identically by both the directory and the profile so they can never disagree about scope. A Person appears when **at least one** is true: **(A)** an active (non-closed) Welfare concern (`WelfareConcernRepository::active_linked_person_ids()`); **(B)** a current Medical & Safety row (`PlayerOperationalMedicalSafetyRepository::all_person_ids_with_current_state()`); **(C)** a current Emergency Contact row (`CurrentEmergencyContactRepository::all_person_ids_with_current_state()`); **(D)** `StaffCompliancePersonEligibility::eligible_person_ids()`. A Person matching multiple reasons appears exactly once. This is deliberately narrower than the full club roster — no new "Welfare-Person" membership table was introduced.

## 2. Welfare People directory

Route `/club-os/welfare/people/?search=...` (`PortalWelfarePeopleDirectoryPage`, backed by `WelfarePersonDirectorySnapshot`, following Welfare's own established snapshot/`MemberExperienceOperationResult` convention). A compact, data-minimised navigation/attention surface: Person name, concise relevance reasons (e.g. "Active Welfare concern · Medical & Safety on file"), and a "Review Welfare Profile" link, plus a simple in-memory name search over the already-bounded candidate set (deliberately not a new database-level search system). Rows never expose medical narrative, emergency-contact phone, credential reference numbers/notes, concern narrative, Finance/billing, home address, or Secretary/member-administration controls.

## 3. Welfare Person profile

Route `/club-os/welfare/people/{PERSON_ID}/` (`PortalWelfarePersonProfilePage`, backed by `WelfarePersonProfileSnapshot`). Denied identically ("The Person could not be found.") for a Person satisfying zero relevance reasons and for a genuinely non-existent Person — Welfare cannot browse an arbitrary Person by guessing an id. Hierarchy: **Identity** (name, photo/avatar via `BrandingService::person_image_data()`, current roles) → **Welfare Concerns** (reuses `WelfareConcernService::list_authorised()`; reference/status/priority/opened-date + "View Concern" link only, never full narrative — Welfare Updates remain the existing short operational handover log, no new case-note system) → **Medical & Safety** (READ-ONLY projection of the canonical `PlayerOperationalMedicalSafetyRepository::find_for_person()`; no new Welfare writer, Welfare was not granted `iexel_manage_registrations`) → **Emergency Contact** (READ-ONLY projection of the canonical `CurrentEmergencyContactRepository::find_for_person()`; no new Welfare writer; remains a separate domain from Medical & Safety, Staff Compliance and Welfare concerns) → **Staff Compliance** (eligible officials/staff only, see below). This is a restricted Welfare projection, not the canonical full Person administration profile — no Finance, Registration administration, Team Assignment or Secretary role-management data appears anywhere on it.

## 4. Staff Compliance on the Welfare profile

Appears **only** when `StaffCompliancePersonEligibility::is_eligible($person_id)` is true — entirely absent (never a placeholder or three "Not Recorded" badges) for an ineligible Person. For an eligible Person, data population is gated on the narrow `can_view_staff_compliance()` read capability (not the stronger manage capability), so an authorised read-only Welfare viewer still sees accurate current state; a separate `can_manage` flag (from `can_manage_staff_compliance()`) gates only the "Manage Compliance" action — preserving the Target-Person-Eligibility-vs-Current-User-Authorization distinction (`MASTER_DEVELOPER_GUIDE.md`). Shows DBS/Safeguarding/First Aid current status (via the same canonical `CredentialStatus::derive()` + shared status-badge semantics — Valid/Expiring Soon/Expired/No Expiry/Not Recorded, never club-accent/gold as severity) and a qualification count, reusing the exact same `PersonCredentialRepository`/`PersonCredentialService`/`PersonCredentialValidator`/`CredentialStatus`/`StaffCompliancePersonEligibility` classes Secretary uses — no duplicate compliance logic anywhere.

## 5. Welfare Staff Compliance management

Route `/club-os/welfare/people/{PERSON_ID}/compliance/` (`PortalWelfarePersonCompliancePage`, `WelfarePersonCredentialRequestHandler`). Supports Add Credential, Correct Credential and Archive Credential with the identical canonical semantics as Secretary: **renewal** is Add Credential → a new row; **correction** updates the same row in place; **archive** is an explicit lifecycle action; no hard delete exists. Authorization requires **both** an authorised Welfare workspace persona (`has_role(WELFARE)` + `can_view_welfare()`) **and** the narrow `can_manage_staff_compliance()` capability, plus target-Person eligibility, all independently re-verified server-side — the identical write-security architecture as Batch B (POST-only, per-action-and-Person/credential nonce with a Welfare-specific prefix, server-side Person/credential resolution, credential-belongs-to-route-Person check, PRG, fixed non-sensitive success notices; cross-Person and fabricated credential ids fail closed).

## 6. Shared Secretary/Welfare compliance architecture (small, reuse-oriented — not a broad refactor)

Batch C did **not** duplicate the Secretary compliance implementation. `PortalSecretaryPersonCompliancePage` and `SecretaryPersonCredentialRequestHandler` each had `final` removed and ~5–6 small `protected`/`protected static` accessor methods extracted (URLs, eyebrow/label copy, the request-handler/feedback class references, required persona, redirect base, nonce-action prefix) — the bulk of the original rendering/write orchestration (~250 lines of presentation, `handle()`/`handle_create()`/`handle_update()`/`handle_archive()`) remains `private`, unchanged, and proven byte-identical/behaviourally-identical for Secretary via live smoke tests before and after. `PortalWelfarePersonCompliancePage extends PortalSecretaryPersonCompliancePage` and `WelfarePersonCredentialRequestHandler extends SecretaryPersonCredentialRequestHandler`, each overriding only the small workspace-identity accessors. A separate small `WelfarePersonCredentialFeedback` class (own transient namespace) mirrors the existing Secretary/Welfare-own-feedback-class precedent used elsewhere in the codebase.

## 7. Secretary vs Welfare workspace boundary (mirror image of Batch B)

Welfare compliance management requires **both** Welfare workspace authorization **and** canonical Staff Compliance management authorization — neither implies the other. Batch B established that Welfare capability alone does not unlock the Secretary route; Batch C proved the mirror: a genuine Club Admin/Secretary-persona user holding `can_manage_staff_compliance()` was denied the Welfare compliance route because their active persona/workspace was Secretary, not Welfare. Target-Person eligibility is independently required in both directions.

## 8. Response protection & dashboard entry point

The Welfare People directory, Person profile and Staff Compliance management page all use the established sensitive-response protection (private/no-store/no-cache/noindex, via the existing `WELFARE_SECTIONS` list that already drove this check) — direct-route authorization fails closed server-side; this is never merely front-end hiding. One new Welfare dashboard action, "Welfare People" (linking to the directory), was added without redesigning the broader Welfare dashboard. The existing "Players Requiring Attention"/"Emergency Contacts" dashboard rows were deliberately **not** rewired to the new profile: those rows specifically surface Persons with **missing** information, which can mean no canonical row exists at all — exactly the case the new inclusion rule would then classify as not currently Welfare-relevant, risking a link that 404s for precisely the Persons it would most often be used for. Documented in an inline code comment in `MemberExperienceService.php`.

## Validation

- `tools/validate-welfare-people-compliance.php` (new) — **123/123**, covering Routing, Authorization, Directory population, Data minimisation, Profile, Compliance writes, Consistency, Audit and Presentation.
- Regression, unaffected: `validate-staff-compliance-foundation.php` (108/108), `validate-staff-compliance-secretary-ui.php` (**98/98**, +1 assertion proving the new `store_feedback()` reuse accessor), `validate-welfare-workspace-batch1.php` (**118/118**, one guard re-scoped to exclude `MemberExperienceService.php` — the same shared-file precedent already applied to the router in Batch B), `validate-secretary-people-foundation.php` (81/81), `validate-secretary-person-editing.php` (39/39), `validate-secretary-person-role-management.php` (262/262), `validate-committee-permissions.php` (105/105), `validate-plain-permalink-portal-routing.php` (55/55), `validate-secretary-team-assignments.php` (174/174), `validate-team-staff-operational-access.php` (55/55), `validate-admin-person-role-sync.php` (54/54), `validate-admin-person-role-dependency-guards.php` (91/91), `validate-player-medical-safety-current-state.php` (190/190), `validate-welfare-dashboard-summary-sql.php` (28/28), `validate-secretary-mobile-responsive.php` (138/138). All changed/new PHP files lint-clean (`php -l`).
- Live, non-destructive database verification: Welfare-authorised directory access; Secretary-only, Committee and ordinary-member denial; each relevance-reason combination (concern-only, medical-only, EC-only, multi-reason) appearing exactly once; a `wp_user_id = 0` eligible coach fully discoverable and manageable; ineligible-Person denial of both the profile's Staff Compliance section and the direct compliance route; role removal/restoration immediately removing/restoring both the section and route while existing credential history remained untouched throughout. All synthetic test data fully restored afterward.
- Product Owner manually accepted: the Welfare Workspace → Welfare People entry point; the People directory at desktop and 320px; the Person profile at 320px with concern + Medical & Safety + Emergency Contact + eligible Staff Compliance; Medical & Safety presentation; Emergency Contact empty-state behaviour; eligible-only Staff Compliance behaviour; and Secretary-only direct Welfare-route denial. Responsive checks passed with no horizontal overflow and no recurrence of the prior Staff Compliance min-content vertical-letter defect at desktop, 768px, 390px and 320px.
- **Secretary/Treasurer caret-browsing diagnostic (separate from Batch C's own scope, performed just before commit):** a Product-Owner-reported flashing text-insertion caret on the static Secretary Command Centre hero heading was formally diagnosed and found to be **browser caret browsing, not a Club OS editable-state defect** — plain non-attributed `<h1>` markup, `isContentEditable === false` at every ancestor to `<html>`, `document.designMode === "off"`, zero `contenteditable` usage anywhere in plugin source, and no relevant caret/editing JS/CSS. This corroborates the existing FIN-031 (Treasurer) finding — see `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s FIN-031 entries, now reconciled to reflect this conclusion. No plugin change was made or warranted.

## Known debt / deferred items (not resolved by this work)

- **Compliance expiry alerts** — not implemented as of Batch C; this was **Staff Compliance Batch D**, at the time the next recommended Staff Compliance batch, expected to link to the real destinations Batch C created (the Secretary compliance route where the active workspace is Secretary, the Welfare Person/Compliance destination where the active workspace is Welfare). **Since implemented exactly as anticipated** (`2bdd62e`) — see "Staff Compliance Batch D" immediately below.
- **Detailed safeguarding case-note system** — still not implemented; Welfare Updates remain the short operational handover mechanism.
- **New Welfare Medical & Safety writer / new Welfare Emergency Contact writer** — deliberately not implemented; both remain read-only projections of the canonical Secretary-owned entities.
- **`validate-current-emergency-contact.php`** — the same pre-existing, unrelated schema/data-version assertion failure carried forward from Batch A/B, re-confirmed via `git stash` to reproduce identically with none of Batch C's changes applied. Not caused by, and not repaired by, Staff Compliance. Re-confirmed identical again during Batch D's own final validation pass.
- All other items already carried forward from Batch A/B above (configurable expiry threshold, hard-coded qualification catalogue, credential hard delete, `validate-visual-foundation.php`) remain unchanged and unresolved by this work.

# Staff Compliance Batch D (Compliance Expiry Alerts)

Merged to plugin `main` at `2bdd62e536beec27f0fec663db710efa93fb59e9` ("feat: add staff compliance expiry alerts"). Surfaces Staff Compliance expiry risk **proactively**, through the existing operational-alert architecture, so Secretary and Welfare can act on it directly from their own dashboards. This is proactive visibility only — no credential lifecycle semantics changed, and no new notification channel was introduced.

## 1. Scope

Alerts are generated only for the three **core** credential categories — DBS, Safeguarding, First Aid — and only for two states: **Expiring Soon** and **Expired**. Qualification-type credentials never generate a Batch D alert. A genuinely absent credential ("Not Recorded") never generates a Batch D alert either — this is an expiry-risk batch, not a missing-compliance assessment; the two must not be conflated in future work.

## 2. Canonical status/threshold rule — no local reimplementation

The provider performs no date arithmetic of its own. Every status is derived via the exact canonical `CredentialStatus::derive()` already used by Secretary and Welfare, against the existing, unconfigurable 42-day `EXPIRING_SOON_WINDOW_DAYS` domain constant. Exact, live-proven boundary behaviour: expired yesterday → Expired; expires today → Expiring Soon (inclusive lower bound); +1/+41/+42 days → Expiring Soon (inclusive upper bound at +42); +43 days → no alert (Valid); no expiry → no alert (No Expiry). Date-only semantics throughout; no timezone off-by-one observed. The threshold remains a domain constant — Batch D does not add a Settings UI or make it configurable.

## 3. Current/relevant credential rule

Only each Person's current/relevant core-type record — the canonical newest non-archived row by `issued_on DESC, id DESC`, identical to `current_core_for_person()`'s own single-Person selection — can drive an alert. A new, general-purpose bulk repository method, `PersonCredentialRepository::current_core_credentials_for_persons(array $person_ids)`, generalises this exact selection across a candidate set in one query (a portable `NOT EXISTS` self-join, not a window function — none exist elsewhere in this codebase). Historical superseded rows and archived rows never independently alert: live-proven with an older-expired-plus-newer-valid DBS pair (no alert, since the current row is valid) and an archived-expired First Aid row (no alert, since archived rows are excluded by the query's own status filter). No credential lifecycle semantics were changed to achieve this.

## 4. Alert provider architecture

A dedicated `ComplianceExpiryAlertsProvider` (`app/core/Dashboard/`), modelled directly on the established `FinanceOperationalAlertsProvider` pattern: same Kernel-constructor shape, same optional-nullable-context `alerts()` signature, same standard `DashboardAlert` output — no new alert DTO, no new alert framework, no new database table, no persisted alert state (computed fresh from canonical state on every call). Registered through the existing aggregation exactly like Finance: merged inside `CommitteeOperationalAlertsProvider::alerts()` (which is how it reaches Secretary, since the Secretary dashboard snapshot reuses this provider unchanged via `MemberExperienceService`'s existing `SECRETARY => committee($context)` dispatch) and merged directly into `MemberExperienceService::welfare()` (since Welfare never goes through `CommitteeOperationalAlertsProvider`). Existing alert bridging (`dashboard_experience_alerts()`, `DashboardAlert → ExperienceAlert`) and existing sorting/deduplication (`sort_alerts()`) are reused unchanged.

## 5. Severity semantics

Expiring Soon → `DashboardAlert` level `warning`. Expired → `DashboardAlert` level `critical`, presented by the existing bridge as the established `urgent` `ExperienceAlert` state. `action_required`/club-accent/gold are never used for compliance severity — the UI's normal club-accent typography remains part of ordinary component chrome, but risk meaning comes entirely from the semantic warning/critical state plus explicit "Expiring Soon"/"Expired" labels in the alert copy, never from colour alone.

## 6. Secretary delivery/routing

Reached through the existing operational-alert aggregation (`CommitteeOperationalAlertsProvider`, reused unchanged by the Secretary dashboard). The action routes to the exact real Secretary Staff Compliance destination for that Person: `home_url('/club-os/secretary/people/{PERSON_ID}/compliance/')`. No new Secretary dashboard and no duplicate compliance page were introduced. Delivery additionally requires the active Secretary workspace persona **and** the narrow `can_manage_staff_compliance()` capability — the same two-layer check the Secretary compliance route itself already enforces.

## 7. Welfare delivery/routing

Merged directly into the existing Welfare dashboard alert flow (`MemberExperienceService::welfare()`, alongside the existing `workspace_communication_alerts()`). The action routes via the canonical `WelfareWorkspaceUrl::person_compliance($person_id)` helper to `/club-os/welfare/people/{PERSON_ID}/compliance/` — never through the Secretary route. Delivery additionally requires the active Welfare workspace persona, `can_view_welfare()`, **and** the narrow `can_manage_staff_compliance()` capability. The Batch C Welfare People entry point remains in place, unreplaced — the new alerts complement it rather than duplicating it.

## 8. Club Admin behaviour

Club Admin receives compliance alerts when operating in an eligible portal persona/workspace context (Secretary or Welfare), via the existing capability-superset override — no special-case code was needed. The `null`-context wp-admin Committee/Executive dashboard deliberately receives **no** Batch D alert, because no canonical wp-admin Staff Compliance destination exists (Batches A–C are portal-only) — this mirrors `FinanceOperationalAlertsProvider`'s own "no valid destination → no alert" pattern. This was an intentional architectural decision, not a gap: no generic Club Admin compliance dashboard was added, and no cross-persona routing was invented.

## 9. Target-Person eligibility vs current-user authorization

Alert generation still requires `StaffCompliancePersonEligibility` (reused, bulk `eligible_person_ids()`, unchanged from Batch C) — entirely separate from whether the *viewer* is authorised to see the alert. Live-proven: removing a Person's final qualifying staff/official role immediately suppressed their active expiry alert while the credential row remained stored, untouched, with no archive/delete; restoring the role immediately restored the alert, with no caching anywhere in the pipeline. An eligible Person needs no WP login of their own for their compliance state to alert (`wp_user_id = 0` proven live). Separately, expiry alerts are never broadcast merely because the target Person is eligible: the active viewer/workspace must independently be authorised, so ordinary Committee, Coach/Manager, Treasurer, Parent and Player active-role contexts receive no Staff Compliance expiry alert regardless of the target Person's eligibility — proven live for all five.

## 10. Data minimisation

Alert copy contains only: Person display name, the established credential display name (`CredentialType::canonical_name()`), Expiring Soon/Expired status, and the expiry date (existing `DisplayDate::date_only()` formatting). No credential reference number, administrative note, safeguarding narrative, medical information, Emergency Contact information or Finance data is ever exposed. No sensitive value is embedded in a URL — Person id reaches every route exclusively through `absint()`-sanitised route helpers.

## 11. Performance and deduplication

No Person/type N+1 queries: one bulk `eligible_person_ids()` call, one bulk `current_core_credentials_for_persons()` call, one bulk `find_identity_summaries()` call per `alerts()` invocation — all SQL lives in the canonical `PersonCredentialRepository`, never in the provider or any dashboard page class. Exactly one logical alert per (Person, core credential type, active dashboard/persona context); the current-record bulk query already guarantees at most one row per pair, so the deterministic `compliance-{person_id}-{credential_type}` alert id can never collide within one call. No new deduplication state was introduced — the existing, established `MemberExperienceService::sort_alerts()` key-based dedup is reused unchanged, exactly as for every other alert source.

## Validation

- `tools/validate-staff-compliance-expiry-alerts.php` (new) — **69/69**, covering Provider architecture, Status→severity mapping, Current/relevant record handling, Boundary/threshold non-reimplementation, Target eligibility, Authorization/persona delivery, Workspace-correct routing, Data minimisation, Deduplication, and Performance/architecture (no N+1).
- Regression, unaffected: `validate-staff-compliance-foundation.php` (108/108), `validate-staff-compliance-secretary-ui.php` (98/98), `validate-welfare-people-compliance.php` (123/123), `validate-welfare-workspace-batch1.php` (118/118), `validate-secretary-people-foundation.php` (81/81), `validate-secretary-mobile-responsive.php` (138/138), `validate-committee-permissions.php` (105/105), `validate-plain-permalink-portal-routing.php` (55/55), `validate-team-staff-operational-access.php` (55/55), `validate-admin-person-role-sync.php` (54/54), `validate-admin-person-role-dependency-guards.php` (91/91), `validate-welfare-dashboard-summary-sql.php` (28/28). All six changed/new PHP files lint-clean (`php -l`).
- **Validator harness dependency fix (not a product change):** `tools/validate-workspace-priority-alert-scoping.php` is a static, no-bootstrap validator that manually `require_once`s each class it depends on. Adding the `ComplianceExpiryAlertsProvider` call inside `CommitteeOperationalAlertsProvider::alerts()` broke this validator's own dependency list (class-not-found, then a class-constant-declaration-time dependency on `CredentialType`). Fixed by adding two narrow `require_once` lines to the validator itself; confirmed via source inspection that this validator's Committee/Treasurer-only fixtures never reach a Secretary/Welfare active_role, so no further mocking was needed. No assertions were removed or weakened — result remained **114/114**.
- Live, non-destructive database verification: every one of the eight required scenarios (DBS expired → critical; Safeguarding/First Aid expiring within threshold → warning; a valid core credential → no alert; a no-expiry core credential → no alert; an older-expired-plus-newer-valid pair → no alert; an archived-expired row → no alert; an eligible Person with no WP account → alert; role removal/restoration → alert suppressed then restored, credential history untouched throughout); the exact 42-day boundary sweep (today/yesterday/+1/+41/+42/+43 days/no-expiry); real end-to-end Secretary and Welfare dashboard snapshots (real WP logins) showing the correct alert with the correct workspace routing; denial for fabricated Committee/Coach/Treasurer/Parent/Player active-role contexts and for a `null` admin context, even while the acting user held admin capability; denial for a genuinely non-privileged real WordPress user forced into a Secretary/Welfare active role. All temporary credential rows deleted, the test Person's role restored, persisted test-role user-meta cleared, and the experience-dashboard cache invalidated for both test accounts afterward.
- Product Owner manually accepted: Secretary desktop (urgent alert for expired DBS, warning alert for expiring First Aid, existing Events/Registration alerts preserved, actions prominent); Welfare desktop (urgent and warning alerts visible, correct Welfare dashboard integration, action routes to the Welfare compliance destination); mobile (Secretary Priority Alerts accepted at 320px, Welfare Priority Alerts accepted at 320/390px, no horizontal overflow, no min-content/vertical-letter regression, action links readable and usable); and the compliance destination itself (Welfare compliance page accepted at 390px, canonical state agreeing with the alert for both an expired DBS and an expiring First Aid). Product Owner conclusion: **"All checks passed."** Visual severity was independently accepted as communicated through more than colour alone (explicit URGENT/WARNING labels, semantic left-border treatment, alert title/state copy) — no new icon system or dashboard redesign was required.

## DevTools 404 observation (deferred technical debt, not a Batch D failure)

During manual acceptance, the Welfare compliance destination page visibly rendered and worked correctly while the browser's DevTools Network panel showed a 404 status for the document request. This was **not treated as a Batch D blocker**: the route's content rendered successfully, the alert action landed on the correct Welfare compliance page, the functional routing validators (`validate-plain-permalink-portal-routing.php`, `validate-welfare-people-compliance.php`) both passed, and a similar development-environment status-code anomaly had been observed before in this project. The route is not believed to be broken, and this status-code behaviour is not claimed to be resolved — it was not investigated or fixed as part of Batch D and remains a separate, deferred technical-debt observation (see "Known Technical Debt / Validator Caveats" in the current handover).

## Known debt / deferred items (not resolved by this work)

- **DevTools 404 status-code observation on the Welfare compliance destination** — see above; genuinely open, deferred, not investigated in this batch.
- **Detailed safeguarding case-note system, configurable compliance expiry threshold, hard-coded qualification catalogue, credential hard delete** — all carried forward unchanged from Batch A/B/C, still deliberately not implemented.
- **Person-level missing-compliance ("Not Recorded") assessment/alerting** — deliberately out of scope for Batch D (an expiry-risk batch, not a missing-compliance assessment); not committed as approved future direction by any authoritative document at this checkpoint.
- **`validate-current-emergency-contact.php`** — the same pre-existing, unrelated schema/data-version assertion failure carried forward from Batch A/B/C, re-confirmed via `git stash` to reproduce identically with none of Batch D's changes applied. Not caused by, and not repaired by, Staff Compliance.
- All other items already carried forward from Batch A/B/C above remain unchanged and unresolved by this work.

---

# MVP Release Candidate Validation Cycle (RC-01 → RC-03-CLOSE)

**Status:** Complete. **Product Owner manual sign-off: PASSED.** Merged to plugin `main` across three focused repair commits — `a197abdd68d824890968ae0a5726e0cd0148273c` (RC-01), `73c576762d5340ddc0cfa8c12d840b1ee10b31b7` (RC-02A-R1) and `3ee4c92963e8721b5562aa3a64e3706f81a346dc` (RC-03-R1) — interleaved with five validation-only tasks (RC-02A, RC-02A closure, RC-02B, RC-03, RC-03-CLOSE) that made no source changes of their own. See `development/DEVELOPMENT_HANDOVER_2026-09-09.md` for the current resume point and the full narrative; this section is the detailed sprint-history record.

This cycle is the transition from "no currently-known unresolved High/MVP implementation blocker" (the prior targeted Release Readiness assessment) to a technically validated, Product-Owner-accepted MVP Release Candidate. **It does not represent production deployment** — see `RELEASE_CHECKLIST.md`'s separate "Release"/"Post-Release" gate for that distinct step.

## 1. RC-01 — Portal Successful-Response HTTP-Status Correction (`a197abd`)

**Defect.** `PortalRouter::render()`'s legitimate-route success path could render its full HTML output while an earlier-resolved HTTP status (frequently a stale 404 inherited from degraded/plain-permalink rewrite resolution) remained the actual header sent to the client — content was correct, status was not.

**Repair.** `ob_start(); status_header( 200 );` immediately before the successful-render output begins, with `ob_end_flush();` at the true end of `render()`. This lets any later, genuine `wp_die()`/`status_header()` call — from a dispatched page class or the router's own not-found branch — still correctly override the optimistic 200 before the buffer is ever flushed to the client. The pre-existing `is_unknown_generic_section()` 404 guard runs unaffected, before the optimistic 200 is ever set. The final "Page not found" fallback branch explicitly re-asserts `status_header( 404 );`, correctly overriding the optimistic 200 for that one genuine outcome. Every pre-existing router-level authorization/validation `wp_die(...)` guard (maintenance-mode 503, wrong-persona 403, missing-Person 400) is preserved byte-for-byte.

**Proof.** The successful Welfare compliance response body was confirmed byte-identical before and after. Real HTTP validation (genuine WordPress auth cookies) against legitimate routes across Secretary, Welfare, Treasurer, Coach and Parent personas returned 200; an unmatched section, an ineligible/nonexistent target Person, a wrong-persona request and an unauthenticated request all continued to return their original 404/403/400/302 — none were normalised to 200. `tools/validate-plain-permalink-portal-routing.php` extended 55 → 64 (structural source-level assertions; live HTTP behaviour cannot be asserted by a static validator and was proven separately, live, as above).

**Nuance preserved from the originating investigation:** the long-lived normal Dev site's compiled `rewrite_rules` option was observed stale for some newer multi-segment routes. RC-02A (below) subsequently proved this is **not** a systemic fresh-install defect: a true fresh activation correctly compiles the complete current rewrite-rule set, including the newer Secretary/Welfare People/Compliance routes. The stale-rule condition is specific to a site not reactivated since those routes were added — a distinct, separate concern from RC-01, relevant background for any future controlled-upgrade work but not something this cycle needed to fix.

## 2. RC-02A — Clean-Install Validation (disposable, no plugin commit)

Read-only-of-source validation on a disposable **IEXEL Club OS Dev RC Clean** site — WordPress 7.1, PHP 8.2.29, MySQL 8.4.0, nginx (deliberately not downgraded to the historical WP 7.0.4 reference; current expected state was derived fresh from source at `a197abd`, not forced to match historical documentation).

**Confirmed healthy:** genuine clean WordPress baseline with zero pre-existing Club OS state; normal `activate_plugin()` succeeds; schema/data version `2026.08.9`/`2026.08.9` matching source constants; `UpgradeRunner` fully current across all 36 registered `UpgradeStep`s; Staff Compliance table installed correctly, empty, with the current capability model correctly scoped (`administrator` and `iexel_welfare_officer` Y/Y, all other roles N/N — no broadening); zero bogus credentials manufactured; administrative authority does not synthesize member identity (the unlinked default administrator resolves no member experience — `MemberExperienceResolver::resolve()` fails closed); 15 system formations, 129 formation-template slots; **current rewrite rules compile correctly on normal activation** — 106 `club-os`-namespaced rules present (of 200 total) immediately after first activation, including every one of the newer multi-segment Secretary/Welfare People/Compliance routes, confirmed via direct native-match testing against `$wp_rewrite->wp_rewrite_rules()` (not merely "content rendered", the actual WordPress rewrite matcher was proven to own these routes, not Club OS's own REQUEST_URI fallback); 3-pass reconciliation byte-identical (idempotent); full deactivate/reactivate lifecycle healthy with no duplication and rewrite rules correctly recompiled on reactivation.

**P2 finding, not fixed:** the actual live database contains **51** `iexel_os_*` tables; `DatabaseManager::CANONICAL_TABLES` lists **49**. The two extra tables (`current_emergency_contacts`, `event_match_live_bench_admissions`) are legitimate, correctly-created, correctly-populated tables simply absent from the inventory list that feeds the plugin's own built-in Release Readiness table-count check — a tooling-completeness gap, not a schema defect.

**P3 methodology finding, not fixed:** `validate-welfare-people-compliance.php` falsely failed one whitespace-literal assertion when run against a `git archive`-exported copy of the RC Clean plugin tree (Windows `core.autocrlf=true` converts the canonical LF-committed source to CRLF on export), while passing 123/123 against the canonical repository checkout of the identical committed source. Zero functional/runtime impact — PHP execution is unaffected by line-ending representation. Recorded as a validation-methodology note for future RC work: run source-literal validators against the canonical checkout, not a `git archive` export, on Windows hosts.

**One genuine P1 was found** — see RC-02A-R1 immediately below.

## 3. RC-02A-R1 — No-Current-Season Team Workspace Fatal Repair (`73c5767`)

**Defect.** `SeasonRepository::create()` defaults every new Season to `is_current = 0` — the default, unremarkable state of any club's very first Season before a Secretary/Admin explicitly marks one current. `TeamWorkspacePage::render()` (`PortalRouter.php`'s `'team'` section) passed `SeasonContext::season_id()`'s nullable `?int` directly into `MemberPortalService::team_viewer_mode()`'s non-nullable `int $season_id = 0` parameter. PHP enforces parameter types at the call boundary — passing `null` here threw an uncaught `TypeError` (HTTP 500) on `/club-os/teams/{id}/`, before `team_viewer_mode()`'s own body (including its `current_user_can('iexel_manage_club_os')` early-return) ever ran.

**Root-cause proof.** Reproduced and resolved purely via test-data: `UPDATE seasons SET is_current = 1 WHERE id = 1` immediately made the identical route return 200, with zero code change — isolating the cause precisely to the absent "current Season" state.

**Repair.** `$context->season_id() ?? 0` at the single confirmed call site. Nothing else changed.

**Why this is safe (proven, not asserted).** `team_viewer_mode()` itself already treats `0` as its own established "no explicit Season, resolve current" sentinel (`$season_id = $season_id ?: absint($current?->id ?? 0)`), and when no current Season exists it already resolves this safely to `''` (not-a-viewer) — no arbitrary/historical Season is ever queried, since the function bails out via `if (!$current || ...) return '';` before any Season-scoped lookup runs. Club Admin and genuine Coach `'manager'` resolution happen *before* this check and are completely unaffected. `TeamWorkspacePage::render()` already contained a full no-current-Season empty-state architecture (`$has_context`, `$read_only`, the pre-existing `missing_current_season` warning from `SeasonContextResolver`, and `render_context_notices()`) that had simply never been reachable because the fatal occurred first — the repair does not invent any of this, it only lets the page reach it.

**Live proof (RC Clean, then reconfirmed on RC Upgrade during RC-03).** No-current-Season: `/club-os/teams/{id}/` → HTTP 200, warning card correctly present, no current-season badge, season-independent content still renders, zero new PHP errors. Current-Season: same route → HTTP 200, normal content, warning correctly absent. A genuinely non-admin unauthorized viewer received identical (non-elevated) content in both states — the repair narrowed nothing and broadened nothing.

**Product Owner manually accepted** the no-current-Season Team Workspace state at desktop, 320px and 390px, with no regression to the current-Season path.

The existing warning copy — "Season configuration warning" / "No canonical current Season is configured." — is unchanged. **This wording is minor future UX polish only, not a release blocker.**

`tools/validate-team-workspace-route-and-display.php` extended 29 → 39.

### Deferred latent finding (P2, not fixed)

`TeamStatisticsService.php:203`, inside `authorisedPlayerHubTeam()`, contains the structurally identical unguarded `SeasonContext::season_id()` → `team_viewer_mode()` pattern. It is **not independently reachable today** — its only two callers (`TeamWorkspacePage.php:486` and `:713-714`) both already short-circuit on `$has_context` before ever invoking it, and `$has_context` is false in exactly the state that would make `season_id()` null. It was not responsible for the RC-02A P1 and was deliberately left untouched, per the explicit narrow scope of the RC-02A-R1 repair batch. Classify as deferred latent hardening debt unless a future caller reaches it without that guard.

## 4. RC-02A Closure Revalidation (disposable, no plugin commit)

Reconfirmed the RC-02A-R1 repair live on RC Clean: no-current-Season Team Workspace → HTTP 200 with the warning card, no fatal, no automatic Season mutation; current-Season path unaffected; both states verified with zero new PHP errors/warnings; rewrite-rule compiled state, Staff Compliance install state and idempotence all reconfirmed unchanged/healthy.

## 5. RC-02B — Supported Existing-Club Upgrade Validation (disposable, no plugin commit)

Read-only-of-source validation on a disposable **IEXEL Club OS Dev RC Upgrade** site.

**Chosen pre-upgrade baseline:** commit `d8d9607` ("Add canonical completed match goal removal"), schema/data version `2026.08.6`. Determined via `git log -S"2026.08.6" -- app/core/Upgrade/UpgradeVersions.php` pickaxe search: `d8d9607` is the immediate parent of the commit that bumped the version to `2026.08.7`, with zero intervening commits — the last genuine point in the actual git history at exactly `2026.08.6`. Independently cross-checked: 47 `CANONICAL_TABLES` entries + 1 separately-created AI activity table = 48 total tables at that commit, matching `MASTER_DEVELOPER_GUIDE.md`'s own historical "48 Club OS-owned tables" reference for the `2026.08.6` baseline exactly; confirmed a genuine ancestor of Staff Compliance Batch A (`git merge-base --is-ancestor`); no Staff Compliance table, capabilities, or `current_emergency_contacts` table present at this commit, consistent with genuinely predating that entire body of work.

**Representative pre-upgrade existing-club fixture** (created using only legitimate production writer APIs at that historical baseline): an active/current `2026/27` Season; a Team/TeamSeason; a Coach Person with an active staff assignment; a Player Person with an active player assignment and DOB; a Parent Person with a `parent_of` relationship to the Player; an Event (fixture type, completed) with a player availability response; a Finance invoice with one line; a Welfare concern; a Player Operational Medical/Safety record.

**Upgrade method:** plugin files replaced in-place with the current committed build (no deactivation, no database reset — the plugin remained continuously "active" per WordPress's own bookkeeping throughout, matching how a real WordPress-mediated plugin file update behaves). The real production upgrade-trigger mechanism was identified by source inspection — `UpgradeAdminController` (registered on `plugins_loaded`) shows an admin-notice "Run Club OS database upgrade" button whenever `UpgradeStatus::current()->ready` is false, POSTing to `admin-post.php?action=iexel_club_os_run_upgrade`, which calls `UpgradeRunner::run('administrator')` then `UpgradeLifecycle::reconcile_schedulers()` on success. The front-end portal was independently confirmed to correctly serve its own pre-existing "Maintenance in progress" 503 guard during the genuine stale-DB window, before the upgrade was invoked.

**Result.** Schema/data reached `2026.08.9`/`2026.08.9`; `UpgradeStatus::current()->ready` became `true`; all 36 current `UpgradeStep` invariants valid; 51 `iexel_os_*` tables (matching the current-HEAD clean-install baseline exactly); Staff Compliance table created correctly with zero bogus credentials and the identical capability distribution to a clean install (no broadening); **every representative fixture record survived field-for-field, row-for-row** across Season, Team, TeamSeason, People, roles, relationships, Team Assignments, Events, availability, Finance invoice/line, Welfare concern and the Medical/Safety record; the current Season remained current (`SeasonRepository::current()` still resolved it, both at the database level and via live Team Workspace rendering); no automatic Season rollover; no duplicate TeamSeason; no silent data loss; no ownership reassignment; 106 `club-os` rewrite rules present post-upgrade, matching the clean-install baseline; formations/slots unchanged at 15/129.

**Idempotence — self-healing confirmed, not a defect.** A second `UpgradeRunner` run, executed immediately after linking a new WP admin account to an existing Coach-assignment-holding Person (a state change introduced for subsequent smoke-testing, not part of the upgrade itself), correctly reported `code: 'upgraded'` because `TeamStaffOperationalAccessBackfill::is_valid()` correctly detected the resulting genuine capability drift (the newly-linked, now-qualifying account had not yet received its direct assigned-Team capability) and `apply()` correctly repaired it. A **third, genuinely clean run**, with no intervening state change, returned `code: 'already_current'` with the schema/data version and table count unchanged. This is the reconciliation architecture's intended self-healing behaviour working correctly, not an idempotence defect — the apparent "re-run" on the second pass was caused entirely by the test harness's own intervening action, not by the plugin.

## 6. RC-03 — Final Representative Persona Validation (disposable, no plugin commit)

A representative, not exhaustive, end-to-end pass across Club Admin, Secretary, Welfare, Treasurer, Coach/Manager, Parent/Guardian, Player, shared Messages/Events/Availability, Staff Compliance, sensitive-workspace boundaries, direct-route negative testing and representative HTTP-status testing — using genuinely single-persona, non-admin test accounts throughout, having learned from earlier RC work that testing negative-authorization cases with an admin-capable account produces misleading results via the legitimate Club-Admin capability-superset override.

**Validated:** administrative authority does not synthesize member identity (a fresh unlinked admin fails to resolve any member experience, and the null-context wp-admin dashboard cannot receive a Staff Compliance alert regardless of capability — confirmed at the exact source guard, `ComplianceExpiryAlertsProvider::alerts()`'s `if (null === $context || ...) return [];`); Secretary cannot enter Welfare-only routes and Welfare cannot enter Secretary-only routes (both denied with a genuinely non-admin, single-persona account); a Coach with no assignment to a Team cannot see that Team's data; a Parent cannot access a non-linked child; a Player cannot access another Player's data; a non-Finance persona cannot reach Treasurer routes; unauthorized Staff Compliance management is denied; an invalid/nonexistent target returns 404; an unauthenticated portal request redirects (302).

**This is a representative final RC pass, not a claim that every possible user journey was exhaustively re-tested.**

**One P1 was found** — see RC-03-R1 immediately below.

## 7. RC-03-R1 — Access-Restricted HTTP-Status Correction (`3ee4c92`)

**Defect.** RC-03 live-reproduced that a genuinely non-admin Coach/Manager with no valid assignment to an existing Team, requesting `/club-os/teams/{id}/`, received the correct "Access restricted" denial *content* but at **HTTP 200** — the same RC-01 optimistic status leaking through one unprotected denial branch: `PortalRouter.php`'s `'team'` section rendered its `else` (denial) branch as plain inline HTML with no `status_header()` call of its own.

**Audit scope.** A narrow source-and-runtime audit found the identical, unprotected pattern in **12 further** inline "Access restricted" denial branches sharing the same `can_manage_team()`/`can_view_team()`/`can_view_event()` shape: Event detail (`$can_view_detail`), Event Attendance, and ten Match-Mode/Event-management sections (matchday, live, report, correction, lineup, goal, substitution, goalkeeper, match-details, and the combined audience/edit branch). Every one of the 13 branches was independently live-reproduced against the pristine pre-fix build (HTTP 200 + "Access restricted") and then against the patched build (HTTP 403, identical unmodified denial body), with legitimate authorized access to the same 13 routes reconfirmed unaffected (200 throughout) and zero new PHP errors/warnings at any point.

**`PortalFinanceWorkspacePage::restricted()` audited and deliberately left unchanged.** Every reachable Finance section already receives an authoritative `wp_die(...,403)` from `PortalRouter`'s own Finance gate (`if (str_starts_with($section, 'finance')) { if (!$context->has_role(TREASURER) || !current_user_can('iexel_view_finance')) wp_die(...,403); ... }`) before the Finance page class is ever instantiated. The underlying `iexel_club_treasurer` WP role grants `iexel_view_finance`, `iexel_manage_finance` and `iexel_manage_billing` together as one fixed bundle, applied atomically by `OperationalRoleAccessManager` — there is no real-world path to hold the first capability without the others. `PortalFinanceWorkspacePage::restricted()`'s internal calls are therefore genuinely unreachable via normal routing today. `PlayerStatisticsPage::restricted()` was confirmed to already correctly call `status_header($response)` before rendering — the established, correct pattern this repair now matches everywhere else it was missing.

**Repair.** Thirteen explicit `status_header( 403 );` calls, each inserted immediately before its existing, byte-for-byte-unmodified "Access restricted" markup. Zero denial content/markup changed. Zero authorization/capability/route-matching logic changed anywhere.

`tools/validate-plain-permalink-portal-routing.php` extended 64 → 91 (27 new assertions proving each corrected branch sets `status_header(403)`, that existing denial copy and every successful-render path are untouched, and that exactly thirteen corrections were made — no prior assertion weakened or removed).

## 8. RC-03-CLOSE — Closure Revalidation (disposable, no plugin commit)

Reconfirmed the committed `3ee4c92` build live on RC Upgrade: all 13 corrected branches → HTTP 403 with unchanged "Access restricted" content and no data leakage; the same 13 routes as the legitimate assigned Coach → HTTP 200; unauthenticated → 302; invalid/nonexistent target → 400/404 as designed; unknown route → 404; `validate-plain-permalink-portal-routing.php` 91/91; all eight directly-relevant regression validators at their established totals (`validate-team-staff-operational-access.php` 55/55, `validate-committee-permissions.php` 105/105, `validate-team-workspace-route-and-display.php` 39/39, `validate-admin-person-role-dependency-guards.php` 91/91, `validate-admin-person-role-sync.php` 54/54, `validate-secretary-people-foundation.php` 81/81, `validate-welfare-people-compliance.php` 123/123, `validate-staff-compliance-secretary-ui.php` 98/98); zero new runtime errors.

**Verdict: RELEASE CANDIDATE PASS.**

## 9. Product Owner Manual Sign-Off

Completed after RC-03-CLOSE, against the final `3ee4c92963e8721b5562aa3a64e3706f81a346dc` build.

**PRODUCT OWNER MANUAL SIGN-OFF: PASSED.**

The MVP Release Candidate is therefore technically validated and Product Owner accepted. This is distinct from, and does not itself constitute, production deployment/release — see `RELEASE_CHECKLIST.md` for that separate gate.

## Known debt / deferred items introduced or reconfirmed by this cycle (not resolved by this work)

- **`DatabaseManager::CANONICAL_TABLES` 49-vs-51 inventory gap** (RC-02A) — P2, tooling-completeness only, not fixed.
- **`TeamStatisticsService.php:203` latent nullable-Season pattern** (RC-02A) — P2, not independently reachable today, not fixed.
- **CRLF source-validator methodology note** (RC-02A) — P3 procedural note about `git archive` exports on Windows hosts, not a source defect, not fixed.
- **No-current-Season warning copy** ("Season configuration warning" / "No canonical current Season is configured.") — unchanged, minor future UX polish only.
- **Guardian Link Role Synchronisation Audit** (Product Owner observation post-RC) — **now resolved.** The audit ran, and its confirmed findings were implemented as Post-RC Guardian Link Alignment Batch 1 (`29220cc`) — see the dedicated section below, `development/DEVELOPMENT_HANDOVER_2026-09-09B.md`, and `development/CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s "Guardian Link Role Synchronisation Audit" section for final delivery detail.
- All pre-existing debt already carried forward through Staff Compliance Batch D (DevTools 404 observation, `validate-current-emergency-contact.php`, Person 19/Team 1 fixture drift, `validate-team-events-badge-mobile-repair.php`, `validate-visual-foundation.php`, Person 176 orphaned Team Assignment, Secretary late-add eligibility, raw `age_group` normalisation, FIN-031) remains unchanged and unresolved by this cycle — none of it was in scope, and none of it is a release blocker per the authoritative docs.
- **`validate-team-workspace-overview-shell-polish.php`** — a pre-existing, unrelated batch-specific git-status hygiene gate reconfirmed (via `git stash`) to fail identically on the clean baseline with zero RC-cycle changes applied; not a regression, not fixed.

---

# Post-RC Guardian Link Alignment Batch 1

**Status: Complete.** Plugin `main` `29220cc0d6be03085c5096bf6bbe3af044d01741` ("fix: align guardian relationship role handling"). This is **post-RC follow-up work**, completed after the MVP Release Candidate validation cycle above and after Product Owner manual sign-off — it does not reopen, extend, or supersede RC-01 through RC-03-CLOSE, and it is not itself a release blocker.

## 1. Origin

A Product Owner workflow observation, recorded as the "Guardian Link Role Synchronisation Audit" candidate in the RC cycle's own follow-up list (see "Known debt / deferred items" above, and `development/DEVELOPMENT_HANDOVER_2026-09-09.md`): manually linking a Person to a Player as Parent/Guardian appeared to require giving that Person the Parent role *first*. A dedicated read-only audit ran first, confirmed the observation was accurate for the Secretary's manual Guardian Links workflow specifically, and found a related Treasurer authorization question that was resolved as part of this same batch (see section 3 below). No source, docs, schema, or capability was changed during the audit itself.

## 2. Secretary Guardian Links — final behaviour

The Secretary's manual "Guardian Links" candidate picker (`PortalSecretaryGuardianLinksPage`) no longer requires an adult Person to already hold an active Parent/Guardian role to appear as a selectable candidate. The canonical write service (`PersonRelationshipManagementService::link_existing_adult()`, under `POLICY_SECRETARY`) now:

- creates the `parent_of`/`guardian_of` relationship, and
- **transactionally ensures** the corresponding canonical role (`parent_of` → active `parent`; `guardian_of` → active `guardian`) as part of the same write, inside the same relationship transaction, via a new transaction-safe role-ensure primitive (`PersonRoleManagementService::ensure_parent_guardian_role_in_transaction()`), mirroring the existing pattern already used for Player-role materialisation elsewhere in the codebase.

RELATIONSHIP and ROLE remain distinct domain concepts (see section 4). Existing unrelated Person roles are preserved; the role-ensure is idempotent (no duplicate role is created if the Person already holds it). This protection is enforced in the domain service itself, so a direct/crafted POST behaves identically to the picker-driven UI path — the picker never was, and still is not, the authorization boundary.

## 3. Treasurer — security closure

A closure review, prompted by the Secretary change above, established that a pure Treasurer (`iexel_manage_finance_relationships`) does **not** hold `iexel_manage_person_roles` — that capability is Secretary-specific, explicitly stripped from the Treasurer WP role by `ClubRoleCapabilityRegistrar`, and granted operationally only via the canonical `secretary` Person role, never `treasurer`. Because Secretary and Treasurer share the same canonical write service, an unconditional role-ensure would have let a pure Treasurer cause a role grant — a capability-gated consequence — through their narrower Finance-relationship authority.

This was corrected using the service's existing policy seam (`POLICY_SECRETARY` / `POLICY_TREASURER`), with no new WP-actor awareness added to the domain layer and no capability added, removed, or reassigned:

- Under `POLICY_TREASURER`, the adult **must already hold the role matching the requested relationship type** before a `parent_of`/`guardian_of` relationship may be created; the role-ensure primitive is never invoked for this policy.
- A genuinely roleless adult is rejected **server-side**, before any transaction begins — zero role and zero relationship side effects.
- The pre-existing incidental "cross-role top-up" (a parent-only adult being silently granted `guardian` when linked `guardian_of`, or vice versa) — traced to pristine code and confirmed **policy-blind, not an intentionally authorised Treasurer capability** — is closed the same way: Treasurer must already hold the *specific* role requested, not merely "either."
- Treasurer's candidate picker (`TreasurerOperationalReadService::relationship_candidates()`) remains role-filtered, unchanged in scope. Its per-candidate eligibility probe was corrected from a hardcoded `parent_of`-only check to checking both relationship types, so an already-valid parent-only or guardian-only candidate is no longer incorrectly hidden merely because the probe used the wrong type — a narrow correctness fix, not a widening of who can appear.

## 4. Architecture preserved: relationship vs role

RELATIONSHIP ("which adult is linked to which Player/child?") and ROLE ("which operational/persona identity does this Person hold?") remain separate domain concepts, stored separately, never collapsed. A canonical family-link workflow may ensure the corresponding role as a *consequence* of relationship creation only where the originating policy is authorised to cause that consequence — Secretary and Treasurer are not equivalent merely because both may create family relationships. See `development/MASTER_DEVELOPER_GUIDE.md`'s new "Family Relationship Role Consequences" durable rule.

## 5. Corrected characterisation of Registration and Prospect

The original audit's Registration and Prospect findings were **overstated** and are corrected here:

- **Registration:** normal current Registration matching/validation (`PeopleRepository::find_matching_parent()`'s own role-gated join, and `PlayerRegistrationValidator`'s explicit role check on a stored `parent_id`) already prevents a roleless existing adult from reaching the parent-link write through the supported workflow. The Batch-1 role-ensure added to `PlayerRegistrationService::link_parent()` is **defense-in-depth / canonical-invariant protection against future upstream validation drift**, not a fix for a currently user-reachable roleless-adult bypass.
- **Prospect:** normal current Prospect guardian matching (`PeopleRepository::find_active_guardian_candidates()`) already requires an active Parent/Guardian role via its own `INNER JOIN`. The Batch-1 role-ensure added to `ProspectConversionGateway` is defense-in-depth / canonical-invariant alignment, and is **effectively a no-op** for a currently matched existing guardian under the supported flow. Prospect conversion does not currently allow a roleless matched guardian through normal matching.

## 6. Unchanged semantics

- Removing a Parent/Guardian relationship (`remove_parent_guardian_relationship()`) does **not** automatically remove the Parent/Guardian role — unchanged. A multi-child guardian therefore retains their role when one child's link is removed.
- `MemberExperienceResolver`'s Parent-persona tolerance is unchanged: either an active role or a linked child remains independently sufficient, and both directions of that tolerance (role-without-relationship, relationship-without-role) remain non-fatal read states.
- No backfill or migration was introduced. No schema change. No capability added, removed, or reassigned.

## 7. Validation

Final focused/regression results:

| Validator | Result |
|---|---|
| `validate-treasurer-finance-relationships.php` | PASS — 264 |
| `validate-secretary-guardian-linking.php` | PASS — 70 |
| `validate-secretary-person-role-management.php` | PASS — 262 |
| `validate-admin-person-role-dependency-guards.php` | PASS — 91 |
| `validate-admin-person-role-sync.php` | PASS — 54 |
| `validate-treasurer-operational-read-access.php` | PASS — 45 |
| `validate-registration-existing-player-link.php` | PASS — 75 |
| `validate-family-relationship-integrity.php` | 70 passed / 1 confirmed baseline-only failure (pre-existing Dev-site fixture drift, reproduced identically on the pristine baseline) |
| `validate-prospect-training-conversion.php` | 1 confirmed baseline-only failure (pre-existing, unrelated TeamSeason/age_group assertion, reproduced identically on the pristine baseline) |

Runtime security proof on disposable RC Upgrade (fixtures created and fully cleaned up afterward, environment restored): Treasurer roleless `parent_of`/`guardian_of` both rejected server-side with zero role/relationship created; Treasurer cross-role top-up rejected; Secretary roleless `parent_of`/`guardian_of` both succeed with the corresponding role ensured — 12/12 security-closure checks passed.

## Known debt / deferred items (not resolved by this work)

None new. This batch introduced no new deferred debt; the two baseline-only validator failures above pre-date this batch and are unrelated to it.

---

# Treasurer Premium Workspace Alignment Batch 1

**Status: Complete.** Plugin `main` `840369102b5b1d24f7701c7d2af3b325971fa824` ("fix: align treasurer finance workspace"). This is **post-RC follow-up work**, completed after the MVP Release Candidate validation cycle and after Post-RC Guardian Link Alignment Batch 1 above — it does not reopen, extend, or supersede either, and it is not itself a release blocker.

## 1. Origin

A read-only Treasurer/Finance workspace UX audit found the Finance workspace's own `.iexel-os-card`/`.iexel-finance-metrics` visual system read as a weaker, more generic light-blue treatment than the shared premium `.iexel-experience-hero`/`.iexel-experience-section`/`.iexel-experience-metrics` vocabulary already used by Secretary, Welfare and Treasurer's own People/Team/Registration pages. The audit proposed exactly one controlled implementation batch: migrate Finance onto the existing shared vocabulary, without redesigning Finance into an immersive dark workspace and without mechanically replacing every legacy card.

## 2. Final behaviour

- **`PortalFinanceWorkspacePage`'s header, KPI strips and page sections** now use the canonical `.iexel-experience-hero` / `.iexel-experience-section` / `.iexel-experience-metrics` / `.iexel-experience-metric` components, matching the light premium administrative treatment already established elsewhere in Club OS. `.iexel-finance-workspace-header` and the page-local `.iexel-finance-metrics` component are retired (confirmed unused before removal).
- **Invoice Detail's primary invoice record is the one deliberate exception, by Product Owner direction.** After the initial light migration was reviewed, the primary invoice summary (invoice reference, recipient, season/scope, payment status, issue/due dates, financial totals) was corrected back onto the existing dark `.iexel-os-card` treatment — the same global rule used elsewhere in Club OS, reused rather than modified. The four supporting Invoice Detail sections (Itemised Charges & Discounts, Payment Allocations, Invoice Timeline, Invoice Notes) remain on the canonical light `.iexel-experience-section` register. The resulting visual rhythm is: light page identity → dark authoritative invoice record → light supporting detail sections. Do not describe this as "every Finance card is dark" or as an immersive dark workspace equivalent to Team Workspace/Matchday Hub — Finance remains a premium **light** administrative workspace with one intentionally dark authoritative record.
- **A genuine mid-batch discovery, corrected in the same batch:** `.iexel-os-card` actually resolves to a dark, gold-accented, white-text treatment via a second, later, more-specific rule in `assets/css/public.css` — an earlier read-only audit had cited only the first (non-winning) plain-light rule. This was found and corrected via live `getComputedStyle()` verification, and a related second regression was found the same way: `design-system.css` independently duplicated dark on-dark colour treatment for `.iexel-billing-schedule-card`, `.iexel-invoice-link` and their meta values (shared with several Team/Coach/Match dark-immersive components), silently overriding the first fix. Both are corrected: `member-experience.css` carries the light-surface colour fixes, and the Finance-only selectors were surgically removed from `design-system.css`'s shared dark-treatment rules, leaving every Team/Coach/Match/Player entry and the global `.iexel-os-card` rule untouched.
- **Light-surface secondary-action readability fix.** `.iexel-button-secondary` is a dark-native component; the four Finance "Back to…"/"View Detail" actions that ended up on a light `.iexel-experience-section` ancestor (Billing Runs list, Invoice Not Found, Billing Run Not Found, Billing Run Detail summary) were rendering white-on-near-white. Each now additionally carries the existing `iexel-fee-rule-back` component — already proven on the light Fee Rule/Discount Policy pages, which reach the same `.iexel-finance-workspace` wrapper via this page's own delegation — rather than a new or duplicated CSS treatment. The one dark-parent instance (Invoice Detail's own restored dark summary) is correctly left as bare `.iexel-button-secondary`.
- **Domain logic, capabilities, routing, schema and audit behaviour are unchanged.** Every diff in `PortalFinanceWorkspacePage.php` is a markup/class-attribute change; no computation, capability gate, form action, nonce or route changed.

## 3. Product Owner visual acceptance

**PASSED.** Accepted surfaces: Finance Overview, Invoices, Invoice Detail, Billing Schedules, Treasurer Dashboard, and 320px Invoice Detail. Accepted design direction: Finance is a premium administrative workspace with rich midnight/navy operational surfaces, a restrained runtime club-accent treatment (never a hardcoded literal colour), light KPI cards intentionally retained as subordinate financial summary tiles, the primary/detail authoritative surface (Invoice Detail's own record) using the richer dark treatment, accepted narrow-screen (320px) responsive behaviour, and no page-level horizontal overflow introduced.

## 4. Validation

Final focused/regression results:

| Validator | Result |
|---|---|
| `validate-parent-family-finance.php` | PASS — 44 |
| `validate-treasurer-billing-run-detail.php` | PASS — 93 |
| `validate-treasurer-directory-ux.php` | PASS — 34 |
| `validate-treasurer-finance-configuration.php` | PASS — 488 |
| `validate-treasurer-finance-relationships.php` | PASS — 264 |
| `validate-treasurer-invoice-detail.php` | PASS — 54 |
| `validate-treasurer-operational-read-access.php` | PASS — 45 |
| `validate-visual-foundation.php` | 1 confirmed baseline-only failure ("Public stylesheet dependency order changed", tied to untouched `PortalRouter.php`, reproduced identically on the pristine baseline — not introduced by this batch) |

PHP lint passed on all touched PHP files throughout. `git diff --check` clean. Non-admin genuinely-restricted Treasurer runtime verification performed on the normal Dev environment (no disposable RC Upgrade fixture available for a non-admin Treasurer persona) via a non-mutating auth-cookie-injection technique — every Finance route inspected desktop and at 320px; functional spot-check of existing Invoice Detail/Billing Run Detail records and the Manual Invoice/Record Payment forms performed read-only (forms confirmed populated and functional; no fabricated invoice/payment mutation was made).

## Known debt / deferred items (not resolved by this work)

- **Finance Reports route defect (open, not fixed).** `finance-reports` is registered as a route with its own title/intro, but the page's `match($section)` dispatcher has no case for it, and it is not linked from the page's own navigation — it silently falls through to Finance Overview content. This was deliberately identified and left unfixed as part of this presentation-only batch, per an explicit pre-edit gate. It is the recommended next small functional Finance batch; do not describe Finance Reports as currently working.
- **`iexel-fee-rule-back` naming debt (deferred).** The reused component correctly delivers the light-surface Finance secondary-action treatment (section 2 above), but its class name is narrower than its actual reuse (it originated on the Fee Rule page). This is naming/architecture debt only — the visual treatment itself is accepted — and renaming it was out of scope for this batch (it would require touching `PortalFeeRuleManagementPage.php` and `PortalDiscountPolicyManagementPage.php` too).
- **Premium Surface Colour Consistency Audit (deferred, future work).** A broader audit of Club OS's premium-surface colour consistency remains future work, not started by this batch. It must not be scoped as "make every pale card dark" or "make every Club OS page identical" — it should distinguish intentionally light subordinate cards (such as Finance's own KPI tiles) from surfaces genuinely inconsistent with the established premium hierarchy, and must preserve the immersive Team/Coach/Match Mode dark treatment where that is the correct, already-accepted design.
