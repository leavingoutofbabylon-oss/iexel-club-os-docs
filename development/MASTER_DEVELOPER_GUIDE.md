# Master Developer Guide

**Version:** 1.0  
**Last Verified:** 2026-07-24  
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
- ✅ Matchday Experience
- ✅ Lineup Builder
- ✅ Reusable Custom Formation Templates

### Current Focus

- Welfare Experience
- End-to-end workflow validation
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