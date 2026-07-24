# Repository Standards

**Applies to:** All `*Repository.php` classes under `app/core/` and `app/`
**Last verified:** 2026-07-24

---

## Overview

Repositories are the only classes permitted to access `$wpdb` directly. Each repository is responsible for a single table or a tightly related set of tables.

---

## Naming

Repository classes are named `{Entity}Repository` (e.g. `PeopleRepository`, `FinanceRepository`). The class is placed in the module directory corresponding to its entity.

---

## Constructor

Repositories receive `$wpdb` and `DatabaseManager` via constructor injection.

```php
public function __construct(
    private readonly \wpdb $wpdb,
    private readonly DatabaseManager $db_manager
) {}
```

The table name is resolved in the constructor:

```php
$this->table = $db_manager->table('people');
```

---

## Method Naming

| Operation | Method pattern |
|---|---|
| Fetch one by ID | `get_by_id( int $id ): ?array` |
| Fetch many | `get_all(): array`, `get_by_{field}( $value ): array` |
| Create | `create( array $data ): int` (returns new ID) |
| Update | `update( int $id, array $data ): bool` |
| Delete | `delete( int $id ): bool` |
| Soft archive | `archive( int $id ): bool` |

---

## Query Preparation

All queries with user-supplied values must use `$wpdb->prepare()`. See [PHP Coding Standards](PHP_CODING_STANDARDS.md) for the `IN` clause pattern.

---

## Return Types

- Single record: return `array|null` (associative array from `$wpdb->get_row(ARRAY_A)`)
- Multiple records: return `array` (always, even if empty)
- Create: return `int` (new row ID, or `0` on failure)
- Update/delete: return `bool`

---

## No Business Logic

Repositories must not contain business logic. Validation, calculations and orchestration belong in services.

---

## Legacy Repositories

The legacy repositories under `app/People/`, `app/Teams/` and `app/TeamAssignments/` are still used by the Kernel. They follow the same standards but are in the older namespace `IexelClubOS\{Module}`. Do not add new methods to legacy repositories; migrate to `app/core/` equivalents instead.
