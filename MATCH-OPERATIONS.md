# Match Operations

The Match Operations MVP provides a secure, mobile-first workflow from match preparation through full-time. It covers fixtures and friendlies managed inside Club OS.

## Preparation Flow

1. Create or open the stored event and confirm its team, date, `HH:MM` time and venue.
2. Configure Match Details: opponent, competition and home, away or neutral location.
3. Build the event audience and collect availability responses.
4. Complete the attendance register where appropriate.
5. Use the Match Lineup Builder to select starters and substitutes, then assign one captain and one goalkeeper from the starters.
6. Review Matchday Hub readiness and enter Match Mode.

The saved selection captures shirt numbers and becomes the pre-match baseline. It is read-only after kickoff.

## Match Readiness Dashboard

Matchday Hub calculates readiness dynamically from stored Match Details, lineup, availability, attendance and match state. It shows preparation actions before kickoff, live actions during the match and completed status after full-time. Readiness is a current operational summary, not a manually maintained flag.

## Kickoff and Live Match States

The normal state sequence is:

```text
Not Started → First Half → Half-Time → Second Half → Full-Time
```

Match Mode prioritises the next valid live action. Supported alternative end states include abandoned, postponed and cancelled where allowed. Reopen Match is available from Full-Time and returns the match to Second Half for authorised correction or continuation.

The current MVP does not include a browser timer, extra time or penalty shootout workflow.

## Goal Attribution

Goal Attribution supports:

- club goals, with a saved-lineup scorer and optional saved-lineup assist;
- opponent goals, with an optional opponent player name;
- club own goals, optionally naming the opponent player credited with the goal;
- opponent own goals, credited to an eligible IEXEL player;
- penalties for normal club or opponent goals.

Each accepted goal writes a stable match incident and updates the home/away score projection in one transaction. Fields not relevant to the selected goal mode are not accepted.

## Rolling Substitutions

Rolling Substitutions follow grassroots roll-on/roll-off rules. Match Mode shows:

- **Current On Pitch**, derived from starters plus active substitution history; and
- **Available Bench**, derived from substitutes and players who have rolled off.

A substitution can only move a currently on-pitch player off and a currently benched player on. The player who leaves joins the bench and can re-enter later. This state is derived by replaying active substitution incidents in sequence; it is not maintained as a separate mutable snapshot.

## Timeline, Undo and Reopen

The match timeline is the ordered view of active goal and substitution incidents.

- **Undo Last Goal** voids the expected latest active goal and reverses its score projection.
- **Undo Last Substitution** voids the expected latest active substitution; replay then derives the restored pitch state.
- **Reopen Match** changes Full-Time back to Second Half and clears the finished timestamp.

Undo does not delete incidents. Stable incident identities, expected-incident checks, request keys and the action-request ledger prevent a repeated request from affecting an earlier action.

## Full-Time Workflow

At Full-Time, the match state and event completion status are stored and live mutation controls are restricted. Coaches can review the score and timeline. If a correction is required, an authorised coach can reopen the match, apply supported corrections, and return it to Full-Time.

Match Reports, Player Ratings and Player of the Match are the next planned workflows and are not described as complete.

## Authoritative Data Sources

| Data | Authoritative source |
|---|---|
| Event identity, team, date, time and venue | Stored event |
| Opponent, competition, home/away/neutral, match state and score projection | Match Details |
| Starting lineup and substitutes | Match selection baseline |
| Goals, substitutions and live timeline | Active match incidents |
| Current on-pitch and bench state | Selection baseline plus replayed active substitutions |
| Participant eligibility | Active team options plus event audience |
| RSVP and attendance summaries | Availability and attendance records |
| Operational audit | Activity log metadata (audit-only) |

## Security Boundary

All Match Operations routes load the stored event and derive its team before authorising. A coach must have an active coach assignment for that team; a club administrator may use the explicit administrator override. Mutations also require event/action-scoped nonces, server-side player allowlists and current-state validation.

Goal, score, state, substitution and undo operations use transactions and row locks. Request keys and database uniqueness constraints provide repeat safety. See [SECURITY.md](SECURITY.md) and [DATABASE.md](DATABASE.md).

## Deferred Capabilities

- Cards and injuries.
- Extra time and penalty shootout.
- Browser match clock.
- AJAX/WebSockets live updates.
- Formations and tactical diagrams.
- Player statistics aggregation and season analytics.
- Match Reports, Player Ratings and Player of the Match.
- PDF export and messaging.
