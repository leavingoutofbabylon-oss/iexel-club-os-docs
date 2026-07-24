# Master Developer Guide

**Last verified:** 2026-07-24

---

## Overview

This guide is the primary entry point for developers working on Club OS. It covers environment setup, the development workflow, and pointers to all detailed documentation.

---

## Prerequisites

| Tool | Required version |
|---|---|
| PHP | 8.1 or higher |
| Composer | 2.x |
| WordPress | 6.4 or higher |
| MySQL / MariaDB | 8.0 / 10.6 or higher |
| Node.js | 18 or higher (for frontend tooling) |
| WP-CLI | 2.x (recommended) |

---

## Repository Setup

```bash
# Clone the source repository (read-only reference)
git clone https://github.com/leavingoutofbabylon-oss/iexel-club-os.git

# Clone the documentation repository
git clone https://github.com/leavingoutofbabylon-oss/iexel-club-os-docs.git

# Install PHP dependencies
cd iexel-club-os
composer install

# Symlink or copy the plugin into a local WordPress installation
ln -s $(pwd) /path/to/wordpress/wp-content/plugins/iexel-club-os
```

---

## Activation

Activate the plugin via WP-CLI or the WordPress admin:

```bash
wp plugin activate iexel-club-os
```

On activation, `Activator::activate()` runs:

1. Registers capabilities and roles via `PermissionManager`
2. Runs `UpgradeRunner` to install all database tables
3. Registers portal rewrite rules and flushes them
4. Sets the `iexel_club_os_activated` flag

---

## Development Workflow

See [BRANCHING_AND_GIT_WORKFLOW.md](BRANCHING_AND_GIT_WORKFLOW.md) for the full branching strategy.

The short version:

1. Create a feature branch from `main`: `feature/{ticket-id}-{description}`
2. Write code following the standards in `standards/`
3. Write or update tests
4. Open a pull request against `main`
5. Pass code review using the [CODE_REVIEW_CHECKLIST.md](CODE_REVIEW_CHECKLIST.md)
6. Merge after approval

---

## Key Architecture Documents

| Document | Purpose |
|---|---|
| [SYSTEM_OVERVIEW.md](../architecture/SYSTEM_OVERVIEW.md) | High-level architecture |
| [MODULE_MAP.md](../architecture/MODULE_MAP.md) | All modules and their responsibilities |
| [SERVICE_CONTAINER_AND_KERNEL.md](../architecture/SERVICE_CONTAINER_AND_KERNEL.md) | DI container and Kernel |
| [DATABASE_ARCHITECTURE.md](../architecture/DATABASE_ARCHITECTURE.md) | Database design and schema |
| [PERMISSIONS_AND_ROLES.md](../architecture/PERMISSIONS_AND_ROLES.md) | Capabilities and roles |
| [PORTAL_ARCHITECTURE.md](../architecture/PORTAL_ARCHITECTURE.md) | Member Portal design |
| [ROUTES_AND_ENTRY_POINTS.md](../architecture/ROUTES_AND_ENTRY_POINTS.md) | All entry points |
| [APPLICATION_LIFECYCLE.md](../architecture/APPLICATION_LIFECYCLE.md) | Boot, activation, upgrade |

---

## Key Reference Documents

| Document | Purpose |
|---|---|
| [CAPABILITY_REFERENCE.md](../reference/CAPABILITY_REFERENCE.md) | All 26 capabilities |
| [ADMIN_MENU_REFERENCE.md](../reference/ADMIN_MENU_REFERENCE.md) | All admin pages |
| [PORTAL_ROUTE_REFERENCE.md](../reference/PORTAL_ROUTE_REFERENCE.md) | All portal routes |
| [REQUEST_ACTION_REFERENCE.md](../reference/REQUEST_ACTION_REFERENCE.md) | All admin_post actions |
| [DATABASE_TABLE_REFERENCE.md](../reference/DATABASE_TABLE_REFERENCE.md) | All database tables |
| [MODULE_STATUS.md](../reference/MODULE_STATUS.md) | Module implementation status |
| [TECHNICAL_DEBT_REGISTER.md](../reference/TECHNICAL_DEBT_REGISTER.md) | Known technical debt |
| [GLOSSARY.md](../reference/GLOSSARY.md) | Domain terminology |

---

## Adding a New Module

1. Create a directory under `app/core/{ModuleName}/`
2. Create a `{ModuleName}Service.php` and `{ModuleName}Repository.php`
3. Register the service in `Kernel.php`
4. Add the module to `ReleaseModuleInventory.php`
5. Register any new capabilities in `ClubRoleCapabilityRegistrar.php` and `ReleaseCapabilityInventory.php`
6. Register any new admin pages in `AdminUI.php` and `ReleaseRouteInventory.php`
7. Register any new portal routes in `PortalRouter.php` and `ReleaseRouteInventory.php`
8. Register any new request handlers in `Application.php`
9. Add any new database tables to `DatabaseManager.php` and `ReleaseSchemaInventory.php`
10. Write an upgrade step in `UpgradeRunner.php`
11. Update `MODULE_STATUS.md` and `DATABASE_TABLE_REFERENCE.md`

---

## Running Tests

```bash
cd iexel-club-os
./vendor/bin/phpunit
```

---

## Release Readiness Check

The Release Readiness page (`/wp-admin/admin.php?page=iexel-club-os-release-readiness`) checks all modules, capabilities, routes and schema against their inventories. Run this check before every release.
