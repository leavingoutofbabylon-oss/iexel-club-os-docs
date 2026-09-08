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

**Final Release Readiness / Club OS v1.0 sign-off.** Internal Club Testing (SEC-001 through SEC-008), the Completed Match Correction architecture (Batches 2A, 2B-1, 2B-2 and their end-to-end acceptance gate), Admin Sidebar Navigation Consolidation (ADM-001/002/003), dark-surface text contrast (OS-029/FIN-028/PL-024), and the subsequent Internal Club Testing remediation programme (Secretary member-maintenance safeguards, canonical Current Emergency Contact management, secretary-assisted password-reset completion alerts, and final pre-merge validator/repository hygiene) are all complete and have been integrated into plugin `main` at `b2b51eb` via a controlled, audited, pure fast-forward (57 commits; final clean-branch pre-merge release gate returned GREEN; post-integration sanity validation returned PASS; zero main-side divergence at integration). This is safe integration into `main`, not final Release Readiness / v1.0 sign-off or production deployment approval — see `RELEASE_CHECKLIST.md` for the remaining gates. A read-only MVP / Release Readiness reconciliation audit (2026-08-26) found no currently-known unresolved High/MVP implementation blocker and confirmed Release Readiness reports Ready. This does not mean the product is finished. Before selecting another roadmap-labelled implementation batch, prefer a small source-first verification of any remaining polish-level candidate (see `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s "Recommended next implementation batch" section) — the same approach that revealed ADM-001/002/003 and OS-029/FIN-028/PL-024 were already complete.

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
- ✅ Completed Match Correction architecture — canonical score reconciliation + Remove Incorrect Goal (Batch 2A), canonical Match incident `timeline_order` (Batch 2B-1: `sequence` is immutable creation/audit order, `timeline_order` owns effective chronological replay/display order), Add Missed Goal with historical eligibility and deterministic equal-minute placement (Batch 2B-2), and a combined end-to-end acceptance gate; implemented, validated and merged to plugin `main` at `b2b51eb`
- ✅ Internal Club Testing remediation programme — secretary member-maintenance safeguards, canonical Current Emergency Contact management (Person-level current state, current-row-authoritative-even-when-empty, exact-current-Season Registration fallback), secretary-assisted password-reset completion alerts (seven-day eligibility lifecycle, canonical Activity attribution), and a final pre-merge validator/repository hygiene batch; merged to plugin `main` at `b2b51eb` via an audited, GREEN-gated, pure fast-forward integration (0 main-side divergence, 57 commits, PASS post-integration validation)
- ✅ Validator hygiene reconciliation (live-goal, substitution/Attendance and Player Progress validators no longer depend on obsolete Event 57 live-state assumptions or the removed WordPress/Gravatar avatar fallback) and the Player Progress canonical MVP decision (embedded Team Workspace → My Progress journey; see `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`)
- ✅ Admin Sidebar Navigation Consolidation & Route Cleanup (ADM-001/002/003, `c88eab9`) — wp-admin navigation is consolidated into logical groups; route-only admin screens remain registered but hidden from the sidebar, reachable through in-page contextual actions. Daily operations should prefer the relevant role/workspace experience where one exists; wp-admin remains the deeper administration/configuration/oversight surface
- ✅ Dark-surface text contrast (OS-029/FIN-028/PL-024, `34cd5d4`) — Team Workspace/Team Hub, Finance/billing/invoice and Player Statistics dark surfaces use on-dark foreground tokens; protected by `tools/validate-dark-surface-contrast.php`
- ✅ Verified Historical Scorer Attribution v1 (CMC-002, `2f3dcee`) — an exceptional, Coach-attested pathway for the rare case where a completed Match's active Club goal has no reliable Tier-1 historical participation evidence (saved Selection + legitimate live-bench admission via `effective_selection()`). Reuses the established void+append correction architecture; requires explicit verification source, evidence note and confirmation; leaves an auditable `match_goal_verified_historical_attribution` record; and is deliberately player-specific and provenance-specific rather than a broadening of normal historical eligibility. See "Verified Historical Scorer Attribution — Historical Eligibility Direction" below and `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` / `SPRINTS.md` for full detail. Browser accepted; merged to plugin `main` at `2f3dcee`.
- ✅ Match Hero Goal-Scorer Presentation (CMC-003, `b37de1c`) with live-eligibility correction and responsive polish, and Primary Immersive Module Accent-Top Consolidation (`54edcb2`/`5616f8b`, the reusable `.iexel-accent-top-module` primitive — see "Primary Immersive Module Accent Treatment" below) — both browser-accepted and merged to plugin `main`.
- ✅ Team Events/Attendance and Shared Messages month-disclosure navigation (`082e418`, `fc9dc8a`), Coach Workspace Batch B — Statistics chooser, inline availability editing, return-to-context redirects (`e796f19`, `a9c5dc7`), Live Match transient success notice auto-dismiss (`22a18fd`), and Event Builder Productivity & Training Only Event Audience Eligibility (`1c97ebb`) — optional End Time, safe non-Match/cross-Team Duplicate Event, weekly independent recurring Events, and deliberate Training Only inclusion in appropriate Event audiences (Current Team + Same Age Group Players and Selected Players) with League/Fixture competitive eligibility unchanged. Training Only participation remains governed entirely by Training Membership — never a Team Assignment. See `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s Coach Workspace section and `SPRINTS.md` for full delivery detail. All browser-accepted and merged to plugin `main` at `1c97ebb`.
- ✅ Welfare Workspace Workflows (`5348403`) — Welfare Concern Directory mobile/filter repair (reuses the existing form-field component, no new design system) and a new short operational **Welfare Update** capability (dedicated append-only persistence, server-derived author/timestamp, 1,000-character plain-text limit, no edit/delete/attachments, generic Activity History never receives the operational text). This remains a data-minimisation boundary, not detailed safeguarding case notes — see `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s Welfare Workspace direction section and `SPRINTS.md` for full delivery detail. At the time of this commit, restricted Welfare Person access and Staff Compliance remained approved future direction, not implemented — **Staff Compliance's canonical foundation, Secretary management, the restricted Welfare People/Person/Compliance projection, and proactive compliance expiry alerting have since all been implemented** (`b5f006a6`, `3352d300`, `cd871f3`, `2bdd62e`; see `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s Welfare Workspace direction section, `SPRINTS.md`'s "Staff Compliance — Batch A, Batch B, Batch C & Batch D" section, and `development/DEVELOPMENT_HANDOVER_2026-09-08C.md` for the current resume point). No further Staff Compliance batch is currently approved future direction.

### Current Focus

Both Release Candidate test environments are verified and accepted:
1. **Environment 1 (Clean Installation):** Verified on WordPress 7.0.4 / PHP 8.2.29 / MySQL 8.4; establishes the clean baseline (48 Club OS-owned tables, schema/data version `2026.08.6`, complete upgrade state across 25/25 steps/results, 15 formations and 129 slots), with AI activity dbDelta reconciliation, unlinked administrator fail-closed identity boundary (*Administrative authority does not create member identity*), pre-output public prospect feedback routing, and canonical empty-site billing scheduler behavior.
2. **Environment 2 (Controlled Upgrade Matrix):** Full-registry idempotent reconciliation pipeline validated across all 4 canonical baselines (`2026.07.1`, `2026.08.2`, `2026.08.5`, `2026.08.6`) plus controlled failure interruption/resume. All 25 registered `UpgradeStep` contracts evaluated in sequence, with safe no-op evaluation on fulfilled invariants (`ran = false`) and transactional application on unfulfilled invariants (`ran = true`). Team references normalized to `TM-%06d`, role capabilities reconciled, business data preserved 100%, and unlinked admins fail closed across all baselines.

Internal Club Testing, the Completed Match Correction architecture, and the subsequent Internal Club Testing remediation programme are complete and merged to plugin `main` at `b2b51eb` (2026-08-29). The next major milestone is formal Release Readiness sign-off toward Club OS v1.0 — see `RELEASE_CHECKLIST.md` for the specific remaining gates. Post-MVP scope remains deferred.

### Next Milestones

1. ✅ Operational MVP Complete
2. ✅ Internal Club Testing (remediation programme integrated into plugin `main` at `b2b51eb`)
3. ⏳ Final Release Readiness / v1.0 sign-off — current priority
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

### Target-Person Eligibility vs Current-User Authorization

These are two separate questions and both must be asked wherever a feature acts on one Person's data on behalf of another (established by Staff Compliance — see `SPRINTS.md`'s "Staff Compliance — Batch A, Batch B, Batch C & Batch D" and `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s Welfare Workspace direction section for the worked example, including Batch D's own alert-generation-vs-alert-delivery application of this same rule):

- **Current-user authorization** — may the acting user perform this action at all (capability, active persona/workspace, nonce, preview state)?
- **Target-Person eligibility** — does the specific Person this action targets qualify for this feature in the first place, independent of who is acting?

Neither answer substitutes for the other, and a broad grant of one must never be read as satisfying the other:

- Club Admin / superuser authority does not bypass target-Person eligibility. An authorised administrator still cannot use a feature on a Person who does not qualify for it.
- A Person being an eligible *target* for a feature does not itself grant that Person (or anyone else) *authorization to act* on it. Eligibility is a property of the data being acted on, not a capability grant.
- Enforce both checks identically everywhere the feature is reachable (summary/read surfaces, the dedicated management route, and every write) — computed live from canonical state, never cached or duplicated — so eligibility can never drift between "the feature is shown" and "the feature can actually be used," and so removing a Person's qualifying state takes effect immediately without special-case cleanup.
- A denial for "target Person does not qualify" and a denial for "target Person does not exist" should normally use the identical response, so a probing request cannot distinguish the two and thereby learn something about a Person it should not otherwise be able to determine.

### Restricted Workspace People Projections

Established by Staff Compliance Batch C's Welfare People/Person projection (see `SPRINTS.md`'s "Staff Compliance — Batch A, Batch B, Batch C & Batch D" section) as a durable rule for any future sensitive workspace that needs its own People surface:

- **A. Expose only the minimum relevant population, never the full canonical People table by default.** A sensitive workspace's own People projection should be scoped by an explicit, unioned relevance rule (e.g. "has an active concern, a current safeguarding-relevant record, or a qualifying role/eligibility"), computed from bounded existence/eligibility queries — never a blanket `PeopleRepository::all()` dump re-filtered client-side, and never a new parallel membership table invented to represent "relevant to this workspace."
- **B. Workspace authorization and domain capability authorization remain separate layers.** Holding a shared domain capability (e.g. `can_manage_staff_compliance()`) must never by itself unlock a different workspace's route, and holding a different workspace's authorization must never by itself satisfy a shared domain capability check. Both must be independently required wherever a restricted route sits at the intersection of a workspace and a shared domain — enforced in both directions (see Batch C's own mirror-image check against Batch B's).
- **C. A restricted workspace Person profile must not become a clone of Secretary's full administration profile.** It should expose only the fields relevant to that workspace's own purpose (safeguarding/medical/contact/compliance for Welfare, for example), omit Finance, Registration administration, Team Assignment and Secretary role-management entirely, and reuse existing canonical read services/entities rather than introducing parallel projections of the same data.

### Operational Alerts for Sensitive Domains

Established by Staff Compliance Batch D's `ComplianceExpiryAlertsProvider` (see `SPRINTS.md`'s "Staff Compliance Batch D" section) as a durable rule for any future alert surfacing sensitive-domain state (safeguarding, compliance, medical, finance) through the existing operational-alert architecture:

- **A. Reuse the canonical domain's own status computation — never a local reimplementation.** An alert provider must derive severity/state via the domain's existing pure function or repository query (e.g. `CredentialStatus::derive()`), never a second copy of a threshold or date calculation. If the canonical computation changes, every alert surfacing it must change with it automatically.
- **B. Route only within the viewer's active, authorized workspace.** An alert's action must link to a destination the *current* active workspace/persona is genuinely authorized to reach — resolved per-workspace (e.g. Secretary → the Secretary route, Welfare → the Welfare route) — never a generic, invented cross-workspace destination merely to have somewhere to send every possible viewer. A workspace with no established destination for that alert type must receive no alert at all, rather than a fabricated one.
- **C. Expose only minimal operational information in alert copy.** Name, category/label and current state (plus a date, if already an established presentation detail) — never reference numbers, administrative notes, case-note narrative, medical detail, or other sensitive payload fields the underlying record may hold.
- **D. Reuse existing alert aggregation, bridging and deduplication — never a parallel alert framework.** A new alert source should be merged into the existing per-persona aggregation point(s) and rendered through the existing alert DTO/presentation component, relying on already-established sorting/deduplication rather than inventing new alert-state plumbing.

### Verified Historical Scorer Attribution — Historical Eligibility Direction

Normal historical scorer/assist correction on a completed Match (`correct()`, Add Missed Goal) remains based on reliable **Tier-1** historical participation evidence only: saved Match Selection **plus** legitimate Match-scoped live-bench admissions, via the established `MatchLiveBenchAdmissionService::effective_selection()` architecture. Event Audience and Attendance are **not** normal historical scorer eligibility evidence and must never be treated as such.

When Tier-1 evidence is genuinely empty for a specific active goal incident, an authorised Coach may use the exceptional **Verified Historical Scorer Attribution** pathway (`CompletedMatchGoalCorrectionService::verify_historical_scorer()`). Its v1 candidate-discovery rule is deliberately narrow: exact Event Audience **or** exact Event Attendance for that exact Match — candidate discovery only, never automatic proof of participation. The Coach must explicitly supply a verified scorer, a verification source (`match_footage` / `club_records` / `first_hand_knowledge`), an evidence note and an explicit confirmation before the write proceeds. The write reuses the established void+append correction architecture (no new persistence primitive), preserves the score, and records a distinct, transactional `match_goal_verified_historical_attribution` audit action.

A valid verified attribution is Player-specific and provenance-specific evidence of participation for **that exact Player, that exact Match** — it credits the verified goal, one appearance, and inclusion in that Player's own historical Match history. It must never fabricate starting/substitute status, minutes, Attendance, rating, POTM or an assist, must never rewrite saved Match Selection, must never broaden `effective_selection()`, and must never imply that any other Event Audience/Attendance participant gained historical eligibility. Data Quality recognises this exception only for the exact active incident + scorer role covered by a live audit record — never as a general outside-selection suppression, and never for assist/player-in/player-out roles. See `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s Coach Workspace section and `SPRINTS.md` for full delivery detail, and the deferred Post-v1 opportunities (Verified Historical Appearance, Verified Historical Assist, Registration/Team-assignment historical-evidence reliability) recorded there.

**Historical eligibility must reflect `effective_selection()`, not raw saved Selection.** `historically_eligible_players()` (Correct Match Record / Add Missed Goal) replays the historical pitch state against `MatchLiveBenchAdmissionService::effective_selection()` — the same Selection-plus-legitimate-live-bench-admission merge every live Match Mode write path already uses — never the raw saved Selection alone. A Player legitimately admitted to the live bench and later substituted on must not become invisible to historical eligibility merely because they were never part of the original saved kickoff Selection.

**Data Quality recovery actions must be truthful.** A Data Quality warning's "Fix"/recovery link must only route to a destination (Correct Match Record, Event Attendance, Match Report) that can genuinely act on that exact warning code. This is a positive allowlist per destination, not a catch-all default — an unmatched code must not silently fall through to a page that cannot actually resolve it. A missing recovery action is preferable to a misleading one.

### Primary Immersive Module Accent Treatment

Club OS's premium dark immersive surfaces (Team Workspace, Match Mode, Matchday Hub, Match Report, Correct Match Record, main Events, Player/Team Statistics) share a restrained club-accent top-edge treatment on their **primary module surfaces**. The colour is always the Club's own runtime-configured **Accent Colour** — never a hardcoded value:

```
Settings "Accent Colour" -> brand_accent -> --iexel-brand-accent
    -> --iexel-color-gold -> var(--iexel-gold)
```

`var(--iexel-gold)` is the established component-level token for this — always reference it (or an alias that resolves to it); never hardcode the IEXEL default (`#cba135`) or describe this treatment as literally "gold" in new code comments.

The reusable primitive is `.iexel-accent-top-module` (`assets/css/public.css`), applied by adding the class to a primary module's own markup alongside its existing class(es). Because a bare single-class rule can lose the cascade to a consumer's own pre-existing `border` shorthand at equal specificity, each real consumer is paired with the modifier class in one compound selector (e.g. `.iexel-events-workspace-header.iexel-accent-top-module`) rather than relying on source order.

The durable design distinction:

- **PRIMARY IMMERSIVE MODULE** (a page-level hero, or a top-level card in a primary grid) → restrained accent top trim.
- **NESTED CONTENT** (individual Player/Attendance/incident rows, stat tiles, form field groups) → no accent top trim by default.
- **INTERACTIVE TASK/FORM SURFACE** (e.g. `TeamEventForm`) → does not automatically inherit primary-module trim merely by reusing a shared card class.
- **SEMANTIC STATE SURFACE** (Data Quality warning cards, danger/success notices) → preserves its own warning/error/success treatment; never overwritten by the branding accent.
- **INTERACTIVE DISCLOSURE/OUTLINE CONTROL** (e.g. Match Recovery/Match Details, "Back to Matchday Hub") → may use the same restrained accent as a full border, matching the page's other premium navigation controls.

This treatment must never be applied to the unrelated, club-wide light `.iexel-os-card` family, and must never spill into a shared component's use on an unrelated page (e.g. `EventAttendancePage.php`'s reuse of `.iexel-match-mode-card` for its own Attendance Change card is deliberately excluded). See `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s Coach Workspace section and `SPRINTS.md` for delivery detail.

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
