# Version 1.1 Planning

**Target:** 1–2 sprints after Version 1.0
**Last verified:** 2026-07-24

---

## Overview

Version 1.1 focuses on post-MVP hardening: resolving known technical debt, completing deferred capabilities, and improving test coverage.

---

## Planned Work

### Finance Export

Implement the `iexel_export_finance` capability:

- CSV export of invoices, payments and outstanding balances
- PDF invoice generation
- Export page at `iexel-club-os-finance-export`

**Effort:** Medium
**Capability:** `iexel_export_finance` (already declared and assigned to Treasurer role)

---

### Weather Integration

Implement real weather data in `WeatherService`:

- Integrate with a weather API (e.g. Open-Meteo, OpenWeatherMap)
- Cache forecasts in transients keyed by postcode hash
- Display weather on event detail pages in the portal

**Effort:** Small
**Note:** `WeatherService` exists but returns placeholder data only

---

### Capability Enforcement

Correct the following capability inconsistencies (see [TECHNICAL_DEBT_REGISTER.md](../reference/TECHNICAL_DEBT_REGISTER.md)):

- `iexel_manage_communications` — update `CommunicationAdminRequestHandler` to check this capability
- `iexel_manage_teams` — update Teams admin pages to check this capability
- `iexel_manage_settings` — update Settings page to check this capability
- `iexel_view_audit_log` — implement Audit Log UI

**Effort:** Small per item

---

### Legacy Repository Migration

Migrate legacy repositories to `app/core/`:

- `app/People/PeopleRepository.php` → `app/core/People/PeopleRepository.php`
- `app/Teams/TeamRepository.php` → `app/core/Teams/TeamRepository.php`
- `app/TeamAssignments/TeamAssignmentRepository.php` → `app/core/TeamAssignments/TeamAssignmentRepository.php`

Update `Kernel.php` to use the migrated repositories.

**Effort:** Medium
**Risk:** Regression risk; requires thorough testing

---

### Test Coverage

Add unit tests for:

- `FinanceService` (invoice creation, payment recording, billing run)
- `SeasonPlanningService` (plan generation, approval, execution)
- `ClubRoleCapabilityRegistrar` (capability registration)
- `UpgradeRunner` (step execution, idempotency)

**Effort:** Medium

---

## Definition of Done for 1.1

- All P2 items in [TECHNICAL_DEBT_REGISTER.md](../reference/TECHNICAL_DEBT_REGISTER.md) are resolved
- Finance export is implemented and tested
- Weather integration is implemented
- All capability inconsistencies are corrected
- Legacy repositories are migrated
- Test coverage targets are met
- Release Readiness page passes
