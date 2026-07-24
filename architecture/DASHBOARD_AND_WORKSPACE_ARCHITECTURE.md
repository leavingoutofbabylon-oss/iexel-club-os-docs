# Dashboard and Workspace Architecture

**Source of truth:** `app/core/Dashboard/`, `app/core/Experience/`, `app/core/UI/Components/Dashboard/`
**Last verified:** 2026-07-24

---

## Overview

Club OS provides two dashboard surfaces:

1. **Executive Dashboard** (wp-admin) — Administrator operational summary with metrics, alerts and activity.
2. **Role-based Workspaces** (portal) — Five role-specific dashboards for Parent, Player, Coach, Committee and Treasurer.

---

## Executive Dashboard

**Service:** `DashboardService`
**Cache:** `iexel_club_os_executive_dashboard` transient, 60-second TTL

The executive dashboard aggregates data from multiple modules into a `DashboardSnapshot`. It is refreshed on demand or after 60 seconds.

### Dashboard Widgets

| Widget key | Title | Data source |
|---|---|---|
| `club_health` | Club Health | People counts, team counts, current season |
| `registration` | Registration | Registration counts by status |
| `events` | Events | Upcoming events with availability and attendance summaries |
| `finance` | Finance | Invoice and payment totals |
| `communications` | Communications | Communication counts by status |
| `season` | Season | Season reconciliation summary |
| `activity` | Recent Activity | Last 10 activity log entries |
| `alerts` | Alerts | Operational alerts (pending registrations, overdue invoices, etc.) |

---

## Committee Dashboard Providers

The Committee workspace uses dedicated data providers:

| Provider | Data |
|---|---|
| `CommitteeClubHealthDataProvider` | People, teams and season health metrics |
| `CommitteeFinanceSummaryProvider` | Finance totals and outstanding balances |
| `CommitteeGovernanceProvider` | Governance metrics |
| `CommitteeMajorEventsProvider` | Upcoming major events |
| `CommitteeOperationalAlertsProvider` | Operational alerts |
| `CommitteeProjectsProvider` | Club projects summary |
| `CommitteeVolunteerSnapshotProvider` | Volunteer and role counts |

---

## Role-based Workspaces

Each experience role has a dedicated portal dashboard page:

| Role | Page class | Portal path |
|---|---|---|
| Parent | `PortalParentDashboardPage` | `/club-os/` (when parent role active) |
| Player | `PortalPlayerDashboardPage` | `/club-os/` (when player role active) |
| Coach | `PortalCoachDashboardPage` | `/club-os/coach` |
| Committee | `PortalCommitteeDashboardPage` | `/club-os/committee` |
| Treasurer | `PortalTreasurerDashboardPage` | `/club-os/treasurer` |

---

## Provider-Widget Pattern

Dashboard data is separated from presentation using the Provider-Widget pattern:

- **Provider** — A PHP class that queries the database and returns a structured array of data.
- **Widget** — A PHP component class that receives provider data and renders HTML.

This separation allows providers to be tested independently of rendering and allows widgets to be reused across different dashboard contexts.

See [`standards/PROVIDER_AND_WIDGET_STANDARDS.md`](../standards/PROVIDER_AND_WIDGET_STANDARDS.md) for implementation standards.
See [`decisions/ADR-002-PROVIDER-WIDGET-PATTERN.md`](../decisions/ADR-002-PROVIDER-WIDGET-PATTERN.md) for the design decision.

---

## Status

**MVP Complete.** Executive dashboard, all committee providers and all role-based workspaces are implemented.
