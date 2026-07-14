# IEXEL Club OS Database

Club OS table names use the WordPress database prefix followed by `iexel_os_`. This document uses the logical names from the plugin's database manager.

## Match Operations Relationships

```text
events
  ├─ event_match_details       one row per match event
  ├─ event_match_selections    selected players for the pre-match baseline
  ├─ event_match_incidents     ordered live goal/substitution ledger
  ├─ event_match_action_requests repeat-safe action claims
  ├─ event_audience            eligible event participants
  ├─ event_availability        RSVP response per participant
  └─ attendance                attendance result per participant

activity_log records audit metadata for important actions.
```

## Relevant Tables

### `events`

- **Purpose:** Authoritative event identity and scheduling record.
- **Important fields:** `id`, `title`, `type`, `team_id`, venue fields, `event_date`, `start_time`, `end_time`, `status`.
- **Constraints/indexes:** Primary key on `id`; indexes on `type`, `team_id`, `venue_id`, `event_date` and `status`.
- **Authoritative role:** Source of event type, stored team, date, time and venue scope.
- **Lifecycle:** Mutable through authorised event workflows.

### `event_match_details`

- **Purpose:** Match-specific configuration, current state and score projection.
- **Important fields:** `event_id`, `opponent_name`, `competition`, `home_away`, `home_score`, `away_score`, `match_state`, `started_at`, `finished_at`.
- **Constraints/indexes:** Unique `event_id`; index on `match_state`.
- **Authoritative role:** Source for opponent, competition, location and match state. Score fields are stored projections maintained alongside active goal incidents.
- **Lifecycle:** Mutable and transactionally locked for live state, goal, undo and reopen operations.

### `event_match_selections`

- **Purpose:** Saved pre-match lineup baseline.
- **Important fields:** `event_id`, `person_id`, `selection_role`, `position`, `display_order`, `shirt_number`, `is_captain`, `is_goalkeeper`.
- **Constraints/indexes:** Unique `(event_id, person_id)`; index on `(event_id, selection_role, display_order)`.
- **Authoritative role:** Baseline for starters, substitutes, shirt-number snapshots and player allowlists used by live match actions.
- **Lifecycle:** Replaceable before kickoff. Lineup mutation is blocked once the match has started; the stored baseline then remains read-only.

### `event_match_incidents`

- **Purpose:** Ordered, durable live ledger for goals and substitutions.
- **Important fields:** `event_id`, `incident_type`, credited side/goal type, period/minute, scorer/assist, player off/on, opponent name, `sequence`, `request_key`, creator and void metadata.
- **Constraints/indexes:** Unique `(event_id, request_key)` prevents duplicate incident actions. Indexes cover event sequence, active incidents by type, player attribution and substitution replay.
- **Authoritative role:** Active incidents are authoritative for the match timeline and live goal/substitution history.
- **Lifecycle:** Append-only. Incidents are voided with actor, time and reason rather than deleted. Stable row identities allow precise undo.

### `event_match_action_requests`

- **Purpose:** Claims repeat-sensitive actions such as substitutions and undo before their effects are applied.
- **Important fields:** `event_id`, `action`, `request_key`, `expected_incident_id`, `incident_id`, `result`, creator and completion timestamps.
- **Constraints/indexes:** Unique `request_key`; indexes on `(event_id, action)` and `expected_incident_id`.
- **Authoritative role:** Idempotency ledger for action processing, including protection against repeated undo/substitution requests.
- **Lifecycle:** Append-only request identity with a mutable result/completion projection.

### `event_audience`

- **Purpose:** Event participant allowlist.
- **Important fields:** `event_id`, `person_id`, `source`, `created_at`.
- **Constraints/indexes:** Unique `(event_id, person_id)`; indexes on event, person and source.
- **Authoritative role:** Required alongside active team eligibility when building match player allowlists and participant visibility.
- **Lifecycle:** Mutable membership set before and around event preparation.

### `event_availability`

- **Purpose:** RSVP response for an event participant.
- **Important fields:** `event_id`, `person_id`, `status`, timestamps.
- **Constraints/indexes:** Unique `(event_id, person_id)`; indexes on event, person and status.
- **Authoritative role:** Source for available, unavailable and pending readiness counts.
- **Lifecycle:** Mutable by authorised participant response workflows.

### `attendance`

- **Purpose:** Records what happened at the event rather than pre-event intent.
- **Important fields:** `event_id`, `person_id`, `status`, `checked_at`, `checked_by`, `notes`.
- **Constraints/indexes:** Unique `(event_id, person_id)`; indexes on event, person and status.
- **Authoritative role:** Source for attendance register state and readiness summaries.
- **Lifecycle:** Mutable through authorised attendance saves.

### `activity_log`

- **Purpose:** Audit record for important system and Match Operations actions.
- **Important fields:** user, action, object type/object, message, metadata and creation time.
- **Constraints/indexes:** Primary key plus indexes on user, action, object type/object and creation time.
- **Authoritative role:** Audit-only. It is not the source used to reconstruct score, timeline or pitch state.
- **Lifecycle:** Append-only audit data.

## Projection and Replay Rules

- Match Details score fields are projections updated in the same transaction as goal creation or undo.
- Current On Pitch and Available Bench are not stored as separate snapshots; they are derived by replaying active substitution incidents over `event_match_selections`.
- Voided incidents remain in the ledger but are excluded from active score, timeline and substitution replay.
- Transactions and row locks ensure validation and mutation use the same current event, details and incident state.
