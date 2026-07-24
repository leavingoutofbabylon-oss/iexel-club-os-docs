# ADR-004: Controlled Database Upgrades via UpgradeRunner

**Status:** Accepted
**Date:** 2025-02-01 (estimated)
**Last verified:** 2026-07-24

---

## Context

WordPress plugins typically use `dbDelta()` for schema management, which handles `CREATE TABLE` and `ADD COLUMN` operations but not `MODIFY COLUMN`, index changes or data migrations. Club OS needs a more controlled upgrade mechanism that can handle complex migrations and be verified for correctness.

---

## Decision

Club OS uses a custom `UpgradeRunner` class that:

1. Maintains an ordered list of named upgrade steps
2. Tracks which steps have been executed in the `system_flags` table
3. Executes only steps that have not yet been run
4. Is idempotent — running the same step twice has no effect

Each upgrade step is a private method named `upgrade_{YYYY_MM}_{description}()`.

---

## Consequences

**Positive:**
- Schema changes are versioned and auditable
- Complex migrations (data transformations, column type changes) are supported
- Idempotency means the runner can be called safely on every activation
- The `ReleaseReadinessService` can verify that all expected steps have been executed

**Negative:**
- More boilerplate than `dbDelta()` alone
- Developers must remember to add upgrade steps for all schema changes
- Steps can never be removed (they must remain for installations upgrading from older versions)

---

## Implementation

- `app/core/Upgrade/UpgradeRunner.php`
- `app/core/Upgrade/UpgradeVersions.php`
- Standards: [DATABASE_STANDARDS.md](../standards/DATABASE_STANDARDS.md)
