# Application Lifecycle

**Source of truth:** `app/core/Application.php`, `app/core/Activator.php`, `app/core/Deactivator.php`
**Last verified:** 2026-07-24

---

## Plugin Lifecycle Events

### Activation

Triggered by `register_activation_hook` in `iexel-club-os.php`.

```
Activator::activate()
├── Check PHP 8.2+ and WordPress 6.7+
├── UpgradeRunner::run('activation')
│   └── Run all upgrade steps in order
├── PermissionManager::register()
│   └── ClubRoleCapabilityRegistrar::register()
│       └── ensure_role() for all 6 Club OS roles
├── Roles::register()
├── SettingsManager::ensure_defaults()
├── UpgradeLifecycle::reconcile_schedulers()
├── PortalRouter::add_rewrite_rules()
├── delete_option('iexel_club_os_rewrite_schema')
└── flush_rewrite_rules()
```

### Normal Request Boot

Triggered by `plugins_loaded` hook.

```
Application::instance()->boot()
├── register_services()
│   └── Bind SettingsManager, ActivityLogger, DatabaseManager,
│       PermissionManager, ModuleManager, AdminUI to Container
├── Register all request handlers (each with new Kernel())
│   ├── PortalRouter
│   ├── AuthenticationRequestHandler
│   ├── AdminAccessBoundary
│   ├── BrandingAdminRequestHandler
│   ├── EntityMediaAdminRequestHandler
│   ├── EntityLifecycleAdminRequestHandler
│   ├── PersonRelationshipRequestHandler
│   ├── RegistrationPortalRequestHandler
│   ├── MemberExperienceRequestHandler
│   ├── CommunicationAdminRequestHandler
│   ├── FinanceAdminRequestHandler
│   ├── TeamAssignmentAdminRequestHandler
│   ├── ClubProjectAdminRequestHandler
│   └── UpgradeAdminController
├── Register WP-Cron listeners
│   ├── iexel_club_os_process_communication → CommunicationService
│   └── iexel_club_os_process_billing_schedules → RecurringBillingService
├── PermissionManager::register()
├── ModuleManager::boot()
│   ├── do_action('iexel_club_os_modules_booting')
│   └── do_action('iexel_club_os_modules_booted')
├── add_action('admin_menu', AdminUI::register_menu)
├── add_action('admin_enqueue_scripts', AdminUI::enqueue_assets)
├── add_action('login_enqueue_scripts', Application::enqueue_login_branding)
├── add_action('wp_head', Application::render_app_icon)
├── add_action('admin_head', Application::render_app_icon)
├── add_action('login_head', Application::render_app_icon)
└── ActivityLogger::log_once_per_request('core_booted')
```

### Deactivation

Triggered by `register_deactivation_hook` in `iexel-club-os.php`.

```
Deactivator::deactivate()
├── CommunicationScheduler::clear_all()
├── WordPressBillingScheduler::clear_all()
├── update_option('iexel_club_os_last_cron_cleanup', evidence)
└── delete_option('iexel_club_os_rewrite_schema')
```

---

## Upgrade State Machine

The `UpgradeRunner` persists its state in the `iexel_club_os_upgrade_state` option. Possible states:

| State | Meaning |
|---|---|
| `running` | Upgrade is currently executing |
| `complete` | All steps completed successfully |
| `failed` | A step failed; error details are stored |
| `already_current` | No upgrade needed |
| `future_version` | Plugin version is ahead of schema version (downgrade guard) |
| `locked` | Another upgrade is already running |

The `UpgradeStatus::current()` method returns a `ready` boolean that gates portal access. If `ready` is false, the portal returns a 503 maintenance page.

---

## Scheduled Tasks

| Hook | Schedule | Processor |
|---|---|---|
| `iexel_club_os_process_communication` | Single event per communication (batched requeue) | `CommunicationService::process_scheduled_communication()` |
| `iexel_club_os_process_billing_schedules` | Hourly recurring | `RecurringBillingService::process_due()` |

Both hooks are cleared on deactivation and reconciled on activation via `UpgradeLifecycle::reconcile_schedulers()`.
