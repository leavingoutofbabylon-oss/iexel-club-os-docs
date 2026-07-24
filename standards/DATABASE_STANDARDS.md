# Database Standards

**Applies to:** All database schema changes in `iexel-club-os`
**Last verified:** 2026-07-24

---

## Overview

Club OS manages its own database schema using `DatabaseManager` and `UpgradeRunner`. No WordPress post types or meta tables are used for Club OS domain data.

---

## Table Naming

All tables use the prefix `{wpdb->prefix}iexel_os_`. Table names are lowercase snake_case.

```
wp_iexel_os_people
wp_iexel_os_finance_invoices
wp_iexel_os_event_match_incidents
```

---

## Column Conventions

| Convention | Rule |
|---|---|
| Primary key | Always `id BIGINT UNSIGNED NOT NULL AUTO_INCREMENT` |
| Foreign keys | Named `{entity}_id BIGINT UNSIGNED NOT NULL` |
| Timestamps | Always `created_at DATETIME NOT NULL` and `updated_at DATETIME NOT NULL` where applicable |
| Soft delete | Use `is_archived TINYINT(1) NOT NULL DEFAULT 0` rather than hard delete where history matters |
| Status fields | Use `VARCHAR(50) NOT NULL DEFAULT 'active'` with documented allowed values |
| JSON fields | Use `LONGTEXT` for JSON columns; never use MySQL JSON type (WordPress 5.x compatibility) |
| Monetary values | Always `DECIMAL(10,2) UNSIGNED NOT NULL DEFAULT '0.00'` |
| Boolean flags | Use `TINYINT(1) NOT NULL DEFAULT 0` |

---

## Schema Changes

All schema changes must go through an upgrade step in `UpgradeRunner`. Never run `ALTER TABLE` outside an upgrade step.

Upgrade steps are named `{YYYY_MM}_{description}` and must be idempotent. Use `dbDelta()` for `CREATE TABLE` and `ALTER TABLE ADD COLUMN` operations. Use direct `$wpdb->query()` for `ALTER TABLE MODIFY COLUMN` and index changes.

```php
// Example upgrade step
private function upgrade_2026_07_add_display_order_to_club_projects(): void {
    $table = $this->db_manager->table('club_projects');
    $wpdb->query(
        "ALTER TABLE `{$table}` ADD COLUMN IF NOT EXISTS `display_order` INT UNSIGNED NOT NULL DEFAULT 0"
    );
}
```

---

## Indexes

Every table must have:
1. A primary key on `id`
2. An index on any column used in a `WHERE` clause
3. A unique index on any column that must be unique

Index names follow the pattern `idx_{table}_{column}`.

---

## Character Set

All tables use `DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci`. This is enforced by `DatabaseManager::get_charset_collate()`.

---

## Foreign Key Integrity

Club OS does not use MySQL foreign key constraints (WordPress compatibility). Referential integrity is enforced at the application layer in repository methods.

---

## Canonical Table List

The `CANONICAL_TABLES` constant in `DatabaseManager` is the authoritative list of all tables. The `ReleaseReadinessService` checks this list on every Release Readiness check. Any new table must be added to `CANONICAL_TABLES`.

---

## Compatibility Upgrades

The `2026_07_compatibility_schema` upgrade step repairs historical schema issues (e.g. signed `DECIMAL` columns in finance tables). This step is idempotent and runs on every upgrade. Do not remove it.
