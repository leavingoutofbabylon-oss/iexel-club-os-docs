# Permissions and Roles Architecture

**Source of truth:** `app/core/Permissions/ClubRoleCapabilityRegistrar.php`, `app/core/Permissions/PermissionManager.php`
**Last verified:** 2026-07-24

---

## Overview

Club OS extends the WordPress capability system with 26 custom capabilities and 6 custom roles. All capabilities are prefixed `iexel_` and are registered on every request via `PermissionManager::register()`.

For the complete capability and role inventory, see [`reference/CAPABILITY_REFERENCE.md`](../reference/CAPABILITY_REFERENCE.md).

---

## Registration

Capabilities and roles are registered in two places:

1. **On activation** — `Activator::activate()` calls `PermissionManager::register()` and `Roles::register()` to ensure capabilities and roles exist in the WordPress database.
2. **On every request** — `Application::boot()` calls `$this->container->get(PermissionManager::class)->register()` to ensure capabilities are always available, even if the database was modified externally.

---

## Capability Hierarchy

```
iexel_manage_club_os          ← Top-level administration
├── iexel_manage_people       ← People management
├── iexel_manage_teams        ← Team administration
├── iexel_manage_events       ← Event management
├── iexel_manage_communications ← Communications
├── iexel_view_audit_log      ← Audit log
├── iexel_manage_settings     ← Settings
├── iexel_view_club_projects  ← View projects
│   ├── iexel_create_club_projects
│   ├── iexel_edit_club_projects
│   ├── iexel_archive_club_projects
│   └── iexel_manage_club_project_visibility
└── iexel_manage_rewards      ← Rewards (placeholder)

iexel_view_finance            ← Finance read access
├── iexel_manage_finance      ← Invoice and payment management
├── iexel_record_payments     ← Payment recording
├── iexel_manage_billing      ← Billing schedules and fee rules
└── iexel_export_finance      ← Finance exports

iexel_coach_portal            ← Coach portal access
├── iexel_manage_assigned_team ← Team management boundary
├── iexel_view_player_statistics ← Player statistics
├── iexel_manage_events       ← Event management
├── iexel_manage_match_reports ← Match reporting
└── iexel_manage_attendance   ← Attendance management

iexel_view_welfare            ← Welfare read access
└── iexel_manage_welfare      ← Welfare management

iexel_parent_portal           ← Parent portal access
```

---

## SensitiveModuleAccess

`SensitiveModuleAccess` provides programmatic access checks for modules that require additional boundaries beyond page-level capabilities. It is used by:

- **Finance module** — to enforce `iexel_view_finance` / `iexel_manage_finance` within portal workspaces
- **Welfare module** — to enforce `iexel_view_welfare` / `iexel_manage_welfare`

---

## TreasurerAccessManager

`TreasurerAccessManager` manages the wp-admin access boundary for the `iexel_club_treasurer` role. Treasurers can access Finance admin pages but are blocked from all other wp-admin functionality.

---

## Design Principles

1. **Capabilities are checked at the handler level**, not just the page level. Every `admin_post_*` handler calls `current_user_can()` before processing any mutation.
2. **Nonces are always checked** alongside capabilities. The pattern is: check method is POST, check capability, check nonce.
3. **Portal access is role-based**, not capability-based. The `MemberExperienceService` determines which workspace to render based on the user's linked Person role, not their WordPress capability.
4. **No capability is invented** for features that do not exist. The `iexel_manage_rewards` and `iexel_manage_teams` capabilities are declared but not yet enforced in any page.
