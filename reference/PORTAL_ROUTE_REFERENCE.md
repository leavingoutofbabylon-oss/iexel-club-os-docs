# Portal Route Reference

**Source of truth:** `app/core/Release/ReleaseRouteInventory.php` and `app/core/Portal/PortalRouter.php`
**Last verified:** 2026-07-24

---

## Overview

All portal routes are prefixed `/club-os/`. Routes are registered as WordPress rewrite rules on the `init` hook and during plugin activation.

---

## Complete Portal Route Inventory

| Pattern | Purpose | Access boundary |
|---|---|---|
| `^club-os/login/?$` | Branded Club OS login | Public; WordPress authentication with nonce-protected POST mutations |
| `^club-os/?$` | Portal dashboard | Authenticated linked person and active experience role |
| `^club-os/([^/]+)/?$` | Portal section (generic) | Section-specific role, family, Team or audience boundary |
| `^club-os/coach/?$` | Coach experience | Active Coach role |
| `^club-os/treasurer/?$` | Treasurer dashboard | Linked Treasurer Person role plus `iexel_view_finance` |
| `^club-os/finance/(invoices(?:/(?:new|bulk))?|payments|outstanding|billing-schedules|fee-rules|discount-policies|billing-runs|reports)?/?$` | Treasurer Finance workspace | Treasurer entitlement plus granular Finance capability |
| `^club-os/teams/([0-9]+)/?$` | Team workspace | `can_view_team`; mutations require `can_manage_team` |
| `^club-os/teams/([0-9]+)/players/([0-9]+)/statistics/?$` | Player statistics | Team management plus stored Player-Team relationship |
| `^club-os/events/([0-9]+)/?$` | Event detail | Event audience or managed Team |
| `^club-os/events/([0-9]+)/attendance/?$` | Attendance register | `can_manage_team` |
| `^club-os/events/([0-9]+)/matchday/?$` | Matchday hub | `can_manage_team` |
| `^club-os/events/([0-9]+)/live/?$` | Live Match Mode | `can_manage_team` and supported Event type |
| `^club-os/events/([0-9]+)/report/?$` | Match report | `can_manage_team` and supported Event type |
| `^club-os/events/([0-9]+)/lineup/?$` | Match lineup | `can_manage_team` and supported Event type |
| `^club-os/events/([0-9]+)/goal/?$` | Goal attribution | `can_manage_team` and supported Event type |
| `^club-os/events/([0-9]+)/substitution/?$` | Substitution | `can_manage_team` and supported Event type |
| `^club-os/events/([0-9]+)/match-details/?$` | Match details | `can_manage_team` and supported Event type |
| `^club-os/events/([0-9]+)/audience/?$` | Event audience | `can_manage_team` |
| `^club-os/events/([0-9]+)/edit/?$` | Event edit | `can_manage_team` |

---

## Finance Sub-sections

The Finance workspace at `/club-os/finance/` provides the following sub-sections:

| Path | Section slug | Purpose |
|---|---|---|
| `/club-os/finance` | `finance` | Finance dashboard |
| `/club-os/finance/invoices` | `finance-invoices` | Invoice list |
| `/club-os/finance/invoices/new` | `finance-invoices-new` | New invoice |
| `/club-os/finance/invoices/bulk` | `finance-invoices-bulk` | Bulk invoice creation |
| `/club-os/finance/payments` | `finance-payments` | Payment list |
| `/club-os/finance/outstanding` | `finance-outstanding` | Outstanding balances |
| `/club-os/finance/billing-schedules` | `finance-billing-schedules` | Billing schedule list |
| `/club-os/finance/billing-schedules/new` | `finance-billing-schedules-new` | New billing schedule |
| `/club-os/finance/billing-schedules/edit` | `finance-billing-schedules-edit` | Edit billing schedule |
| `/club-os/finance/fee-rules` | `finance-fee-rules` | Fee rule management |
| `/club-os/finance/discount-policies` | `finance-discount-policies` | Discount policy management |
| `/club-os/finance/billing-runs` | `finance-billing-runs` | Billing run history |
| `/club-os/finance/reports` | `finance-reports` | Finance reports |

---

## Query Variables

The following WordPress query variables are registered by `PortalRouter::query_vars()`:

| Variable | Purpose |
|---|---|
| `iexel_club_os_portal` | Signals that this is a portal request (value: `1`) |
| `iexel_club_os_section` | The section slug |
| `event_id` | Event ID for event sub-pages |
| `team_id` | Team ID for team workspace |
| `person_id` | Person ID for person-scoped pages |
| `preview_player_id` | Player ID for statistics preview |

---

## Portal Page Class Mapping

| Section slug | Page class |
|---|---|
| `login` | `PortalLoginPage` |
| *(dashboard)* | Role-based (Parent/Player/Coach/Committee/Treasurer dashboard) |
| `coach` | `PortalCoachDashboardPage` |
| `treasurer` | `PortalTreasurerDashboardPage` |
| `finance*` | `PortalFinanceWorkspacePage` |
| `teams/{id}` | `PortalTeamsPage` |
| `events/{id}` | `PortalEventDetailPage` |
| `events/{id}/attendance` | `EventAttendancePage` (portal) |
| `events/{id}/matchday` | `MatchdayHubPage` |
| `events/{id}/live` | `MatchModePage` |
| `events/{id}/report` | `MatchReportPage` |
| `events/{id}/lineup` | `MatchLineupPage` |
| `events/{id}/goal` | `MatchGoalAttributionPage` |
| `events/{id}/substitution` | `MatchSubstitutionPage` |
| `events/{id}/match-details` | `PortalMatchDetailsPage` |
| `events/{id}/audience` | `PortalEventAudiencePage` |
| `events/{id}/edit` | `PortalEventEditPage` |
| `registrations` | `PortalRegistrationsPage` |
| `register` | `PortalRegistrationWizardPage` |
| `registration-status` | `PortalRegistrationStatusPage` |
| `registration-submitted` | `PortalRegistrationSubmittedPage` |
| `announcements` | `PortalAnnouncementsPage` |
| `committee` | `PortalCommitteeDashboardPage` |
