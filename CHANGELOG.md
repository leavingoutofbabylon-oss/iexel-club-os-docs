# Changelog

All notable changes to **IEXEL Club OS** are documented here.

This project follows a sprint-based development process with milestone releases.

---

# Unreleased

## Match Operations MVP

### Added

- Match Readiness Dashboard with dynamic preparation and live-match status.
- Match Details configuration for opponent, competition and home, away or neutral status.
- Secure Match Mode routes within Club OS.
- Match Lineup Builder with starters, substitutes, captain and goalkeeper selection.
- Match shirt-number snapshots stored with the pre-match selection.
- Live match progression through first half, half-time, second half and full-time, plus supported terminal states.
- Transactionally maintained live score projection.
- Goal Attribution for club goals, opponent goals, club own goals and opponent own goals.
- Penalty and assist attribution where applicable, with optional opponent player names.
- Match incident timeline backed by stable incident identities.
- Durable Undo Last Goal and Reopen Match workflows.
- Grassroots Rolling Substitutions with player re-entry.
- Current On Pitch and Available Bench views derived from the saved lineup and active substitutions.
- Undo Last Substitution.
- Match action request ledger for repeat-safe undo and substitution actions.
- Matchday Hub integration for match preparation and live actions.

### Improved

- Matchday Hub readiness is calculated from current match details, lineup, availability, attendance and match state.
- Saved lineups become read-only after kickoff.
- Match Mode prioritises the actions relevant to the current live state.
- Match Details appear consistently across Event Detail, the Events listing, Matchday Hub and Match Mode.
- Times are presented in `HH:MM` format.
- Match navigation remains inside Club OS.
- RSVP and attendance submissions use Post/Redirect/Get (PRG).
- Mobile Match Mode and substitution controls are touch-friendly and responsive.

### Security

- Stored-event team authorisation for match reads and mutations.
- Server-derived team identity; posted team identifiers are not trusted.
- Event- and action-scoped nonces.
- Idempotent request keys for incident and action requests.
- Transactional score, goal, substitution and undo operations with row locking.
- Direct event-route access protection and distinct read/write permission checks.
- Event audience and eligible-player allowlists.
- Lineup eligibility enforcement, including active assignment and audience membership checks.
- Database uniqueness constraints for event-scoped selections, incidents and action requests.

### Fixed

- Repeated undo requests can no longer affect earlier goals.
- Coaches cannot access unrelated event details by changing route identifiers.
- The Events listing no longer exposes unrelated team events.
- Event Detail RSVP uses the compatible event-scoped nonce.
- Attendance saves no longer leave header warnings after redirects.
- Event times are normalised correctly.
- Opponent goals no longer require an IEXEL player.
- Goal forms no longer show fields irrelevant to the selected goal mode.
- Notice and destructive-action contrast has been improved.

---

## Sprint 19 — Team Workspace Foundation

### Added

- Team Workspace, team navigation, squad summaries, availability summaries, season statistics, quick actions and upcoming events.
- Team-specific event repository methods.

### Security

- Team-level coach authorisation, active assignment validation, administrator override and portal-based access control.

### Improved

- Coaches remain inside Club OS for team navigation and squad/event summaries.

---

## Earlier Completed Foundations

- Sprint 18 — Coach Workspace.
- Sprint 17 — Portal Shell and Matchday Portal.
- Sprint 16 — RSVP Engine.
- Sprint 15 — Event Portal.
- Sprint 14 — Events Module.
- Sprint 13 — Club Portal.
- Sprint 12 — Teams.
- Sprint 11 — People.
- Sprint 10 — Core Platform.

See [SPRINTS.md](SPRINTS.md) for delivery and validation detail.

---

# MVP Progress

**Current estimated overall progress: approximately 83%.**

Football operations are substantially complete for the Match Operations MVP. The wider club MVP still requires communications, finance, rewards, reporting and final product polish. See [FEATURE_STATUS.md](FEATURE_STATUS.md) and [ROADMAP.md](ROADMAP.md).
