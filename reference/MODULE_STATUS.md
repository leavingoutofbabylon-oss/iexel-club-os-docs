# Module Status Register

**Source of truth:** Source code inspection of `iexel-club-os`
**Last verified:** 2026-07-24

---

## Status Definitions

| Status | Meaning |
|---|---|
| **Complete** | Fully implemented, tested and production-ready |
| **MVP Complete** | Implemented to MVP standard; known gaps documented |
| **In Progress** | Partially implemented; active development |
| **Partial** | Structural code exists; significant functionality missing |
| **Placeholder** | Directory or class exists; no functional implementation |
| **Planned** | Documented in roadmap or inventory; not yet started |
| **Post-MVP** | Intentionally deferred after Release 1.0 |
| **Deprecated** | Legacy code retained for compatibility; no new consumers |

---

## Module Status

| Module | Status | Notes |
|---|---|---|
| Application boot | **Complete** | Boot, activation, deactivation, upgrade pipeline all operational |
| Container | **Complete** | Minimal singleton DI container |
| Permissions | **Complete** | All 26 capabilities and 6 roles registered |
| People | **MVP Complete** | CRUD, roles, WordPress user linking operational. Club ID generation, welfare fields present |
| Teams | **MVP Complete** | Team CRUD, assignments operational. `iexel_manage_teams` capability not yet enforced |
| Seasons | **MVP Complete** | Season lifecycle, team seasons, reconciliation, backfill and context resolution operational |
| Season Planning | **MVP Complete** | Plan generation, approval and transactional execution operational |
| Relationships | **MVP Complete** | Family relationships, billing contact, team membership operational |
| Venues | **Complete** | Venue CRUD and map link formatting operational |
| Events | **MVP Complete** | Event lifecycle, audience, team workspace operational |
| Attendance | **MVP Complete** | Availability, attendance register, team attendance service operational |
| Match Mode | **MVP Complete** | Lineup, state, score, goals, substitutions, goalkeeper changes, incidents, undo, reports, ratings operational |
| Formation Engine | **Complete** | System templates seeded (5v5, 7v7, 9v9, 11v11), lineup validation operational |
| Football Statistics | **MVP Complete** | Player and team statistics derived from incidents. Eligibility policy operational |
| Player Registrations | **MVP Complete** | Administrator and family registration workflows operational |
| Finance | **MVP Complete** | Invoices, payments, billing schedules, fee rules, discount policies, billing runs operational. Export not yet implemented |
| Communications | **MVP Complete** | Email sending, scheduling, templates, delivery audit operational. `iexel_manage_communications` capability inconsistency present |
| Member Portal | **MVP Complete** | All five experience roles operational. Profile switching operational |
| Executive Dashboard | **MVP Complete** | All widgets and alerts operational. 60-second cache |
| Club Projects | **Complete** | Full project lifecycle, visibility, ordering operational. Not listed in `ReleaseModuleInventory`; tracked separately. |
| Branding and Media | **MVP Complete** | Brand palette, login branding, app icon, entity media operational |
| Activity Log | **MVP Complete** | Global activity log operational. Domain-specific timelines partially implemented |
| Weather | **Placeholder** | `WeatherService` exists; returns cached placeholder forecast only |
| Rewards | **Placeholder** | `iexel_manage_rewards` capability declared; no implementation |
| Audit Log UI | **Planned** | `iexel_view_audit_log` capability declared; no admin page |
| Finance Export | **Planned** | `iexel_export_finance` capability declared; no export implementation |

---

## Legacy Code Status

| Directory | Status | Notes |
|---|---|---|
| `app/People/` | **Active (legacy)** | `PeopleRepository` still used by Kernel; not yet migrated to `app/core/` |
| `app/Teams/` | **Active (legacy)** | `TeamRepository` still used by Kernel |
| `app/TeamAssignments/` | **Active (legacy)** | `TeamAssignmentRepository` still used by Kernel |
| `app/Permissions/` | **Active (legacy)** | `PermissionManager` and `Roles` still used by Activator |
| `app/Database/` | **Deprecated** | Legacy database helpers; no new consumers |
| `app/Helpers/` | **Deprecated** | Legacy helper functions; no new consumers |
| `app/Services/` | **Deprecated** | Legacy service classes; no new consumers |
