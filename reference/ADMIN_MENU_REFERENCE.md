# Admin Menu Reference

**Source of truth:** `app/core/UI/AdminUI.php` (registration) and `app/core/Release/ReleaseRouteInventory.php` (route inventory)
**Last verified:** 2026-08-26, against `AdminUI::register_menu()` directly and the passing 227-check `tools/validate-admin-navigation-consolidation.php`, following Admin Sidebar Navigation Consolidation & Route Cleanup (ADM-001/002/003, `c88eab9`, 2026-08-21).

---

## Overview

All Club OS admin pages are registered under the top-level menu slug `iexel-club-os`. Pages are accessed via:

```
/wp-admin/admin.php?page={slug}
```

The top-level menu item and all 54 sub-pages are registered in one place: `AdminUI::register_menu()`, hooked via `add_action('admin_menu', ...)` in `app/core/Application.php`. There are **55 registered admin routes** in total: **19 visible sidebar items** (`add_submenu_page('iexel-club-os', ...)`) and **36 hidden route-only items** (`add_submenu_page(null, ...)`) — registered so WordPress still recognises the screen and enforces its capability, without cluttering the sidebar. Hidden pages are reached through in-page contextual actions (e.g. an "Add Person" button on the People list) rather than direct sidebar navigation.

An old, pre-consolidation foundation-era scaffold class, `app/UI/AdminMenu.php`, also exists in the codebase but is never hooked to `admin_menu` and has zero call sites — it does not register anything and is not part of the live menu.

---

## Visible sidebar items (19)

Registered in this exact order; `tools/validate-admin-navigation-consolidation.php` enforces both the exact set and the exact order.

| # | Slug | Title | Capability | Page class |
|---|---|---|---|---|
| 1 | `iexel-club-os` | Dashboard | `iexel_manage_club_os` | `DashboardPage` (falls back to `WelfareDashboardPage` for Welfare-only users; `wp_die(403)` otherwise) |
| 2 | `iexel-club-os-people` | People | `iexel_manage_people` | `PeoplePage` |
| 3 | `iexel-club-os-teams` | Teams | `iexel_manage_club_os` | `TeamsPage` |
| 4 | `iexel-club-os-team-assignments` | Team Assignments | `iexel_manage_club_os` | `TeamAssignmentsPage` |
| 5 | `iexel-club-os-events` | Events | `iexel_manage_club_os` | `EventsPage` |
| 6 | `iexel-club-os-venues` | Venues | `iexel_manage_club_os` | `VenuesPage` |
| 7 | `iexel-club-os-seasons` | Seasons | `iexel_manage_club_os` | `SeasonsPage` |
| 8 | `iexel-club-os-team-seasons` | Team Seasons | `iexel_manage_club_os` | `TeamSeasonsPage` |
| 9 | `iexel-club-os-registrations` | Registrations | `iexel_manage_club_os` | `RegistrationsPage` |
| 10 | `iexel-club-os-registration-review` | Review Queue | `iexel_manage_club_os` | `RegistrationReviewQueuePage` |
| 11 | `iexel-club-os-finance` | Finance | `iexel_view_finance` | `FinancePage` |
| 12 | `iexel-club-os-communications` | Communications | `iexel_manage_club_os` | `CommunicationsPage` |
| 13 | `iexel-club-os-club-projects` | Club Projects | `iexel_view_club_projects` | `ClubProjectsPage` |
| 14 | `iexel-club-os-welfare` | Welfare Dashboard | `iexel_view_welfare` | `WelfareDashboardPage` |
| 15 | `iexel-club-os-welfare-concerns` | Welfare Concerns | `iexel_view_welfare` | `WelfareConcernsPage` |
| 16 | `iexel-club-os-user-links` | Member Linking | `iexel_manage_club_os` | `UserLinksPage` |
| 17 | `iexel-club-os-settings` | Settings | `iexel_manage_club_os` | `SettingsPage` |
| 18 | `iexel-club-os-status` | System Status | `iexel_manage_club_os` | `SystemStatusPage` |
| 19 | `iexel-club-os-release-readiness` | Release Readiness | `iexel_manage_club_os` | `ReleaseReadinessPage` |

---

## Hidden route-only items (36)

Registered with a `null` parent slug so WordPress still recognises the screen and enforces the listed capability, but the item does not appear in the sidebar. Reached via a contextual in-page action (button/link) rather than direct navigation, except where noted.

| Slug | Title | Capability | Page class | Reached from |
|---|---|---|---|---|
| `iexel-club-os-committee-dashboard` | Committee Dashboard | `iexel_manage_club_os` | `CommitteeDashboardPage` | **No current in-app link** — portal `PortalCommitteeDashboardPage` is the canonical Committee experience; this admin duplicate has no discoverability path (see Section on residual follow-up below) |
| `iexel-club-os-member-dashboard` | Member Dashboard | `iexel_manage_club_os` | `MemberDashboardPage` | Member Linking workflow |
| `iexel-club-os-ai` | AI Workspace | `iexel_manage_club_os` | `AIWorkspacePage` | **No current in-app link to the full page** — the Dashboard embeds `AIWorkspacePage::render_assistant()` inline; the full standalone page is registered but unlinked |
| `iexel-club-os-add-person` | Add Person | `iexel_manage_people` | `AddPersonPage` | People list |
| `iexel-club-os-person-profile` | Person Profile | `iexel_manage_people` | `PersonProfilePage` | People list |
| `iexel-club-os-add-team` | Add Team | `iexel_manage_club_os` | `AddTeamPage` | Teams list; also Team Profile "Edit Team" |
| `iexel-club-os-team-profile` | Team Profile | `iexel_manage_club_os` | `TeamProfilePage` | Teams list |
| `iexel-club-os-edit-assignment` | Edit Assignment | `iexel_manage_club_os` | `EditTeamAssignmentPage` | Team Assignments list |
| `iexel-club-os-add-event` | Add Event | `iexel_manage_club_os` | `AddEventPage` | Events list |
| `iexel-club-os-event-audience` | Event Audience | `iexel_manage_club_os` | `EventAudiencePage` | Event detail workflow |
| `iexel-club-os-event-hub` | Event Hub | `iexel_manage_club_os` | `EventHubPage` | Event detail workflow |
| `iexel-club-os-event-attendance` | Attendance Register | `iexel_coach_portal` (narrower than the parent menu's admin capability) | `EventAttendancePage` | Event/Matchday workflow |
| `iexel-club-os-add-venue` | Add Venue | `iexel_manage_club_os` | `AddVenuePage` | Venues list |
| `iexel-club-os-add-season` | Add Season | `iexel_manage_club_os` | `AddSeasonPage` | Seasons list / `SeasonAdminNavigation` |
| `iexel-club-os-season-planning` | Season Planning | `iexel_manage_club_os` | `SeasonPlanningPage` | `SeasonAdminNavigation` |
| `iexel-club-os-season-system` | Season System | `iexel_manage_club_os` | `SeasonSystemPage` | `SeasonAdminNavigation` |
| `iexel-club-os-new-registration` | New Registration | `iexel_manage_club_os` | `NewRegistrationPage` | Registrations list / `RegistrationAdminNavigation` |
| `iexel-club-os-finance-invoice` | Finance Invoice | `iexel_manage_finance` | `FinanceInvoicePage` | Finance page "Create Invoice" |
| `iexel-club-os-finance-payment` | Record Payment | `iexel_record_payments` | `FinancePaymentPage` | Finance page "Record Payment" |
| `iexel-club-os-billing-schedules` | Billing Schedules | `iexel_manage_billing` | `BillingSchedulesPage` | `FinanceAdminNavigation` |
| `iexel-club-os-billing-schedule-edit` | Edit Billing Schedule | `iexel_manage_billing` | `BillingScheduleEditPage` | Billing Schedules list |
| `iexel-club-os-fee-rules` | Fee Rules | `iexel_manage_billing` | `FeeRulesPage` | `FinanceAdminNavigation` |
| `iexel-club-os-fee-rule-edit` | Edit Fee Rule | `iexel_manage_billing` | `FeeRuleEditPage` | Fee Rules list |
| `iexel-club-os-discount-policies` | Discount Policies | `iexel_manage_billing` | `DiscountPoliciesPage` | `FinanceAdminNavigation` |
| `iexel-club-os-discount-policy-edit` | Edit Discount Policy | `iexel_manage_billing` | `DiscountPolicyEditPage` | Discount Policies list |
| `iexel-club-os-billing-runs` | Billing Runs | `iexel_view_finance` | `BillingRunsPage` | `FinanceAdminNavigation` |
| `iexel-club-os-communications-compose` | Compose | `iexel_manage_club_os` | `CommunicationComposePage` | Communications page |
| `iexel-club-os-communications-scheduled` | Scheduled Communications | `iexel_manage_club_os` | `CommunicationsPage` (same class as the visible Communications item; renders a scheduled-focused view) | Communications page |
| `iexel-club-os-communications-templates` | Communication Templates | `iexel_manage_club_os` | `CommunicationTemplatesPage` | Communications page |
| `iexel-club-os-communications-deliveries` | Communication Delivery Log | `iexel_manage_club_os` | `CommunicationDeliveryLogPage` | Communications page |
| `iexel-club-os-communication` | Communication Detail | `iexel_manage_club_os` | `CommunicationDetailPage` | Communications/Delivery Log list |
| `iexel-club-os-club-project-add` | Add Club Project | `iexel_create_club_projects` | `AddClubProjectPage` | Club Projects page |
| `iexel-club-os-club-project-edit` | Edit Club Project | `iexel_edit_club_projects` | `EditClubProjectPage` | Club Projects page |
| `iexel-club-os-welfare-concern-add` | Add Welfare Concern | `iexel_manage_welfare` | `AddWelfareConcernPage` | Welfare Concerns page |
| `iexel-club-os-welfare-concern` | Welfare Concern | `iexel_view_welfare` | `WelfareConcernPage` | Welfare Concerns page |
| `iexel-club-os-entity-lifecycle` | Entity Lifecycle | `iexel_manage_club_os` | `EntityLifecyclePage` | People/Team Profile "Manage Archive / Delete"/"Lifecycle" actions |

---

## Capability boundary notes

- `iexel-club-os-event-attendance` is gated by `iexel_coach_portal`, narrower than the general `iexel_manage_club_os` capability used for most of the menu — verified as an intentional, tighter-than-parent boundary, not a mismatch.
- Welfare items (`iexel-club-os-welfare`, `-welfare-concerns`) require `iexel_view_welfare`; `iexel-club-os-welfare-concern-add` requires the stricter `iexel_manage_welfare`.
- Finance items split across `iexel_view_finance` (read), `iexel_manage_finance` (invoices), `iexel_record_payments` (payments) and `iexel_manage_billing` (schedules/fee rules/discount policies/billing runs).
- Club Projects splits `iexel_view_club_projects` (list) from `iexel_create_club_projects` / `iexel_edit_club_projects` (mutating actions).
- The top-level `iexel-club-os` menu capability is resolved dynamically: `iexel_manage_club_os` if the user has it, otherwise `iexel_view_welfare` — `dashboard_page()` itself then routes a Welfare-only user to `WelfareDashboardPage` and fails closed with `wp_die(403)` for anyone with neither.

## Known residual gap (non-blocking)

`ReleaseRouteInventory::administrator()` does not currently enumerate 10 of the 55 routes above: `iexel-club-os-committee-dashboard`, `iexel-club-os-ai`, `iexel-club-os-club-projects`, `iexel-club-os-club-project-add`, `iexel-club-os-club-project-edit`, `iexel-club-os-welfare`, `iexel-club-os-welfare-concerns`, `iexel-club-os-welfare-concern-add`, `iexel-club-os-welfare-concern`, `iexel-club-os-entity-lifecycle`. Current Release Readiness duplicate-route checks still pass (there is nothing to duplicate against); this is an inventory-completeness gap and a candidate for a small future cleanup batch, not a routing or security defect — every route above is still independently capability-enforced by `add_submenu_page()` regardless of inventory coverage.
