# IEXEL Club OS Architecture

## Purpose

IEXEL Club OS is a modular WordPress-based football club operating system. WordPress supplies authentication, user accounts, plugin runtime and website content; Club OS supplies portal-first club and football operations.

## Core Principles

- Repository-based data access and service-based business rules.
- Stored records, rather than route or form input, determine security scope.
- UI components contain presentation logic and no direct SQL.
- Pages compose components and delegate mutations to services.
- Transactions, row locks, uniqueness constraints and idempotency protect live match operations.
- Portal interfaces are responsive and touch-friendly.

## Platform Layers

```text
WordPress authentication and runtime
  → Club OS routes and permission boundary
  → Pages and reusable UI components
  → Domain services
  → Repositories
  → Club OS database tables
```

Core platform services include the application/kernel, service container, database manager, settings, modules, activity logging and portal permissions. Domain repositories cover people, teams, assignments, events, venues, audience, availability, attendance and Match Operations.

## Match Operations Services

| Service | Responsibility |
|---|---|
| `MatchModeService` | Builds the authorised Match Mode workspace from event, details, lineup, availability, attendance and incident data. |
| `MatchReadinessService` | Calculates preparation and live-status summaries for Matchday Hub. |
| `MatchEligiblePlayerService` | Builds the server-side eligible-player allowlist from active team assignments and event audience membership. |
| `MatchLineupSubmissionService` | Validates and stores the pre-match lineup, captain, goalkeeper and shirt-number snapshots. |
| `MatchPitchStateService` | Replays active substitution incidents over the saved lineup to derive Current On Pitch and Available Bench. |
| `MatchStateService` | Enforces match-state transitions, full-time completion and reopen behaviour. |
| `MatchGoalService` | Validates Goal Attribution and writes the goal incident and score projection transactionally. |
| `MatchSubstitutionService` | Validates and records Rolling Substitutions against the current derived pitch state. |
| `MatchIncidentUndoService` | Voids the most recent expected goal and reverses its score projection transactionally. |
| `MatchSubstitutionUndoService` | Voids the most recent expected substitution and protects repeated undo requests. |

Supporting services include match detail submission, score projection, state normalisation and shirt-number resolution.

## Match Operations Repositories

- `MatchDetailsRepository` owns the one-per-event match configuration and projected score/state row.
- `MatchSelectionRepository` owns the saved pre-match lineup baseline.
- `MatchIncidentRepository` owns the append-only goal/substitution ledger and action-request claims.
- Existing event, attendance, availability and event-audience repositories supply the surrounding matchday context.

Database access remains inside repositories. Transaction-owning domain services coordinate repository calls but UI pages and components do not execute SQL.

## Authoritative Data Rules

- The stored event is authoritative for identity, event type, date, time, venue and team.
- Match Details stores opponent, competition, home/away/neutral location, projected score and match state.
- Match selections store the immutable pre-match baseline after kickoff, including role, order, position, captain, goalkeeper and shirt-number snapshots.
- Active match incidents are the authoritative live ledger for goals and substitutions.
- Score columns in Match Details are projections maintained transactionally from goal actions and undo.
- Current on-pitch and bench state is derived by replaying active substitution incidents over the saved lineup.
- The activity log is audit-only and is not used to reconstruct match state.
- A mutation requires authorisation against the team on the stored event.
- Posted event, team, person and role values are treated as requests and validated against stored allowlists and current state.

## Request Lifecycle

```text
Route event ID
  → load stored event
  → derive stored team
  → authorise
  → validate event/action-scoped nonce
  → lock rows
  → validate current state and allowlists
  → mutate transactionally
  → write audit metadata
  → commit
  → PRG redirect
```

Read routes first apply event visibility rules. Write routes additionally require `can_manage_team()` for the stored event team. Administrator capability provides the deliberate club-wide override.

## Match State and Projections

The normal live progression is:

```text
Not Started → First Half → Half-Time → Second Half → Full-Time
```

Supported terminal alternatives include abandoned, postponed and cancelled where allowed by the state rules. Reopen Match changes Full-Time back to Second Half and clears the finished timestamp. Extra time and penalty shootout states are not part of the current MVP.

Goal and substitution requests use stable request keys. Incidents are never deleted during ordinary operation; undo marks an incident void and preserves its identity and audit metadata. The action-request ledger separately protects undo and substitution actions from being applied twice.

## Portal and UI Architecture

Club OS uses route-specific page classes and reusable components inside the shared portal shell. Matchday Hub presents readiness and preparation; Match Mode prioritises state, score, Goal Attribution, Rolling Substitutions and timeline actions. Match Details are reused across Event Detail, Events listing, Matchday Hub and Match Mode.

All times shown to users use `HH:MM`. Mutating form workflows use PRG so refreshes do not repeat successful actions or leave stale form warnings.

## Related Documentation

- [Match Operations](MATCH-OPERATIONS.md)
- [Database](DATABASE.md)
- [Security](SECURITY.md)
- [Roadmap](ROADMAP.md)
