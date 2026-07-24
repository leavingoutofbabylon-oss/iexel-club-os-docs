# ADR-003: Repository-Service Separation

**Status:** Accepted
**Date:** 2025-01-01 (estimated)
**Last verified:** 2026-07-24

---

## Context

Early Club OS code mixed database access and business logic in the same class. This made testing difficult, created tight coupling between the database schema and business rules, and made it hard to reason about what a class was responsible for.

---

## Decision

Club OS enforces a strict separation between:

- **Repositories** — responsible only for database access for a specific entity. Named `*Repository`. The only classes permitted to use `$wpdb` directly.
- **Services** — responsible for business logic and orchestration. Named `*Service`. Receive repositories via constructor injection.

---

## Consequences

**Positive:**
- Services can be unit-tested with mock repositories
- Database schema changes are isolated to repository classes
- Business logic is easier to reason about
- Consistent naming makes the codebase navigable

**Negative:**
- More classes per domain
- Requires discipline to keep repositories free of business logic

---

## Implementation

- Repositories: `app/core/{Module}/{Module}Repository.php`
- Services: `app/core/{Module}/{Module}Service.php`
- Standards: [REPOSITORY_STANDARDS.md](../standards/REPOSITORY_STANDARDS.md), [SERVICE_STANDARDS.md](../standards/SERVICE_STANDARDS.md)

---

## Legacy Violation

The legacy repositories under `app/People/`, `app/Teams/` and `app/TeamAssignments/` pre-date this decision and contain some business logic. They are being migrated incrementally. See [TECHNICAL_DEBT_REGISTER.md](../reference/TECHNICAL_DEBT_REGISTER.md).
