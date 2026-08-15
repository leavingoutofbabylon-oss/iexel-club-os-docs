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

### Environment 2: Upgrade from Previous Version (Pending)

1. Install the previous version of Club OS
2. Create test data (people, teams, events, finance records)
3. Upgrade to the RC version
4. Verify all upgrade steps complete without errors
5. Verify all existing data is intact
6. Verify Release Readiness page passes

---

## RC Sign-off

The RC is signed off when:

1. Both test environments pass all tests (Environment 1 clean installation verified; Environment 2 upgrade matrix pending)
2. No P1 bugs are found during RC testing
3. The product owner has reviewed and approved the release

---

## Release Process

After RC sign-off, follow the [RELEASE_CHECKLIST.md](../development/RELEASE_CHECKLIST.md).
