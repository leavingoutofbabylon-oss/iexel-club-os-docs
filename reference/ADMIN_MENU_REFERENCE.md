# Admin Menu Reference

**Source of truth:** `app/core/Release/ReleaseRouteInventory.php` and `app/core/UI/AdminUI.php`
**Last verified:** 2026-07-24

---

## Overview

All Club OS admin pages are registered under the top-level menu slug `iexel-club-os`. Pages are accessed via:

```
/wp-admin/admin.php?page={slug}
```

The top-level menu item is registered with `add_menu_page`. All sub-pages use `add_submenu_page`.

---

## Complete Admin Page Inventory

| Slug | Title | Required capability | Hidden |
|---|---|---|---|
| `iexel-club-os` | Dashboard | `iexel_manage_club_os` | No |
| `iexel-club-os-people` | People | `iexel_manage_people` | No |
| `iexel-club-os-add-person` | Add Person | `iexel_manage_people` | No |
| `iexel-club-os-person-profile` | Person Profile | `iexel_manage_people` | No |
| `iexel-club-os-teams` | Teams | `iexel_manage_club_os` | No |
| `iexel-club-os-add-team` | Add Team | `iexel_manage_club_os` | No |
| `iexel-club-os-team-profile` | Team Profile | `iexel_manage_club_os` | No |
| `iexel-club-os-team-assignments` | Team Assignments | `iexel_manage_club_os` | No |
| `iexel-club-os-edit-assignment` | Edit Assignment | `iexel_manage_club_os` | No |
| `iexel-club-os-events` | Events | `iexel_manage_club_os` | No |
| `iexel-club-os-add-event` | Add Event | `iexel_manage_club_os` | No |
| `iexel-club-os-event-audience` | Event Audience | `iexel_manage_club_os` | Yes |
| `iexel-club-os-event-hub` | Event Hub | `iexel_manage_club_os` | Yes |
| `iexel-club-os-event-attendance` | Attendance Register | `iexel_coach_portal` | Yes |
| `iexel-club-os-venues` | Venues | `iexel_manage_club_os` | No |
| `iexel-club-os-add-venue` | Add Venue | `iexel_manage_club_os` | No |
| `iexel-club-os-user-links` | Member Linking | `iexel_manage_club_os` | No |
| `iexel-club-os-member-dashboard` | Member Dashboard | `iexel_manage_club_os` | No |
| `iexel-club-os-seasons` | Seasons | `iexel_manage_club_os` | No |
| `iexel-club-os-add-season` | Add Season | `iexel_manage_club_os` | No |
| `iexel-club-os-team-seasons` | Team Seasons | `iexel_manage_club_os` | No |
| `iexel-club-os-season-planning` | Season Planning | `iexel_manage_club_os` | No |
| `iexel-club-os-season-system` | Season System | `iexel_manage_club_os` | No |
| `iexel-club-os-registrations` | Registrations | `iexel_manage_club_os` | No |
| `iexel-club-os-new-registration` | New Registration | `iexel_manage_club_os` | No |
| `iexel-club-os-registration-review` | Review Queue | `iexel_manage_club_os` | No |
| `iexel-club-os-finance` | Finance | `iexel_view_finance` | No |
| `iexel-club-os-finance-invoice` | Finance Invoice | `iexel_manage_finance` | Yes |
| `iexel-club-os-finance-payment` | Record Payment | `iexel_record_payments` | Yes |
| `iexel-club-os-billing-schedules` | Billing Schedules | `iexel_manage_billing` | No |
| `iexel-club-os-billing-schedule-edit` | Edit Billing Schedule | `iexel_manage_billing` | Yes |
| `iexel-club-os-fee-rules` | Fee Rules | `iexel_manage_billing` | No |
| `iexel-club-os-fee-rule-edit` | Edit Fee Rule | `iexel_manage_billing` | Yes |
| `iexel-club-os-discount-policies` | Discount Policies | `iexel_manage_billing` | No |
| `iexel-club-os-discount-policy-edit` | Edit Discount Policy | `iexel_manage_billing` | Yes |
| `iexel-club-os-billing-runs` | Billing Runs | `iexel_view_finance` | No |
| `iexel-club-os-communications` | Communications | `iexel_manage_club_os` | No |
| `iexel-club-os-communications-compose` | Compose | `iexel_manage_club_os` | No |
| `iexel-club-os-communications-scheduled` | Scheduled Communications | `iexel_manage_club_os` | No |
| `iexel-club-os-communications-templates` | Communication Templates | `iexel_manage_club_os` | No |
| `iexel-club-os-communications-deliveries` | Communication Delivery Log | `iexel_manage_club_os` | No |
| `iexel-club-os-communication` | Communication Detail | `iexel_manage_club_os` | Yes |
| `iexel-club-os-settings` | Settings | `iexel_manage_club_os` | No |
| `iexel-club-os-status` | System Status | `iexel_manage_club_os` | No |
| `iexel-club-os-release-readiness` | Release Readiness | `iexel_manage_club_os` | No |

> **Hidden** pages are registered with `add_submenu_page` but are not shown in the sidebar navigation. They are accessed programmatically via redirect after a form submission.

---

## Page Class Mapping

| Slug | Page class |
|---|---|
| `iexel-club-os` | `DashboardPage` |
| `iexel-club-os-people` | `PeoplePage` |
| `iexel-club-os-add-person` | `AddPersonPage` |
| `iexel-club-os-person-profile` | `PersonProfilePage` |
| `iexel-club-os-teams` | `TeamsPage` |
| `iexel-club-os-add-team` | `AddTeamPage` |
| `iexel-club-os-team-profile` | `TeamProfilePage` |
| `iexel-club-os-team-assignments` | `TeamAssignmentsPage` |
| `iexel-club-os-edit-assignment` | `EditTeamAssignmentPage` |
| `iexel-club-os-events` | `EventsPage` |
| `iexel-club-os-add-event` | `AddEventPage` |
| `iexel-club-os-event-audience` | `EventAudiencePage` |
| `iexel-club-os-event-hub` | `EventHubPage` |
| `iexel-club-os-event-attendance` | `EventAttendancePage` |
| `iexel-club-os-venues` | `VenuesPage` |
| `iexel-club-os-add-venue` | `AddVenuePage` |
| `iexel-club-os-user-links` | `UserLinksPage` |
| `iexel-club-os-member-dashboard` | `MemberDashboardPage` |
| `iexel-club-os-seasons` | `SeasonsPage` |
| `iexel-club-os-add-season` | `AddSeasonPage` |
| `iexel-club-os-team-seasons` | `TeamSeasonsPage` |
| `iexel-club-os-season-planning` | `SeasonPlanningPage` |
| `iexel-club-os-season-system` | `SeasonSystemPage` |
| `iexel-club-os-registrations` | `RegistrationsPage` |
| `iexel-club-os-new-registration` | `NewRegistrationPage` |
| `iexel-club-os-registration-review` | `RegistrationReviewQueuePage` |
| `iexel-club-os-finance` | `FinancePage` |
| `iexel-club-os-finance-invoice` | `FinanceInvoicePage` |
| `iexel-club-os-finance-payment` | `FinancePaymentPage` |
| `iexel-club-os-billing-schedules` | `BillingSchedulesPage` |
| `iexel-club-os-billing-schedule-edit` | `BillingScheduleEditPage` |
| `iexel-club-os-fee-rules` | `FeeRulesPage` |
| `iexel-club-os-fee-rule-edit` | `FeeRuleEditPage` |
| `iexel-club-os-discount-policies` | `DiscountPoliciesPage` |
| `iexel-club-os-discount-policy-edit` | `DiscountPolicyEditPage` |
| `iexel-club-os-billing-runs` | `BillingRunsPage` |
| `iexel-club-os-communications` | `CommunicationsPage` |
| `iexel-club-os-communications-compose` | `CommunicationComposePage` |
| `iexel-club-os-communications-templates` | `CommunicationTemplatesPage` |
| `iexel-club-os-communications-deliveries` | `CommunicationDeliveryLogPage` |
| `iexel-club-os-communication` | `CommunicationDetailPage` |
| `iexel-club-os-settings` | `SettingsPage` |
| `iexel-club-os-status` | `SystemStatusPage` |
| `iexel-club-os-release-readiness` | `ReleaseReadinessPage` |
