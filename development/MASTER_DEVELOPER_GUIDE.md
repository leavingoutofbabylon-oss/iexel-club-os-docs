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
**Last Verified:** 2026-08-14
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

Complete all remaining operational experiences before Release Readiness.

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
- ✅ MVP Priority Alert persona scoping (implementation, source validation and LocalWP manual acceptance complete; committed and pushed on `fix/mvp-priority-alert-persona-scoping`; pending merge to `main`)

### Current Focus

Team Staff Operational Access Reconciliation and Player Profile A are implementation complete and have passed LocalWP manual acceptance; the accumulated batch remains pending intentional commit. The existing front-end Player Workspace at `/club-os/teams/{TEAM_ID}/players/{PERSON_ID}/` has been hardened and completed for Player Profile A. A linked active Coach, Manager or Assistant Coach must operate through the Coach experience, hold `iexel_manage_assigned_team`, and have exactly one active staff assignment on the exact active route Team and exact active current TeamSeason; a linked active Club Admin retains the established `iexel_manage_club_os` override. Ordinary Secretary remains on the Secretary Person Profile and Parent, Player, Treasurer, Welfare and Committee personas are not broadened.

Player Profile A authorizes the complete actor/target/Team/current-Season context once and passes an immutable scope into one unified read model. The target must be an active Player with exactly one active Player assignment on that exact TeamSeason, so Training Only, former, inactive and registered-but-unassigned Players fail closed. The read-only profile shows minimum identity and assignment data without exact DOB, a minimal current-Season Registration status, known-youth guardian name/relationship/telephone, and the existing exact-Season `EmergencyContactService` projection.

Current Operational Medical & Safety is now a dedicated non-Season Person-level singleton (`player_operational_medical_safety`), with at most one current row per canonical Person. Admin and active Secretary users with `iexel_manage_registrations` may replace or explicitly clear the four bounded current fields through the protected Secretary Person workflow. Authorized current-Team Coach, Manager and Assistant Coach users receive only those four current fields read-only through Player Profile A; no history, provenance, editor metadata, Welfare or Finance data is exposed. Registration remains immutable historical evidence. Only allergies and medication may be seeded prospectively on the first exact transition to `registered`, only when no current row exists; `medical_notes` and `emergency_information` are never seeded, existing Players receive no historical bulk backfill, and an explicit all-empty current row never resurrects Registration data. Emergency Contact remains the separate who-to-contact projection. Welfare, Finance and safeguarding cases remain separate domains. Secretary Person Profile, the Medical & Safety editor and Player Profile A use private/no-store/no-cache/noindex response protection, and activity events contain metadata and changed-field names only, never medical content. LocalWP acceptance confirmed the Secretary workflow, explicit empty current state, assigned-Team Coach read-only projection, cross-Team denial, Training Only isolation, and first seeding only at the final `registered` transition. It also confirmed allergies and medication seed without medical notes or emergency information, an existing current row is not overwritten, the persisted Training Member Registration type remains authoritative through successful submission, mobile layouts at 600px, 390px and 360px, and the intended private/no-store/no-cache/noindex response headers. Implementation and manual acceptance are complete; intentional commit is still pending.

- Continue final role/workspace MVP gap auditing and release-readiness review against the Experience Review & Roadmap
- Complete commit review for the accepted Prospect → Training Only Batch 2B
- Complete commit review for accepted Batch 2D-A
- Keep historical-only Player Experience, Parent Preview policy and any Training self-service workspace separate
- Complete intentional commit review for the accepted Player Profile A / Team Staff / Current Medical & Safety batch
- Complete merge review for the accepted MVP Priority Alert persona-scoping repair
- Internal club MVP testing

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
