# Technical Debt Register

**Source of truth:** Source code inspection of `iexel-club-os`
**Last verified:** 2026-07-24

---

## Overview

This register documents known technical debt, inconsistencies and deferred work in the Club OS codebase. Items are categorised and prioritised.

Items marked **P1** should be addressed before Release 1.0. Items marked **P2** are post-MVP. Items marked **P3** are long-term.

---

## Release Readiness Risks

| Item | Priority | Description |
|---|---|---|
| Empty module registry (`medium.module-registry-empty`) | P2 | The `ModuleManager` fires lifecycle actions but no concrete class registers a `ModuleInterface` implementation. Domain areas resolve through `Kernel` instead. Target release: Post-1.0. |
| Audit coverage inconsistent (`medium.audit-coverage-inconsistent`) | P2 | Communications, Finance and Match operations maintain timelines, while several direct administrator-page mutations do not demonstrate equivalent audit records. Direct People, Team, Venue, user-link and some Event mutations do not consistently call `ActivityLogger`. Target release: Post-1.0. |

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

<!-- AS03-20261114 -->
## AS-03 release assurance and accepted/deferred scope — 14 November 2026

The agreed Assistant Secretary MVP is accepted following AS-02B.8. [Current closure](https://github.com/leavingoutofbabylon-oss/iexel-club-os/blob/e6d0795cfb925b52d51ae05457da6aee0a566a6d/development/ASSISTANT_SECRETARY_MVP_CLOSURE.md) and [outstanding register](https://github.com/leavingoutofbabylon-oss/iexel-club-os/blob/e6d0795cfb925b52d51ae05457da6aee0a566a6d/development/ASSISTANT_SECRETARY_OUTSTANDING.md) separate implementation, engineering evidence, Academy observations, production certification and main integration.

**Release/engineering gates, not automatically post-MVP:** native MySQL transaction/rollback/concurrency/ambiguous COMMIT; remaining authenticated HTTP and complete Registration independent approval/eligible competitive progression; documented legacy validator/harness failures and downstream gaps; the retained duplicate PermissionManager declaration; private Communications host/storage readiness and fail-closed uploads; historical public-file remediation and wider exact-artifact install/upgrade/recovery safeguards. Older Priority labels elsewhere in this register remain historical and do not downgrade these current assurance requirements.

**Known validator findings retained:** Committee Projects cross-Season summary assertion; Committee Communications missing-resolver harness; Training management old Secretary/Admin-only assertion; Training mobile overflow assertion; Secretary quick-actions count; Returning Player policy assertion. Also retain Registration pathways mismatch, navigation harness abort/unexecuted downstream checks and prior age-fixture warnings. No expectation is weakened and no failed suite is relabelled green.

**Manual checks still open:** ordinary linked member email update; complete live submission/independent approval; eligible Training-to-competitive completion; invitation delivery/password recovery; other unexecuted release/role checks. Tom's officer-role Training restriction, Test Parent/Jess's protected-authority login-email restriction and Jess's administrator linking are resolved by Product Owner evidence. Do not weaken officer protection or claim notification delivery from visible controls.

**Visual/usability follow-ups:** global blue-on-blue contrast, Venue detail/success presentation, minor Portal Account wording and bounded Assistant Secretary refinements. They do not replace security/storage/transactional certification. No outstanding repair is implemented or newly authorised by this register entry.
<!-- /AS03-20261114 -->
