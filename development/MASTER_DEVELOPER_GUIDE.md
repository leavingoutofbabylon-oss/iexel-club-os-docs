# AI Entry Point

If you are an AI coding agent, read AGENTS.md first.

AGENTS.md defines:

- repository workflow
- engineering standards
- review process
- reporting expectations

This document remains the authoritative source for Club OS architecture.

# Master Developer Guide

**Version:** 1.0  
**Last Verified:** 2026-08-15
**Applies To:** Operational MVP

---

# Overview

This guide is the primary entry point for all developers and AI assistants working on Club OS.

It explains how Club OS is engineered, how development is organised, and where to find detailed technical documentation.

Every contributor should read this guide before making architectural or implementation changes.

---

# Project Status at a Glance

### Current Phase

**Operational MVP**

### Current Priority

Progress from completed RC validation environments (Environment 1 Clean Install and Environment 2 Controlled Upgrade Matrix verified and accepted) to Internal Club Testing and final Release Readiness sign-off.

### Recently Completed

- ✅ AI Workspace and routing
- ✅ People and Teams
- ✅ Events and Attendance
- ✅ Matchday Experience & Lineup Builder
- ✅ Welfare Experience Foundation & Safeguarding
- ✅ Secretary Command Centre (Teams, Assignments, Venues, Portal Accounts, Events)
- ✅ Club-Wide Registration Coverage & Directory
- ✅ Member Active/Inactive Lifecycle Management
- ✅ Parent Selected-Child & Player Event Scoping (OS-028)
- ✅ Parent All-Children Event Identity & Independent Multi-Child RSVP
- ✅ Parent Family Finance & Invoice Detail Experience (OS-030)
- ✅ Treasurer Finance & Invoice Lifecycle MVP (FIN-027)
- ✅ Committee Workspace & Native Operations (Club Projects CRUD, Communications, Audience Builder v2)
- ✅ Prospect → Training Only Batch 2B (manual acceptance passed; pending commit)

- ✅ Training Membership Visibility & Secretary Management Batch 2C (implementation and LocalWP manual acceptance complete)
- ✅ Atomic Match Player → Training Only Transition Batch 2D-A + Match Event Ownership Repair (manual acceptance passed; pending commit)
- ✅ Registered-only Training Only → Match Player Batch 2D-B1 + Training Player-role normalisation (accepted and merged)
- ✅ Secretary-native Registration setup for Training Only Players Batch 2D-B2 (final acceptance passed; merged on `main`)

- ✅ Team Staff Operational Access Reconciliation (implementation and LocalWP manual acceptance complete; pending intentional commit)
- ✅ Front-end Player Profile A — Security, Core Workspace and Current Operational Medical/Safety (implementation and LocalWP manual acceptance complete; pending intentional commit)
- ✅ MVP Priority Alert persona scoping (implementation, source validation and LocalWP manual acceptance complete; implementation merged to plugin `main`, acceptance documentation merged to docs `main`, and OS-032 formally closed for MVP)
- ✅ MVP Release Readiness Integrity Batches 1, 2, 2.5 and 3 (implementation, source validation and LocalWP manual acceptance complete; plugin implementation merged to plugin `main`, documentation reconciliation merged to docs `main`, and the workstream formally complete)
- ✅ RC Clean-Install Blocker Repair Gate 2C (post-commit verification and pre-merge audit complete; merged on plugin `main` at `e3f115dce90a04f3812036334317f691ba367b42`)
- ✅ RC Controlled Upgrade Matrix Gate 2 (Environment 2 verified across Rows 1–4 and Interruption/Resume; full-registry reconciliation architecture confirmed and accepted)
- ✅ MVP Internal Club Testing: SEC-001 (Canonical Team Season Provisioning), SEC-002 (Grassroots Play-Up Eligibility), SEC-004/005 (Meet Time Unification), SEC-006 (Committee Event Routing), SEC-007A/B/C (Event Audience Policy, Flexible Builder & Privacy-Safe RSVP), and SEC-008 (Coach Football Event Scope Hardening, Training Meet Time Policy & Matchday Hub Location Repair `2370551`)

### Current Focus

Both Release Candidate test environments are verified and accepted:
1. **Environment 1 (Clean Installation):** Verified on WordPress 7.0.4 / PHP 8.2.29 / MySQL 8.4; establishes the clean baseline (48 Club OS-owned tables, schema/data version `2026.08.6`, complete upgrade state across 25/25 steps/results, 15 formations and 129 slots), with AI activity dbDelta reconciliation, unlinked administrator fail-closed identity boundary (*Administrative authority does not create member identity*), pre-output public prospect feedback routing, and canonical empty-site billing scheduler behavior.
2. **Environment 2 (Controlled Upgrade Matrix):** Full-registry idempotent reconciliation pipeline validated across all 4 canonical baselines (`2026.07.1`, `2026.08.2`, `2026.08.5`, `2026.08.6`) plus controlled failure interruption/resume. All 25 registered `UpgradeStep` contracts evaluated in sequence, with safe no-op evaluation on fulfilled invariants (`ran = false`) and transactional application on unfulfilled invariants (`ran = true`). Team references normalized to `TM-%06d`, role capabilities reconciled, business data preserved 100%, and unlinked admins fail closed across all baselines.

The next major milestone is Internal Club Testing followed by formal Release Readiness sign-off. Post-MVP scope remains deferred.

### Next Milestones

1. Operational MVP Complete
2. Internal Club Testing
3. Release Readiness
4. Club OS v1.0

### Before Starting Any New Feature

Ask yourself:

- Does this help complete the Operational MVP?
- Can I reuse an existing component?
- Does this introduce unnecessary technical debt?
- Does it follow the Club OS Engineering Rules?

---

# First Day on Club OS

Before writing any code:

- Read this guide from start to finish.
- Review the current Project Status.
- Read the Architecture documents relevant to your feature.
- Confirm the current MVP priorities.
- Create or switch to the correct feature branch.
- Ensure your work does not duplicate an existing component.
- Ask before introducing new architecture if unsure.

While developing:

- Keep changes focused on a single feature.
- Reuse existing Services, Repositories and Components.
- Follow the Club OS Engineering Rules.
- Update documentation if architecture changes.
- Test locally before requesting review.

Before completing a feature:

- Review your own changes.
- Check against the Code Review Checklist.
- Verify that no unrelated files were modified.
- Ensure the feature supports the current MVP goals.

---

# Club OS Engineering Principles

## Project Vision

Club OS is being developed as a premium football club operating system rather than a traditional WordPress plugin.

The objective is to provide a scalable, modular and maintainable platform capable of supporting football clubs of all sizes while delivering a modern, professional user experience.

Every architectural decision should favour long-term maintainability over short-term convenience.

---

## Development Philosophy

The project follows a number of core engineering principles:

- Build reusable systems before individual features.
- Extend existing components before creating new ones.
- Keep business logic inside Services and Repositories.
- Keep UI components focused on presentation.
- Maintain strict separation between Admin and Portal experiences.
- Security and permissions are mandatory, never optional.
- Database changes must always be handled through controlled upgrade routines.
- Every new feature should improve the platform rather than increase technical debt.

---

## Current Development Phase

The current objective is Operational MVP completion.

Current priorities are:

1. Complete all operational experiences.
2. Validate end-to-end workflows.
3. Prepare for internal club testing.
4. Complete Release Readiness.
5. Release Club OS v1.0.

Visual refinements and advanced features should not delay MVP completion unless they significantly improve usability or operational workflows.

---

# Club OS Engineering Rules

These rules apply to every feature, module and pull request.

### Architecture

- Always extend the existing architecture before introducing a new one.
- Reuse existing Services, Repositories and Components wherever possible.
- Avoid duplicate business logic.
- Keep modules loosely coupled and highly cohesive.
- Prefer composition over duplication.

### Channel-Neutral Communications

Club OS Communications are based on canonical recipient identity, not on a specific portal role.

A communication marked visible in Club OS Messages may be delivered to an authorised recipient experience according to:
- canonical person identity;
- audience resolution;
- recipient snapshot;
- communication visibility;
- role/experience permissions;
- safeguarding policy.

Do not architect the Communications domain around "Parent Portal" semantics. Parent, Player, Coach, Committee and other authorised experiences should reuse the canonical Communications domain where appropriate rather than creating duplicate communication stores. Presentation layers may differ by role, but canonical communication and recipient data should remain shared.

### Recipient vs Email Eligibility

A valid Club OS recipient is NOT the same thing as an email-eligible recipient.

A person may:
- be a valid canonical Club OS recipient;
- appear in recipient Messages;
- lack a valid email address.

Email eligibility must therefore remain a delivery-channel concern and must not determine whether a person is a valid Club OS recipient.

### Youth / Adult Player Classification Direction

Player identity is unified under a single canonical `Player` role, with age/safeguarding classification sitting beneath Player identity rather than creating duplicate roles or workspaces.

Player classification model:
- **Known Youth**: Age verified under statutory adult threshold (<18). Full safeguarding rules, linked guardian oversight, and Welfare audit apply.
- **Known Adult**: Age verified adult (>=18). Receives standard player communications; youth guardian rules do not apply.
- **Age Unknown**: Date of birth missing or unverified. Age Unknown MUST receive the SAFEST applicable youth-level communication protections until the person's age/classification is resolved, while retaining the domain fact that age is unverified.

Classification basis: `date_of_birth` is the canonical basis for classification. Team names or team age groups must NOT be used as the sole safeguarding source of truth.

### Youth Communication Safeguarding Principles

Youth communication safeguarding distinguishes between guardian visibility/oversight and email delivery:
- Do NOT automatically generate duplicate email delivery to linked guardians when an audience already targets both Players and Guardians.
- Safeguarding controls separately determine: Club OS recipient status, linked guardian Club OS visibility, guardian email copying, Welfare audit logging, Welfare notifications, and Welfare approval.
- Routine team announcements must not automatically generate unnecessary Welfare notifications.
- **Direct Youth Communication Safeguard**: Club OS must not create an unsupervised private communication pathway between an adult club official and a youth player. Direct/specific youth-player communication requires explicit safeguarding controls (guardian visibility/oversight, sender capability checks, audit logging, direct object access controls, and information isolation).

### Database

- Never modify database tables directly.
- All schema changes must go through UpgradeRunner.
- Preserve backwards compatibility wherever possible.
- Never delete production data during upgrades.

### User Interface

- Reuse existing UI Components before creating new ones.
- Follow the Club OS Design System and Design Tokens.
- Build mobile-first.
- Keep Admin and Portal experiences separate.
- Prioritise usability over visual complexity.

### Security

- Every action must be authorised.
- Validate and sanitise all user input.
- Escape all output.
- Never trust request data.
- Default to the least privilege required.

### Development Workflow

- One feature branch per feature.
- Keep pull requests focused.
- Do not mix unrelated changes.
- Review all AI-generated code before merging.
- Test locally before creating a pull request.

### Documentation

- Update documentation when architecture changes.
- Update references when adding modules.
- Record significant architectural decisions as ADRs where appropriate.
- Keep documentation aligned with the implementation.

### MVP Principle

Before adding new functionality always ask:

> Does this help complete the Operational MVP?

If the answer is **No**, the work should normally be scheduled after MVP unless it fixes a defect or significantly improves usability.

---

# Prerequisites

---

# Where to Go Next

After reading this guide, developers should continue with:

1. BRANCHING_AND_GIT_WORKFLOW.md
2. SYSTEM_OVERVIEW.md
3. MODULE_MAP.md
4. CODE_REVIEW_CHECKLIST.md
5. AI_DEVELOPER_GUIDE.md (when working on AI features)

These documents expand on the standards introduced in this guide and should be treated as the authoritative references for their respective areas.
