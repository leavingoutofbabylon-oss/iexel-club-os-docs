# Database Architecture

**Source of truth:** `app/core/Database/DatabaseManager.php`
**Last verified:** 2026-07-24

---

## Overview

Club OS owns 42 custom MySQL tables. All tables are created and maintained exclusively by `DatabaseManager`. No other code creates or alters tables.

All table names follow the pattern: `{wpdb->prefix}iexel_os_{logical_name}`

For example, with the default WordPress prefix `wp_`, the `people` table is `wp_iexel_os_people`.

---

## Table Naming Convention

```php
// In DatabaseManager:
public function table(string $name): string {
    global $wpdb;
    return ($this->table_prefix ?? $wpdb->prefix) . 'iexel_os_' . $name;
}
```

The `$this->table_prefix` parameter allows `DatabaseManager` to be instantiated with a custom prefix for testing.

---

## Canonical Table List

The `CANONICAL_TABLES` constant defines the authoritative list of all 42 tables:

```php
public const CANONICAL_TABLES = [
    'activity_log', 'system_flags', 'people', 'person_roles', 'person_relationships',
    'teams', 'team_assignments', 'venues', 'events', 'event_audience', 'attendance',
    'event_availability', 'seasons', 'team_seasons', 'player_registrations',
    'formation_templates', 'formation_template_slots', 'event_match_details',
    'event_match_selections', 'event_match_lineups', 'event_match_incidents',
    'event_match_action_requests', 'event_match_reports', 'event_match_player_ratings',
    'finance_accounts', 'finance_invoices', 'finance_invoice_lines', 'finance_payments',
    'finance_payment_allocations', 'finance_invoice_events', 'finance_billing_schedules',
    'finance_fee_rules', 'finance_discount_policies', 'club_projects',
    'finance_billing_runs', 'finance_billing_run_items', 'communications',
    'communication_recipients', 'communication_deliveries', 'communication_templates',
    'communication_attachments', 'communication_events',
];
```

See [`reference/DATABASE_TABLE_REFERENCE.md`](../reference/DATABASE_TABLE_REFERENCE.md) for the full schema documentation of each table.

---

## Schema Versioning

Club OS uses two independent version numbers stored as WordPress options:

| Option | Constant | Purpose |
|---|---|---|
| `iexel_club_os_schema_version` | `UpgradeVersions::SCHEMA_VERSION` | DDL changes (table creation, column additions) |
| `iexel_club_os_data_version` | `UpgradeVersions::DATA_VERSION` | Data migrations and seed data |

The upgrade pipeline compares the stored version against the current version to determine whether an upgrade is needed.

---

## Upgrade Pipeline

Schema and data changes are applied through the `UpgradeRunner`. Each step is idempotent — the `is_valid()` callable checks whether the step has already been applied before `apply()` is called.

Current upgrade steps (as of 0.2.10-dev):

| Step ID | Kind | Description |
|---|---|---|
| `2026_07_legacy_unique_preflight` | data | Remove duplicate legacy audience and attendance rows before unique indexes are reconciled. |
| `2026_07_canonical_schema` | schema | Install or reconcile all canonical Club OS tables. |
| `2026_07_compatibility_schema` | schema | Repair known historical columns, indexes and signed finance fields. |
| `2026_07_legacy_data` | data | Normalise supported legacy match data after schema reconciliation. |
| `2026_07_formation_templates_and_lineup_refactor` | schema | Create formation templates, refactor match lineup to metadata-only, extend match selections with formation data. |
| `2026_07_seed_formation_templates` | data | Seed system formation templates (7v7, 9v9, 11v11) into the database. |
| `2026_07_seed_5v5_formation_templates` | data | Seed 5v5 system formation templates (1-2-1, 2-1-1, 1-1-2) into the database. |