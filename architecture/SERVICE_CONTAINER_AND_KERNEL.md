# Service Container and Kernel

**Source of truth:** `app/core/Container/Container.php` and `app/core/Kernel.php`
**Last verified:** 2026-07-24

---

## Two Patterns

Club OS uses two complementary dependency injection patterns that serve different purposes.

---

## 1. Application Container (`Container`)

**File:** `app/core/Container/Container.php`
**Namespace:** `IEXEL\ClubOS\Core\Container`

The `Container` is a minimal singleton DI container used exclusively by `Application` to manage the six core infrastructure services. It supports only singleton bindings.

```php
final class Container {
    public function singleton($id, callable $factory): void;
    public function get($id): mixed;
}
```

Services registered in the container:

| Service class | Accessor |
|---|---|
| `SettingsManager` | `$container->get(SettingsManager::class)` |
| `ActivityLogger` | `$container->get(ActivityLogger::class)` |
| `DatabaseManager` | `$container->get(DatabaseManager::class)` |
| `PermissionManager` | `$container->get(PermissionManager::class)` |
| `ModuleManager` | `$container->get(ModuleManager::class)` |
| `AdminUI` | `$container->get(AdminUI::class)` |

The container is only used by `Application`. All other code uses `Kernel`.

---

## 2. Kernel (Service Locator)

**File:** `app/core/Kernel.php`
**Namespace:** `IEXEL\ClubOS\Core`

`Kernel` is a lazy-initialising service locator. Each public method instantiates its service on first call and caches it as a private property using `??=`. Each request handler receives its own `Kernel` instance.

### Complete Service Accessor Inventory

The following table lists every public accessor method on `Kernel` as of version 0.2.10-dev.

| Accessor | Returns | Module |
|---|---|---|
| `version()` | `string` | Core |
| `database()` | `DatabaseManager` | Database |
| `settings()` | `SettingsManager` | Settings |
| `logger()` | `ActivityLogger` | Activity |
| `people()` | `PeopleRepository` | People |
| `teams()` | `TeamRepository` | Teams |
| `team_assignments()` | `TeamAssignmentRepository` | Teams |
| `venues()` | `VenueRepository` | Venues |
| `season_repository()` | `SeasonRepository` | Seasons |
| `current_season()` | `CurrentSeasonService` | Seasons |
| `team_season_repository()` | `TeamSeasonRepository` | Seasons |
| `team_seasons()` | `TeamSeasonService` | Seasons |
| `season_reconciliation()` | `SeasonReconciliationService` | Seasons |
| `season_backfill_planner()` | `SeasonBackfillPlanner` | Seasons |
| `season_backfill()` | `SeasonBackfillService` | Seasons |
| `season_link_migration_planner()` | `SeasonLinkMigrationPlanner` | Seasons |
| `season_link_migration()` | `SeasonLinkMigrationService` | Seasons |
| `season_context_resolver()` | `SeasonContextResolver` | Seasons |
| `season_context()` | `SeasonContextService` | Seasons |
| `age_group_progression()` | `AgeGroupProgressionService` | Season Planning |
| `football_format_progression()` | `FootballFormatProgressionService` | Season Planning |
| `season_plan_validator()` | `SeasonPlanValidator` | Season Planning |
| `season_planning_contributors()` | `array` | Season Planning |
| `season_planning()` | `SeasonPlanningService` | Season Planning |
| `season_plan_serializer()` | `SeasonPlanSerializer` | Season Planning |
| `season_plan_fingerprints()` | `SeasonPlanFingerprintService` | Season Planning |
| `season_plan_repository()` | `SeasonPlanRepository` | Season Planning |
| `season_execution_gateway()` | `CanonicalSeasonExecutionGateway` | Season Planning |
| `season_plan_approval()` | `SeasonPlanApprovalService` | Season Planning |
| `season_execution_contributors()` | `array` | Season Planning |
| `season_plan_transaction()` | `WordPressSeasonPlanTransaction` | Season Planning |
| `season_plan_execution()` | `SeasonPlanExecutionService` | Season Planning |
| `player_registrations()` | `PlayerRegistrationRepository` | Registrations |
| `player_registration_validator()` | `PlayerRegistrationValidator` | Registrations |
| `player_registration_service()` | `PlayerRegistrationService` | Registrations |
| `parent_registration_portal()` | `ParentRegistrationPortalService` | Registrations |
| `events()` | `EventRepository` | Events |
| `team_events_workspace()` | `TeamEventsWorkspaceService` | Events |
| `event_location_resolver()` | `EventLocationResolver` | Events |
| `event_audience()` | `EventAudienceRepository` | Events |
| `event_audience_builder()` | `EventAudienceBuilder` | Events |
| `branding()` | `BrandingManager` | Branding |
| `branding_service()` | `BrandingService` | Branding |
| `weather()` | `WeatherService` | Weather |
| `user_links()` | `UserLinkManager` | Users |
| `permissions()` | `PermissionManager` | Permissions |
| `portal()` | `MemberPortalService` | Portal |
| `availability()` | `AvailabilityRepository` | Attendance |
| `team_availability()` | `TeamAvailabilityService` | Attendance |
| `attendance()` | `AttendanceRepository` | Attendance |
| `team_attendance()` | `TeamAttendanceService` | Attendance |
| `match_details()` | `MatchDetailsRepository` | Match Mode |
| `match_details_submission()` | `MatchDetailsSubmissionService` | Match Mode |
| `match_selection()` | `MatchSelectionRepository` | Match Mode |
| `match_shirt_number_resolver()` | `MatchShirtNumberResolver` | Match Mode |
| `match_eligible_players()` | `MatchEligiblePlayerService` | Match Mode |
| `match_lineup_submission()` | `MatchLineupSubmissionService` | Match Mode |
| `match_lineup_repository()` | `MatchLineupRepository` | Match Mode |
| `formation_template_repository()` | `FormationTemplateRepository` | Match Mode |
| `formation_validator()` | `FormationValidator` | Match Mode |
| `formation_engine()` | `FormationEngine` | Match Mode |
| `match_incidents()` | `MatchIncidentRepository` | Match Mode |
| `match_state()` | `MatchStateService` | Match Mode |
| `match_goals()` | `MatchGoalService` | Match Mode |
| `match_incident_undo()` | `MatchIncidentUndoService` | Match Mode |
| `match_mode_requests()` | `MatchModeRequestHandler` | Match Mode |
| `match_mode()` | `MatchModeService` | Match Mode |
| `match_pitch_state()` | `MatchPitchStateService` | Match Mode |
| `match_readiness()` | `MatchReadinessService` | Match Mode |
| `match_reports()` | `MatchReportRepository` | Match Mode |
| `match_player_ratings()` | `MatchPlayerRatingRepository` | Match Mode |
| `match_report_service()` | `MatchReportService` | Match Mode |
| `match_substitutions()` | `MatchSubstitutionService` | Match Mode |
| `match_substitution_undo()` | `MatchSubstitutionUndoService` | Match Mode |
| `match_goalkeeper_state()` | `MatchGoalkeeperStateService` | Match Mode |
| `match_goalkeeper_changes()` | `MatchGoalkeeperChangeService` | Match Mode |
| `relationships()` | `PersonTeamMembershipService` | Relationships |
| `person_relationships()` | `PersonRelationshipRepository` | Relationships |
| `relationship_reconciliation()` | `RelationshipReconciliationService` | Relationships |
| `sensitive_access()` | `SensitiveModuleAccess` | Permissions |
| `coach_dashboard()` | `CoachDashboardService` | Portal |
| `statistics_eligibility()` | `StatisticsEligibilityPolicy` | Statistics |
| `match_incident_statistics()` | `MatchIncidentStatisticsMapper` | Statistics |
| `player_statistics_repository()` | `PlayerStatisticsRepository` | Statistics |
| `football_statistics()` | `FootballStatisticsEngine` | Statistics |
| `match_result_projection()` | `MatchResultProjection` | Statistics |
| `team_statistics_repository()` | `TeamStatisticsRepository` | Statistics |
| `player_statistics()` | `PlayerStatisticsService` | Statistics |
| `team_statistics()` | `TeamStatisticsService` | Statistics |
| `finance_repository()` | `FinanceRepository` | Finance |
| `finance_validator()` | `FinanceValidator` | Finance |
| `finance()` | `FinanceService` | Finance |
| `recurring_billing_repository()` | `RecurringBillingRepository` | Finance |
| `recurring_billing()` | `RecurringBillingService` | Finance |
| `communication_repository()` | `CommunicationRepository` | Communications |
| `communication_audience()` | `CommunicationAudienceResolver` | Communications |
| `communication_validator()` | `CommunicationValidator` | Communications |
| `communication_scheduler()` | `CommunicationScheduler` | Communications |
| `communications()` | `CommunicationService` | Communications |
| `member_experience_resolver()` | `MemberExperienceResolver` | Portal |
| `member_experience()` | `MemberExperienceService` | Portal |
| `club_projects()` | `ClubProjectRepository` | Projects |
| `club_project_validator()` | `ClubProjectValidator` | Projects |
| `club_project_service()` | `ClubProjectService` | Projects |
| `dashboard()` | `DashboardService` | Dashboard |
| `authentication()` | `AuthenticationService` | Authentication |
| `entity_dependency_inspector()` | `EntityDependencyInspector` | Entity Lifecycle |
| `entity_lifecycle()` | `EntityLifecycleService` | Entity Lifecycle |

---

## Usage Pattern

```php
// In a request handler:
final class MyRequestHandler {
    public function __construct(private Kernel $kernel) {}

    public function register(): void {
        add_action('admin_post_my_action', [$this, 'handle']);
    }

    public function handle(): void {
        $result = $this->kernel->my_service()->do_something();
    }
}

// In Application::boot():
(new MyRequestHandler(new Kernel()))->register();
```

---

## Design Rationale

See [`decisions/ADR-003-REPOSITORY-SERVICE-SEPARATION.md`](../decisions/ADR-003-REPOSITORY-SERVICE-SEPARATION.md) for the rationale behind the Kernel pattern.

The key properties of this design are:

1. **Lazy initialisation** — Services are only instantiated when first accessed, reducing memory usage for requests that only touch a subset of modules.
2. **Contextual Kernel Sharing** — Kernels are shared within specific contexts to enable service reuse and caching. The shared billing Kernel is used by `FinanceAdminRequestHandler`, `TeamAssignmentAdminRequestHandler`, `ClubProjectAdminRequestHandler`, and the billing cron closure. The shared communication Kernel is used by `CommunicationAdminRequestHandler` and the communication cron closure.
3. **No global state** — There is no static service registry. All service resolution flows through `Kernel` instances.
4. **Testability** — `Kernel` can be subclassed or mocked in tests to override specific services.
