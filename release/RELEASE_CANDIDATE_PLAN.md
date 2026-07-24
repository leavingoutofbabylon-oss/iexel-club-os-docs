# Release Candidate Plan

**Last verified:** 2026-07-24

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

### Environment 1: Clean Installation

1. Install WordPress on a clean database
2. Activate Club OS
3. Verify activation completes without errors
4. Verify all database tables are created
5. Verify Release Readiness page passes
6. Run through the following workflows:
   - Create a person, team, season and event
   - Record attendance for an event
   - Run Match Mode for a match event
   - Create an invoice and record a payment
   - Send a communication
   - Submit a player registration
   - Create a Club Project
   - Log in to the Member Portal as each of the five experience roles

### Environment 2: Upgrade from Previous Version

1. Install the previous version of Club OS
2. Create test data (people, teams, events, finance records)
3. Upgrade to the RC version
4. Verify all upgrade steps complete without errors
5. Verify all existing data is intact
6. Verify Release Readiness page passes

---

## RC Sign-off

The RC is signed off when:

1. Both test environments pass all tests
2. No P1 bugs are found during RC testing
3. The product owner has reviewed and approved the release

---

## Release Process

After RC sign-off, follow the [RELEASE_CHECKLIST.md](../development/RELEASE_CHECKLIST.md).
