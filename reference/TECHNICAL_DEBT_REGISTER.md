# Technical Debt Register

**Source of truth:** Source code inspection of `iexel-club-os`
**Last verified:** 2026-07-24

---

## Overview

This register documents known technical debt, inconsistencies and deferred work in the Club OS codebase. Items are categorised and prioritised.

Items marked **P1** should be addressed before Release 1.0. Items marked **P2** are post-MVP. Items marked **P3** are long-term.

---

## Capability Inconsistencies

| Item | Priority | Description |
|---|---|---|
| `iexel_manage_communications` not enforced | P2 | The `CommunicationAdminRequestHandler` checks `iexel_manage_club_os` instead of `iexel_manage_communications`. Should be corrected when the Communications module is hardened. |
| `iexel_manage_teams` not enforced | P2 | Declared in `CAPABILITIES` but not checked in any page or handler. Teams admin pages use `iexel_manage_club_os`. |
| `iexel_view_audit_log` not enforced | P2 | Declared but no admin page or handler checks it. |
| `iexel_manage_settings` not enforced | P2 | Declared but the Settings page uses `iexel_manage_club_os`. |
| `iexel_export_finance` not implemented | P2 | Declared and assigned to Treasurer role but no export functionality exists. |
| `iexel_manage_rewards` placeholder | P3 | Declared but Rewards module is not implemented. |

---

## Legacy Code Migration

| Item | Priority | Description |
|---|---|---|
| `app/People/PeopleRepository.php` | P3 | Legacy repository still used by Kernel. Should be migrated to `app/core/People/`. |
| `app/Teams/TeamRepository.php` | P3 | Legacy repository still used by Kernel. Should be migrated to `app/core/Teams/`. |
| `app/TeamAssignments/TeamAssignmentRepository.php` | P3 | Legacy repository still used by Kernel. |
| `app/Permissions/PermissionManager.php` | P3 | Legacy class still used by Activator. Duplicate of `app/core/Permissions/PermissionManager.php`. |
| `app/Database/` | P3 | Deprecated; no new consumers. Can be removed after confirming no external references. |
| `app/Helpers/` | P3 | Deprecated; no new consumers. |
| `app/Services/` | P3 | Deprecated; no new consumers. |

---

## SQL Placeholder Pattern

| Item | Priority | Description |
|---|---|---|
| `IN ({$placeholders})` pattern | P2 | Multiple repositories use `implode(',', array_fill(...))` with `phpcs:ignore WordPress.DB.PreparedSQL.InterpolatedNotPrepared` to build `IN` clauses. This is a PHPCS suppression, not a security issue (values are properly prepared), but should be replaced with a helper method for consistency. Affected files: `PeopleRepository`, `TeamAssignmentRepository`, `AttendanceRepository`, `AvailabilityRepository`, `CommunicationAudienceResolver`, `EventRepository`, `BillingAudienceResolver`. |

---

## Weather Module

| Item | Priority | Description |
|---|---|---|
| Weather is a placeholder | P3 | `WeatherService` returns a cached placeholder forecast. No real weather API integration exists. The `iexel_weather_{postcode-hash}` transient is set but the data is synthetic. |

---

## Finance Module

| Item | Priority | Description |
|---|---|---|
| Finance export not implemented | P2 | `iexel_export_finance` capability is declared and assigned to the Treasurer role, but no export page or handler exists. |
| Signed finance field compatibility | P1 (done) | The `2026_07_compatibility_schema` upgrade step repairs historical signed `DECIMAL` columns in finance tables. This step is idempotent and runs on every upgrade. |

---

## Rewrite Rule Management

| Item | Priority | Description |
|---|---|---|
| Rewrite rule schema version stamp | P2 | The `iexel_club_os_rewrite_schema` option is used to avoid unnecessary `flush_rewrite_rules()` calls on every request. This option must be deleted on deactivation and after any rewrite rule change. The current implementation handles this correctly but the mechanism is fragile and undocumented. |

---

## Documentation Discrepancies

| Item | Priority | Description |
|---|---|---|
| *(None known at time of writing)* | — | Any discrepancy found between this documentation and source code should be added here. |
