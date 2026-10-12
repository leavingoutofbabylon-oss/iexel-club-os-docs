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
**Last Verified:** 2026-10-12 (Reconciliation checkpoint: HEAD `bf6df68`, schema `2026.10.20`, Mobile UX Batches 1–5 delivered on `main`, MOB-008A in plugin working tree; 8 workspace walkthroughs provisionally accepted)
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

**Current plugin baseline: `bf6df68a5774395b7a131b49a070daebf878f446`, `main`, clean tracked index synchronized with `origin/main` (with MOB-008A uncommitted changes in plugin working tree awaiting acceptance); database schema version `2026.10.20`.**

The Product Owner has completed mobile workspace and WordPress Admin UX walkthroughs across all eight primary surfaces:
1. **Parent / Guardian**
2. **Secretary**
3. **Treasurer**
4. **Committee**
5. **Coach / Manager**
6. **Player**
7. **Welfare**
8. **WordPress Admin**

Each workspace is formally recorded as **UX walkthrough complete / provisionally accepted**, with outstanding findings remaining open until implemented, validated, and accepted. Unresolved issues are strictly not marked as fixed or claimed as final release acceptance.

Five Mobile UX implementation batches are delivered and merged to plugin `main`:
- **Mobile UX Batch 1 (`28264dc`):** MOB-005 — Coach lineup builder draft persistence and player profile access.
- **Mobile UX Batch 2 (`bc5ab91`):** MOB-006 / MOB-007 — Coach lineup builder bulk attendance and match status reliability.
- **Mobile UX Batch 3 (`4e259f9`):** MOB-009 / MOB-010 / MOB-011 — Football fixture-card presentation unification across Parent and Coach hubs with responsive opponent name wrapping.
- **Mobile UX Batch 4 (`fa72493`):** MOB-008 — Parent Team Hub inline per-child RSVP controls and scroll position preservation.
- **Mobile UX Batch 5 (`bf6df68`):** MOB-001 — Parent invoice currency encoding repair (£ symbol correction).

Additionally, **MOB-008A** (Parent Event Detail RSVP Return Navigation) is implementation-complete in the plugin working tree (4 modified files, 1 untracked validator) and awaiting Product Owner manual acceptance.

The Prospect Trial Period milestone, Fundraising (F1 Team Appeals, F2–F4 Spot the Ball, F5 Back My Game), SumUp Hosted Online Payments, Club Shop (Batches 1–4A), Disposable Validator Safety Architecture, and AdminUI Route Parity remain delivered and integrated on plugin `main`. Use [the 2026-09-30 handover (updated with Sections 7 and 8)](DEVELOPMENT_HANDOVER_2026-09-30.md) as the authoritative resume point.

Outstanding review findings are structured into a 4-tier delivery classification:
- **Tier A — Release-Critical:** Security, safeguarding, permission leaks, broken essential workflows, data integrity, payment correctness, and required release controls (Youth purchasing/entry safeguarding in Shop, Spot the Ball & Appeals; Committee permission boundaries & data minimisation; MOB-008A RSVP return navigation; Private encrypted backup vault B4D validation).
- **Tier B — MVP Usability & Operational Improvements:** Essential live operation workflows, including SET-001 operational settings separation, Secretary Create Event mobile selector overflow fix, WordPress Admin Fundraising menu cleanup, Parent RSVP wording distinction, Committee communications approval gate, Coach bulk event responses, and Back My Game supporter visibility.
- **Tier C — North Star Visual Polish:** Non-blocking styling and consistency refinements (OS-011 Welfare Concern Detail hierarchy, Coach Premium Squad Availability polish, Player match deep links and drilldown).
- **Tier D — Post-MVP:** Modular settings evolution (SET-003/SET-004), full operational migration away from WordPress Admin, video training library/wizard, direct Prospect-to-match registration seam, and F6 Club Draw.

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
- ✅ Prospect → Training Only Batch 2B (manual acceptance passed; established canonical pathway)
- ✅ Training Membership Visibility & Secretary Management Batch 2C
- ✅ Atomic Match Player → Training Only Transition Batch 2D-A + Match Event Ownership Repair
- ✅ Registered-only Training Only → Match Player Batch 2D-B1 + Training Player-role normalisation
- ✅ Secretary-native Registration setup for Training Only Players Batch 2D-B2
- ✅ Team Staff Operational Access Reconciliation
- ✅ Front-end Player Profile A — Security, Core Workspace and Current Operational Medical/Safety
- ✅ MVP Priority Alert persona scoping (OS-032 formally closed for MVP)
- ✅ MVP Release Readiness Integrity Batches 1, 2, 2.5 and 3
- ✅ RC Clean-Install Blocker Repair Gate 2C (`e3f115dce90a04f3812036334317f691ba367b42`)
- ✅ RC Controlled Upgrade Matrix Gate 2 (Clean install & upgrade matrix validated)
- ✅ Completed Match Correction architecture (Batches 2A, 2B-1, 2B-2, CMC-001)
- ✅ Internal Club Testing remediation programme (`b2b51eb`)
- ✅ Admin Sidebar Navigation Consolidation & Route Cleanup (ADM-001/002/003, `c88eab9`)
- ✅ Dark-surface text contrast (OS-029/FIN-028/PL-024, `34cd5d4`)
- ✅ Verified Historical Scorer Attribution v1 (CMC-002, `2f3dcee`)
- ✅ Match Hero Goal-Scorer Presentation (CMC-003, `b37de1c`) and Primary Immersive Accent-Top (`54edcb2`/`5616f8b`)
- ✅ Welfare Workspace Workflows (`5348403`) and Staff Compliance Batches A–D (`b5f006a6`, `3352d300`, `cd871f3`, `2bdd62e`)
- ✅ Registration Packages Arc (RP-B `c0936ed`, RP-C `e8283e9`, Post-RP `4285091`)
- ✅ Prospect Trial Period / Come and Try (`e5426be`)
- ✅ Fundraising Team Appeals & Public Supporter Journey (F1, `745f8d4` to `a8b555f`)
- ✅ Spot the Ball Competition Lifecycle & Adjudication (F2-F4, `f77d507` to `c6e86bc`)
- ✅ Back My Game Supporter Subscriptions (F5, `3d47049` to `6d6c457`)
- ✅ Hosted Online Payments & SumUp Checkout Foundation (`be36f2e`, `f89087a`, `caab932`)
- ✅ Club Shop Foundation, Member Retail & Secretary Fulfillment (Batches 1-4A, `6163554` to `a8c66c5`)
- ✅ Disposable Validator Safety Architecture & Test Isolation (368 assertions PASS)
- ✅ AdminUI Route Inventory Parity (56/56 routes PASS, `1342540`)
- ✅ Mobile UX Batch 1 — Coach Lineup Draft Preservation & Player Access (MOB-005, `28264dc`)
- ✅ Mobile UX Batch 2 — Coach Lineup Builder Bulk Attendance Reliability (MOB-006/MOB-007, `bc5ab91`)
- ✅ Mobile UX Batch 3 — Unified Football Fixture Cards & Heading Wrapping (MOB-009/MOB-010/MOB-011, `4e259f9`)
- ✅ Mobile UX Batch 4 — Parent Team Hub Inline RSVP & Scroll Position Preservation (MOB-008, `fa72493`)
- ✅ Mobile UX Batch 5 — Parent Invoice Payment Currency Encoding Repair (MOB-001, `bf6df68`)

### Current Focus

The Product Owner walkthroughs across all eight workspaces have completed, transitioning Club OS from active discovery to focused MVP completion:
1. **Walkthrough Closure:** All eight workspaces are provisionally accepted with known findings catalogued into Tier A/B/C/D.
2. **Implementation Sequence:** Controlled, risk-ordered batches starting with MOB-008A closure and Tier A release-critical safeguards, progressing to Tier B operational improvements, then Tier C polish.
3. **Disaster Recovery / Vault (B4D):** End-to-end payload population, verification, and restore of the private encrypted backup vault (`IEXEL_RC_VAULT`).

**Preserved Operational Boundaries & Deferred Scope:**
- **Admin Recovery Invariant:** `/wp-admin/` remains permanently accessible for technical support, database upgrades, and recovery diagnostics; operational management shifts to the portal.
- **Registration Discovery Seams:** The direct Prospect-to-competitive Match Registration invitation (`ProspectLifecycle::INVITED_MATCH_REGISTRATION`) remains an open operational seam.
- **Commercial & Architecture Boundaries:** General package amendments/upgrades post-registration remain deferred; multi-club branding remains future work; Finance Reports is an intentionally removed unfinished scaffold requiring fresh product definition; Club Draw (F6) remains future compliance-gated work.

### Next Milestones

1. ✅ Operational MVP Core & Commercial Extensions (Core Operations, Registrations, Finance, Welfare, Compliance, Trialists, Fundraising F1–F5, Club Shop Batches 1–4A, Mobile UX Batches 1–5 integrated on `main`)
2. ✅ Internal Club Testing (remediation programme integrated into plugin `main` at `b2b51eb`)
3. ✅ MVP Release Candidate validated + Product Owner sign-off PASSED (RC-01 → RC-03-CLOSE, plugin `main` `3ee4c92`)
4. ✅ Mobile & WordPress Admin UX Walkthroughs (Provisionally accepted across all 8 workspaces; 4-tier completion plan established)
5. ⏳ Implementation of Tier A Release-Critical & Tier B MVP Usability Batches
6. ⏳ Private Encrypted Backup Vault End-to-End Validation (B4D payload population, verification, and restore)
7. ⏳ Release/deployment gate (tagging, production deployment, post-release monitoring) — see `RELEASE_CHECKLIST.md`
8. Club OS v1.0
9. 📋 Post-MVP Evolution (Tier D, F6 Club Draw, Advanced Onboarding Wizard & Video Library)

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

The Operational MVP Release Candidate is technically validated and accepted. The current baseline includes completed Registration Packages, Registration integrity workflows and Prospect Trial Period; remaining MVP/open work must be reassessed before a new batch is selected.

Current priorities are:

1. Select the next documented MVP/open item with the Product Owner/lead developer.
2. Reassess Internal Club Testing preparation against the current accepted build.
3. Preserve the separate release/deployment gate; no deployment is authorized by this checkpoint.

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

### Portal Response Status Integrity

Established by the MVP Release Candidate validation cycle (RC-01, `a197abd`; RC-03-R1, `3ee4c92` — see `SPRINTS.md`'s "MVP Release Candidate Validation Cycle" section for the full defect history) as a durable rule for `PortalRouter` and any future portal render path:

- **A. A successful-render optimistic HTTP status must never mask a later, more authoritative outcome.** `PortalRouter::render()` sets `status_header( 200 )` early, inside an output buffer, specifically so that any later genuine `wp_die()` or explicit `status_header()` call — from a dispatched page class, an authorization guard, or a not-found branch — can still correctly override it before the buffer flushes. Any future change to this buffering/status architecture must preserve that override ordering; do not set a success status after a point where a later guard could no longer act on it.
- **B. A restricted/denial render path must explicitly establish its own correct HTTP status.** Rendering "Access restricted" (or an equivalent denial) as inline HTML inside `render()`'s output buffer, without an explicit `status_header( 403 )` (or the appropriate code) immediately before it, silently inherits whatever status is already in effect — which, per rule A, defaults to the optimistic 200. This was the exact root cause found in 13 separate branches during RC-03-R1. **Any new denial-rendering branch inside a buffered success path must call the correct `status_header()` itself; it cannot rely on an earlier guard having already set one.**
- **C. Do not treat a page rendering the right content as proof the HTTP status is also right.** Denial content, capability checks and route matching can all be completely correct while the response status is still wrong — these are independent concerns and must be verified independently, ideally with a real HTTP client, not merely by inspecting rendered output.

### Clean-Install / Onboarding State Tolerance

Established by RC-02A-R1 (`73c5767` — see `SPRINTS.md`'s "MVP Release Candidate Validation Cycle" section) as a durable rule for any feature that depends on canonical Season (or similarly-scoped) state:

- A genuinely fresh club onboarding onto Club OS, or a club adopting Club OS mid-season, may legitimately have Teams and People before any Season has been marked current — `SeasonRepository::create()` deliberately defaults every new Season to not-current. **No feature may fatal on this state**, and no feature may silently work around it by automatically creating a Season, automatically marking one current, or falling back to an arbitrary historical Season. The correct behaviour is the one already established by `TeamWorkspacePage`: resolve a nullable/absent current-Season context safely (coalescing to an established sentinel value, never passing `null` into a non-nullable parameter), surface the existing, already-established warning, and let season-independent content continue to render.

### Family Relationship Role Consequences

Established by Post-RC Guardian Link Alignment Batch 1 (plugin `main` `29220cc` — see `SPRINTS.md`'s "Post-RC Guardian Link Alignment Batch 1" section) as a durable rule for `PersonRelationshipManagementService` and any future canonical family-relationship or role-management writer:

- **A. Parent/Guardian relationship and Person role are separate domain concepts.** The relationship answers "which adult is linked to which Player/child?"; the role answers "which operational/persona identity does this Person hold?" Never collapse them into one concept, even when a workflow creates both together.
- **B. Canonical relationship creation may ensure a corresponding role only when the originating workflow policy is authorised to do so.** Do not assume that every actor authorised to manage a family relationship is authorised to grant a Person role — verify the actual capability chain for that specific policy before allowing a role-write side effect.
- **C. Secretary and Treasurer are a concrete example of this boundary, not a special case to special-case around.** Secretary holds `iexel_manage_person_roles` (bundled with its registration-management authority); Treasurer deliberately does not. A shared write service used by both must gate any role-granting side effect per-policy, using its own existing policy parameter — never a blanket behaviour applied to every caller of a shared method.
- **D. Security must be enforced server-side, inside the domain/service layer; a candidate picker's own filtering is presentation, not authorization.** A picker that happens to hide ineligible candidates must never be relied upon as the actual security boundary — prove rejection happens in the service even via a direct/crafted request.

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

### Finance Workspace Visual Hierarchy

Established by Treasurer Premium Workspace Alignment Batch 1 (plugin `main` `8403691` — see `SPRINTS.md`'s "Treasurer Premium Workspace Alignment Batch 1" section) as a durable rule for `PortalFinanceWorkspacePage` and any future Finance-workspace presentation change:

- **A. Finance is a premium administrative workspace whose surface treatment follows visual hierarchy and semantic purpose, not a single light-or-dark default.** Its page framing and the great majority of its sections currently use the shared `.iexel-experience-hero` / `.iexel-experience-section` / `.iexel-experience-metrics` / `.iexel-experience-metric` vocabulary — the same components Secretary, Welfare and Treasurer's own People/Team/Registration pages already use — and rich midnight/navy operational/detail surfaces (see B) remain an accepted part of Finance's presentation, not something to be lightened away. Finance must not be pushed toward the fully immersive dark treatment used by Team Workspace, Match Mode or Matchday Hub, and must equally not regress toward broadly pale/generic light operational cards — which surface is dark and which is light is decided by that surface's own hierarchy and semantic role, not by a blanket "Finance is light" assumption.
- **B. Invoice Detail's own primary invoice record is a single, deliberate, Product-Owner-directed exception.** Only the authoritative invoice summary (reference, recipient, season/scope, status, dates, totals) uses the existing dark `.iexel-os-card` treatment, reused rather than modified; every other Invoice Detail section (Itemised Charges & Discounts, Payment Allocations, Invoice Timeline, Invoice Notes) uses the canonical light `.iexel-experience-section`. Do not generalise this one exception into "Finance cards are dark," and do not extend it to any other Finance surface without a fresh, explicit Product Owner decision.
- **C. Light KPI/summary tiles are intentionally subordinate, not a design gap.** `.iexel-experience-metric`'s light neutral-tile treatment is deliberate wherever it appears in Finance (including nested inside the one dark Invoice Detail record, where a light KPI tile on a dark card is an established, self-contained pattern) — it must not be "fixed" toward a dark treatment by a future batch without a specific finding, not a stylistic assumption.
- **D. A component's colour treatment is only as safe as every ancestor it can appear under.** `.iexel-button-secondary` and any similarly dark-native shared component may render unreadable if its ancestor changes from dark to light (or vice versa) without checking every page that reuses it. Before changing a section's light/dark treatment, trace every shared component nested inside it (including via `getComputedStyle()` on the live page, not just a source-code cascade read) rather than assuming an isolated class-name grep found every relevant rule — a second, independent dark-treatment source can exist in a different stylesheet (`design-system.css`, in this batch) and silently win the cascade.
- **E. "Gold"/accent colour follows the same runtime-token rule as elsewhere in Club OS** (see "Primary Immersive Module Accent Treatment" above) — never hardcode a literal accent colour in new Finance code or describe a treatment as literally "gold."

### Registration Commercial History and Post-Registration Package Arrangements

Established by the Registration Packages arc (RP-B, RP-C, and Post-Registration Package Arrangement `4285091`) as durable architectural invariants:

- **A. Registration Commercial Snapshot is Immutable:** The original Registration captures and freezes the historical commercial decision agreed at registration time. If a family completed registration without selecting a package under an active `allow_registration_without_package` policy, `player_registrations.package_id` and `package_snapshot` remain strictly `NULL` (meaning "No package selected during registration"). The original Registration record must NEVER be rewritten, updated, or backfilled to pretend that a package was chosen during registration.
- **B. Post-Registration Package Arrangement is a Separate Canonical Event:** When an initial package is subsequently agreed for an already-registered player who originally had no package, it must be recorded as a distinct, first-class business event owned by `RegistrationPackageArrangement` and the `registration_package_arrangements` table (`UNIQUE KEY uk_registration_id`). It is never collapsed into the historical registration row.
- **C. Snapshot Integrity:** The arrangement record persists a complete, immutable commercial snapshot (`package_snapshot`) capturing package identity, name, base price, currency, description, inclusions, selected add-on snapshots (with their canonical charge types and prices), total arranged amount, timestamp, and arranging actor ID. Future edits or archiving of Treasurer package/extra catalogue definitions cannot alter past arrangements.
- **D. Operational Ownership and Persona Boundaries:** Post-registration package arrangement is operationally owned by the Treasurer under `iexel_manage_billing` and `MemberExperienceRole::TREASURER` (`/club-os/treasurer/registrations/{id}/arrange-package/`). Secretary has contextual read-only visibility into the arranged package without billing mutation actions or Finance invoice controls. Parents/guardians have zero execution authority over this workflow.
- **E. Decoupled Downstream Finance Handoff:** For billable arrangements, `FinanceService::create_post_registration_package_invoice()` creates a standard `Draft` invoice with polymorphic provenance (`source_type = 'registration_post_package'`, `source_id = registration_id`) linked to the arrangement. The resulting invoice enters the existing Treasurer Finance lifecycle. No online cart, checkout, automatic payment collection, or automatic invoice issuing is introduced. Zero-value arrangements create zero invoices.
- **F. Strict Single-Arrangement Scope:** An eligible Registration may have at most one post-registration package arrangement, enforced at both application service and database constraint levels. This is NOT a general package amendment, upgrade, downgrade, or multiple-purchase workflow.
- **G. Dual-Layer Pathway Applicability:** Registration Packages enforce pathway applicability (`is_applicable_to`), and attached Extras/Add-ons ALSO retain their own independent pathway applicability (`applies_to_pathway`). An attached Extra is offered only when the package is pathway-eligible, the Extra is attached to the package, the Extra itself is pathway-eligible, and active/archive rules are satisfied. This is intentional Treasurer-controlled catalogue behaviour; attached extras do not automatically bypass their own configured pathway restrictions.

### Registration Journey Identity and Person-First Staff Integrity

The canonical linked journey is **Person + Season + Registration pathway**, independent of which family member or Staff actor starts it. Parent draft ownership/identity hardening (`67ac823`) preserves linked-child identity and authorized family ownership, resumes the canonical journey and fails closed on ambiguous active equivalents; request parameters cannot transfer ownership or replace identity. Attempt-token, Information Requested correction/resubmission and commercial snapshot rules remain in force.

**Modern Staff Registration is Person-first.** Secretary deliberately selects an existing active Player; first name, last name and DOB remain locked and authoritative in People. Ordinary Registration editing/autosave normalizes identity FROM Person and never silently syncs identity TO Person. Authorized corrections belong at `/club-os/secretary/people/{id}/edit/`. Registration is not an alternative Person-creation workflow and does not make Staff DOB directly editable. The wizard states: "This Registration is linked to the existing Club OS Person. Player identity details are managed in People."

#### Duplicate or ambiguous active journeys: Guided Conflict Resolution

More than one active equivalent journey fails closed into Secretary discovery/operational surfaces and a dedicated comparison (`RegistrationConflictService`, `e303ca96234c8c2530aae776ea55914d3a5dc02d`). The guided mutation is bounded to exactly two existing-Person-linked Drafts with the same canonical journey key; mixed lifecycle states, larger groups and unsupported identities remain fail-closed for club review. Secretary deliberately selects a survivor with no automatic preselection, enters a reason of 3–500 characters and explicitly confirms. Actor-bound version checks detect stale/conflict-changed state; Person/child mutex and locked Registration rows protect transactional revalidation and resolution.

The selected survivor remains unchanged. The selected duplicate becomes **Withdrawn retained history**, never deleted. No Registration information, Package selection or commercial snapshot is merged/copied. Mandatory audit records survivor, duplicate, actor, reason and timestamp; audit failure rolls back withdrawal. Resolved conflicts leave active surfaces, while unrelated unresolved conflicts remain. Sensitive medical/welfare details are not duplicated into comparison; contextual detail navigation returns to an active comparison without changing ordinary Registration detail navigation.

#### Historical unlinked Secretary Draft: Bounded Legacy Recovery

`LegacyStaffRegistrationRecoveryService` (`55ee697c796dbde93e481b45b5809422d7f3be0a`) bridges into the modern Staff workflow, not a generic migration tool. Eligibility requires a Secretary-origin, unlinked `new_player`, Draft at Step 1, valid active Season, no incompatible submission/review/approval history, no guardian bindings, no commercial selection and otherwise valid Staff-editable state. Unsupported shapes fail closed; ordinary Staff save cannot bypass recovery for an unlinked Draft.

The selected active Player must have verified, nonempty canonical names and a valid nonfuture DOB in People. Eligible Draft → deliberate existing active Player selection → legacy/canonical identity comparison → reason (3–500 characters) and unchecked explicit confirmation → authorized POST/nonce and stale/collision revalidation → atomic recovery → **same Registration ID**, canonical Person link and name/DOB normalized FROM Person, pathway `new_player` → `returning_player` → mandatory audit → same modern linked Staff Draft resumes. Trusted Secretary context is required; preview and other persona contexts are denied. Actor-bound version checks cover Draft, Person, Season and collisions. Person mutex, locked Person/roles and Draft, shared Season lock and journey row locks protect the transaction; audit failure rolls back recovery.

Collision checking uses **selected Person + existing Season + Returning Player**, including family-owned Drafts and excluding Rejected/Withdrawn history. Zero other active equivalents permits recovery; one rejects and directs to that existing journey; multiple reject into the established Conflict workflow. Recovery cannot bypass conflict detection.

Recovery creates/mutates no Person, performs no automatic name/DOB matching or Player selection, creates/deletes no Registration, and provides no arbitrary Staff DOB editing, guardian migration, Package/commercial recovery, Finance handoff or Trialist Conversion recovery. Training Member/participation eligibility and downstream Registration → Finance boundaries remain unchanged. Delivery evidence and protected Zayne #558 investigation context are in `SPRINTS.md` and the latest handover.

### Prospect Trial Period and Training Only Boundary

`ProspectTrialService` owns pre-membership participation rules and audited Secretary/assigned-Team Coach operations; `ProspectTrialSessionRepository` owns repeatable, dated sessions in `prospect_trial_sessions`. The branded public Come and Try route records Prospect-level participation consent and, for youth, responsible-adult authority. Historical enquiries receive no fabricated consent or sessions during upgrade. Youth participation requires explicit evidence and confirmed safety/emergency readiness; Coach/Manager visibility is restricted to their assigned Team and an active, ready Prospect. Brief operational notes use the shared auto-grow control, are bounded to 500 characters and are omitted from activity metadata.

Trial sessions remain attached to the Prospect, separate from canonical Event attendance. A trial does not create a Person, canonical guardian relationship, Team Assignment, Registration, Finance record or fixture eligibility. Deliberate Prospect conversion reuses the canonical TrainingMembership domain and age-group eligibility policy, recommends the natural football age group from DOB and Season, and offers the one-year-up choice only when eligible. Conversion preserves Prospect session history; Prospect-level permission is not unrestricted ongoing Registration or guardian consent. Training Only creates no competitive assignment or fixture eligibility. Schema version `2026.09.4` and release inventories include the new table and route scope. The direct Prospect-to-competitive Match Registration invitation remains a separate deferred seam.

### Youth Safeguarding Purchasing and Entry Boundaries

Established by the commercial and fundraising MVP arcs to ensure strict compliance with statutory child safeguarding and payment card guidelines:

- **Club Shop Purchasing Permissions:** Minor youth players (<18) must not execute direct online hosted credit/debit card checkout without an authenticated adult guardian. Youth cart checkout must either require linked adult guardian authentication or default to offline payment instructions under guardian oversight.
- **Spot the Ball Entry Safeguarding:** Youth entry into Spot the Ball competitions requires explicit adult guardian authorization. Minor winnings and prize settlements must route strictly to verified adult guardians via the established prize bridge; minors may not receive direct cash or voucher disbursements without adult guardian confirmation.
- **Fundraising Appeal Attribution:** Public appeal sharing links that attribute fundraising to a youth player require issuance by an authenticated canonical adult guardian (`FundraisingShareAttributionPolicy`). Club OS must never create public child seller profiles, individual minor donation landing pages, or public youth profile URLs.

### Committee Permission Boundaries and Data Minimisation

Established as a durable security and data-protection invariant for the Committee workspace:

- **Executive Governance vs Confidentiality:** Committee workspace is designed for club leadership, governance, and project management. Committee membership alone does not grant access to confidential safeguarding records, individual member financial ledgers, or private medical data.
- **Excluded Sensitive Domains:** General Committee views must strictly exclude:
  - Confidential Welfare safeguarding notes, concern narratives, and updates;
  - Individual member debtor ledgers, itemised family invoices, and personal payment allocations (Treasurer and Club Admin retain billing management);
  - Registration medical notes, doctor details, and specific medication requirements (Welfare and assigned Team staff retain operational access).
- **Club-Wide Communications Approval Gate:** Routine committee operational messaging is permitted, but general committee members sending club-wide broadcasts to all members or parents require an administrative approval gate (Secretary or Club Admin sign-off) to prevent unauthorised mass distributions.
- **Team Oversight Data Minimisation:** Committee team oversight surfaces provide squad counts, coaching coverage, and operational indicators without exposing unnecessary player personal data or contact information.

### WordPress Admin Architecture and Recovery Access Retention

Established to preserve system reliability and platform continuity during the progressive migration of operational features to the portal:

- **Operational vs Administrative Boundary:** Operational club workflows (People, Teams, Events, Registrations, Finance, Shop, Fundraising) are natively engineered in the portal. Operational settings (Season dates, Age Groups, Club contacts) are separated from Brand Studio under SET-001 for MVP.
- **Permanent Support & Recovery Invariant:** The WordPress administrative dashboard (`/wp-admin/`) remains permanently available and supported for system administrators. Technical support, database upgrades (`UpgradeRunner`), recovery diagnostics, plugin lifecycle management, and disaster recovery functions must never be removed or disabled from `/wp-admin/`.
- **Post-MVP Modular Evolution:** Broader modular multi-club profile architectures (SET-003 / SET-004) and full sunsetting of operational WordPress Admin menus remain Post-MVP.

### Operational Onboarding Workstream Standards

Established as the quality and safety framework for the planned role-specific Club OS how-to guides:

- **Role Coverage:** Dedicated, practical guides are planned for seven distinct roles: Secretary, Treasurer, Coach / Manager, Welfare Officer, Committee Member, Parent / Guardian, and Player.
- **Real Verified Workflows:** Guides must document actual, verified system workflows, tested step-by-step against the active implementation baseline.
- **Strict Privacy Invariant:** Guides and visual illustrations must exclusively use synthetic, sample test data. Zero real member names, contact details, payment information, or safeguarding references may ever appear in training material.
- **Scope Boundary:** A full interactive setup wizard and video training library are classified as Post-MVP.

### Parent Priority Alerts RSVP Window and Sorting Invariants (PRN-002)

Established to ensure actionable clarity and prevent distant fixtures from crowding out imminent events in the Parent / Guardian workspace:

- **Rolling Seven-Day Window:** Unanswered event RSVP requests in the Parent Priority Alerts feed are bounded by a rolling seven-day window calculated in the club's configured timezone (`wp_timezone()`), covering the remainder of today plus the next seven calendar days (`setTime(23, 59, 59)->modify('+7 days')`). Past events and events beyond the seven-day boundary are strictly excluded.
- **Ascending Chronological Sort:** Eligible routine RSVP alerts are sorted in ascending chronological order by event start date and time (`$event_date . ' ' . $start_time`), rather than descending creation timestamp (`created_at`). Nearest upcoming events always appear first.
- **Display Limit Precedence:** The chronological ascending sort is applied *before* the feed display limit (e.g. 3 alerts) is evaluated, guaranteeing that nearer events are never sliced off by far-future fixtures.
- **Feed Isolation & Urgency Precedence:** The seven-day date window applies strictly to routine Parent event RSVP requests; higher-priority notifications (e.g. event cancellations, urgent updates, action-required announcements) and non-Parent personas remain unaffected. Urgent communications continue to sort above routine RSVPs by priority score.

### Three-Tier Deployment Pipeline Architecture

Established to guarantee safe, zero-disruption live releases for Club OS:

1. **Tier 1 — Local Development & Validation:** Engineering, unit testing, and focused validator runs executed on local development instances (`localhost` / LocalWP).
2. **Tier 2 — Pre-Production Staging & Update Rehearsal:** A dedicated operational staging website used exclusively for pre-production testing, update rehearsal, and Product Owner acceptance.
   - *Environment Isolation:* Must use isolated test database instances, test payment rails (e.g. SumUp Sandbox), safe outbound email routing (e.g. Mailpit interception), and strict access controls.
   - *Production Equivalence:* PHP runtime version, webserver configuration, and database engine must replicate production specifications.
   - *Rehearsal Gate:* All schema upgrades (`UpgradeRunner`), data migrations, rollback steps, and browser acceptance walkthroughs must be executed and verified in pre-production prior to production release.
3. **Tier 3 — Production Live Operations (IEXEL FC):** The live production deployment for IEXEL FC.
   - *Organizational Decoupling:* **IEXEL FC is an independent football club and the first live deployment customer of Club OS.** It is completely distinct from the Club OS commercial entity.
   - *Release Controls:* Every production deployment must use an immutable, versioned Git release tag (`vX.Y.Z`).
   - *Backup Gate:* A full, verified database backup must be captured immediately prior to triggering any upgrade.
   - *Migration Safety & Rollback:* Migrations must execute transactionally and idempotently via `UpgradeRunner`. Every release must define a documented rollback procedure.
   - *Post-Deployment Smoke Verification:* Execution of automated non-mutating smoke validators immediately following deployment.

### Commercial Product Architecture & Package Boundaries

Established to clarify the modular product offerings and licensing tiers:

- **Core Operating System (Plugin):** The WordPress Club OS plugin (`iexel-club-os`) is the standalone, full-featured operating system providing all operational, financial, safeguarding, and team management capabilities.
- **Plugin-Only Deployment:** Member clubs with an existing compatible WordPress website install and run the plugin within their existing website environment.
- **Optional Premium Club OS Website Theme:** Clubs lacking a modern web presence can purchase the optional premium Club OS website theme alongside the plugin. The theme provides a cohesive public club presence and integrated member portal framing.
- **Universal Mobile App Inclusion:** The future Club OS mobile application is **included with every active Club OS licence**, regardless of whether the club deploys the standalone plugin or purchases the optional website theme. Mobile app access is a universal licence entitlement, not a theme-dependent upsell.
- **Scope Boundary:** Both the premium website theme and the native mobile app are classified as Post-MVP initiatives. The initial IEXEL FC deployment operates entirely on the core plugin within the approved mobile-responsive web portal.

### Post-MVP Commercial Licensing Architecture & Club OS Control Centre

Established to govern commercial customer lifecycle management, subscription compliance, and technical support:

- **Central Licensing Engine:** Commercial licensing operates via a central licensing API managing cryptographically signed license keys, activation handshakes, subscription tier verification, and authenticated package updates.
- **Lifecycle & Grace Periods:** Licenses follow annual or monthly subscription lifecycles. Prior to expiration, automated administrative warnings alert club managers. A defined grace period ensures accidental subscription lapses do not immediately disrupt club matches or youth training.
- **Restricted Data Access Mode:** If a license reaches full expiry or is suspended:
  - Routine matchday, lineup, training, and general member portal operations are suspended.
  - Authorized club administrators retain persistent access to export data (GDPR subject access compliance, statutory accounting archives, and player history exports).
  - License renewal and support communication tools remain accessible.
- **Administrative Governance:** License suspension, revocation, and reinstatement protocols are controlled via cryptographically signed commands and recorded in the audit log.
- **Club OS Control Centre:** A private commercial administration platform used exclusively by Club OS business operators to manage:
  - Customer club records, key contacts, contract terms, and subscription billing.
  - License provisioning, renewals, and tier upgrades.
  - Technical support ticketing and high-level anonymous telemetry (e.g. Club OS plugin version, active extensions, PHP/MySQL version, schema version).
- **Strict Data Minimisation Invariant:** The Club OS Control Centre must **never** ingest, sync, or centrally store player personal data, child safeguarding case notes, medical questionnaires, or member billing transaction histories. Member data remains sovereign within the customer club's own database.
- **Authorized Support Access Invariant:** Technical support access to customer installations must be explicitly requested or authorized by a club administrator, tokenized, time-limited, and fully audited. Club OS must never include hidden permanent administrative backdoors or unmonitored remote access.
- **Realistic PHP Enforcement Model:** Commercial licensing on self-hosted customer PHP infrastructure is designed around commercial contract terms, update distribution, and authenticated services—not security-through-obscurity or claims of unbreakable bytecode obfuscation.

### Public Demonstration Environment & Long-Term League OS Horizon

- **Public Demonstration Environment (Post-MVP):** A dedicated, public-facing demonstration instance designed for prospective customer walkthroughs.
  - *Data Isolation:* Populated exclusively with synthetic, realistic football club data (fictional players, coaches, teams, matches, and finances).
  - *Automated Reset Engine:* Scheduled automated database wipe-and-reseed cycles (e.g. nightly or hourly) restoring the demo to a pristine baseline.
  - *Permission Sandboxing:* Dangerous administrative capabilities (code editing, arbitrary plugin upload, core WordPress settings) are strictly locked down.
- **League OS Vision (~5-Year Horizon):** A long-term strategic vision for a centralized platform serving football leagues and associations.
  - Potential scope includes league-wide fixture generation, divisional tables, referee assignment, disciplinary reporting, and secure league-to-club fixture syndication.
  - **Scope Isolation:** League OS is strictly outside the immediate MVP, initial club deployment, and near-term commercial delivery roadmaps.

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
