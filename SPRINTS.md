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
