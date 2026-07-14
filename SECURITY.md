# IEXEL Club OS Security

## Security Boundary

The stored event defines the team and event type used for authorisation. Route and form values identify a requested resource or action; they do not establish permission scope.

For Match Operations mutations, Club OS loads the event, derives its stored `team_id`, and then calls `can_manage_team()` before changing match data.

## Team Management Permission

`can_manage_team()` allows access when either:

- the current user has the club-wide `iexel_manage_club_os` capability (the administrator override); or
- the current user has coach portal capability, is linked to a person, and has an active coach assignment for the stored team.

An identifier posted by a client cannot grant access to a different team.

## Event Visibility and Read/Write Separation

- Club administrators can view events across the club.
- An active coach can view events for teams they manage.
- A participant can view an event when they have an active player context and belong to that event's audience.
- Listing queries use the same visibility context so unrelated team events are not returned.
- Read access to Event Detail does not imply mutation access. Match Details, lineup, attendance and live controls require management permission for the stored event team.
- Direct-ID routes repeat these checks after loading the stored event; hiding a navigation link is not treated as authorisation.

## Audience and Player Eligibility

Event audience membership is the participant visibility boundary. Match player allowlists are built server-side from current eligible team players, permitted same-age-team options and the stored event audience.

Lineup submissions are rejected when a person is duplicated, is no longer active/eligible, or is outside that allowlist. Captain and goalkeeper must be starters. Goal and substitution services validate submitted player roles against the saved lineup and current derived pitch state.

Club OS does not trust posted team, person or role identifiers without checking them against these stored allowlists.

## Request Protection

- State-changing forms use WordPress nonces scoped to the event and action where appropriate.
- Nonce validation complements authorisation; it does not replace it.
- Goal and incident requests use stable idempotent request keys.
- The incident constraint on `(event_id, request_key)` blocks duplicate incident insertion.
- The match action request ledger claims repeat-sensitive substitution and undo requests.
- Undo requests name the expected latest incident, preventing a repeat from moving backwards to an earlier goal or substitution.
- Database uniqueness constraints provide a final integrity layer beneath service validation.

## Transactions and Locking

Live state, goals, substitutions, undo and reopen workflows run in database transactions. Relevant event, Match Details, incident and action-request rows are locked before the service validates current state and applies changes.

A typical mutation follows:

```text
load stored event
  → derive stored team
  → authorise
  → validate nonce and request key
  → start transaction and lock rows
  → validate current state and player allowlists
  → write incident/projection/audit metadata
  → commit
  → redirect
```

If validation or persistence fails, the transaction is rolled back.

## Post/Redirect/Get

RSVP, attendance and Match Operations forms redirect after processing. PRG reduces accidental browser resubmission, clears stale form state and works with request-key idempotency for repeat safety.

## Audit and Authoritative Records

Match incidents preserve creator and void metadata. The activity log records important operational actions, including state changes and reopen activity. Audit data supports investigation but does not replace authoritative events, Match Details, selections or incidents.

See [DATABASE.md](DATABASE.md) for table constraints and [ARCHITECTURE.md](ARCHITECTURE.md) for the request lifecycle.
