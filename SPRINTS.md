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
