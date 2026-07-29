# Events and Matchday Architecture

**Source of truth:** `app/core/Events/`, `app/core/Attendance/`, `app/core/MatchMode/`, `app/core/Registrations/`
**Last verified:** 2026-07-29

---

## Overview

The Events module manages the full lifecycle of club events (training sessions, matches, tournaments). The Matchday module provides the live match operations surface for coaches managing a match in real time.

---

## Event Lifecycle

1. **Creation** — Administrator or coach creates an event with type, date, time, venue and team assignment.
2. **Audience building** — `EventAudienceBuilder` populates `event_audience` with all eligible attendees based on team membership.
3. **Availability** — Audience members submit availability responses stored in `event_availability`.
4. **Attendance** — On the day, the coach records actual attendance in `attendance`.
5. **Match operations** — For match events, the Matchday Hub provides access to lineup, live match mode, goal attribution, substitutions and match report.

---

## Event Types

Events have a `type` field. The following types unlock match-specific operations:

- `fixture` — Full match with lineup, live mode, incidents and report
- `friendly` — Friendly match (same operations as `fixture`)
- `training` — Training session (attendance only, no match operations)
- `tournament` — Tournament event

---

## Audience System

`EventAudienceRepository` stores the audience for each event. `EventAudienceBuilder` populates the audience from team membership at the time of event creation. The audience can be manually adjusted by an administrator.

---

## Attendance and Availability

| Table | Purpose |
|---|---|
| `event_availability` | Pre-event RSVP responses (available, unavailable, unknown) |
| `attendance` | Post-event attendance register (attended, absent, late) |

---

## Match Mode

The Match Mode module provides live match operations:

| Service | Responsibility |
|---|---|
| `MatchModeService` | Orchestrate match state transitions |
| `MatchStateService` | Track match state (not started, first half, half time, second half, full time) |
| `MatchLineupSubmissionService` | Submit and validate match lineup |
| `MatchGoalService` | Record and undo goals |
| `MatchSubstitutionService` | Record and undo substitutions |
| `MatchSubstitutionUndoService` | Undo the last substitution incident |
| `MatchGoalkeeperChangeService` | Record goalkeeper changes |
| `MatchGoalkeeperStateService` | Determine goalkeeper at specific sequences or minutes |
| `MatchIncidentRepository` | Store all match incidents (goals, cards, substitutions) |
| `MatchIncidentUndoService` | Undo the last incident |
| `MatchPitchStateService` | Track current pitch state (players on pitch, positions) |
| `MatchEligiblePlayerService` | Resolve eligible players for an event |
| `MatchReadinessService` | Pre-match readiness checks |
| `MatchReportService` | Post-match report and player ratings |
| `MatchDetailsSubmissionService` | Submit match details (score, result) |
| `FormationEngine` | Formation template management and lineup validation |

---

## Formation System

The `FormationEngine` manages formation templates and validates lineups against them.

System formation templates are seeded during the upgrade pipeline:

| Format | Templates |
|---|---|
| 5v5 | 1-2-1, 2-1-1, 1-1-2 |
| 7v7 | Standard 7v7 formations |
| 9v9 | Standard 9v9 formations |
| 11v11 | Standard 11v11 formations |

---

## Matchday Saved-Squad and Emergency-Contact Projection

`MatchdayHubPage` builds one event-scoped Match Mode workspace and reuses its saved `starters`, saved `substitutes` and `eligible_players`. The selected-squad card shows the saved pre-match lineup before kickoff and the derived on-pitch/bench projection during or after play. The emergency-contact projection always remains based on the saved selected squad rather than live substitution state.

The emergency-contact dependency flow is:

```text
PlayerRegistrationRepository
  → EmergencyContactService
  → MatchdayEmergencyContactsProvider
  → MatchdayEmergencyContactsCard
  → MatchdayHubPage
```

| Boundary | Responsibility |
|---|---|
| `PlayerRegistrationRepository` | Return bounded, minimal candidates for the exact player and exact event season, limited to caller-supplied lifecycle statuses. |
| `EmergencyContactService` | Accept only `registered` or `approved`, reject ambiguity, normalize the optional name and callable telephone, and return an internal typed resolution. |
| `MatchdayEmergencyContactsProvider` | Validate fixture/friendly scope, re-authorise against the stored event team, intersect saved starters/substitutes with eligible active People, and emit a UI-safe projection. |
| `MatchdayEmergencyContactsCard` | Render escaped HTML only, including `tel:` links only when a callable telephone is available. |
| `PortalRouter` | Protect every Matchday response as private, non-cacheable and non-indexable before authentication or page rendering. |

The MVP reads one emergency contact from the exact-season player registration. It does not fall back to parent, guardian, billing contact, People email/telephone, another season, or Welfare/medical providers. Duplicate eligible registrations fail closed. Internal statuses, registration identifiers, medical data and Welfare data do not enter the UI projection.

No contact data is transported through JavaScript, REST, AJAX, logs, snapshots or transients. The feature required no schema change.

---

## Portal Routes for Events

| Route | Purpose | Access |
|---|---|---|
| `/club-os/events/{id}` | Event detail | Event audience or managed Team |
| `/club-os/events/{id}/attendance` | Attendance register | `can_manage_team` |
| `/club-os/events/{id}/matchday` | Matchday hub | `can_manage_team` |
| `/club-os/events/{id}/live` | Live Match Mode | `can_manage_team` and match event |
| `/club-os/events/{id}/report` | Match report | `can_manage_team` and match event |
| `/club-os/events/{id}/lineup` | Match lineup | `can_manage_team` and match event |
| `/club-os/events/{id}/goal` | Goal attribution | `can_manage_team` and match event |
| `/club-os/events/{id}/substitution` | Substitution | `can_manage_team` and match event |
| `/club-os/events/{id}/match-details` | Match details | `can_manage_team` and match event |
| `/club-os/events/{id}/audience` | Event audience | `can_manage_team` |
| `/club-os/events/{id}/edit` | Event edit | `can_manage_team` |

---

## Status

**MVP Complete.** Full event lifecycle, audience, attendance, saved starter/substitute selection, Matchday emergency contacts, match mode, goals, substitutions, goalkeeper changes, incidents, undo, match state, match report and player ratings are implemented.
