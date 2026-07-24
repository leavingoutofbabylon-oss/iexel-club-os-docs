# Code Review Checklist

**Last verified:** 2026-07-24

---

## Overview

Use this checklist when reviewing pull requests for `iexel-club-os`.

---

## Security

- [ ] All `$_POST`, `$_GET` and `$_REQUEST` values are sanitised
- [ ] All output is escaped at the point of output
- [ ] All database queries use `$wpdb->prepare()`
- [ ] All admin pages and handlers check the correct capability
- [ ] All form submissions verify a nonce
- [ ] No sensitive data (passwords, tokens, PII) is logged

---

## Architecture

- [ ] New classes follow the correct naming convention
- [ ] Services do not access `$wpdb` directly
- [ ] Repositories do not contain business logic
- [ ] New capabilities are registered in `ClubRoleCapabilityRegistrar` and `ReleaseCapabilityInventory`
- [ ] New admin pages are registered in `AdminUI` and `ReleaseRouteInventory`
- [ ] New portal routes are registered in `PortalRouter` and `ReleaseRouteInventory`
- [ ] New database tables are added to `DatabaseManager` and `ReleaseSchemaInventory`
- [ ] New database tables have an upgrade step in `UpgradeRunner`

---

## Code Quality

- [ ] PHPCS passes with no new suppressions (or suppressions are justified)
- [ ] No `var_dump`, `print_r` or `error_log` left in production code
- [ ] No hardcoded IDs, URLs or credentials
- [ ] No direct `echo` in service or repository classes
- [ ] All new public methods have PHPDoc comments

---

## Tests

- [ ] New functionality has unit tests
- [ ] Tests cover at least one error path
- [ ] All tests pass

---

## Documentation

- [ ] `MODULE_STATUS.md` is updated if module status changed
- [ ] `TECHNICAL_DEBT_REGISTER.md` is updated if new debt is introduced
- [ ] `DATABASE_TABLE_REFERENCE.md` is updated if new tables are added
- [ ] `CAPABILITY_REFERENCE.md` is updated if new capabilities are added
- [ ] `ADMIN_MENU_REFERENCE.md` is updated if new admin pages are added
- [ ] `PORTAL_ROUTE_REFERENCE.md` is updated if new portal routes are added

---

## Release Readiness

- [ ] The Release Readiness page passes after the change is deployed to a test environment
