# Capability Reference

**Source of truth:** `app/core/Permissions/ClubRoleCapabilityRegistrar.php` and `app/core/Release/ReleaseCapabilityInventory.php`
**Last verified:** 2026-07-24

---

## Overview

Club OS registers 26 custom WordPress capabilities, all prefixed `iexel_`. They are registered on every request via `PermissionManager::register()` which calls `ClubRoleCapabilityRegistrar::register()`.

---

## Complete Capability Inventory

| Capability | Purpose | Registered to roles |
|---|---|---|
| `iexel_manage_club_os` | Full Club OS administration and Release Readiness | `iexel_club_admin`, `administrator` |
| `iexel_manage_people` | People and Person media management | `iexel_club_admin`, `administrator` |
| `iexel_manage_teams` | Team administration (declared; not yet enforced) | `iexel_club_admin`, `administrator` |
| `iexel_manage_events` | Event management (football roles) | `iexel_club_admin`, `iexel_head_coach`, `iexel_coach`, `administrator` |
| `iexel_manage_assigned_team` | Stored active Coach-Team boundary | `iexel_club_admin`, `iexel_head_coach`, `iexel_coach`, `administrator` |
| `iexel_view_player_statistics` | Player statistics within managed Team | `iexel_club_admin`, `iexel_head_coach`, `iexel_coach`, `administrator` |
| `iexel_manage_match_reports` | Match reporting | `iexel_club_admin`, `iexel_head_coach`, `iexel_coach`, `administrator` |
| `iexel_manage_attendance` | Attendance management | `iexel_club_admin`, `iexel_head_coach`, `iexel_coach`, `administrator` |
| `iexel_view_finance` | Read Finance data | `iexel_club_admin`, `iexel_club_treasurer`, `administrator` |
| `iexel_manage_finance` | Manage Finance (invoices, payments) | `iexel_club_admin`, `iexel_club_treasurer`, `administrator` |
| `iexel_record_payments` | Record and allocate Finance payments | `iexel_club_admin`, `iexel_club_treasurer`, `administrator` |
| `iexel_manage_billing` | Manage Billing Schedules, Fee Rules and Discount Policies | `iexel_club_admin`, `iexel_club_treasurer`, `administrator` |
| `iexel_export_finance` | Export Finance data (declared; not yet implemented) | `iexel_club_admin`, `iexel_club_treasurer`, `administrator` |
| `iexel_view_welfare` | Read welfare information | `iexel_club_admin`, `iexel_welfare_officer`, `administrator` |
| `iexel_manage_welfare` | Manage welfare information | `iexel_club_admin`, `iexel_welfare_officer`, `administrator` |
| `iexel_manage_rewards` | Rewards administration (placeholder; not yet implemented) | `iexel_club_admin`, `administrator` |
| `iexel_manage_communications` | Communications administration | `iexel_club_admin`, `administrator` |
| `iexel_view_audit_log` | Audit log viewing (declared; not yet enforced) | `iexel_club_admin`, `administrator` |
| `iexel_manage_settings` | Settings administration (declared; not yet enforced) | `iexel_club_admin`, `administrator` |
| `iexel_view_club_projects` | View Club Projects in administration | `iexel_club_admin`, `administrator` |
| `iexel_create_club_projects` | Create Club Projects | `iexel_club_admin`, `administrator` |
| `iexel_edit_club_projects` | Edit Club Projects | `iexel_club_admin`, `administrator` |
| `iexel_archive_club_projects` | Archive and restore Club Projects | `iexel_club_admin`, `administrator` |
| `iexel_manage_club_project_visibility` | Show or hide Club Projects from Committee Workspace | `iexel_club_admin`, `administrator` |
| `iexel_coach_portal` | Coach portal access | `iexel_head_coach`, `iexel_coach`, `administrator` |
| `iexel_parent_portal` | Parent portal access | `iexel_parent`, `administrator` |

---

## WordPress Roles Registered by Club OS

| Role slug | Display name | Capability set |
|---|---|---|
| `iexel_club_admin` | IEXEL Club Admin | All 24 `CAPABILITIES` constants |
| `iexel_head_coach` | IEXEL Head Coach | Football capabilities |
| `iexel_coach` | IEXEL Coach | Football capabilities |
| `iexel_parent` | IEXEL Parent / Guardian | `iexel_parent_portal` only |
| `iexel_club_treasurer` | IEXEL Club Treasurer | Finance capabilities |
| `iexel_welfare_officer` | IEXEL Welfare Officer | `iexel_view_welfare`, `iexel_manage_welfare` |

**Football capabilities** (Head Coach and Coach):
`iexel_coach_portal`, `iexel_manage_assigned_team`, `iexel_view_player_statistics`, `iexel_manage_events`, `iexel_manage_match_reports`, `iexel_manage_attendance`

**Finance capabilities** (Treasurer):
`iexel_view_finance`, `iexel_manage_finance`, `iexel_record_payments`, `iexel_manage_billing`, `iexel_export_finance`

> **Important:** The `iexel_club_treasurer` role explicitly has `manage_options`, `activate_plugins`, `edit_plugins`, `edit_theme_options`, `list_users`, `create_users`, `edit_users`, `delete_users`, `promote_users` and `iexel_manage_club_os` **removed** to prevent wp-admin access beyond the Finance workspace.

---

## Known Inconsistencies

- `iexel_manage_teams` is declared in `CAPABILITIES` but is not currently checked in any page or handler. Reserved for a future Teams administration boundary.
- `iexel_manage_rewards` is declared but the Rewards module is a placeholder. Do not gate any production code on this capability.
- `iexel_manage_communications` is declared but the Communications admin handler currently checks `iexel_manage_club_os`. Tracked in Technical Debt Register.
- `iexel_view_audit_log` and `iexel_manage_settings` are declared but not currently checked in any page.
- `iexel_export_finance` is declared but no export functionality is implemented.
