# MVP Status

**Last verified:** 2026-07-24

---

## Overview

This document tracks the MVP release status of Club OS. The MVP is defined as the first production-ready release that delivers the core value proposition: a complete club management platform for grassroots football clubs.

---

## MVP Definition

The MVP delivers:

1. Complete member and team management
2. Season and event management
3. Match Mode for live match operations
4. Finance management (invoices, payments, billing)
5. Member Portal with five experience roles
6. Communications (email)
7. Player registrations
8. Club Projects (governance)
9. Executive Dashboard

---

## Module MVP Status

| Module | MVP Status | Notes |
|---|---|---|
| People | **MVP Complete** | |
| Teams | **MVP Complete** | |
| Seasons | **MVP Complete** | |
| Season Planning | **MVP Complete** | |
| Venues | **Complete** | |
| Events | **MVP Complete** | |
| Attendance | **MVP Complete** | |
| Match Mode | **MVP Complete** | |
| Football Statistics | **MVP Complete** | |
| Player Registrations | **MVP Complete** | |
| Finance | **MVP Complete** | Export deferred to 1.1 |
| Communications | **MVP Complete** | |
| Member Portal | **MVP Complete** | |
| Executive Dashboard | **MVP Complete** | |
| Club Projects | **Complete** | |
| Branding | **MVP Complete** | |
| Activity Log | **MVP Complete** | |
| Weather | **Placeholder** | Deferred to 1.1 |
| Rewards | **Placeholder** | Deferred to 2.0 |

---

## MVP Blockers

The following items must be resolved before the MVP release:

1. All P1 items in [TECHNICAL_DEBT_REGISTER.md](../reference/TECHNICAL_DEBT_REGISTER.md) must be resolved
2. Release Readiness page must pass on a clean installation
3. Release Readiness page must pass on an upgrade from the previous version
4. All P1 security items in the Code Review Checklist must be verified

---

## Post-MVP Deferred Items

The following items are intentionally deferred after the MVP release:

- Finance export (`iexel_export_finance`)
- Weather integration
- Rewards module
- Audit Log UI
- `iexel_manage_teams` capability enforcement
- Legacy repository migration
