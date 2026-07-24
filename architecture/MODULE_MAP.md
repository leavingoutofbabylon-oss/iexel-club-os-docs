# Module Map

**Source of truth:** `app/core/Release/ReleaseModuleInventory.php` and `app/core/` directory
**Last verified:** 2026-07-24

---

## Overview

Club OS is organised into 20 functional modules. Each module is a directory under `app/core/` containing all PHP classes for that domain. Modules do not have explicit module manifest files; the `ReleaseModuleInventory` class provides the canonical module list.

The `ModuleManager` provides an extension point for third-party modules via the `iexel_club_os_modules_booting` action hook. Currently, no external modules are shipped, and no internal domain areas register a `ModuleInterface` implementation. Domain areas resolve through `Kernel` instead.

---

## Module Inventory

| Key | Name | Area | Primary components | Responsibility |
|---|---|---|---|---|
| `application` | Application boot | Core | `Application`, `Container`, `ModuleManager` | Boot orchestration and WordPress registration |
| `people` | People | People | `PeopleRepository`, `PersonForm`, `ClubIdGenerator` | Person records, roles and WordPress user links |
| `teams` | Teams and assignments | Teams | `TeamRepository`, `TeamAssignmentRepository` | Team, squad and assignment lifecycle |
| `seasons` | Seasons | Seasons | `SeasonRepository`, `TeamSeasonRepository`, `CurrentSeasonService` | Season context, canonical links, reconciliation and backfill |
| `season-planning` | Season planning | Season Planning | `SeasonPlanningService`, `SeasonPlanRepository`, contributors | Plan generation, approval and transactional execution |
| `relationships` | Relationships and family | Relationships | `PersonRelationshipRepository`, `PersonTeamMembershipService` | Family, guardian, billing-contact and team membership boundaries |
| `venues` | Venues | Venues | `VenueRepository`, `VenueMapLink` | Venue storage and location formatting |
| `events` | Events and audience | Events | `EventRepository`, `EventAudienceRepository`, `EventAudienceBuilder` | Event lifecycle, audience and Team workspace |
| `attendance` | Attendance and availability | Attendance | `AttendanceRepository`, `AvailabilityRepository`, `TeamAttendanceService` | Invitee responses and attendance registers |
| `match-mode` | Match operations | Match Mode | Match services and repositories | Lineups, incidents, match state, reports, ratings and undo flows |
| `statistics` | Football statistics | Statistics | `PlayerStatisticsService`, `TeamStatisticsService`, `FootballStatisticsEngine` | Derived player and Team performance |
| `registrations` | Player registrations | Registrations | `PlayerRegistrationService`, repository and validator | Administrator and family registration workflows |
| `finance` | Finance and billing | Finance | `FinanceService`, `RecurringBillingService`, repositories and validators | Invoices, payments, policies, schedules and billing runs |
| `communications` | Communications | Communications | `CommunicationService`, repository, validator and sender | Email, announcements, recipient snapshots and delivery audit |
| `portal` | Member portal and experience | Portal | `PortalRouter`, `MemberPortalService`, `MemberExperienceService`, `AdminAccessBoundary` | Parent, Player, Coach, Committee and Treasurer experiences |
| `dashboard` | Executive dashboard | Dashboard | `DashboardService` | Administrator operational summary and alerts |
| `branding-media` | Branding and Media | Branding and Media | `BrandingService` and media request handlers | Brand palette, image attachments, focal positions and fallbacks |
| `permissions` | Permissions | Permissions | `PermissionManager`, `ClubRoleCapabilityRegistrar`, `SensitiveModuleAccess` | Roles, capabilities and sensitive-module boundaries |
| `activity` | Activity and timelines | Audit | `ActivityLogger` and domain event tables | Global activity plus finance, communication and match timelines |
| `weather` | Weather | Weather | `WeatherService` | Cached placeholder forecast only |

---

## Directory Structure

```
app/
├── core/                          ← All modern module code
│   ├── Application.php            ← Application singleton and boot orchestration
│   ├── Kernel.php                 ← Service locator for all domain services
│   ├── Activator.php              ← Plugin activation handler
│   ├── Deactivator.php            ← Plugin deactivation handler
│   ├── Activity/                  ← ActivityLogger
│   ├── Attendance/                ← Attendance and availability repositories and services
│   ├── Authentication/            ← AuthenticationService, AdminAccessBoundary
│   ├── Branding/                  ← BrandingService, BrandingManager, media handlers
│   ├── Communications/            ← Full communications module
│   ├── Container/                 ← Minimal DI container
│   ├── Dashboard/                 ← DashboardService and committee data providers
│   ├── Database/                  ← DatabaseManager (schema owner)
│   ├── EventAudience/            ← EventAudienceBuilder, EventAudienceRepository
│   ├── EntityLifecycle/           ← EntityLifecycleService, EntityDependencyInspector
│   ├── EventProgress/             ← EventProgressManager
│   ├── Events/                    ← Event entity, repository, workspace service
│   ├── Experience/                ← MemberExperienceService, role snapshots
│   ├── Finance/                   ← Full finance and billing module
│   ├── FootballStatistics/        ← FootballStatisticsEngine, read models, projections
│   ├── Logging/                   ← ActivityLogger (alias)
│   ├── MatchMode/                 ← All match operation services and repositories
│   ├── Modules/                   ← ModuleManager, ModuleInterface
│   ├── Permissions/               ← PermissionManager, ClubRoleCapabilityRegistrar
│   ├── Portal/                    ← PortalRouter, MemberPortalService, CoachDashboardService
│   ├── Projects/                  ← ClubProject entity, service, repository
│   ├── Registrations/             ← Player registration workflow
│   ├── Relationships/             ← Person relationships and team membership
│   ├── Release/                   ← Release readiness inventories and service
│   ├── SeasonPlanning/            ← Season plan generation, approval, execution
│   ├── Seasons/                   ← Season and TeamSeason lifecycle
│   ├── Settings/                  ← SettingsManager, BrandingManager
│   ├── Statistics/                ← Player and team statistics services
│   ├── UI/                        ← All PHP UI components, pages and layouts
│   │   ├── AdminUI.php            ← Admin menu registration
│   │   ├── Components/            ← Reusable PHP components
│   │   ├── Design/                ← DesignTokens
│   │   ├── Layouts/               ← Layout templates
│   │   └── Pages/                 ← All admin and portal page classes
│   ├── Upgrade/                   ← UpgradeRunner, UpgradeVersions, UpgradeLock
│   ├── Users/                     ← UserLinkManager
│   ├── Venues/                    ← VenueRepository
│   └── Weather/                   ← WeatherService
├── Database/                      ← Legacy database helpers (deprecated)
├── Helpers/                       ← Legacy helper functions (deprecated)
├── People/                        ← Legacy PeopleRepository (still active)
├── Permissions/                   ← Legacy PermissionManager and Roles (still active)
├── Services/                      ← Legacy service classes (deprecated)
├── TeamAssignments/               ← TeamAssignmentRepository (still active)
└── Teams/                         ← Legacy TeamRepository (still active)
```

> **Note:** The `app/` root-level directories (`People/`, `Teams/`, `TeamAssignments/`, `Permissions/`) contain legacy code that is still actively used. They are not deprecated but have not been migrated to `app/core/`. Do not move them without a migration plan.

---

## Module Status Summary

See [`reference/MODULE_STATUS.md`](../reference/MODULE_STATUS.md) for the complete status register.

| Module | Status |
|---|---|
| Application boot | Complete |
| People | MVP Complete |
| Teams and assignments | MVP Complete |
| Seasons | MVP Complete |
| Season planning | MVP Complete |
| Relationships | MVP Complete |
| Venues | Complete |
| Events and audience | MVP Complete |
| Attendance | MVP Complete |
| Match operations | MVP Complete |
| Football statistics | MVP Complete |
| Player registrations | MVP Complete |
| Finance and billing | MVP Complete |
| Communications | MVP Complete |
| Member portal and experience | MVP Complete |
| Executive dashboard | MVP Complete |
| Branding and Media | MVP Complete |
| Permissions | Complete |
| Activity and timelines | MVP Complete |
| Weather | Placeholder |
