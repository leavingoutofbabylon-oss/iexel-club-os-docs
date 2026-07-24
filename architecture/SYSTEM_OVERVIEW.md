# System Overview

**Source of truth:** `iexel-club-os/iexel-club-os.php` and `app/core/Application.php`
**Version:** 0.2.10-dev
**Last verified:** 2026-07-24

---

## What Club OS Is

IEXEL Club OS is a single WordPress plugin (`iexel-club-os`) that provides a complete football club operating system for IEXEL F.C. It is **proprietary** software developed exclusively for IEXEL F.C. and is not distributed publicly.

The plugin requires:

- **WordPress** 6.7 or later
- **PHP** 8.2 or later
- **MySQL** 5.7+ or MariaDB 10.3+ (via `$wpdb`)

There are no Composer runtime dependencies. The autoloader is a custom PSR-4 implementation registered via `spl_autoload_register` in the plugin bootstrap file.

---

## Two Surfaces

Club OS delivers two distinct user-facing surfaces that share the same PHP codebase and database.

### 1. Administrator Surface (wp-admin)

The administrator surface is a set of pages registered under the WordPress admin menu using `add_menu_page` and `add_submenu_page`. All pages are registered under the top-level slug `iexel-club-os`.

Access to each page is controlled by a WordPress capability. The `AdminAccessBoundary` class prevents non-Club-OS users from accessing wp-admin entirely.

See [`reference/ADMIN_MENU_REFERENCE.md`](../reference/ADMIN_MENU_REFERENCE.md) for the full page inventory.

### 2. Member Portal (frontend)

The member portal is a custom frontend surface mounted at `/club-os/`. It uses WordPress rewrite rules to intercept requests and render PHP templates that output complete HTML pages, bypassing the active WordPress theme entirely.

The portal is role-aware. After authentication, the `MemberExperienceService` resolves the current user's active experience role and renders the appropriate workspace. The five experience roles are:

| Role | Workspace |
|---|---|
| Parent | Parent dashboard with child profiles, registrations and events |
| Player | Player dashboard with upcoming events and statistics |
| Coach | Coach workspace with team management, events and match operations |
| Committee | Committee dashboard with governance, projects and finance overview |
| Treasurer | Finance workspace with full billing and invoice management |

See [`reference/PORTAL_ROUTE_REFERENCE.md`](../reference/PORTAL_ROUTE_REFERENCE.md) for the full route inventory.

---

## Boot Sequence

The plugin boots on the `plugins_loaded` hook via:

```php
add_action('plugins_loaded', static function () {
    \IEXEL\ClubOS\Core\Application::instance()->boot();
});
```

`Application::boot()` performs the following steps in order:

1. **Register services** — Binds `SettingsManager`, `ActivityLogger`, `DatabaseManager`, `PermissionManager`, `ModuleManager` and `AdminUI` as singletons in the `Container`.
2. **Register request handlers** — Instantiates and registers all `admin_post_*` and `wp_ajax_*` handlers. Each handler receives its own `Kernel` instance.
3. **Register scheduled task listeners** — Binds `iexel_club_os_process_communication` and `iexel_club_os_process_billing_schedules` WP-Cron hooks to their respective service methods.
4. **Register UpgradeAdminController** — Registers the upgrade admin page and AJAX handler.
5. **Boot PermissionManager** — Registers all custom Club OS capabilities and roles via `ClubRoleCapabilityRegistrar`.
6. **Boot ModuleManager** — Fires `iexel_club_os_modules_booting` and `iexel_club_os_modules_booted` action hooks for third-party module registration.
7. **Register admin menu** — Hooks `AdminUI::register_menu` to `admin_menu`.
8. **Register branding hooks** — Hooks login page branding and app icon rendering.
9. **Log boot event** — Writes a `core_booted` activity log entry.

---

## Activation and Deactivation

### Activation (`Activator::activate`)

1. Checks PHP 8.2 and WordPress 6.7 minimum versions.
2. Runs `UpgradeRunner::run('activation')` — installs or upgrades the full database schema.
3. Registers capabilities and roles via `PermissionManager` and `Roles::register()`.
4. Ensures settings defaults via `SettingsManager::ensure_defaults()`.
5. Reconciles WP-Cron schedulers via `UpgradeLifecycle::reconcile_schedulers()`.
6. Registers portal rewrite rules and flushes the WordPress rewrite rule cache.

### Deactivation (`Deactivator::deactivate`)

1. Clears all scheduled `iexel_club_os_process_communication` WP-Cron events.
2. Clears all scheduled `iexel_club_os_process_billing_schedules` WP-Cron events.
3. Records deactivation evidence in `iexel_club_os_last_cron_cleanup` option.
4. Deletes the `iexel_club_os_rewrite_schema` option so rewrite rules are re-registered on next activation.

---

## Namespace and Autoloading

All Club OS PHP classes use the namespace `IEXEL\ClubOS\` and map to the `app/` directory:

```
IEXEL\ClubOS\Core\Kernel              → app/core/Kernel.php
IEXEL\ClubOS\Core\Finance\Invoice    → app/core/Finance/Invoice.php
IEXEL\ClubOS\People\PeopleRepository → app/People/PeopleRepository.php
```

There is no Composer autoloader. The autoloader is registered in `iexel-club-os.php`.

---

## Two Service Container Patterns

Club OS uses two complementary dependency injection patterns:

### 1. Application Container (`Container`)

A minimal singleton DI container used by `Application` to manage the five core infrastructure services: `SettingsManager`, `ActivityLogger`, `DatabaseManager`, `PermissionManager`, `ModuleManager` and `AdminUI`. These services are shared across the entire request.

### 2. Kernel (Service Locator)

`Kernel` is a lazy-initialising service locator that provides access to all domain services. Each domain service is instantiated on first access via a public accessor method (e.g. `$kernel->finance_service()`, `$kernel->events()`). Services are cached as private properties using `??=`.

Each request handler receives its own `Kernel` instance, preventing cross-handler state pollution.

See [`architecture/SERVICE_CONTAINER_AND_KERNEL.md`](SERVICE_CONTAINER_AND_KERNEL.md) for the full service accessor inventory.

---

## Database

Club OS owns 42 custom database tables, all prefixed with `{wpdb->prefix}iexel_os_`. Tables are created and maintained by `DatabaseManager::install()` and the `UpgradeRunner` pipeline.

See [`reference/DATABASE_TABLE_REFERENCE.md`](../reference/DATABASE_TABLE_REFERENCE.md) for the full table inventory.
See [`architecture/DATABASE_ARCHITECTURE.md`](DATABASE_ARCHITECTURE.md) for schema design decisions.

---

## Upgrade System

Club OS uses a custom upgrade pipeline (`UpgradeRunner`) that runs sequentially ordered steps. Each step has a unique string ID, a kind (`schema` or `data`), an `apply()` callable and an `is_valid()` callable. Schema steps run directly. Data steps are wrapped in a MySQL transaction.

The upgrade state is persisted in the `iexel_club_os_upgrade_state` WordPress option and is visible on the System Status admin page.

---

## Key WordPress Integration Points

| Hook | Purpose |
|---|---|
| `plugins_loaded` | Boot the entire application |
| `register_activation_hook` | Run database install and setup |
| `register_deactivation_hook` | Clear cron jobs and rewrite rules |
| `admin_menu` | Register wp-admin pages |
| `admin_enqueue_scripts` | Enqueue admin CSS/JS |
| `login_enqueue_scripts` | Inject branded login page styles |
| `wp_head` / `admin_head` / `login_head` | Render custom app icon |
| `init` | Register portal rewrite rules |
| `template_redirect` | Intercept portal requests and render portal pages |
| `iexel_club_os_process_communication` | WP-Cron: process scheduled communications |
| `iexel_club_os_process_billing_schedules` | WP-Cron: process due billing schedules |
| `iexel_club_os_modules_booting` | Extension point for module registration |
| `iexel_club_os_modules_booted` | Extension point for post-boot module setup |

---

## Related Documents

- [`architecture/MODULE_MAP.md`](MODULE_MAP.md) — Complete module inventory
- [`architecture/SERVICE_CONTAINER_AND_KERNEL.md`](SERVICE_CONTAINER_AND_KERNEL.md) — Kernel service accessor inventory
- [`architecture/PORTAL_ARCHITECTURE.md`](PORTAL_ARCHITECTURE.md) — Portal routing and experience system
- [`architecture/DATABASE_ARCHITECTURE.md`](DATABASE_ARCHITECTURE.md) — Database design
- [`reference/DATABASE_TABLE_REFERENCE.md`](../reference/DATABASE_TABLE_REFERENCE.md) — Full table inventory
- [`reference/CAPABILITY_REFERENCE.md`](../reference/CAPABILITY_REFERENCE.md) — Roles and capabilities
