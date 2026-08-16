# Release Candidate Plan

**Last verified:** 2026-08-15

---

## Overview

This document describes the plan for the Club OS 1.0 Release Candidate (RC) process.

---

## RC Criteria

A Release Candidate is created when:

1. All MVP features are implemented and merged to `main`
2. All P1 technical debt items are resolved
3. PHPCS passes with no errors
4. All tests pass
5. Release Readiness page passes on a clean installation
6. Release Readiness page passes on an upgrade from the previous version

---

## RC Testing Plan

### Environment 1: Clean Installation (Verified & Merged)

**Status:** Clean installation verified on WordPress 7.0.4 / PHP 8.2.29 / MySQL 8.4; blocker repairs merged on `main` (`e3f115dce90a04f3812036334317f691ba367b42`).

1. Install WordPress on a clean database (12 baseline tables).
2. Activate Club OS without errors.
3. Verify all 48 database tables are created (47 canonical + 1 AI activity table).
4. Verify schema and data versions are `2026.08.6` with `complete` upgrade status (25/25 steps/results), 15 system formations and 129 formation slots.
5. Verify zero unexpected business fixtures created on initial activation.
6. Verify clean deactivation and reactivation lifecycle with 2/2 repeated schema reconciliation passes producing zero dbDelta warnings and zero malformed SQL.
7. Verify Member Experience identity boundaries fail closed for unlinked administrators (*Administrative authority does not create member identity*).
8. Verify Public Prospect Intake operates with pre-output feedback consumption, valid PRG flow, one-time error display, zero headers-already-sent warnings and zero route inventory warnings.
9. Verify billing scheduler contract on an empty installation: `iexel_club_os_process_billing_schedules = 0` when no billing schedules exist (intentional current behavior).
10. Verify technical test suites: focused validators 3/3 PASS, full non-mutating validator gate 68/68 PASS, 5/5 controlled mutating validator evidence preserved, PHP lint 8/8 PASS.

### Environment 2: Controlled Upgrade Matrix (Verified & Accepted)

**Status:** Controlled upgrade matrix verified on WordPress 7.0.4 / PHP 8.2.29 / MySQL 8.4 against disposable RC clean database (`127.0.0.1:10010`); development database (`127.0.0.1:10005`) and production plugin source (`e3f115dce90a04f3812036334317f691ba367b42`) remained untouched.

#### UpgradeRunner Reconciliation Architecture

`UpgradeRunner` operates as a **full-registry idempotent reconciliation pipeline** rather than a version-sliced migration filter:
- For any **non-current installation** (Rows 1–3):
  - All 25 registered `UpgradeStep` contracts are evaluated sequentially.
  - Each step executes its `is_valid()` predicate first.
  - If already satisfied: `ran = false` and no database mutation occurs.
  - If not satisfied: `ran = true`, `apply()` executes (inside a transaction for data steps), and the contract is re-validated.
  - Every successfully verified step is appended to `completed_steps`.
- Persisted `completed_steps` records all verified/satisfied upgrade invariants, not merely mutating operations.
- `schema_version` and `data_version` do NOT filter the step registry, and individual steps do NOT use from-version boundaries.
- The previous pre-execution assumption of "18 / 9 / 2" applicable steps was a theoretical estimate of newly introduced migrations per baseline, not `UpgradeRunner` execution semantics.
- For an **already-current installation** (Row 4): `UpgradeVersions::is_current()` and `all_valid($steps)` evaluate to true, immediately returning `already_current` with 0 steps executed.

#### Accepted Matrix Execution Evidence

1. **Row 1 (`baseline_oldest_2026_07_1` - Commit `906960b`):**
   - **Pre-upgrade:** Schema `2026.07.1`, Data `2026.07.1`, 41 Club OS tables.
   - **Fixtures:** Person (Secretary One), User `sec1` (admin), Secretary/Committee roles, Team `OLD-REF-1`, Season `2026/27`, TeamSeason, Scheduled Match, Completed Match.
   - **Execution:** 25 steps evaluated in 2.0803s (18 mutating, 7 no-op/reconciliation).
   - **Post-upgrade:** Schema `2026.08.6`, Data `2026.08.6`, 48 tables (47 canonical + 1 AI activity), team reference normalized to `TM-000001`, Secretary capabilities backfilled, events preserved. **Result: PASS**.

2. **Row 2 (`baseline_mid_2026_08_2` - Commit `ddb784e`):**
   - **Pre-upgrade:** Schema `2026.08.2`, Data `2026.08.2`, 44 Club OS tables.
   - **Fixtures:** Person (Coach Bob), User `coach2`, Coach role, Team `OLD-TM-2`, Season, TeamSeason, TeamAssignment (`assignment_role = 'head_coach'`).
   - **Execution:** 25 steps evaluated in 1.4483s (10 mutating, 15 no-op/reconciliation).
   - **Post-upgrade:** Schema `2026.08.6`, Data `2026.08.6`, 48 tables (47 canonical + 1 AI activity), team reference normalized to `TM-000001`, Coach `iexel_manage_assigned_team` capability reconciled. **Result: PASS**.

3. **Row 3 (`baseline_recent_2026_08_5` - Commit `0d62f56`):**
   - **Pre-upgrade:** Schema `2026.08.5`, Data `2026.08.5`, 47 Club OS tables.
   - **Fixtures:** Person (Manager Alice), Player (Player Timmy), User `mgr3`, Manager role, Team `OLD-TM-3`, Season, TeamSeason, TeamAssignment (`assignment_role = 'manager'`), TrainingMembership (`U13`, active).
   - **Execution:** 25 steps evaluated in 1.3500s (3 mutating, 22 no-op/reconciliation).
   - **Post-upgrade:** Schema `2026.08.6`, Data `2026.08.6`, 48 tables (47 canonical + 1 AI activity), team reference normalized to `TM-000001`, Manager team capability reconciled, Player role backfilled. **Result: PASS**.

4. **Row 4 (`baseline_current_2026_08_6` - Commit `e3f115d` - Idempotence):**
   - **Pre-upgrade:** Clean installation at Schema `2026.08.6`, Data `2026.08.6`, 48 Club OS tables.
   - **Execution:** Secondary `UpgradeRunner` run returned `code: already_current`, 0 steps executed in 0.3523s.
   - **Post-upgrade:** 48 tables, 0 errors, 0 mutations, lock not asserted. **Result: PASS**.

#### Controlled Interruption & Resume Verification

- **Interrupted Failure State:** Injected failure at step `2026_07_welfare_concerns` with `retry_count = 0`.
- **Pre-Resume Guard:** `UpgradeStatus::current()->state` reported `failed`, `ready = false`, and blocked normal startup with user notice *"The last controlled Club OS database upgrade did not complete."*
- **Resume Execution:** Invoked `UpgradeRunner->run()`; resumed from pending step, executed remaining pipeline to completion.
- **Post-Resume State:** `status = 'complete'`, `retry_count = 1`, lock cleanly released, final Schema/Data `2026.08.6`.
- **Safety:** Failure injection was database-state based only; production plugin source was not modified.

#### Data Integrity & Safety Findings

- **Business Data Preservation:** People, WP user linkages, roles, Teams, Seasons, TeamSeasons, TeamAssignments, TrainingMemberships, Event lifecycles, and Match states were 100% preserved.
- **Identity Invariant:** *Administrative authority does not create member identity*. Unlinked administrators fail closed across all upgraded baselines with zero synthetic `person_id = 0` personas.
- **Team References:** Stored team references converged cleanly to `TM-%06d` with zero duplicate references.
- **Formations & System Data:** System formations (15) and slots (129) preserved without duplication.
- **Risks:** Zero duplicate-data risk, zero destructive-reapplication risk, zero capability regression, and zero historical event/match data corruption.

---

## RC Sign-off

The RC is signed off when:

1. Both test environments pass all tests:
   - **Environment 1 (Clean Installation):** ✅ **PASSED** (verified on WP 7.0.4 / PHP 8.2.29 / MySQL 8.4; blocker repairs merged).
   - **Environment 2 (Controlled Upgrade Matrix):** ✅ **PASSED** (Rows 1–4 and Interruption/Resume verified).
2. No P1 bugs are found during RC testing (0 P1 bugs found).
3. Product Owner review and final release authorization.

---

## Release Process

After RC sign-off, follow the [RELEASE_CHECKLIST.md](../development/RELEASE_CHECKLIST.md).
