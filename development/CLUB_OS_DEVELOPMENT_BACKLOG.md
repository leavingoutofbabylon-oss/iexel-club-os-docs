# Your Club OS — Consolidated Development Continuity & MVP Completion Register

> **Document Role:** Single authoritative living development register reconciling all repository documentation, handovers, Git history, codebase evidence, Product Owner requirements, deferred post-MVP commitments, technical debt, and release gates.
> **Created:** 2026-11-25 (`DEVELOPMENT-BACKLOG-001`)
> **Last Updated:** 2026-11-25 (`DEVELOPMENT-BACKLOG-001A` — Preview Player Experience regressions, actual Player workspace reconciliation & proposed critical-risk prioritisation)
> **Scope:** Academy MVP Completion → Public Commercial Release → Post-MVP Roadmap
> **Product Philosophy:** *Minimal Administration. Maximum Engagement.*
> **Standing Release Acceptance Rule:** Verify Web Push notification subscription persistence (Notifications remain **On**) after **every** Academy WordPress plugin ZIP replacement (`Replace current with uploaded`).

---

## Status Classification Key

| Status | Meaning |
| :--- | :--- |
| `COMPLETE` | Implemented, verified, and accepted with supporting Product Owner / Academy acceptance evidence (and committed/pushed where recorded). |
| `IMPLEMENTED — NEEDS VERIFICATION` | Implemented in repository code (and/or automated tests passing), but live Academy/production manual acceptance or final reconciliation verification is still open. |
| `PARTIALLY IMPLEMENTED` | Core foundation or subset of stages/surfaces exists in code, with concrete remaining scope or gaps verified in the codebase. |
| `REGRESSION` | Previously implemented/accepted capability that is currently broken, bypassed, or degraded in the live codebase. |
| `OUTSTANDING` | Approved or queued requirement with no implementation yet in the codebase. |
| `BLOCKED` | Cannot proceed until an explicit upstream dependency, Product Owner policy decision, or environment prerequisite is resolved. |
| `DEFERRED` | Explicitly deferred beyond Academy MVP (either pre-public commercial release or Post-MVP) — retained visibly and never silently promoted or dropped. |
| `WITHDRAWN` | Explicitly withdrawn by the Product Owner — retained in traceability only to prevent accidental reinstatement. |

---

## 1. Current Confirmed Development Checkpoint

### 1.1 Plugin Application Repository
- **Worktree Path:** `c:\Users\leavi\Local Sites\iexel-club-os-dev\worktrees\notify001b2-ordinary-events`
- **Branch:** `feature/notify004a-adult-web-push`
- **Confirmed HEAD:** `26df8cf3884d0d286a6075d81a4c677e61e1abfe` (`feat: add Secretary staff compliance workspace`, 2026-11-25)
- **Upstream Synchronisation:** `0` ahead / `0` behind `origin/feature/notify004a-adult-web-push`
- **Staged Files:** `0`
- **Working-Tree Inventory:** Exactly `14` uncommitted files (`11` pending `NOTIFY-COMPLIANCE-001` files + `3` protected `NOTIFY-004B` diagnostic files — see Section 5)
- **Automatic Staff Compliance Notifications:** **DISABLED (default OFF)** (`auto_compliance_enabled => false`)
- **Latest Accepted Batch:** `SECRETARY-COMPLIANCE-001` — all 5 Academy acceptance checks passed (notification persistence, Secretary Staff Compliance navigation & directory, profile heading & credential management, workspace boundaries), `17/17` pre-commit regression suites passed, committed & pushed at `26df8cf3884d0d286a6075d81a4c677e61e1abfe`.
- **Canonical Schema / Data Versions (`app/core/Upgrade/UpgradeVersions.php`):** `SCHEMA_VERSION = '2026.11.23'`, `DATA_VERSION = '2026.10.4'`; `DatabaseManager::CANONICAL_TABLES` defines `73` canonical tables.

### 1.2 Documentation Repository
- **Repository Path:** `c:\Users\leavi\Local Sites\iexel-club-os-dev\app\public\wp-content\plugins\iexel-club-os-docs`
- **Branch:** `docs/registration-package-step-validation`
- **HEAD:** `cc16d2ce251f3c10b974f53cda6f6f5ea6441998` (synchronised with upstream)
- **Existing Uncommitted Changes Preserved:** `6` modified files (`SPRINTS.md`, `development/CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`, `development/CLUB_OS_MVP_TO_PRODUCTION_RELEASE_STRATEGY.md`, `development/DEVELOPMENT_HANDOVER_2026-09-30.md`, `development/MASTER_DEVELOPER_GUIDE.md`, `development/RELEASE_CHECKLIST.md`) and `2` untracked files (`development/ACADEMY_PASSWORD_RESET_EMAIL_TESTING.md`, `development/ACADEMY_REGISTRATION_PACKAGE_PROGRESSION_REPAIR_2026-10-22.md`), plus this newly authored register (`development/CLUB_OS_DEVELOPMENT_BACKLOG.md`).

### 1.3 Recent Confirmed Commit Timeline (Plugin Worktree)

| Commit | Date | Batch / Summary |
| :--- | :--- | :--- |
| `26df8cf` | 2026-11-25 | `SECRETARY-COMPLIANCE-001` — Dedicated Secretary Staff Compliance workspace |
| `0bfdafc` | 2026-11-25 | `UX-ALERTS-001` + `POLISH` — Unified North Star Priority Alerts + `#ef4444` urgent border + Secretary collapsible Quick Actions |
| `f72ffa7` | 2026-11-25 | `WELFARE-UX-001C` + `POLISH` + `POLISH-FIX` — Personal Qualifications & Compliance + Account dropdown polish + notification update persistence |
| `07d9943` | 2026-11-25 | `WELFARE-UX-001B` + `FIX` + `POLISH` — Welfare Staff Compliance directory, pagination (`PER_PAGE=5`), and Welfare People role badges/filters |
| `e436a6b` | 2026-11-25 | `NOTIFY-ONBOARD-001B` + `UX-POLISH-001..004` — Web Push onboarding banner, Install trigger, gold circular avatar & universal dropdowns |
| `c93bddf` | 2026-11-24 | `NOTIFY-QUALITY-001B` — Contextual Web Push notification copy in service worker |
| `51b0408` | 2026-11-24 | `FIN-UI-001` — Member invoice notice contrast improvement |
| `76c5489` | 2026-11-24 | `MSG-ACCESS-001B` + `HOTFIX-DASH-001A` — Restore Welfare messages & PHP packaging integrity gate |
| `5fe299d` | 2026-11-24 | `MSG-UX-001B` — Unify executive announcement button styling |
| `f2b837d` | 2026-11-24 | `SHOP-ACCESS-001B/C` — Personal Club Shop access across workspaces |
| `aa9d54c` | 2026-11-24 | `BRAND-001B/C` — Commercial rebrand to *Your Club OS* |
| `8835b62` | 2026-11-24 | `SHOP-PAY-001` — Treasurer manual Club Shop payment recording |
| `5b79c5c` | 2026-11-24 | `SHOP-NOTIFY-001/001A` — Secretary Club Shop fulfilment alerts, push persona persistence & Treasurer Shop mobile alignment |
| `952b37f` | 2026-11-24 | `NOTIFY-010A` — Finance invoice & Club Shop notifications + email headers |
| `8e8bfeb` | 2026-11-23 | `NOTIFY-009B` + `NOTIFY-009B1` — Secretary/AS Priority Alerts & recipient-centred announcement alerts |
| `39a4b43` | 2026-11-23 | `NOTIFY-009D` + `AGE-001` + `AGE-001A` — Event-aware routing, Manual Adult Verification & People UX polish |
| `001e61f` | 2026-11-23 | `NOTIFY-009A` — Latest Event Update only per event in Priority Alerts |
| `0dbfdd8` / `17cb2f7` | 2026-11-23 | `SCHED-001B` / `SCHED-001C` — Self-hosted WP-CLI scheduled runner + recipient snapshot fix |
| `68066b0` | 2026-11-23 | `NOTIFY-008B` / `NOTIFY-008C` — Safeguarded Player push & iPhone Home Screen PWA SW registration |
| `431d8d0` | 2026-11-22 | `NOTIFY-006A..007C` — Automatic push delivery, immediate dispatch, tap navigation & silent recovery |
| `a7efc32` / `50656ae` | 2026-11-22 | `COACHING-EXPERIENCE-SLICE-01/02A/02B` — Saved Training Session Plans & 9-category / 54-drill library |
| `96cbcda` | 2026-11-22 | `TRAINING-LIFECYCLE-FOUNDATION-01` — Unified multi-role Event navigation & automatic training lifecycle |

---

## 2. Source Documents & Reconciliation Findings

### 2.1 Authoritative Sources Audited
- **Documentation Repo (`iexel-club-os-docs`):** `development/MASTER_DEVELOPER_GUIDE.md`, `SPRINTS.md`, `development/CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`, `development/CLUB_OS_MVP_TO_PRODUCTION_RELEASE_STRATEGY.md`, `development/RELEASE_CHECKLIST.md`, `development/CLUB_OS_SELF_HOSTED_SCHEDULER_DEPLOYMENT_RUNBOOK.md`, `development/B4D-04A_*.md`, `reference/TECHNICAL_DEBT_REGISTER.md`, `README.md`, `roadmap/VERSION_1_1.md`, `roadmap/VERSION_2_0.md`.
- **Plugin Repository (`worktrees/notify001b2-ordinary-events`):** `AGENTS.md`, `development/VISUAL_SURFACE_CONTRAST.md`, `development/ASSISTANT_SECRETARY_OUTSTANDING.md`, `development/ASSISTANT_SECRETARY_MVP_CLOSURE.md`, `development/COMMUNICATIONS_PRIVATE_ATTACHMENTS.md`, `app/` runtime source, `assets/css/` & `assets/js/`, `tools/validate-*.php` (`453` validator scripts), and Git history.
- **Historical Handovers (`worktrees/*-evidence/`):** `SHOP-ACCESS-001B`, `BRAND-001B`, `SHOP-PAY-001`, `SHOP-NOTIFY-001`, `NOTIFY-010A`, `NOTIFY-009B1`, `NOTIFY-009B`, `AGE-001`, `NOTIFY-009D`, `NOTIFY-009A`, `SCHED-001C-Final`, `SCHED-001B-Accepted`, `NOTIFY-008D-and-SCHED-001A`, `NOTIFY-008C-Accepted`, `NOTIFY-008A` review pack, `NOTIFY-004B-02` evidence.

### 2.2 Key Reconciliation Findings (Resolving Historical Documentation Drift)
1. **Docs repo lags plugin HEAD by 14 commits (Nov 23–25):** `SPRINTS.md` and `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` do not yet record the 14 accepted/committed batches delivered between 2026-11-23 and 2026-11-25 (`NOTIFY-009A/B/B1/D`, `AGE-001/A`, `NOTIFY-010A`, `SHOP-NOTIFY-001`, `SHOP-PAY-001`, `BRAND-001B/C`, `SHOP-ACCESS-001B/C`, `MSG-UX-001B`, `MSG-ACCESS-001B`, `FIN-UI-001`, `NOTIFY-QUALITY-001B`, `NOTIFY-ONBOARD-001B`, `UX-POLISH-001..004`, `WELFARE-UX-001B/C`, `UX-ALERTS-001`, `SECRETARY-COMPLIANCE-001`, `COACHING-EXPERIENCE-SLICE-01/02A/02B`).
2. **Stale "Open" entries inside `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` & `SPRINTS.md`:**
   - `SET-001`, `ADM-005`, `PRN-001`, and `CCH-001` are confirmed **closed/accepted** in `PLAN02-B01`/`B02` (`a7502ac`, `5c911e8`) despite still appearing as open Tier B rows in older tables of the same Roadmap file.
   - `NOTIFY-009A` and `NOTIFY-009B` are listed as "Proposed / not yet implemented" at the bottom of Roadmap & `SPRINTS.md` despite being **accepted, committed & pushed** (`001e61f`, `8e8bfeb`).
   - `MOB-008A` is listed as "awaiting acceptance" in `MASTER_DEVELOPER_GUIDE.md:120` despite being accepted (`75c14aa`).
   - `B03-PORT-01` (case-sensitive autoload `app/Core` vs `app/core`) is listed as open in Oct 21 release strategy text, whereas `validate-case-sensitive-autoload.php` now passes (`0` failures) and Academy Linux activation succeeded.
3. **Nov 24 handovers predate commits:** Handovers for `SHOP-NOTIFY-001/A`, `SHOP-PAY-001`, `BRAND-001B/C`, and `SHOP-ACCESS-001B/C` describe their work as "uncommitted/unpushed"; Git history confirms all four are **committed and pushed** (`5b79c5c`, `8835b62`, `aa9d54c`, `f2b837d`). Follow-ups they queued (`FIN-UI-001`, `NOTIFY-QUALITY-001B`, `SHOP-NOTIFY-001`, `SHOP-ACCESS-001`) are also committed.
4. **Codebase audit corrected four key assumptions:**
   - **Duplicate Merge (`§5.8`):** Clean-case merge execution (`PersonMergeExecutor`) *does* exist, but is **broken in live UI** due to a `comparison_version` hash mismatch and carries a **critical silent safety bypass** checking non-existent Finance & Welfare table names (see `PEOPLE-MERGE-001`).
   - **Parent Home Registration Leak (`§5.3`):** Confirmed **P0 cross-family data-exposure defect** — `MemberExperienceService::parent()` and `parent_children_cards()` omit `->in_context('parent')`, exposing all club registrations and club-wide `under_review` alerts to multi-role Secretaries/Club Admins on Parent Home.
   - **Lineup Custom Alignment (`§5.1`):** Did **not** regress — intact from `90164d5`, but snaps only to *assigned* slots (zero snap targets when dragging empty custom slots), lacks pitch centre-line snap, is pointer-only, and uses a tight `1.5%` threshold.
   - **`OS-031` Lightbox (`§4.5`):** Image lightbox JS exists in `communications.js`, but `.iexel-lightbox-*` CSS lives only in `executive-dashboard.css`, which is **not enqueued** on `/club-os/messages/` for Parents, Players, Coaches, Treasurers, or Welfare Officers — rendering an unstyled broken block at the bottom of `<body>`!
5. **Explicitly Withdrawn Item:** The Treasurer *Recent Payments* heading change was explicitly withdrawn by the Product Owner (`WITHDRAWN`) and is not reinstated.
6. **Product Owner Player Workspace Clarification & Critical-Risk Prioritisation (`DEVELOPMENT-BACKLOG-001A`):**
   - **Actual Player Workspace vs Preview Player Experience:** The Product Owner confirmed that the **actual Player workspace** correctly displays the premium North Star experience and is working satisfactorily (`PL-021..025` remain `COMPLETE` and protected against unnecessary redevelopment or restyling). The two reported regressions specifically affect the **Preview Player Experience** accessed from the Parent workspace (`PLAYER-PREVIEW-UX-001`: Regression A — legacy visual styling, including `PortalShell.php:31` excluding `$context->preview` from `.iexel-experience-shell--player`; Regression B — missing dedicated Exit Preview / Return to Parent control).
   - **Proposed P0 Risk Containment (Subject to PO Approval):** Because `PARENT-EXPERIENCE-001A` (cross-family registration data exposure) and `PEOPLE-MERGE-001` (silent Finance/Welfare table-name bypass) represent P0 risks, the development lead proposes moving `PARENT-EXPERIENCE-001A` and adding a server-side containment task (`PEOPLE-MERGE-SAFETY-001`) into **Batch 1** alongside Staff Compliance notifications, while retaining full duplicate merge repair (`PEOPLE-MERGE-001`) in **Batch 4** and placing `PLAYER-PREVIEW-UX-001` in **Batch 2**.

---

## 3. Completed Development Register (Prevent Unnecessary Redevelopment)

The following capabilities are verified **COMPLETE** (implemented, validated, and accepted/committed) and must **not** be rebuilt:

| Ref | Capability / Batch | Verified Commit(s) | Acceptance / Evidence |
| :--- | :--- | :--- | :--- |
| **SECRETARY-COMPLIANCE-001** | Dedicated Secretary Staff Compliance workspace (`/club-os/secretary/staff-compliance/`), nav after People, `PER_PAGE=5` pagination, Secretary Profile `Qualifications & Compliance` heading | `26df8cf` | 5/5 Academy checks passed; 17/17 regression suites (54/54 focused) |
| **UX-ALERTS-001 / POLISH** | Universal North Star glass Priority Alerts across Player, Parent, Coach; `#ef4444` urgent left border; Secretary collapsible Quick Actions circle fix | `0bfdafc` | 5/5 Academy checks passed (incl. notification persistence); 63/63 focused checks |
| **WELFARE-UX-001C / POLISH / FIX** | Personal Qualifications & Compliance (`/club-os/account/qualifications-compliance/`), premium midnight-blue/gold Account dropdown, notification persistence across WP ZIP replacement | `f72ffa7` | Academy acceptance passed incl. ZIP replacement & real Club Shop push delivery; 30/30 focused + 12/12 persistence checks |
| **WELFARE-UX-001B / FIX / POLISH** | Welfare Staff Compliance directory (`/club-os/welfare/staff-compliance/`) with `PER_PAGE=5` pagination, Welfare People role badges & role filter | `07d9943` | Academy accepted; 52/52 focused checks |
| **NOTIFY-ONBOARD-001B + UX-POLISH-001..004** | Non-modal push onboarding banner (14d/30d/60d backoff), Install trigger in Account menu, universal midnight-blue/gold Account & Viewing Mode dropdowns, gold circular avatar | `e436a6b` | Academy accepted (Android Chrome PWA install/reinstall & Android Edge controls) |
| **NOTIFY-QUALITY-001B** | Contextual privacy-safe Web Push notification copy in `assets/pwa/service-worker.js` | `c93bddf` | Committed & pushed; Academy ZIP validated |
| **FIN-UI-001** | Member invoice notice contrast improvement | `51b0408` | Committed & pushed; Academy ZIP validated |
| **MSG-ACCESS-001B + HOTFIX-DASH-001A** | Restored Welfare Messages access & automated PHP ZIP packaging integrity validator (`validate-hotfix-dash-001-php-packaging-integrity.php`) | `76c5489` | Committed & pushed; 9/9 packaging integrity checks |
| **MSG-UX-001B** | Unified executive announcement button styling | `5fe299d` | Committed & pushed |
| **SHOP-ACCESS-001B/C** | Personal Club Shop access & storefront styling across all active non-preview workspaces (preserving Secretary operational Shop separation) | `f2b837d` | Committed & pushed; Academy evidence recorded |
| **BRAND-001B/C** | Commercial rebrand to *Your Club OS* (footer, emails, gold OS coin icons/favicons; removed hardcoded `IEXEL FC` leaks — note 1 residual leak found in `PortalPlayerStatsPage.php:35` tracked in `PLAYER-UX-001`) | `aa9d54c` | Committed & pushed |
| **SHOP-PAY-001** | Treasurer manual Club Shop payment recording (Cash, Bank Transfer, Other) | `8835b62` | Committed & pushed |
| **SHOP-NOTIFY-001/001A** | Secretary paid Club Shop Priority Action + adult Secretary fulfilment push + push persona persistence + Treasurer Shop Orders Awaiting Payment mobile alignment (`shop-finance.css:57-67`) | `5b79c5c` | Committed & pushed |
| **NOTIFY-010A** | Finance invoice issued/reminder email+push & Club Shop fulfilment notifications (`paid`, `preparing`, `ready_for_collection`, self-cancel) + From/Reply-To headers *(1 open natural overdue cron verification tracked separately)* | `952b37f` | Academy accepted for interactive paths; committed & pushed |
| **NOTIFY-009B / 009B1** | Secretary & AS Priority Alerts parity; recipient-centred Important Announcement alerts & Broadcast vs Announcement composer clarity *(1 open weekend non-recipient manual test tracked separately)* | `8e8bfeb` | Academy accepted; 16/16 + 10-group validators |
| **NOTIFY-009D + AGE-001 + AGE-001A** | Event-aware notification routing (`?event_persona=`); Manual Adult Verification Policy (`6` columns, `3` methods, revoke, audit, push integration); People directory & Edit Person UX polish | `39a4b43` | Academy accepted; 28/28 AGE-001 + 14-group NOTIFY-009D validators |
| **NOTIFY-009A** | Latest Event Update only per recipient/event in Priority Alerts (history preserved) | `001e61f` | Academy accepted |
| **SCHED-001B / 001C** | Self-hosted WP-CLI unattended scheduled task runner (`wp iexel-club-os run-scheduled`) + CAS lock + Audience Snapshot display fix | `17cb2f7`, `0dbfdd8` | Academy unattended acceptance passed (production host cron setup remains release gate) |
| **NOTIFY-003A..008C** | Installable PWA foundation, adult Web Push, durable `push_jobs` queue, automatic delivery & tap navigation, safeguarded youth Player push (`has_active_guardian_link()`), iPhone Home Screen PWA SW registration | `fccff06`, `8aaecc3`, `7964816`, `a1722cf`, `864dbf3`, `431d8d0`, `68066b0` | Academy accepted (3/5 `NOTIFY-008D` manual negative checks passed; all 5 automated) |
| **TRAINING-LIFECYCLE-FOUNDATION-01** | Unified multi-role Event navigation & automatic Training window progression (`Upcoming → Started → Past/Finished`) | `96cbcda` | Committed & pushed |
| **COACHING-EXPERIENCE-SLICE-01/02A/02B** | Training Session Plan **Plan** (saved plans, optimistic concurrency, historical lock, 9-category / 54-drill SVG library) and **Coach** (pitch-side stepper viewer) stages | `50656ae`, `a7efc32` | Committed & pushed (`Reflect` Slice 03 tracked separately in `EVENTS-EXPERIENCE-001`) |
| **OS-010 (Staff Compliance A–D)** | Canonical Batch A credential domain (`42`-day window), Secretary Person Compliance UI (B), Welfare People & Compliance (C), Compliance Expiry Priority Alerts (D) | `b5f006a6`, `3352d300`, `cd871f3`, `2bdd62e` | Academy accepted; 108 + 111 + 123 + 69 validator assertions passing |
| **OS-032 + MOB-001..011 + VIS-01..01D** | Priority Alert persona scoping (140 checks), Mobile UX Batches 1–5 + `MOB-008A`, Dark-Surface Contrast closure (`23,124` automated checks + 18/18 Academy checks) | `34cd5d4`, `75c14aa`, `d2ccbfd`, etc. | Formally accepted & closed |
| **AS-01 / AS-02 / AS-03** | Assistant Secretary operational persona, delegated registrations/people/comms/projects & strict security boundaries | `e6d0795` | Committed & accepted |
| **FIN-027..030, FIN-032, FIN-033, F1–F5, RP-A..C, HME-01A..D, CMC-001..003, PL-021..025, SET-001, ADM-001..003/005/006, PRN-001/002, CCH-001, COM-001, YTH-001..003, SEC-001..008, RR-001** | Finance lifecycle, Fee Rules & Discount Policies, Fundraising F1–F5 (Appeals, Spot the Ball, Back My Game), Registration Packages, Training Memberships & Match/Training transitions, Historical Match Entry, Completed Match Correction, Player My Stats & My Season foundations, Brand Studio separation, Parent RSVP copy & Coach bulk availability, youth shopping/fundraising safeguards | Verified in `SPRINTS.md`, Roadmap & Git log | Accepted MVP foundations |

---

## 4. Active Pre-MVP Backlog

Every active pre-MVP requirement is catalogued below with verified codebase evidence, honest status, priority, release target, dependencies, proposed grouped batch, remaining work, and required Product Owner decisions/screenshots.

### 4.1 Staff Compliance Notifications, Personal Reminders & Proposed P0 Containment (Batch 1)

> **Proposed Critical-Risk Prioritisation (Subject to Product Owner Approval):** Alongside Staff Compliance officer/personal notifications and `WELFARE-TEST-001`, the development lead proposes moving `PARENT-EXPERIENCE-001A` (P0 cross-family registration data exposure) and adding `PEOPLE-MERGE-SAFETY-001` (P0 server-side containment preventing unsafe duplicate merges until full Batch 4 repair) into **Batch 1**. No application implementation will begin until the Product Owner approves this prioritisation.

#### `NOTIFY-COMPLIANCE-001-FIX` — Complete Proactive Officer Staff Compliance Expiry Reminders
- **Status:** `PARTIALLY IMPLEMENTED` (11 uncommitted working-tree files with 3 confirmed defects + 1 scheduler allowlist gap; currently default OFF)
- **Original Source:** `NOTIFY-COMPLIANCE-001` pending working tree + Prompt §4.1
- **Expected Behaviour:** Consolidated daily email and privacy-safe Web Push reminders at 30, 14, and 7 days before expiry, and on expiry, delivered to all authorised active Secretaries and Welfare Officers using canonical eligibility, per-recipient deduplication, atomic locking, and lock-screen privacy (zero staff names, credential details, or confidential data).
- **Current Implementation Evidence:** Uncommitted `app/core/StaffCompliance/StaffComplianceNotificationService.php` (621 lines), `tools/validate-notify-compliance-001.php` (476 lines), and 9 modified files (`Application.php`, `Kernel.php`, `PushAutomaticNotificationDispatcher.php`, `PushDeliveryQueue.php`, `PushPilot.php`, `PushPilotConfig.php`, `PushPilotController.php`, `PushControlsPage.php`, `assets/pwa/service-worker.js`). Confirmed defects:
  1. **Role key defect (2 files + masked test):** `StaffComplianceNotificationService.php:385,426,447` queries `r.role_key IN ('welfare', 'secretary')` instead of canonical `'welfare_officer'`; `PushPilot.php:237` also checks `in_array('welfare', $roles, true)` on tap authorisation; `validate-notify-compliance-001.php` masks it by stubbing `'welfare'`.
  2. **Cross-recipient deduplication suppression:** `StaffComplianceNotificationService.php:209-235, 278-283, 305-320` stores milestone keys globally per channel in `iexel_staff_compliance_reminder_ledger` rather than per-recipient, suppressing delivery/retry to other authorised officers once any single officer succeeds.
  3. **Non-atomic lock:** `StaffComplianceNotificationService.php:188-194` uses TOCTOU `get_transient`/`set_transient` instead of atomic `add_option`/CAS lock.
  4. **Newly identified CLI runner gap:** `app/core/Scheduling/ScheduledTaskRunner.php:28-39` (`allowed_hooks()`) omits `iexel_staff_compliance_expiry_check`, preventing unattended execution via `SCHED-001B`.
- **Acceptance Evidence:** None yet (never enabled on Academy).
- **Priority / Target:** **P1 — Academy MVP**
- **Dependencies:** `SCHED-001B` (`17cb2f7`), `WELFARE-UX-001B` (`07d9943`), `SECRETARY-COMPLIANCE-001` (`26df8cf`).
- **Proposed Batch:** **Batch 1 — Staff Compliance Notifications & Personal Reminders**
- **Remaining Work:** Fix `welfare_officer` in service, tap router, and validator (also route Secretary taps to `/club-os/secretary/staff-compliance/` and Welfare taps to `/club-os/welfare/staff-compliance/`); convert ledger/daily dedupe to per-recipient `(recipient_person_id, credential_id, expires_on, milestone, channel)`; replace transient lock with atomic CAS lock; register hook in `ScheduledTaskRunner::allowed_hooks()`.
- **PO Decisions / Screenshots Required:** Confirm whether officer reminders should default OFF until enabled post-verification in Academy Notification Controls (required: default OFF).

#### `WELFARE-NOTIFY-002` — Personal Staff Credential Expiry Reminders
- **Status:** `OUTSTANDING`
- **Original Source:** `WELFARE-UX-001C` / Prompt §4.1
- **Expected Behaviour:** Consolidated personal expiry reminders (email + adult Web Push) for eligible active staff about their own canonical Person credentials (DBS, First Aid, Safeguarding, and qualifications **with** an expiry date) at 30, 14, 7 days and on expiry, routing to `/club-os/account/qualifications-compliance/`. Qualifications without expiry dates must never trigger reminders. Separate explicit admin toggle (default OFF), independent of officer reminders. Privacy-safe lock-screen copy.
- **Current Implementation Evidence:** Read-only viewing exists at `PortalPersonalQualificationsCompliancePage.php` (`f72ffa7`), but **zero** reminder/notification code exists for personal staff expiry reminders.
- **Acceptance Evidence:** None.
- **Priority / Target:** **P1 — Academy MVP**
- **Dependencies:** `WELFARE-UX-001C` (`f72ffa7`), `NOTIFY-COMPLIANCE-001-FIX` (shared scheduler, atomic lock, per-recipient ledger).
- **Proposed Batch:** **Batch 1 — Staff Compliance Notifications & Personal Reminders**
- **Remaining Work:** Implement personal reminder projection (reusing `StaffCompliancePersonEligibility` & `PersonalStaffComplianceAccess`), separate `auto_personal_compliance_enabled` control (default OFF) in `PushPilotConfig` & `PushControlsPage`, distinct privacy-safe push destination routing to `AccountUrl::qualifications_compliance()`, per-recipient dedupe, and unit/runtime validator.
- **PO Decisions / Screenshots Required:** Confirm personal reminder schedule matches 30 / 14 / 7 / 0 days (same as officer reminders).

#### `WELFARE-TEST-001` — Combined Staff Compliance Notification End-to-End Acceptance
- **Status:** `OUTSTANDING`
- **Original Source:** Prompt §4.1
- **Expected Behaviour:** Combined end-to-end automated and Academy acceptance covering officer reminders, personal reminders, email + Web Push delivery, per-recipient deduplication, permissions, CLI scheduler integration, lock-screen privacy, default-OFF/toggle controls, and notification persistence across plugin update.
- **Current Implementation Evidence:** Partial validator (`validate-notify-compliance-001.php`, currently masking `welfare` defect); no personal reminder coverage.
- **Acceptance Evidence:** None yet.
- **Priority / Target:** **P1 — Academy MVP**
- **Dependencies:** `NOTIFY-COMPLIANCE-001-FIX`, `WELFARE-NOTIFY-002`.
- **Proposed Batch:** **Batch 1 — Staff Compliance Notifications, Personal Reminders & Proposed P0 Containment** (audit confirms `NOTIFY-COMPLIANCE-001-FIX`, `WELFARE-NOTIFY-002`, and `WELFARE-TEST-001` cleanly deliver as one coherent programme & single Academy acceptance pass).
- **Remaining Work:** Comprehensive combined validator + controlled Academy acceptance protocol.

#### `PARENT-EXPERIENCE-001A` — Parent Home Registration Active-Persona Scoping (Multi-Role Secretary Data Exposure)
- **Status:** `REGRESSION` (Active P0 cross-family data-exposure defect)
- **Original Source:** Prompt §5.3 (`DEVELOPMENT-BACKLOG-001`) / Proposed Batch 1 elevation (`DEVELOPMENT-BACKLOG-001A`)
- **Expected Behaviour:** Viewing Parent Home as a multi-role Secretary or Club Admin must display **only** the authenticated Parent's own family registrations and family registration alerts — never club-wide Secretary registration records or other families' `under_review` notes.
- **Current Implementation Evidence:** Confirmed defect at `app/core/Experience/MemberExperienceService.php:953` (`parent_children_cards()`) and `992` (`parent()`), which call `$this->kernel->parent_registration_portal()->registrations()` **without** `->in_context('parent')`. Because `ParentRegistrationPortalService::$wizard_context` defaults to `null`, `can_manage_club_wide()` (`lines 164-167`) returns `true` for Secretaries/Admins and returns `player_registrations()->all()` across the entire club, leaking into both the Parent Home Registration widget (`line 998`) and `registration-info-req-{id}` Priority Alerts (`line 995`).
- **Acceptance Evidence:** None (reported by PO on Academy).
- **Priority / Target:** **P0 (Security / Data Minimisation) — Academy MVP**
- **Dependencies:** Subject to Product Owner approval of Batch 1 critical-risk prioritisation (**Decision D13**).
- **Proposed Batch:** **Batch 1 — Proposed Critical-Risk Elevation** *(moved from Batch 2 because of P0 cross-family data-exposure risk; subject to PO approval)*.
- **Remaining Work:** Enforce strict parent/family scoping (`in_context('parent')` + explicit `$c->person_id` / `$child_ids` filtering) in `MemberExperienceService::parent()` and `parent_children_cards()`, ensure `ParentRegistrationPortalService` does not leak shared state across calls, and add permanent multi-role Secretary+Parent regression validator.

#### `PEOPLE-MERGE-SAFETY-001` — Server-Side Duplicate Merge Safety Containment (Interim P0 Guard)
- **Status:** `OUTSTANDING` *(Proposed Batch 1 containment task; subject to PO approval)*
- **Original Source:** `DEVELOPMENT-BACKLOG-001A` §4 (derived from P0 safety bypass discovered in `PEOPLE-MERGE-001`)
- **Expected Behaviour:** Prevent unsafe duplicate merge execution **server-side** until the full `PEOPLE-MERGE-001` repair is implemented and accepted in Batch 4. Must investigate and enforce canonical server-side fail-closed protection at the request/executor boundary (`PersonMergeExecutor` / `PortalRouter` / POST handler) — **never relying solely on hiding or disabling a UI button**.
- **Current Implementation Evidence:** `PersonMergeExecutor.php:734,747` checks non-existent Finance & Welfare table names (`invoices`, `payments`, `billing_schedules`, `shop_orders`, `safeguarding_concerns`, `medical_notes`, `player_welfare_cases`) and skips `person_credentials`, silently returning zero blockers (currently masked in the UI only by the `comparison_version` hash mismatch bug, which must not be relied upon as a security boundary).
- **Acceptance Evidence:** None.
- **Priority / Target:** **P0 (Data Integrity & Safeguarding Containment) — Academy MVP**
- **Dependencies:** Subject to Product Owner approval of Batch 1 critical-risk prioritisation (**Decision D13**). Full repair remains retained in **Batch 4 (`PEOPLE-MERGE-001`)**.
- **Proposed Batch:** **Batch 1 — Proposed P0 Containment** *(subject to PO approval)*.
- **Remaining Work:** Investigate minimal server-side containment (either fail-closed guard on `execute_clean_merge` until Batch 4 or immediate canonical Finance/Welfare/Compliance table blocker fix + server-side guard), add automated runtime test proving direct POST attempts cannot bypass safety checks, and verify zero regression to read-only duplicate detection.

---

### 4.2 Parent Experience, Preview Player Experience & Welfare Polish (Batch 2)

> **Cross-Reference:** `PARENT-EXPERIENCE-001A` (P0 Parent Home registration active-persona scoping) is proposed for elevation into **Batch 1** (Section 4.1) subject to Product Owner approval (**Decision D13**). If not approved for Batch 1, it remains P0 at the head of Batch 2.

#### `PLAYER-PREVIEW-UX-001` — Preview Player Experience Visual Parity & Return Navigation
- **Status:** `REGRESSION` — Product Owner confirmed *(both regressions recorded under one requirement with distinct acceptance criteria)*
- **Original Source:** `DEVELOPMENT-BACKLOG-001A` §2 (Product Owner clarification separating satisfactory actual Player workspace from Preview Player Experience regressions)
- **Priority / Target:** **P2 — Academy MVP**
- **Dependencies:** None (must not disturb accepted actual Player workspace `PL-021..025`).
- **Proposed Batch:** **Batch 2 — Parent Experience & Welfare**
- **Cross-Reference:** Distinct from `PLAYER-UX-001` (Section 4.6, actual Player workspace). Do not duplicate scope across requirements.

##### Regression A — Legacy Visual Presentation
- **Observed Behaviour:**
  - Preview Player Experience displays older Club OS visual styling when accessed from the Parent workspace.
  - Light grey/white page background instead of the current North Star stadium background.
  - Legacy white Quick Actions container rather than the premium midnight-blue glass component.
  - Unwanted decorative circle beside the Quick Actions heading.
  - Inconsistent visual presentation compared with the actual Player workspace.
- **Current Investigation Lead (Read-Only Evidence):** `app/core/UI/Components/Portal/PortalShell.php:31` evaluates `$is_player = MemberExperienceRole::PLAYER === $context->active_role && ! $context->preview;`, which explicitly omits `.iexel-experience-shell--player` when `$context->preview === true`. Full rendering, shell, stylesheet, asset-loading, and component differences must be investigated prior to implementation.
- **Expected Behaviour:**
  - Preview Player Experience must visually match the actual Player workspace.
  - Reuse the existing North Star visual foundation, stadium background, premium blue glass components, typography, spacing, cards, buttons, and responsive layouts.
  - Preserve clear Parent Preview identification and viewing context.
  - Do **not** create a separate duplicated visual architecture.
  - Do **not** unnecessarily modify the accepted actual Player workspace.

##### Regression B — Missing Exit Preview / Return to Parent Navigation
- **Observed Behaviour:**
  - A dedicated button previously allowed a Parent to exit the Preview Player Experience and return to their own Parent workspace; that button is now missing (exact original wording unconfirmed).
- **Expected Behaviour:**
  - Investigate Git history and existing preview navigation architecture to establish the original return behaviour and why it regressed.
  - Restore a clearly visible, dedicated Exit Preview control (recommended wording: **Exit Preview — Return to Parent View**, or an appropriately concise equivalent consistent with existing Club OS terminology).
  - Position the control prominently within the preview experience so it is immediately discoverable on mobile and desktop.
  - Style the control using the established North Star midnight-blue-and-gold design system.
  - Return the authenticated Parent to their own Parent workspace using the canonical workspace/context-switching mechanism and cleanly clear the active child-preview context.
  - Do **not** rely on browser history, browser Back navigation, or the Viewing Mode dropdown as the sole means of exiting preview.
  - Do **not** sign the user out, change their underlying identity, or introduce a new independent persona-switching architecture.

##### Security & Safeguarding Requirements (Visual Parity Must Not Mean Permission Parity)
- Preserve Guardian authorisation and active relationship checks.
- Preserve canonical authenticated Parent identity and linked-child data scoping.
- Preserve all existing preview restrictions — never grant Player mutation permissions through Parent Preview.
- Never expose unrelated children, other families' information, or privileged operational controls.
- Ensure exiting preview restores the Parent workspace cleanly rather than leaving stale Player Preview context active.

##### Required Future Implementation Acceptance Criteria (All 11 Mandatory)
1. Compare the actual Player workspace and Preview Player Experience side by side on mobile and desktop.
2. Confirm matching stadium backgrounds, glass components, visual hierarchy, and responsive presentation.
3. Confirm Parent Preview identification remains clear.
4. Confirm the dedicated Exit Preview control is visible and accessible.
5. Confirm selecting Exit Preview returns directly to the authenticated Parent's own workspace.
6. Confirm preview context is correctly cleared.
7. Confirm the Parent can subsequently preview an authorised linked child again.
8. Confirm existing multi-child and multi-role boundaries remain intact.
9. Confirm no inappropriate Player actions become available through preview.
10. Confirm the actual Player workspace remains visually and functionally unchanged.
11. Confirm notification subscription persistence after the Academy plugin ZIP replacement.

#### `PARENT-EXPERIENCE-001B` — Second Authorised Parent/Guardian Back My Game Link Access
- **Status:** `PARTIALLY IMPLEMENTED` (Blocked by per-issuer scoping, one-time hash storage & `AGE_UNKNOWN` silent skip)
- **Original Source:** Prompt §5.3
- **Expected Behaviour:** Every authorised active Parent/Guardian of a linked child must be able to see, activate, and share/copy the child's Back My Game link without depending on being the first/issuing Guardian, while preserving individual safeguarding restrictions and relationship authorisation.
- **Current Implementation Evidence:** Three verified root causes:
  1. `BackMyGameInvitationService.php:50` queries `latest_for_actor_destination_subject(..., $actor_id, $player_id)` (`created_by_person_id = %d`), and `FundraisingShareLinkService.php:92, 196` + `BackMyGameInvitationService.php:103` scope uniqueness and revocation to the individual issuing guardian rather than household `(campaign, player)`.
  2. `FundraisingShareLinkService.php:52-53, 118` & `PortalParentBackMyGamePage.php:14, 211-216` store only a SHA-256 `token_hash` and show the raw URL once on activation/replace, so neither Guardian 1 (after reload) nor Guardian 2 can copy an existing active link without replacing/revoking it.
  3. `BackMyGameAuthorityPolicy.php:30-36` / `FundraisingShareAttributionPolicy.php:34-38` enforce `KNOWN_ADULT` (`classify_person()`), silently skipping all children (`continue` at `BackMyGameInvitationService.php:45`) if a second guardian has no DOB and no AGE-001 manual verification.
- **Acceptance Evidence:** None (reported by PO on Academy).
- **Priority / Target:** **P1 — Academy MVP**
- **Dependencies:** `AGE-001` (`39a4b43`).
- **Proposed Batch:** **Batch 2 — Parent Scoping, Back My Game Multi-Guardian & Welfare Polish**
- **Remaining Work:** Scope active Back My Game invitation lookup/lifecycle per `(campaign, player)` across any authorised active Guardian; decide/implement safe link re-copying (or encrypted/retrievable share token vs per-guardian link) while keeping revocation/rotation safe; surface clear non-silent state if a guardian lacks adult verification.
- **PO Decisions / Screenshots Required:** **Decision D1:** Should both authorised Guardians share one household Back My Game link (requiring safe retrieval for re-copying, or replacing resets for both), or should each authorised Guardian hold their own independent link for the same child? Also confirm whether a second Guardian without DOB/AGE-001 verification should see an explicit "Adult verification required" explanation rather than "No eligible Player".

#### `BMG-001` — Parent Back My Game Linked Child Supporter & Pledge Status Visibility
- **Status:** `OUTSTANDING`
- **Original Source:** `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` / `CLUB_OS_MVP_TO_PRODUCTION_RELEASE_STRATEGY.md` (B03-N4)
- **Expected Behaviour:** Authorised Parents can view privacy-safe supporter/pledge status summary for their linked child's Back My Game invitations.
- **Current Implementation Evidence:** Not implemented on `PortalParentBackMyGamePage.php`.
- **Acceptance Evidence:** None.
- **Priority / Target:** **P2 — Academy MVP (Conditional on PO scope approval)**
- **Dependencies:** `PARENT-EXPERIENCE-001B`.
- **Proposed Batch:** **Batch 2** (if approved for MVP) or defer explicitly to Post-MVP.
- **PO Decisions / Screenshots Required:** **Decision D2:** Confirm exact privacy-safe fields visible to Parents (e.g., supporter count & pledge total vs supporter names) and whether `BMG-001` stays in Academy MVP or moves to Post-MVP.

#### `WELFARE-POLISH-001` — Welfare People Directory Pagination, Section Spacing & Mobile Readability
- **Status:** `PARTIALLY IMPLEMENTED` (Staff Compliance pagination `PER_PAGE=5` is ALREADY COMPLETE on Welfare & Secretary; Welfare People pagination & Welfare section spacing are missing)
- **Original Source:** Prompt §5.4 + `OS-011` (`CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`)
- **Expected Behaviour:** Add `DirectoryPagination` to `/club-os/welfare/people/` matching the accepted Staff Compliance pagination pattern (preserving search, role filter, eligibility & privacy); fix zero-gap touching `<section class="iexel-experience-section">` cards across Welfare sub-pages (`PortalWelfarePeopleDirectoryPage`, `PortalWelfareConcernsPage`, `PortalWelfareStaffCompliancePage`, `PortalWelfarePersonProfilePage`); polish `OS-011` Concern Detail card hierarchy; fix cramped `521px–900px` rows and unstyled `select` inside `.iexel-welfare-people-search`.
- **Current Implementation Evidence:** Confirmed `MemberExperienceService.php:608-684` & `WelfarePersonDirectorySnapshot.php:18-28` & `PortalWelfarePeopleDirectoryPage.php:92-141` have zero pagination; `assets/css/member-experience.css:56` has no sibling `.iexel-experience-section + .iexel-experience-section` spacing rule in `.iexel-experience-main`; `member-experience.css:5199` omits `select` styling.
- **Acceptance Evidence:** None.
- **Priority / Target:** **P1 — Academy MVP**
- **Dependencies:** `WELFARE-UX-001B` (`07d9943`).
- **Proposed Batch:** **Batch 2 — Parent Scoping, Back My Game Multi-Guardian & Welfare Polish**
- **Remaining Work:** Add `paged` filtering-before-pagination to `welfare_people_directory()`, add pagination payload to `WelfarePersonDirectorySnapshot`, render `DirectoryPagination` on `PortalWelfarePeopleDirectoryPage`, add vertical spacing between consecutive `.iexel-experience-section` blocks, refine Concern Detail hierarchy (`OS-011`) and mobile/tablet card responsiveness.

---

### 4.3 Coach Matchday & Events Experience (Batch 3)

#### `COACH-MATCH-001A` — Lineup Builder Mobile Wrapping, Custom Alignment Enhancement & Pitch Drag Lock
- **Status:** `PARTIALLY IMPLEMENTED` (Alignment exists from `90164d5` with gaps; mobile wrapping is defective; pitch drag lock is unimplemented)
- **Original Source:** Prompt §5.1
- **Expected Behaviour:** (1) Player names on mobile Lineup Builder cards (e.g., *Jonathan*) wrap cleanly without awkward mid-word character splits; (2) custom formation horizontal & vertical alignment assistance works reliably (including empty/unassigned custom slots, pitch centre-line snap `x=50%`, practical mobile tolerance, and keyboard support); (3) explicit Lock/Unlock player movement toggle on the pitch prevents accidental movement while scrolling on mobile while preserving intentional editing and formation saving.
- **Current Implementation Evidence:**
  - Wrapping: `assets/css/member-experience.css:6284, 6340-6355` applies `overflow-wrap: anywhere` on `44px`/`64px` pitch cards (36px inner width at `<=360px`), splitting names mid-word.
  - Alignment: `assets/js/match-lineup.js:1082-1118, 1257-1315` has H/V guides & snap (added in `90164d5`, no regression) but filters snap targets to `assignedBySlot[...]` only, has no centre-line snap, pointer-only, and caps threshold at `1.5%`.
  - Drag lock: Zero implementation; `public.css:6335` unconditionally sets `touch-action: none` and `match-lineup.js:1289` starts drag at `5px`.
- **Acceptance Evidence:** None (PO screenshots available prior to implementation).
- **Priority / Target:** **P1 — Academy MVP**
- **Dependencies:** None.
- **Proposed Batch:** **Batch 3 — Coach Matchday, Lineup Builder & Events Experience**
- **PO Decisions / Screenshots Required:** **Screenshots S1:** Product Owner mobile Lineup Builder screenshots showing name wrapping and custom alignment/scroll-drag pain points.

#### `COACH-MATCH-001B` — Match Mode Live Squad Bulk Attendance, Bulk Bench Selection & Vacant Pitch Entry
- **Status:** `PARTIALLY IMPLEMENTED` (Starting with empty/incomplete lineup is allowed today; bulk Live Squad attendance/bench and vacant pitch entry without an outgoing player are NOT implemented)
- **Original Source:** Prompt §5.1
- **Expected Behaviour:** (1) Bulk attendance updates and bulk bench additions directly inside Match Mode's Live Squad section (reusing existing Match Hub / Lineup Builder attendance & selection logic rather than single-player tap-and-redirect loops); (2) allow eligible players to enter vacant pitch positions after match start (including matches started with an empty or incomplete lineup) **without** requiring an outgoing player, while preserving valid substitution history, participation records, goalkeeper rules, and match state replay.
- **Current Implementation Evidence:**
  - `MatchModeLiveBenchCard.php` & `match-mode-player-actions.js` only support single-player popup -> redirect to `/attendance/?person_id=...` -> single-player `MatchLiveBenchAdmissionService::admit($event_id, $person_id)`.
  - `MatchStateService` already permits starting with 0 or partial starters, but `MatchLineupSubmissionService.php:98-101` locks lineup edits once started, and `MatchSubstitutionService.php:90-97,157-162`, `MatchSubstitutionGoalkeeperTransitionService.php:140-147`, `MatchPitchStateService.php:69-72`, and `MatchSubstitutionFormCard.php:24,53-54` strictly require a non-empty `$player_out_person_id`.
- **Acceptance Evidence:** None.
- **Priority / Target:** **P1 — Academy MVP**
- **Dependencies:** None.
- **Proposed Batch:** **Batch 3 — Coach Matchday, Lineup Builder & Events Experience**
- **Remaining Work:** Add bulk attendance + bulk bench admission controls/endpoints in Match Mode reusing existing attendance/bench services; introduce a clean canonical vacant-position pitch-entry action/incident (distinct from 1-for-1 substitution) handled safely by `MatchPitchStateService`, `MatchReportService`, undo, and participation stats.

#### `COACH-MATCH-001C` — Match Report Circular Player Avatars (Saved Lineup & Ratings Consistency)
- **Status:** `REGRESSION` / `PARTIALLY IMPLEMENTED`
- **Original Source:** Prompt §5.1
- **Expected Behaviour:** Saved lineup and Player Ratings sections on Match Report render consistent circular player profile images matching Player of the Match.
- **Current Implementation Evidence:**
  - `MatchRatingsCard.php:20` renders `PersonAvatar::render(..., 'is-compact')`, but `assets/css/public.css:7135` (`.iexel-match-report-player > span`, specificity `0,1,1`) overrides `.iexel-person-avatar` (`0,1,0`), distorting the avatar into a gold-padded rounded rectangle (`border-radius: 8px; padding: 10px 4px; background: var(--iexel-gold)`).
  - `MatchSummaryCard.php:46-49, 57-59` renders **no** avatars on Saved Lineup and `MatchReportService.php:239-240` does not hydrate `profile_image` onto `$workspace['starters']` / `$workspace['substitutes']`.
  - Minor layout tweak: `.iexel-match-report-potm` (`public.css:7168`) has 2 grid columns for 3 read-only children.
- **Acceptance Evidence:** None (PO screenshots available).
- **Priority / Target:** **P2 — Academy MVP**
- **Dependencies:** None.
- **Proposed Batch:** **Batch 3 — Coach Matchday, Lineup Builder & Events Experience**
- **PO Decisions / Screenshots Required:** **Screenshots S2:** Product Owner Match Report screenshot if any additional visual expectations apply.

#### `EVENTS-EXPERIENCE-001A` — Event Detail & Matchday Hub Hero Consolidation + Training Hub Terminology
- **Status:** `PARTIALLY IMPLEMENTED` (Coach Match deduplicated; Coach non-Match, Parent/Player Event Detail, and Matchday Hub repeat hero facts; Training events leak `Matchday Hub` terminology)
- **Original Source:** Prompt §5.2
- **Expected Behaviour:** (1) Consolidate key event details into the event hero banner and eliminate repeated `EventInfoGrid`/`EventVenueCard`/`EventCountdownCard`/`MatchdayVenueCard` blocks across Coach non-Match, Parent/Player event pages (using Coach match hero as visual foundation without exposing Coach-only controls), and Matchday Hub; (2) replace inappropriate `Matchday Hub` terminology on Training events with canonical **Training Hub** (or **Session Hub**) terminology across headings, navigation, breadcrumbs, edit redirects, and attendance backlinks, integrating Plan · Coach · Reflect cleanly.
- **Current Implementation Evidence:**
  - Duplication confirmed at `PortalEventDetailPage.php:454-482, 641-645, 992-1000` and `MatchdayHubPage.php:60-65, 136`.
  - `Matchday Hub` leakage confirmed at `EventAttendancePage.php:227-228` (`Back to Matchday Hub` for all non-live events), `PortalEventEditPage.php:43` (unconditional redirect to `matchday`), `PortalRouter.php:2607-2609` (breadcrumb `'Matchday Hub'`), `CoachActionsCard.php:117`, and `MatchdayHubPage.php` / `MatchdayTimelineCard.php`.
- **Acceptance Evidence:** None.
- **Priority / Target:** **P1 — Academy MVP**
- **Dependencies:** `TRAINING-LIFECYCLE-FOUNDATION-01` (`96cbcda`).
- **Proposed Batch:** **Batch 3 — Coach Matchday, Lineup Builder & Events Experience**
- **PO Decisions / Screenshots Required:** **Decision D3:** Confirm preferred label — **Training Hub** vs **Session Hub** — for Training events.

#### `EVENTS-EXPERIENCE-001B` — Plan · Coach · Reflect Training Reflection Stage (`COACHING-EXPERIENCE-SLICE-03`)
- **Status:** `PARTIALLY IMPLEMENTED` (`Plan` & `Coach` complete in Slices 01–02B [`50656ae`, `a7efc32`]; `Reflect` is a read-only `'Preview Only'` stub)
- **Original Source:** `COACHING-EXPERIENCE-SLICE-01/02A/02B` + Prompt §5.2
- **Expected Behaviour:** Complete the **Reflect** stage (Slice 03) on finished training sessions without rebuilding completed Plan or Coach functionality: coach-authored post-session reflection persistence, optimistic concurrency/audit, appropriate lifecycle gate (`TrainingSessionPlanPolicy::can_reflect()` already pre-wired at lines `88-99`), and Academy acceptance on the now-finished training event.
- **Current Implementation Evidence:** `TrainingSessionPlanPage.php:27, 1451-1504` renders static `'Preview Only'` reflection prompts from `TrainingSessionPlanPreviewService.php:80` with zero form, POST handler, DB table/columns, or repository.
- **Acceptance Evidence:** Slices 01–02B committed & packaged; Slice 03 not built; finished training event now ready on Academy.
- **Priority / Target:** **P1 — Academy MVP**
- **Dependencies:** `COACHING-EXPERIENCE-SLICE-02B` (`a7efc32`), `EVENTS-EXPERIENCE-001A`.
- **Proposed Batch:** **Batch 3 — Coach Matchday, Lineup Builder & Events Experience**
- **Remaining Work:** Additive reflection persistence (schema migration + repository/service), Reflect form & read-only summary in `TrainingSessionPlanPage.php`, integration with Training Hub summary card, permanent validator, and Academy acceptance.

#### `EVENTS-EXPERIENCE-001C` — Recurring Event Series & Future-Occurrence Audience Editing
- **Status:** `OUTSTANDING`
- **Original Source:** Prompt §5.2
- **Expected Behaviour:** Allow authorised Coaches/Secretaries to add participants to future occurrences of an existing recurring event series with explicit scope choice (`This event only` vs `This and future events in the series`), preserving historical occurrences, existing attendance/RSVP responses, deduplicating audience rows, and avoiding repeat invitations/notifications to already-invited participants.
- **Current Implementation Evidence:** `DatabaseManager.php:413-445` (`events` table) has **zero** series/recurrence columns; `EventCreationService.php:11-37` and `TeamEventForm.php:228-250` create unlinked independent rows; `PortalEventAudiencePage.php`, `PortalEventEditPage.php`, and `PortalSecretaryEventProfilePage.php` edit only a single `$event_id`.
- **Acceptance Evidence:** None.
- **Priority / Target:** **P1 — Academy MVP**
- **Dependencies:** `SEC-009` (if Specific People modal is reused), canonical `EventAudienceBuilder` & `EventNotificationVisibility`.
- **Proposed Batch:** **Batch 3 — Coach Matchday, Lineup Builder & Events Experience**
- **Remaining Work:** Add nullable additive series linkage column (e.g. `recurrence_series_id` / `series_uuid` + index via `UpgradeRunner`) populated on recurring event creation; add scoped batch audience addition across current + future non-cancelled/non-past occurrences in series; ensure notifications/invitations fire only for newly added participants. *(Note: historical pre-existing recurring events created before this column will remain single-event unless matched/linked explicitly — disclose clearly.)*

#### `SEC-009` — Secretary Create Event "Specific People" Selector Modal Mobile Overflow
- **Status:** `IMPLEMENTED — NEEDS VERIFICATION` (reproduce on current HEAD per B03 before editing)
- **Original Source:** `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` / `CLUB_OS_MVP_TO_PRODUCTION_RELEASE_STRATEGY.md` (B03-N5)
- **Expected Behaviour:** "Specific People" selector modal on Secretary Create/Edit Event has zero horizontal overflow at `320px–390px`.
- **Current Implementation Evidence:** Still open in Release Strategy; should be verified and resolved alongside Event Audience work in Batch 3 (or Global UX).
- **Priority / Target:** **P2 — Academy MVP**
- **Proposed Batch:** **Batch 3** (or Batch 7 Global UX).

---

### 4.4 People Identity, Youth Player & Guardian Registration, and Safe Duplicate Merge (Batch 4)

#### `PEOPLE-001` — Youth Player & Guardian Registration Workflow (During Add Person)
- **Status:** `OUTSTANDING`
- **Original Source:** `IEXEL-Club-OS-Development-Handover-AGE-001.md`, `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md:933-937`, Prompt §5.7
- **Expected Behaviour:** During `/club-os/secretary/people/new/`, detect a proven under-18 youth Player from canonical DOB (`PersonAgeClassification::classify()`), offer inline Parent/Guardian capture, search/suggest potential existing adult Guardian records by name/email/phone (supporting multi-child families without creating duplicate Persons and **never** auto-merging), or create a new canonical Guardian Person and link the active `parent_of`/`guardian_of` relationship atomically, while keeping Person creation strictly separate from portal account provisioning and preserving adult/youth/unknown-age safeguarding. Also align `PortalSecretaryGuardianLinksPage.php:38` to use `classify_person()` (respecting AGE-001).
- **Current Implementation Evidence:** `PortalSecretaryPersonAddPage.php` (468 lines) currently has **no** dynamic youth-player detection for standard `player` role, **no** inline Guardian fields, and **no** existing Guardian matcher (line 314 tells the Secretary to navigate away to Guardian Links afterwards). `AGE-001` and `AGE-001A` are confirmed `COMPLETE` (`39a4b43`).
- **Acceptance Evidence:** None.
- **Priority / Target:** **P1 — Academy MVP**
- **Dependencies:** `AGE-001` (`39a4b43`).
- **Proposed Batch:** **Batch 4 — People Identity, Youth Guardian Registration & Duplicate Merge Repair**
- **Remaining Work:** Add progressive DOB-triggered Youth Guardian section to `PortalSecretaryPersonAddPage`, safe existing-Guardian candidate search (name/email/phone, explicit Secretary confirmation required, zero auto-merge), atomic creation + relationship link service, and `classify_person()` alignment on `PortalSecretaryGuardianLinksPage`.

#### `PEOPLE-MERGE-001` — Duplicate Detection & Merge Execution Repair and Safety Hardening
- **Status:** `REGRESSION` (Implemented in commits `92f97b1`..`00b86d9`, but broken in live UI and carrying a critical Finance/Safeguarding silent safety bypass)
- **Original Source:** Prompt §5.8 + commits `92f97b1`..`00b86d9`
- **Expected Behaviour:** Authorised full Secretaries can detect duplicates, switch proposed survivor cleanly, reconcile contact details safely, keep separate records, or execute a transactional clean-case merge that accurately blocks on **all** canonical Finance, Welfare/Medical, Staff Compliance, Account, Privileged Role, and Event/Match dependencies, preserving relationships, registrations, and mandatory audit history.
- **Current Implementation Evidence:** Codebase audit confirmed **7 concrete defects** in live HEAD:
  1. **[CRITICAL — ALWAYS FAILS]** `PortalSecretaryPersonMergePreviewPage.php:920,1049` submits `$model['version']` (preview hash), whereas `PersonMergeExecutor.php:162` and `PersonDuplicateReviewService.php:78` check `$case['version']` (case hash) — so both *Resolve Duplicate* and *Confirm Separate Members* always fail (`stale_comparison` / `comparison_changed`).
  2. **[CRITICAL — BROKEN SURVIVOR SWITCH]** `PortalSecretaryPersonMergePreviewPage.php:409,427,451` omits `comparison_version` on survivor switch URLs/forms, causing `PersonMergePreviewService.php:64-65` to throw; survivor radio buttons (`line 404`) sit outside any `<form>` with no JS listener.
  3. **[CRITICAL — NON-FUNCTIONAL CONTACT RECONCILIATION]** Contact radios (`lines 497,501`) are hardcoded `disabled`; `WordPressPersonMergeTransaction.php:265` omits `email, phone, address` from `lock_pair_for_update()`, so `PersonMergeExecutor.php:294,324` never updates contact fields.
  4. **[CRITICAL — SILENT SAFETY BYPASS]** `PersonMergeExecutor.php:734,747` checks non-existent table names (`invoices`, `payments`, `billing_schedules`, `shop_orders`, `safeguarding_concerns`, `medical_notes`, `player_welfare_cases`) instead of canonical `finance_invoices`, `finance_payments`, `finance_billing_schedules`, `club_shop_orders`, `finance_accounts`, `fundraising_*`, `welfare_concerns`, `player_operational_medical_safety`, and skips `person_credentials` completely — silently returning 0 blockers!
  5. Undefined `$identity_confirmed` variable (`PortalSecretaryPersonMergePreviewPage.php:821,840,860,871`).
  6. 404 broken link to `/club-os/secretary/people/guardians/` (`line 576`; canonical is `/club-os/secretary/guardian-links/`).
  7. Preflight key mismatch (`clean_case_resolution` vs `clean_case`, `line 163`) and duplicate DOM `id="section-e-title"` (`lines 904,931,966`).
- **Acceptance Evidence:** Failed PO usability expectations on Academy (matches root causes above).
- **Priority / Target:** **P0 (Data Integrity & Safeguarding Safety) — Academy MVP**
- **Dependencies:** Follows interim server-side containment `PEOPLE-MERGE-SAFETY-001` (proposed for **Batch 1** subject to PO approval — Decision **D13**).
- **Proposed Batch:** **Batch 4 — People Identity, Youth Guardian Registration & Duplicate Merge Repair** *(full merge repair remains in Batch 4; interim server-side safety containment is proposed for Batch 1 under `PEOPLE-MERGE-SAFETY-001`)*.
- **Remaining Work:** Fix all 7 defects (especially canonical table blocker checks including `person_credentials`, `version` contract alignment, survivor switching, contact reconciliation, 404 link, and UI tokenisation), add end-to-end runtime regression tests covering Finance/Welfare/Compliance blocker enforcement and clean merge execution, and verify manually on Academy.

---

### 4.5 Treasurer Mobile UX, Fundraising Payment Methods & Training Only Fee Rules (Batch 5)

#### `FINANCE-UX-001` — Treasurer Mobile, Fundraising Payment Methods & Club Shop Finance Polish
- **Status:** `PARTIALLY IMPLEMENTED` (Orders Awaiting Payment mobile alignment ALREADY FIXED in `5b79c5c` / `shop-finance.css:57-67`; remaining 4 sub-issues confirmed open)
- **Original Source:** Prompt §5.5 (note: *Recent Payments heading* explicitly `WITHDRAWN` by PO)
- **Expected Behaviour:**
  1. Fix Fundraising `View Campaign` button mobile card overflow (`PortalTreasurerFundraisingPage.php:376`: `<a>` with `width: 100%; padding: 10px 16px` missing `box-sizing: border-box` overflows by `32px`).
  2. Display actual recorded payment methods (`FundraisingOrder::$payment_method` / `finance_payments.method`) on Appeal campaign detail pages (`PortalTreasurerAppealCampaignPage.php:95-124`, `PortalSecretaryFundraisingDetailPage.php:195-334`) and complete method mapping on `PortalTreasurerBackMyGameCampaignPage.php:48-56` (already displayed on main Treasurer Fundraising page for Member Appeals & Spot the Ball, and on Spot the Ball detail page — never fabricate missing values).
  3. Eliminate unnecessary mobile horizontal scroll on Finance Overview Income Source Breakdown (`PortalFinanceWorkspacePage.php:430-459` inherits `.iexel-finance-table-scroll table { min-width: 640px }` at `member-experience.css:237` despite only 3 compact columns).
  4. Polish Club Shop Finance (`PortalTreasurerShopFinancePage.php` + `shop-finance.css`): consistent compact From/To date filter sizing and styled `Clear` button; clarify or add genuine all-orders view (currently `"View all orders →"` at `line 69` routes to `/club-os/finance/club-shop/pending/` unpaid-only); fix individual order page backlink (hardcoded to `/pending/` even for paid orders), `.iexel-shop-bank-confirm` checkbox sizing, and mobile CTA alignment.
  5. Re-verify Orders Awaiting Payment mobile alignment (`shop-finance.css:57-67`) without rebuilding it.
- **Acceptance Evidence:** Orders Awaiting Payment fixed in `5b79c5c`; other 4 defects confirmed open in code.
- **Priority / Target:** **P1 — Academy MVP**
- **Dependencies:** None.
- **Proposed Batch:** **Batch 5 — Treasurer Mobile UX, Club Shop Finance & Training Only Fee Rules**
- **PO Decisions / Screenshots Required:** **Decision D4:** On Club Shop Finance, should `"View all orders →"` link to a new Treasurer All Orders directory (paid + awaiting payment + cancelled) or simply be relabelled `"View pending orders →"` for MVP?

#### `FINANCE-FEES-001` — Training Only Fee Rules & Match Player Transition Billing
- **Status:** `OUTSTANDING`
- **Original Source:** Prompt §5.6 (no prior specification existed in `iexel-club-os-docs`)
- **Expected Behaviour:** Allow Treasurer Fee Rules and Billing Schedules to target active `TrainingMembership` participants (not solely `team_assignments`), and support clean future billing when a member transitions between Training Only and Match Player without duplicating charges, mutating previously issued invoices, or creating unintended retrospective billing.
- **Current Implementation Evidence:**
  - `FeeRule.php` / `FeeRuleValidator.php:70` (hardcodes `U7–U18` regex, excluding `U5`, `U6`, `Senior`) / `BillingAudienceResolver.php:23-120` (`INNER JOIN team_assignments` / rejects `missing_team_season`) completely exclude all `TrainingMembership` records.
  - `TrainingMatchPlayerTransitionService.php` & `MatchPlayerTrainingTransitionService.php` have zero Finance interaction.
  - Helpful readiness hook: `FinanceIntelligenceService.php:554,578` already maps `'training_fee'` and `'training_membership'` invoice line types to `FinancialSummary::SOURCE_TRAINING` (`'Training-Only Fees'`).
- **Acceptance Evidence:** None.
- **Priority / Target:** **P1 — Academy MVP (Requires PO policy decisions before implementation)**
- **Dependencies:** PO decisions D5–D8 (Section 10).
- **Proposed Batch:** **Batch 5 — Treasurer Mobile UX, Club Shop Finance & Training Only Fee Rules**
- **PO Decisions / Screenshots Required:** **Decisions D5–D8** (see Section 10: mid-cycle transition timing — next billing cycle vs pro-rata; existing current-month invoice handling; automatic vs Treasurer-reviewed schedule transition; expanding age groups to `U5`/`U6`/`Senior` & keeping `entire_club` Match-Player-only vs explicit `training_only` target; sibling `DiscountPolicy` inclusion; unregistered training-only billing eligibility).

#### `FIN-031` — Treasurer Static Text Caret Cursor
- **Status:** `IMPLEMENTED — NEEDS VERIFICATION` (2026-09-08 diagnostic showed browser caret browsing, not a Club OS code defect; awaiting PO confirmation to close)
- **Original Source:** `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`
- **Priority / Target:** **P3 — Close on PO confirmation**
- **Proposed Batch:** Confirm closure during Batch 5 review.

---

### 4.6 Notifications Programme, Personal Account & Remaining Member Experiences (Batch 6)

#### `NOTIFY-FINANCE-001` — Treasurer Overdue Invoice Full-Settlement Notifications
- **Status:** `OUTSTANDING`
- **Original Source:** Prompt §4.3 (provisional reference)
- **Expected Behaviour:** When a confirmed payment (manual recording, bank reconciliation, credit allocation, or online SumUp checkout) **fully settles** a previously **overdue** invoice, notify authorised active adult Treasurers (privacy-safe lock-screen copy with zero names/amounts/sensitive details; route to authorised `/club-os/finance/invoices/{id}/`) so they stop chasing it. Keep partially paid invoices outstanding without firing full-settlement notices; prevent duplicate notifications; preserve financial audit history; consider suppressing self-notification when the Treasurer personally records the payment.
- **Current Implementation Evidence:** Zero Treasurer payment-settlement notifications exist in `InvoiceNotificationService.php`, `ShopPaymentSettlementService.php`, or `PushAutomaticNotificationDispatcher.php`. Exact post-`COMMIT` integration points verified at `InvoiceOnlinePaymentSettlementService::settle_attempt()` (`line 177`) and `FinanceService` → `FinanceRepository::allocate()` (`line 419`). `Invoice::is_overdue()` and `FinanceOperationalAlertsProvider` derive live from `status IN ('issued','part_paid') AND due_date < today`, so overdue totals and dynamic Priority Alerts automatically clear upon `status = 'paid'`.
- **Acceptance Evidence:** None.
- **Priority / Target:** **P1 — Academy MVP**
- **Dependencies:** `NOTIFY-010A` (`952b37f`).
- **Proposed Batch:** **Batch 6 — Remaining Notifications, Personal Account & Member Experiences**
- **PO Decisions / Screenshots Required:** **Decision D9:** Confirm (a) both email + Web Push or Web Push only, (b) suppress self-notification when the acting Treasurer records a manual payment themselves (recommended: yes, suppress self-push/email while keeping on-screen confirmation), and (c) gate under existing `auto_finance_enabled` or a dedicated toggle.

#### `NOTIFY-009C` — Mobile Push Notification Grouping Investigation & Refinement (Android & iOS)
- **Status:** `OUTSTANDING`
- **Original Source:** `SCHED-001C-Final`, `NOTIFY-009A/B/B1`, `NOTIFY-010A`, `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`, Prompt §4.2
- **Expected Behaviour:** Refine Service Worker notification `tag` / `renotify` / grouping behaviour across Android and iOS so concurrent/distinct notifications do not overwrite unrelated alerts while related updates group cleanly.
- **Current Implementation Evidence:** Not implemented (`assets/pwa/service-worker.js` uses current flat tag behaviour).
- **Priority / Target:** **P2 — Academy MVP**
- **Proposed Batch:** **Batch 6 — Remaining Notifications, Personal Account & Member Experiences**

#### `NOTIFY-PRIORITY-001` — Priority Alert-to-Push Coverage Audit & Committee/Treasurer Alert Scoping Fix
- **Status:** `OUTSTANDING`
- **Original Source:** `NOTIFY-009B1` Sec 4 (product rule: *every new actionable Priority Alert must have an associated push pathway*) + `NOTIFY-009B1` Sec 5 #2 / `NOTIFY-010A` Sec 4 (Treasurer operational Priority Alerts leaking into Committee workspace) + Prompt §4.2
- **Expected Behaviour:** Audit all actionable Priority Alerts against automatic push pathways (closing gaps cleanly within adult/youth safeguards) and stop Treasurer operational alerts from leaking into the Committee workspace (`COM-002` alignment).
- **Current Implementation Evidence:** `UX-ALERTS-001` (`0bfdafc`) completed the North Star UI; the cross-workspace alert-to-push coverage audit and Committee/Treasurer alert scoping fix remain open.
- **Priority / Target:** **P2 — Academy MVP**
- **Proposed Batch:** **Batch 6 — Remaining Notifications, Personal Account & Member Experiences**

#### `NOTIFY-010B` — Registration Lifecycle Notifications
- **Status:** `OUTSTANDING` (recovered from `NOTIFY-010A` handover Sec 4)
- **Original Source:** `IEXEL-Club-OS-Development-Handover-NOTIFY-010A.md`
- **Expected Behaviour:** Notify Parents/families via email + eligible Web Push when a Registration transitions to `under_review` (information requested), `approved`, or `rejected`.
- **Priority / Target:** **P2 — Academy MVP (or confirm deferral if time-constrained)**
- **Proposed Batch:** **Batch 6** (confirm MVP inclusion with PO).

#### `NOTIFY-VERIFY-001` — Remaining Open Notification Manual Acceptance Checks
- **Status:** `IMPLEMENTED — NEEDS VERIFICATION`
- **Original Source:** `NOTIFY-008D`, `NOTIFY-009B1`, `NOTIFY-010A` handovers
- **Expected Behaviour:** Complete the 3 small outstanding Academy live verification checks: (1) `NOTIFY-009B1` non-recipient separate-account announcement visibility/safeguarding check; (2) `NOTIFY-010A` natural overdue invoice cron transition (`iexel_club_os_check_overdue_invoices`), rollout floor skip, and repeat-run dedupe; (3) remaining 2/5 `NOTIFY-008D` manual negative checks (all 5 already automated).
- **Priority / Target:** **P2 — Academy MVP**
- **Proposed Batch:** Verify alongside Batch 1 / Batch 6 Academy acceptance.

#### `ACCOUNT-UX-001` — Portal-Native Personal Account / My Profile Page
- **Status:** `OUTSTANDING` (Active broken-loop UX bug for all non-admin members)
- **Original Source:** Prompt §4.4
- **Expected Behaviour:** Introduce a secure, portal-native `/club-os/account/` (**My Profile**) page using the authenticated user's canonical Person identity, membership/role summary, and appropriate self-service account/password controls, replacing the broken `/wp-admin/profile.php` link in `PortalHeader.php:65` while preserving `Qualifications & Compliance`, `Notifications`, `Install Your Club OS`, and `Sign out`.
- **Current Implementation Evidence:** `PortalHeader.php:65-69` links `Account` to `get_edit_profile_url($c->user_id)` (`/wp-admin/profile.php`), which `AdminAccessBoundary.php:43-48` actively blocks for every non-admin member, logging `wp_admin_access_blocked` and bouncing them back to their dashboard! `AccountUrl.php` currently only exposes `qualifications_compliance()`.
- **Acceptance Evidence:** None.
- **Priority / Target:** **P1 — Academy MVP**
- **Dependencies:** `WELFARE-UX-001C` (`f72ffa7`).
- **Proposed Batch:** **Batch 6 — Remaining Notifications, Personal Account & Member Experiences**
- **PO Decisions / Screenshots Required:** **Decision D10:** Should My Profile be read-only identity + change-password link for MVP, or allow self-service editing of personal email/phone/address (with audit logging and safeguarding guard for youth accounts)?

#### `PLAYER-UX-001` — Actual Player Workspace: Pending Functional Commitments (`PL-026`, `PL-027`) & Reverification-Only Audit Notes
- **Status:** `IMPLEMENTED — NEEDS VERIFICATION` / `OUTSTANDING` (`PL-021..025` remain `COMPLETE` and accepted; PO confirmed actual Player workspace is visually and functionally satisfactory)
- **Original Source:** `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` (`PL-026`, `PL-027`), Prompt §4.5 (`DEVELOPMENT-BACKLOG-001`), reconciled per `DEVELOPMENT-BACKLOG-001A` §3
- **Scope Boundary:** Covers **actual Player workspace** only. Do **not** reopen or unnecessarily restyle accepted actual Player Experience functionality (`PL-021..025`). Preview Player Experience regressions are tracked separately under **`PLAYER-PREVIEW-UX-001`** (Batch 2, Section 4.2) — do not duplicate its scope here.
- **Expected Behaviour & Remaining Items (Do Not Assume Redevelopment):**
  1. **Retained Functional Commitments (Pending Explicit PO Confirmation — Decision D13):** `PL-026` (My Stats expandable match-by-match breakdown) and `PL-027` (My Progress contextual deep links into completed Match Reports) remain recorded from the roadmap; confirm explicitly with the PO before scheduling implementation rather than assuming redevelopment is required.
  2. **Reverification-Only Code Audit Observations (Do Not Automatically Change):** Previously noted actual-Player codebase observations — hardcoded `IEXEL F.C.` at `PortalPlayerStatsPage.php:35`, `.iexel-experience-shell--parent`-only selectors at `member-experience.css:8729-8730, 8765-8766`, and Player Quick Actions spacing/placement (`PortalDashboardLayout.php:67`) — must be **reverified against the live Academy actual Player workspace** before making any change, ensuring the accepted North Star actual Player workspace is not disturbed.
- **Priority / Target:** **P2 — Academy MVP (Pending PO confirmation)**
- **Proposed Batch:** **Batch 6 — Remaining Notifications, Personal Account & Member Experiences**

#### `OS-031` — In-App Image & Attachment Viewer (Lightbox CSS Fix & Non-Image Viewer)
- **Status:** `PARTIALLY IMPLEMENTED` / `REGRESSION` (Broken overlay for all non-executive members on `/club-os/messages/`)
- **Original Source:** `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` (`OS-031`), Prompt §4.5
- **Expected Behaviour:** Viewing image/attachment links in Club Announcements opens a clean, accessible in-app viewer with visible Close control, Escape/backdrop dismissal, focus restoration, and download link across **all** member workspaces (Parent, Player, Coach, Treasurer, Welfare, Secretary, Committee) without forcing browser Back navigation.
- **Current Implementation Evidence:** `PortalAnnouncementsPage.php:275-294` + `assets/js/communications.js:433-490` implement the image lightbox, **but** `.iexel-lightbox-*` CSS lives exclusively in `assets/css/executive-dashboard.css:972-1065`, which `PortalRouter.php:276-283` does **not** enqueue for `/club-os/messages/`! Result: non-executive members get an unstyled DOM block dumped at the bottom of `<body>`. Non-image attachments (PDFs) open in an external tab/download only.
- **Priority / Target:** **P1 (Image Lightbox Fix) — Academy MVP**; richer inline PDF viewer optional/post-MVP if browser sandbox constraints apply.
- **Proposed Batch:** **Batch 6 — Remaining Notifications, Personal Account & Member Experiences**

#### `MSG-BACKLINK-001` — Club Announcements Visited Backlink & "Read Announcement" Contrast
- **Status:** `PARTIALLY IMPLEMENTED` (Fixed for Executive & Coach shells only; still broken for Parent & Player shells)
- **Original Source:** `SCHED-001C-Final`, `NOTIFY-009B1` Sec 5 #3, `NOTIFY-010A` Sec 4, Prompt §4.5
- **Expected Behaviour:** `← All announcements` (`PortalAnnouncementsPage.php:256`) and `"Read announcement"` links maintain high-contrast gold/white styling on both `:link` and `:visited` states with `>=44px` touch target across **all** workspaces (including Parent and Player).
- **Current Implementation Evidence:** `member-experience.css:11034-11049` (Executive) and `11114-11125` (Coach) use `:any-link`; Parent & Player shells (`8125-8127`) lack `:visited` / `:any-link` specificity, allowing browser/theme purple visited links.
- **Priority / Target:** **P1 — Academy MVP**
- **Proposed Batch:** **Batch 6** (or Batch 7 Global UX).

#### `SHOP-CANCEL-001` & `FIN-MYFINANCE-001` & `COM-002` — Recovered Pre-MVP Commitments
- **`COM-002` (Committee Data Minimisation):** `IMPLEMENTED — NEEDS VERIFICATION` / `OUTSTANDING` — Verify strict exclusion of confidential Welfare notes, debtor ledgers, medical records, and leaked Treasurer alerts from Committee surfaces (`SPRINTS.md` / Roadmap Tier A). **Target:** Batch 6.
- **`SHOP-CANCEL-001` (Club Shop Cancellation UX & Secretary/Club-Initiated Cancellation):** `OUTSTANDING` (recovered from `NOTIFY-010A` handover). **Target:** Batch 6 (or confirm deferral to Post-MVP).
- **`FIN-MYFINANCE-001` (Minimal `My Finance` for non-Parent adults):** `OUTSTANDING` (recovered from `NOTIFY-010A` handover — invoice ownership labels + non-Parent adult invoice access). **Target:** Batch 6 (confirm MVP vs Post-MVP with PO).

---

### 4.7 Global Visual/Mobile Polish & Academy MVP Feedback (Batch 7)

#### `GLOBAL-UX-001` — Cross-Workspace Visual, Contrast, Backlink & Mobile Polish
- **Status:** `PARTIALLY IMPLEMENTED` (`VIS-01..01D` contrast baseline closed `23,124` checks, but concrete portal defects remain + PO WhatsApp screenshot review pending)
- **Original Source:** Prompt §5.9 + `development/ASSISTANT_SECRETARY_OUTSTANDING.md` + Academy Oct 22 UX observations
- **Expected Behaviour:** Resolve all remaining cross-workspace visual/contrast/mobile issues:
  1. **Guardian Links notice contrast (`PortalSecretaryGuardianLinksPage.php:73-75, 196-198`):** Replace unstyled WP-Admin `.notice notice-success`/`notice-error` with canonical `.iexel-experience-notice` semantic classes (and audit `PortalTreasurerRegistrationDetailPage.php:47,55`, `PortalTreasurerRegistrationArrangePackagePage.php:102`, `PortalSecretaryPersonEditPage.php:465`).
  2. **Global `:visited` backlink & button styling:** Add explicit `:visited` / `:any-link` protection to `.iexel-experience-hero a`, `.iexel-experience-button`, and portal backlinks in `assets/css/design-system.css` so visited links never turn unreadable dark purple on midnight-blue surfaces.
  3. **Tokenise remaining hardcoded/malformed inline styles:** `PortalSecretaryPersonMergePreviewPage.php` inline dark colors, `PortalSecretaryPersonProfilePage.php:603` malformed `style="color: #94a3b8; italic"`, and `ASSISTANT_SECRETARY_OUTSTANDING.md` items (venue detail readability, success-message presentation, Portal Account presentation).
  4. **Academy Oct 22 UX observations:** Team Season Edit Snapshot long-page jump, Team Assignments form styling, Add Person Club Roles spacing.
  5. **Screenshot-Driven Polish Placeholder (`GLOBAL-UX-001-SCREENSHOTS`):** Dedicated slot for Product Owner screenshots from the private WhatsApp development group (supplied workspace-by-workspace prior to Batch 7; agent never accesses WhatsApp directly) plus a comprehensive rendered-browser visual sweep (`320px`, `360px`, `390px`, `412px`, `1280px`).
  - *Note:* Global restriction of text/image selection is explicitly **NOT** an MVP requirement (deferred Post-MVP; must never block copying addresses, contacts, or payment references).
- **Priority / Target:** **P1 — Academy MVP**
- **Proposed Batch:** **Batch 7 — Global Visual/Mobile Polish & MVP Feedback**
- **PO Decisions / Screenshots Required:** **Screenshots S3:** Supply remaining workspace visual defect screenshots from PO review group prior to Batch 7.

#### `MVP-FEEDBACK-001` — In-App Issues, Fixes & Suggestions (Academy MVP Tester Feedback)
- **Status:** `OUTSTANDING` (100% greenfield — verified zero existing feedback/support tables, routes, or forms in codebase)
- **Original Source:** Prompt §5.10
- **Expected Behaviour:** Lightweight in-app feedback submission form (categories: *Something isn't working*, *Suggest an improvement*, *General product suggestion*) capturing submission date, category, concise message, and current workspace context; authorised administrator feedback inbox with simple lifecycle (`New`, `Under Review`, `Planned`, `Resolved`); strict data minimisation, privacy, and youth submission safeguards (no complex ticketing platform).
- **Priority / Target:** **P1 — Academy MVP**
- **Proposed Batch:** **Batch 7 — Global Visual/Mobile Polish & MVP Feedback**
- **PO Decisions / Screenshots Required:** **Decision D11:** Confirm youth submission policy (recommended: adult accounts submit directly; youth Player accounts either disabled with "Ask your Parent/Guardian or Coach to submit feedback" OR parent-reviewed/no free-text PII). Confirm who can view/manage the inbox (Club Admin only vs Club Admin + Secretary).

---

### 4.8 Release Readiness Gate (Batch 8 — Academy MVP vs Commercial Release)

See **Section 8 (Public Commercial Release Requirements)** and **Section 9 (Technical Debt & Validation Limitations)** for the full structured gate matrix (`M01`–`M18`, `B4D-04A`, `NOTIFY-004B` diagnostic closeout, Apple PWA/device acceptance, clean install/upgrade matrix, and `P2P-01..12` conditional decision).

---

## 5. Pending & Protected Working-Tree Implementation Inventory

Exactly **14 files** remain uncommitted in `c:\Users\leavi\Local Sites\iexel-club-os-dev\worktrees\notify001b2-ordinary-events`. **All 14 must remain byte-identical** until explicitly targeted by their respective authorised batches.

### 5.1 Pending `NOTIFY-COMPLIANCE-001` Implementation (11 Files — Target: Batch 1 `NOTIFY-COMPLIANCE-001-FIX`)

| File | Git State | Verified SHA-256 | Notes |
| :--- | :--- | :--- | :--- |
| `app/core/Application.php` | Modified | `8944B077A0183E442C51613BD7DA7C14A45499817B022B6B4431D6228CA3B7B6` | Registers daily hook `iexel_staff_compliance_expiry_check` |
| `app/core/Communications/PushAutomaticNotificationDispatcher.php` | Modified | `2F012477B125EA695A303E4CADBD8D40B69D0493B18C3619FA0AA01192684E73` | Adds `enqueue_staff_compliance()` gated on `auto_compliance_enabled` |
| `app/core/Communications/PushDeliveryQueue.php` | Modified | `FE402FFE028D56A86E76A17DD09305601604CD322E5927D1C22BFF3EEBC71397` | Adds adult-only `staff_compliance` destination type |
| `app/core/Communications/PushPilot.php` | Modified | `38F429E465A84FA8B5C733453B2DE4128BEE5FE15B71E5665B31781B36803D2A` | Tap destination auth (**contains `welfare` role bug at L237**) |
| `app/core/Communications/PushPilotConfig.php` | Modified | `8DF41C5A9F22B7CE93D200D4218B00E4D36823CE99078AA683118BA5F07E91A0` | Defaults `auto_compliance_enabled => false` (OFF) |
| `app/core/Communications/PushPilotController.php` | Modified | `3CBA060167E607CB365B696C8739952AE181C2B3CA18C2A2BF4C408C2EA0BD85` | Admin toggle & manual dry/live run handler |
| `app/core/Kernel.php` | Modified | `B16E78F075D149B879015CC4D37D11793EFA8E8942392FD4B7C6076566174929` | Wires `staff_compliance_notification_service()` |
| `app/core/UI/Pages/PushControlsPage.php` | Modified | `32517CB6EA00B569DFBACD4B0EBFF8A8F55E66C9AB55F1BFF2502DC3C012796C` | Admin UI toggle & manual run button (disabled when OFF) |
| `assets/pwa/service-worker.js` | Modified | `01934991D6590C7F8836B321532B3FCDBE66C9B4C0C054960EA17C7CF4C17481` | Privacy-safe static lock-screen copy for `staff_compliance` |
| `app/core/StaffCompliance/StaffComplianceNotificationService.php` | Untracked | `81BDD2839B0361E1A735B58FACE5D1EDC8EE3A2DB36E750A5BB6EDE1A45F9917` | Contains all 3 known defects (`welfare` role key, cross-recipient dedupe, non-atomic transient lock) |
| `tools/validate-notify-compliance-001.php` | Untracked | `F81D89AD1E16FC8AB28E14BB0C8C0F85FE3963D22AA2A4DBB1B9A5795E6FECE8` | Masks `welfare` defect via stubbed role key |

### 5.2 Protected `NOTIFY-004B` Diagnostic Files (3 Files — Deferred Until Post-Academy MVP / Pre-Public Commercial Release)

| File | Git State | Verified SHA-256 | Notes |
| :--- | :--- | :--- | :--- |
| `app/core/Events/EventNotificationVisibility.php` | Modified | `0F082C179222EF82D0573693B2630170D76A0F65B86AA1B70B9B6EB0C19E6896` | Adds optional `?string &$stage = null` with 12 diagnostic stage codes. **Academy ZIPs always package committed `HEAD` blob.** |
| `tools/validate-notify004b-tap-diagnostic.php` | Untracked | `69AD1E94B6E288E3C65D46815C5CFCAF7FB23C47CADBBF771AB21D84CF4BC61D` | Retired harness referencing legacy `diagnostic_arm`/`diagnostic_claim` methods (excluded from Academy ZIPs) |
| `tools/validate-notify004b-tap-diagnostic-browser.cjs` | Untracked | `CE69C929C27BF9DC976FBD629B9F8DD562675FB1D516BF9143C588882A0F3EEE` | Retired browser diagnostic harness (excluded from Academy ZIPs) |

---

## 6. Proposed Accelerated Implementation Programme (8 Coherent Batches)

To meet the Product Owner's deadline without compromising safeguarding, financial integrity, or privacy, the active pre-MVP work is consolidated into **8 coherent, end-to-end batches** (reducing fragmented micro-releases and repetitive manual acceptance cycles):

| Batch | Name & Scope | Included Refs | Dependencies & Prerequisite PO Input | Targeted Academy Manual Acceptance |
| :--- | :--- | :--- | :--- | :--- |
| **Batch 1** *(Recommended Next; P0 changes subject to PO approval)* | **Staff Compliance Notifications, Personal Reminders & Proposed P0 Containment** | `NOTIFY-COMPLIANCE-001-FIX`, `WELFARE-NOTIFY-002`, `WELFARE-TEST-001`, plus proposed P0 additions: `PARENT-EXPERIENCE-001A` (**P0**), `PEOPLE-MERGE-SAFETY-001` (**P0** server-side containment) | **D13** (PO approval of proposed P0 elevation into Batch 1; Staff Compliance notifications build directly on 11 pending files + `SCHED-001B`) | Single combined check: notification persistence on ZIP replace, default-OFF verification, enable officer & personal toggles, verify Welfare + Secretary + staff email & push delivery, per-recipient dedupe, lock-screen privacy, CLI runner; verify multi-role Secretary on Parent Home sees own family only; verify unsafe duplicate merge blocked server-side |
| **Batch 2** | **Parent Experience, Preview Player Experience & Welfare Polish** | `PARENT-EXPERIENCE-001B`, `PLAYER-PREVIEW-UX-001` (Regressions A & B — North Star visual parity + Exit Preview navigation), `WELFARE-POLISH-001` (incl. `OS-011`), optional `BMG-001` *(plus `PARENT-EXPERIENCE-001A` if not approved for Batch 1)* | **D1** (BMG shared vs per-guardian link), **D2** (`BMG-001` MVP inclusion) | Verify 2nd Guardian sees/copies/manages BMG; verify all 11 `PLAYER-PREVIEW-UX-001` acceptance criteria side-by-side with unchanged actual Player workspace; Welfare People pagination & section spacing on mobile + desktop; notification persistence |
| **Batch 3** | **Coach Matchday, Lineup Builder & Events Experience** | `COACH-MATCH-001A/B/C`, `EVENTS-EXPERIENCE-001A/B/C`, `SEC-009` | **S1/S2** (Lineup/Match Report screenshots), **D3** (Training Hub vs Session Hub) | Mobile Lineup wrapping, alignment & drag lock; Match Mode bulk attendance/bench & vacant pitch entry; Match Report avatars; Training Hub + finished-session **Reflect** persistence; recurring series future-audience addition; notification persistence |
| **Batch 4** *(P0 Repair)* | **People Identity, Youth Player & Guardian Registration & Full Duplicate Merge Repair** | `PEOPLE-001`, `PEOPLE-MERGE-001` (**P0** full repair following Batch 1 `PEOPLE-MERGE-SAFETY-001` containment) | Follows `PEOPLE-MERGE-SAFETY-001` containment | Add youth Player -> suggest existing Guardian / create new Guardian atomically (zero auto-merge); full Duplicate Merge survivor switch, contact reconciliation, Finance/Welfare/Compliance blocker enforcement, clean-case merge & Keep Separate; notification persistence |
| **Batch 5** | **Treasurer Mobile UX, Fundraising Payment Methods & Training Only Fee Rules** | `FINANCE-UX-001`, `FINANCE-FEES-001`, `FIN-031` (close) | **D4** (Shop View All Orders), **D5–D8** (Training Only fee & transition billing policy) | Mobile View Campaign card fit, Appeal payment methods, Income Source Breakdown zero horizontal scroll, Shop filters/detail controls; Training Only fee rule creation, billing run & Match Player transition; notification persistence |
| **Batch 6** | **Remaining Notifications, Personal Account & Member Experiences** | `NOTIFY-FINANCE-001`, `NOTIFY-009C`, `NOTIFY-PRIORITY-001`, `COM-002`, `ACCOUNT-UX-001`, `PLAYER-UX-001` (`PL-026/027` pending PO confirm; actual Player visual items reverify-only), `OS-031`, `MSG-BACKLINK-001`, `NOTIFY-VERIFY-001`, optional `NOTIFY-010B` / `SHOP-CANCEL-001` / `FIN-MYFINANCE-001` | **D9** (`NOTIFY-FINANCE-001` channel/self-suppress), **D10** (My Profile editability), **D13** (`PL-026/027` confirm) | Overdue invoice full vs partial settlement Treasurer notice; My Profile navigation (no WP-Admin redirect loop); non-executive image lightbox; Parent/Player visited announcement backlinks; confirmed actual-Player commitments without disturbing accepted `PL-021..025`; notification persistence |
| **Batch 7** | **Global Visual/Mobile Polish & Academy MVP Feedback** | `GLOBAL-UX-001` (incl. Guardian Links notice, global `:visited`, `GLOBAL-UX-001-SCREENSHOTS`), `MVP-FEEDBACK-001` | **S3** (PO WhatsApp screenshots), **D11** (Feedback youth policy & inbox access) | Cross-workspace rendered browser sweep (`320px–1280px`), submit & triage feedback items as adult + verify youth boundary; notification persistence |
| **Batch 8** | **Final Academy MVP & Public Commercial Release Readiness** | `B4D-04A`, `NOTIFY-004B` diagnostic closeout, Apple PWA/device acceptance, clean install & upgrade matrix, validator debt cleanup, `main` promotion & release tagging (`M01–M18`) | Local MySQL/nginx restored or staging DB host; **D12** (`P2P-01..12` v1.0 inclusion/exclusion) | Full release readiness sign-off (distinct Academy MVP sign-off vs Public Commercial Release sign-off) |

> **Governance & Efficiency Guardrail:** All proposed priority changes remain subject to explicit Product Owner approval before application implementation. **The accelerated programme must not be interpreted as authorisation for unrestricted simultaneous implementation or unrelated refactoring.** Cosmetic/visual fixes within Batches 2, 5, 6, and 7 allow bounded autonomy to resolve adjacent contrast, spacing, and wrapping defects in one pass while preserving safeguarding, identity, permission, finance, and notification validation. Each batch runs targeted automated validators + headless Chrome multi-viewport checks + one concise Academy acceptance checklist (always including notification persistence).

---

## 7. Post-MVP Backlog (Explicitly Deferred — Do Not Promote Without PO Approval)

All deferred commitments recovered from `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`, `MASTER_DEVELOPER_GUIDE.md`, `SPRINTS.md`, Nov 2026 handovers, and Prompt §7:

| Ref / Area | Deferred Requirement | Source |
| :--- | :--- | :--- |
| **NOTIFY-SETTINGS-001** | Member-facing grouped notification category controls (including Select All / Deselect All) with separate explicit youth safeguards | Prompt §4.2 |
| **PWA-INSTALL-REMINDER-001** | Non-permanent PWA install reminder cadence / backoff (currently permanent one-shot `localStorage` flag) | Prompt §4.2 |
| **SCHED-FUTURE** | Lower-friction scheduling setup & scheduler health diagnostics UI | `MASTER_DEVELOPER_GUIDE.md`, `SPRINTS.md` |
| **COM-SCALE-001** | Push delivery scale-out beyond bounded immediate/opportunistic batches for large club-wide audiences | Experience Roadmap L909 |
| **YOUTH-PUSH-DEEPLINK** | Direct `?communication_id=<id>` deep link for youth `communication` push taps (currently lands on `/club-os/messages/`) | `NOTIFY-008B/C` handover |
| **BRAND-ANIM-001** | Optional subtle reduced-motion animated loading treatment for the gold OS coin | `BRAND-001B` handover |
| **I18N-001** | Multilingual / multi-locale product support | `BRAND-001B` handover |
| **WEATHER-001** | Real weather API integration (replacing dormant `WeatherService` / `EventWeatherCard` placeholder) | Prompt §7, `ReleaseBaseline` |
| **GAMIFY-001** | Rewards, achievements, XP, leaderboards, Player development journeys & team challenges (`iexel_manage_rewards`) | Prompt §7, Roadmap |
| **COACH-POST-001** | Coach development pointers, travel time, richer Matchday Notes, match clock/timer, extra time, penalties, cards/injuries, tactical diagrams, AJAX/WebSockets, PDF match exports, Venue/Address Finder & Recent Grounds | Prompt §7, `SPRINTS.md`, Roadmap |
| **COMMITTEE-HEALTH-001** | Committee Team Health Dashboard & Team Health Profiles (`OS-002`, `OS-006`) | Prompt §7, Roadmap |
| **WELFARE-ADV-001** | Advanced Welfare concern edit/archive lifecycle (`OS-009`), detailed case notes, follow-up reminders, secure document uploads, external referrals, AI summaries, concern comms, compact filters (`OS-012`) | Prompt §7, `SPRINTS.md`, Roadmap |
| **COMPLIANCE-ADV-001** | Compliance messaging, document uploads, renewal submissions, professional qualification portfolios, configurable expiry threshold UI, missing-compliance ("Not Recorded") alerting, standalone Volunteer compliance eligibility review | Prompt §7, Roadmap L709 |
| **COMMS-RICH-001** | Richer club communications, photo galleries, club content, configurable Secretary email/reply-to addresses, authorised club mailbox integration, taster/trial email invitations | Prompt §7, Roadmap |
| **FINANCE-ADV-001** | Genuine Finance Reports (`FIN-033` future scope), CSV/PDF exports (`iexel_export_finance`), advanced bank reconciliation, richer online payment integrations, general post-registration package upgrades/amendments, `F6 Club Draw` lottery, `FND-001` QR fundraising attribution | Prompt §7, Roadmap, `TECHNICAL_DEBT_REGISTER.md` |
| **SET-002 / 003 / 004** | Image cropping/positioning/zoom/focal-point controls (`SET-002`); modular Club/System/Experience settings (`SET-003`); Club Profile presets (`SET-004`: Grassroots/Academy/Semi-Pro/Pro/Custom) | Prompt §7, Roadmap |
| **ADM-004** | Sensitive-role & Assistant Secretary approval governance workflows; full operational migration away from `/wp-admin/` (keeping permanent `/wp-admin/` recovery invariant `ADM-006`) | Prompt §7, Roadmap |
| **AUDIT-001** | Broader `ActivityLogger` coverage across direct admin People/Team/Venue/user-link/Event mutations | Prompt §7, `TECHNICAL_DEBT_REGISTER.md` |
| **CLEANUP-001** | Dormant placeholder cleanup (`modules/`, `WeatherService`, `EventWeatherCard`, `EventRewardsCard`, `AvailabilitySummaryCard`, `EventStatusCard`, `MatchdayNotesCard`, legacy `PortalShellLayout`, duplicate `app/Permissions/PermissionManager.php`) | Prompt §7, `ReleaseBaseline` |
| **TEXT-SELECT-001** | Optional selective UI text/image selection restrictions (must never disable copying addresses, contact details, or payment references) | Prompt §5.9 |
| **CMC-POST-V1** | Verified Historical Appearance, Verified Historical Assist, Historical Registration candidate evidence, effective-dated Team-assignment history | Roadmap L654–679 |
| **PROSPECT-POST-001** | Direct Prospect → Competitive Match Registration (`INVITED_MATCH_REGISTRATION`), Prospect trial integration with Team training events, Training Member portal, Historical former-Player experience | Roadmap L528–538 |
| **COMMERCIAL-ECOSYSTEM** | Commercial Licensing Engine & signed updates, Club OS Control Centre (no-PII sovereign data), Optional Premium Club OS Website Theme, Universal Native Mobile App, Public Demo Environment (auto-reseed), Multi-Club Productisation, Role Onboarding Setup Wizard & Video Training Library, League OS Vision | `MASTER_DEVELOPER_GUIDE.md` |

---

## 8. Public Commercial Release Requirements (Distinction: Academy MVP vs Commercial Release)

| Gate | Academy MVP | Public Commercial Release | Current State |
| :--- | :---: | :---: | :--- |
| **Active Pre-MVP Batches 1–7** | Required | Required | In progress (Batches 1–7 queued) |
| **Notification Delivery & Update Persistence** | Required (checked after every Academy ZIP replace) | Required | Passing on Android Chrome & Edge; standing release rule retained |
| **Safeguarding, Identity & Role/Workspace Permission Regression** | Required | Required | Ongoing automated + manual verification (P0 fixes in Batches 2 & 4) |
| **Financial Integrity Regression** | Required | Required | Automated passing; Batch 5 expands for Training Only fee rules |
| **Case-Sensitive Autoload & PHP Packaging Integrity** | Required | Required | Passing (`validate-case-sensitive-autoload.php` `0` failures; `validate-hotfix-dash-001-php-packaging-integrity.php` `9/9`) |
| **Local/Staging DB-Backed WordPress Runtime Testing** | Recommended (mitigated by Academy live tests) | **Required** | **BLOCKED locally** (Local MySQL/nginx stopped) |
| **Clean Installation & Retained-Data Upgrade Matrix (`CP-CERT-INSTALL` / `CP-CERT-UPGRADE`)** | Partial (Academy upgrade tested) | **Required** | Uncertified against latest artifact (`M13`) |
| **Apple Device / iOS Safari Home Screen PWA Acceptance** | Recommended | **Required** | iPhone SW registration repaired (`68066b0`); full Apple push & UX sign-off still open |
| **Final Mobile (`320–412px`) & Desktop (`1280–1440px`) Cross-Workspace Review (`M09–M10`)** | Required (Batch 7 sweep) | **Required** | Scheduled in Batch 7 & Batch 8 |
| **Protected `NOTIFY-004B` Diagnostic Closeout** | **Deferred** (excluded from Academy ZIPs) | **Required before commercial release** | 3 protected files remain uncommitted in plugin working tree |
| **Production Host Cron Verification (`SCHED-001B`)** | Academy verified (`SCHED-001C`) | **Required on production host** | Unchecked in `RELEASE_CHECKLIST.md` |
| **Disaster Recovery Vault (`B4D-04A` / `IEXEL_RC_VAULT`, `M14`)** | Planning baseline complete | **Required** | End-to-end backup, off-device custody & restore rehearsal open |
| **Role How-To Guides & Admin Recovery Guide (`M15`)** | Optional | **Required** (7 role guides + admin guide, synthetic data only) | Not yet authored |
| **Branch Promotion (`main`), Version Bump, `release/{v}` & `v{v}` Tag (`M16–M18`)** | Work proceeds on `feature/notify004a-adult-web-push` | **Required** | All recent work on feature branch; merge to `main` & fresh prod install pending |
| **Pay-to-Play (`P2P-01..12`)** | Conditional / Unapproved | Conditional / Unapproved | Awaits explicit PO ratification or exclusion (`D12`) |

---

## 9. Technical Debt & Validation Limitations

1. **Local WordPress DB Runtime Blocked:** Local MySQL/nginx in LocalWP is currently stopped (`Error establishing a database connection` on `wp-load.php`). Automated CLI tests run zero-DB against real runtime classes/repositories; live MySQL-backed runtime validation requires starting LocalWP services or running against an isolated staging DB before commercial release.
2. **Legacy Validator Drift (5 Verified Failure Root Causes + Documented Legacy Items):**
   - `tools/validate-secretary-command-centre.php`: Fatal error — stub block omits `get_user_by()` needed by `OperationalRoleAccessManager::sync_user()`.
   - `tools/validate-secretary-people-foundation.php`: Outdated regex on `PortalSecretaryPersonProfilePage.php:273` predating AS-02/AS-03 `! $delegated &&` guard.
   - `tools/validate-secretary-people-permissions.php`: Hardcodes old `UpgradeVersions::SCHEMA_VERSION === '2026.10.21'` and `2026_10_historical_match_evidence` as final step (current is `2026.11.23`).
   - `tools/validate-secretary-mobile-responsive.php`: Fails on `!important` added later to `.iexel-experience-dashboard--secretary` grid (`member-experience.css:7186-7207`).
   - `tools/validate-as01-assistant-secretary-foundation.php`: Fails asserting Assistant Secretary nav omits `shop` (intentionally superseded by `SHOP-ACCESS-001B` `f2b837d`).
   - Additional drifted legacy validators documented in `ASSISTANT_SECRETARY_OUTSTANDING.md` & handovers: `validate-parent-priority-alerts-rsvp-window.php`, `validate-role-aware-navigation.php`, `validate-visual-foundation.php`, `validate-treasurer-finance-configuration.php`, and SQLite-dependent merge validators requiring `pdo_sqlite`.
3. **Stale Release & Schema Metadata:**
   - `ReleaseReadinessService.php:70` says `38-table inspection` vs `73` actual canonical tables in `DatabaseManager::CANONICAL_TABLES`.
   - `ReleaseBaseline.php:97-98` lists 11 JS / 6 CSS assets vs actual 20 JS / 14 CSS files; `scheduled_cleanup_ready()` checks 2 cron hooks while `hooks()` lists 4.
   - `ReleaseSchemaInventory::TABLE_CONTRACTS` still describes `person_duplicate_reviews` as having no merge capability.
4. **Architecture & Tooling Debt:**
   - Duplicate `app/Permissions/PermissionManager.php` alongside canonical `app/core/Permissions/PermissionManager.php`; empty `modules/` registry; legacy `app/Database/`, `app/Helpers/`, `app/Services/`.
   - Capability enforcement parity gaps (`iexel_manage_communications`, `iexel_manage_teams`, `iexel_view_audit_log`, `iexel_manage_settings` falling back to `iexel_manage_club_os` in admin handlers; unimplemented `iexel_export_finance`).
   - `FinancialSummary::unallocated_receipts_count` undefined property & 500-row unpaid hydration cap noted in `ASSISTANT_SECRETARY_OUTSTANDING.md`.
   - No `phpcs.xml` / Composer dev tooling; fragile `iexel_club_os_rewrite_schema` stamp convention; `iexel-fee-rule-back` CSS naming debt.
5. **Documentation Repo Drift:** `README.md`, `TECHNICAL_DEBT_REGISTER.md`, `RELEASE_CHECKLIST.md`, `MASTER_DEVELOPER_GUIDE.md`, `SPRINTS.md`, and `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` carry outdated headers, conflicting baseline SHAs, and 6+2 uncommitted edits on `docs/registration-package-step-validation` (reconcile in a dedicated documentation housekeeping commit when authorised).

---

## 10. Product Owner Decisions & Screenshot Evidence Required

### 10.1 Decisions Required Before Corresponding Batches

| ID | Batch | Decision Needed | Recommended Default |
| :--- | :---: | :--- | :--- |
| **D1** | Batch 2 | **Back My Game Multi-Guardian Link Model (`PARENT-EXPERIENCE-001B`):** Share one retrievable household link across all authorised active Guardians for a child, OR issue independent links per Guardian? Also show explicit "Adult verification required" notice when a 2nd Guardian is `AGE_UNKNOWN`? | Shared household `(campaign, player)` link viewable/copyable by any authorised active adult Guardian + explicit adult-verification notice (never silent empty state). |
| **D2** | Batch 2 | **`BMG-001` Scope:** Include Parent Back My Game supporter/pledge summary in Academy MVP (and confirm privacy-safe fields: totals/count only vs supporter names), or defer to Post-MVP? | Defer to Post-MVP unless needed for Academy fundraising launch; if included, show aggregate count & total only. |
| **D3** | Batch 3 | **Training Event Terminology (`EVENTS-EXPERIENCE-001A`):** Preferred canonical label — **Training Hub** or **Session Hub**? | **Training Hub** (mirrors *Matchday Hub* cleanly for grassroots coaches). |
| **D4** | Batch 5 | **Club Shop Finance (`FINANCE-UX-001`):** Should `"View all orders →"` link to a new Treasurer All Orders directory (paid + awaiting payment + cancelled) or be relabelled `"View pending orders →"`? | Add a simple status filter (`Awaiting payment` / `Paid` / `All`) on the Treasurer Club Shop Orders directory so `"View all orders →"` is truthful. |
| **D5** | Batch 5 | **Training Only → Match Player Transition Billing (`FINANCE-FEES-001`):** When a player transitions mid-month, apply the new fee rule from the **next monthly billing cycle** (leaving current issued invoice immutable) or compute mid-month pro-rata / top-up invoices? | **Next billing cycle** (preserves immutable issued invoice ledger & avoids complex credit-note/pro-rata accounting for MVP). |
| **D6** | Batch 5 | **Schedule Transition Behaviour (`FINANCE-FEES-001`):** Automatically pick up/drop transitioned players on the next billing run (with a clear Treasurer preview banner of transitioned players), or require manual Treasurer schedule reassignment? | Dynamic resolution at billing run time with an explicit "Transitioned since last run" indicator in the billing preview. |
| **D7** | Batch 5 | **Training Only Fee Rule Scope (`FINANCE-FEES-001`):** Expand Fee Rule age groups beyond `U7–U18` to include `U5`, `U6`, and `Senior`? Keep existing `entire_club` schedules Match-Player-only (requiring explicit `training_only` target) so existing schedules never accidentally double-bill? | **Yes** to both — expand to `U5–U18 + Senior`, and keep `entire_club` Match-Player-only with explicit `training_only` rule/audience target. |
| **D8** | Batch 5 | **Training Only Discounts & Registration Status (`FINANCE-FEES-001`):** Do Training Only members count toward family sibling `DiscountPolicy` tiers? Can Training Only members without a `registered` competitive `PlayerRegistration` be billed? Is a one-off Match Player joining fee triggered on upgrade? | Allow billing active `TrainingMembership` without competitive registration; apply sibling discounts only if explicitly opted in on the policy; handle one-off joining fees manually or via explicit one-off fee rule. |
| **D9** | Batch 6 | **Treasurer Overdue Settlement Notice (`NOTIFY-FINANCE-001`):** Deliver via **Email + Web Push** or **Web Push only**? Suppress self-notification when the acting Treasurer manually records the payment? Gate under `auto_finance_enabled` or a dedicated toggle? | Email + Web Push, suppress self-notification for the acting Treasurer (keep on-screen confirmation), and gate under `auto_finance_enabled` (or separate default-OFF toggle if preferred). |
| **D10** | Batch 6 | **Personal Account / My Profile (`ACCOUNT-UX-001`):** Read-only canonical identity + change-password flow for MVP, or allow adults to edit their own email/phone/address? | Read-only canonical identity, membership/role summary & secure password change for MVP (safest against identity/email drift before public release). |
| **D11** | Batch 7 | **MVP Feedback Safeguarding (`MVP-FEEDBACK-001`):** Restrict submissions to adults (with helpful message for youth Players), and who accesses the inbox (Club Admin only vs Club Admin + Secretary)? | Adult-only submission for MVP (no youth free-text PII risk); Club Admin inbox (with optional Secretary read access). |
| **D12** | Batch 8 | **Pay-to-Play (`P2P-01..12`) & Optional Queue (`NOTIFY-010B`, `SHOP-CANCEL-001`, `FIN-MYFINANCE-001`):** Confirm which (if any) are required for Academy MVP vs formally deferred to Post-MVP. | Defer `P2P-01..12` to Post-MVP unless explicitly ratified for 2026/27 season; decide `NOTIFY-010B` / `SHOP-CANCEL-001` / `FIN-MYFINANCE-001` before Batch 6. |
| **D13** | Batch 1 / Batch 6 | **Proposed Critical-Risk Prioritisation & Actual-Player Commitments (`DEVELOPMENT-BACKLOG-001A`):** (a) Approve elevating `PARENT-EXPERIENCE-001A` (P0 data leak) and adding `PEOPLE-MERGE-SAFETY-001` (P0 server-side duplicate-merge containment) into **Batch 1** alongside Staff Compliance notifications (retaining full merge repair in Batch 4); (b) confirm whether `PL-026` and `PL-027` (`PLAYER-UX-001`) are still desired for Academy MVP or deferred to Post-MVP. | Approve proposed Batch 1 P0 containment (`PARENT-EXPERIENCE-001A` + `PEOPLE-MERGE-SAFETY-001`) for immediate risk reduction; confirm `PL-026`/`PL-027` before Batch 6 without disturbing the accepted actual Player workspace. |

### 10.2 Product Owner Screenshots Needed Before Implementation
- **S1 (Before Batch 3):** Mobile Lineup Builder screenshots (player name wrapping e.g. *Jonathan*, custom formation alignment, accidental scroll-drag).
- **S2 (Before Batch 3):** Match Report saved lineup / ratings screenshot (if additional polish beyond circular avatars is desired).
- **S3 (Before Batch 7):** Workspace-grouped screenshots from the PO's private WhatsApp development group for `GLOBAL-UX-001-SCREENSHOTS`.

---

## 11. Requirement Traceability Register

Every requirement in `DEVELOPMENT-BACKLOG-001` (§4–§8) and every recovered roadmap/handover commitment is mapped 1:1 below:

| Stable Ref | Requirement Summary | Source | Status | Release Target | Batch |
| :--- | :--- | :--- | :--- | :--- | :---: |
| `NOTIFY-COMPLIANCE-001-FIX` | Officer Staff Compliance expiry reminders (3 defects + CLI runner hook) | Prompt §4.1, pending tree | `PARTIALLY IMPLEMENTED` | Academy MVP | Batch 1 |
| `WELFARE-NOTIFY-002` | Personal staff credential expiry reminders (separate default-OFF control) | Prompt §4.1 | `OUTSTANDING` | Academy MVP | Batch 1 |
| `WELFARE-TEST-001` | Combined Staff Compliance notification E2E acceptance | Prompt §4.1 | `OUTSTANDING` | Academy MVP | Batch 1 |
| `NOTIFY-009A` | Latest Event Update only per event in Priority Alerts | Handover, `001e61f` | `COMPLETE` | Academy MVP | Done |
| `NOTIFY-009B` / `009B1` | Secretary/AS Priority Alerts & recipient-centred announcement alerts | Prompt §4.2, `8e8bfeb` | `COMPLETE` *(1 manual test in `NOTIFY-VERIFY-001`)* | Academy MVP | Done / B6 |
| `NOTIFY-009C` | Mobile push notification grouping (Android & iOS) | Prompt §4.2, Roadmap | `OUTSTANDING` | Academy MVP | Batch 6 |
| `NOTIFY-009D` | Event-aware notification workspace routing | Prompt §4.2, `39a4b43` | `COMPLETE` | Academy MVP | Done |
| `NOTIFY-PRIORITY-001` | Priority Alert-to-push coverage audit & Committee/Treasurer alert scoping | Prompt §4.2, `NOTIFY-009B1` | `OUTSTANDING` | Academy MVP | Batch 6 |
| `NOTIFY-010A` | Finance invoice & Club Shop notifications | Handover, `952b37f` | `COMPLETE` *(1 cron check in `NOTIFY-VERIFY-001`)* | Academy MVP | Done / B6 |
| `NOTIFY-010B` | Registration lifecycle notifications (`under_review`/`approved`/`rejected`) | `NOTIFY-010A` handover | `OUTSTANDING` | Academy MVP / Confirm | Batch 6 |
| `NOTIFY-VERIFY-001` | Remaining 3 live manual notification checks (`009B1`, `010A` cron, `008D`) | Handovers | `IMPLEMENTED — NEEDS VERIFICATION` | Academy MVP | Batch 1/6 |
| `NOTIFY-004B-CLOSEOUT` | Protected diagnostic files closeout (preserve tap fix) | Prompt §4.2, §8 | `DEFERRED` | Public Commercial Release | Batch 8 |
| `NOTIFY-SETTINGS-001` | Grouped member category notification controls + youth safeguards | Prompt §4.2 | `DEFERRED` | Post-MVP | Post-MVP |
| `PWA-INSTALL-REMINDER-001` | Non-permanent PWA install reminder cadence | Prompt §4.2 | `DEFERRED` | Post-MVP | Post-MVP |
| `NOTIFY-FINANCE-001` | Treasurer overdue invoice full-settlement notification | Prompt §4.3 | `OUTSTANDING` | Academy MVP | Batch 6 |
| `ACCOUNT-UX-001` | Portal-native My Profile (`/club-os/account/`) replacing broken WP-Admin link | Prompt §4.4 | `OUTSTANDING` | Academy MVP | Batch 6 |
| `PL-021..025` | Actual Player My Season, My Stats, Quick Actions below hero, contrast, Progress *(PO confirmed satisfactory — do not reopen/restyle)* | Roadmap, `001A` §2–3 | `COMPLETE` | Academy MVP | Done |
| `PLAYER-UX-001` (`PL-026/027`) | Actual Player workspace only: `PL-026`/`PL-027` retained pending explicit PO confirm; code audit visual notes reverify-only *(distinct from `PLAYER-PREVIEW-UX-001`)* | Prompt §4.5, Roadmap, `001A` §3 | `IMPLEMENTED — NEEDS VERIFICATION` / `OUTSTANDING` | Academy MVP / Confirm | Batch 6 |
| `PLAYER-PREVIEW-UX-001` | Preview Player Experience visual parity (Regression A: North Star styling) & Exit Preview / Return to Parent navigation (Regression B) — 11 acceptance criteria | `DEVELOPMENT-BACKLOG-001A` §2 | `REGRESSION` *(PO confirmed)* | Academy MVP | Batch 2 |
| `OS-031` | In-app image/attachment viewer (lightbox CSS missing on `/club-os/messages/`) | Prompt §4.5, Roadmap | `PARTIALLY IMPLEMENTED` / `REGRESSION` | Academy MVP | Batch 6 |
| `MSG-BACKLINK-001` | Club Announcements visited backlink & `"Read announcement"` contrast (Parent/Player) | Prompt §4.5, `SCHED-001C` | `PARTIALLY IMPLEMENTED` | Academy MVP | Batch 6 |
| `COACH-MATCH-001A` | Lineup Builder mobile name wrapping, alignment gaps & pitch drag lock | Prompt §5.1 | `PARTIALLY IMPLEMENTED` | Academy MVP | Batch 3 |
| `COACH-MATCH-001B` | Match Mode Live Squad bulk attendance/bench & vacant pitch entry | Prompt §5.1 | `PARTIALLY IMPLEMENTED` | Academy MVP | Batch 3 |
| `COACH-MATCH-001C` | Match Report circular avatars on Saved Lineup & Ratings | Prompt §5.1 | `REGRESSION` | Academy MVP | Batch 3 |
| `EVENTS-EXPERIENCE-001A` | Event hero consolidation (Parent/Player/non-Match/Matchday Hub) & Training Hub terminology | Prompt §5.2 | `PARTIALLY IMPLEMENTED` | Academy MVP | Batch 3 |
| `EVENTS-EXPERIENCE-001B` | Training Session Plan **Reflect** persistence (`COACHING-EXPERIENCE-SLICE-03`) | Prompt §5.2, `a7efc32` | `PARTIALLY IMPLEMENTED` | Academy MVP | Batch 3 |
| `EVENTS-EXPERIENCE-001C` | Recurring event series linkage & future-occurrence audience updates | Prompt §5.2 | `OUTSTANDING` | Academy MVP | Batch 3 |
| `SEC-009` | Secretary Create Event Specific People modal mobile overflow | Roadmap / Release Strategy | `IMPLEMENTED — NEEDS VERIFICATION` | Academy MVP | Batch 3 |
| `PARENT-EXPERIENCE-001A` | Multi-role Secretary Parent Home registration scoping (P0 cross-family data leak) | Prompt §5.3, `001A` §4 | `REGRESSION` | Academy MVP | Batch 1 *(Proposed P0)* |
| `PARENT-EXPERIENCE-001B` | Authorised second Parent/Guardian Back My Game link access | Prompt §5.3 | `PARTIALLY IMPLEMENTED` | Academy MVP | Batch 2 |
| `BMG-001` | Parent Back My Game supporter/pledge status visibility | Roadmap / Release Strategy | `OUTSTANDING` | Academy MVP / Confirm | Batch 2 |
| `WELFARE-POLISH-001` | Welfare People pagination, touching section spacing, mobile polish & `OS-011` | Prompt §5.4, Roadmap | `PARTIALLY IMPLEMENTED` | Academy MVP | Batch 2 |
| `WELFARE-UX-001B` / `SECRETARY-COMPLIANCE-001` | Welfare & Secretary Staff Compliance directories & `PER_PAGE=5` pagination | `07d9943`, `26df8cf` | `COMPLETE` | Academy MVP | Done |
| `FINANCE-UX-001` | View Campaign overflow, Appeal payment methods, Income Breakdown mobile, Shop Finance filters/orders/detail *(Orders Awaiting Payment already fixed in `5b79c5c`)* | Prompt §5.5 | `PARTIALLY IMPLEMENTED` | Academy MVP | Batch 5 |
| `FINANCE-UX-RECENT-HEADING` | Treasurer *Recent Payments* heading change | Prompt §5.5 | `WITHDRAWN` | N/A | Withdrawn |
| `FINANCE-FEES-001` | Training Only Fee Rules & Match Player transition billing | Prompt §5.6 | `OUTSTANDING` | Academy MVP | Batch 5 |
| `FIN-031` | Treasurer static text caret cursor (browser caret browsing) | Roadmap | `IMPLEMENTED — NEEDS VERIFICATION` | Close on PO confirm | Batch 5 |
| `AGE-001` / `AGE-001A` | Manual Adult Verification Policy & People UX polish | `39a4b43`, Handover | `COMPLETE` | Academy MVP | Done |
| `PEOPLE-001` | Youth Player & Guardian Registration during Add Person (no auto-merge) | Prompt §5.7, `AGE-001` handover | `OUTSTANDING` | Academy MVP | Batch 4 |
| `PEOPLE-MERGE-SAFETY-001` | Server-side containment preventing unsafe duplicate merges until Batch 4 repair (not UI-button-only) | `DEVELOPMENT-BACKLOG-001A` §4 | `OUTSTANDING` *(Proposed P0)* | Academy MVP | Batch 1 *(Proposed P0)* |
| `PEOPLE-MERGE-001` | Full duplicate detection & merge repair (7 defects incl. Finance/Welfare table bypass) | Prompt §5.8, `001A` §4 | `REGRESSION` | Academy MVP | Batch 4 |
| `GLOBAL-UX-001` | Cross-workspace contrast, Guardian Links notice, global `:visited`, overflow & PO screenshot sweep | Prompt §5.9 | `PARTIALLY IMPLEMENTED` | Academy MVP | Batch 7 |
| `TEXT-SELECT-001` | Selective UI text/image selection restrictions | Prompt §5.9 | `DEFERRED` | Post-MVP | Post-MVP |
| `MVP-FEEDBACK-001` | In-app Issues, Fixes & Suggestions + admin inbox | Prompt §5.10 | `OUTSTANDING` | Academy MVP | Batch 7 |
| `COM-002` | Committee data minimisation (Welfare/debtor/medical exclusion) | `SPRINTS.md`, Roadmap | `IMPLEMENTED — NEEDS VERIFICATION` | Academy MVP | Batch 6 |
| `SHOP-CANCEL-001` | Club Shop member cancellation clarity & Secretary cancellation workflow | `NOTIFY-010A` handover | `OUTSTANDING` | Academy MVP / Confirm | Batch 6 |
| `FIN-MYFINANCE-001` | Minimal `My Finance` for non-Parent adults | `NOTIFY-010A` handover | `OUTSTANDING` | Academy MVP / Confirm | Batch 6 |
| `B4D-04A` | Encrypted backup vault (`IEXEL_RC_VAULT`) end-to-end verification & restore | Release Strategy, `B4D-04A` docs | `OUTSTANDING` | Public Commercial Release | Batch 8 |
| `P2P-01..12` | Pay-to-Play U6–U16 2026/27 policy & workflow contracts | Release Strategy | `BLOCKED` *(awaiting PO inclusion decision)* | Unapproved / Conditional | Batch 8 / Post-MVP |
| `RR-COMMERCIAL-001` | Clean install/upgrade matrix, Apple PWA acceptance, DB-backed runtime, host cron, role guides, validator cleanup, `main` promotion (`M01–M18`) | Prompt §8, `RELEASE_CHECKLIST.md`, Release Strategy | `OUTSTANDING` / `BLOCKED` *(local MySQL stopped)* | Public Commercial Release | Batch 8 |
| Post-MVP Items (§7) | Weather, Rewards/XP, Team Health, Advanced Welfare/Compliance/Finance/Comms, `SET-002..004`, `ADM-004`, Audit, Placeholder cleanup, Licensing/Theme/Native App/Demo/League OS | Prompt §7, Roadmap, Master Guide | `DEFERRED` | Post-MVP | Post-MVP |

---

## 12. Backlog Maintenance Rules

1. **Update after every accepted batch (mandatory record fields):** Every accepted future development batch must record all of the following immediately upon closeout:
   - Requirement references covered.
   - Updated implementation status.
   - Automated validation evidence.
   - Academy manual acceptance evidence.
   - Confirmed commit SHA and push status.
   - Remaining limitations or follow-up requirements.
   - Any newly discovered regressions.
   - Explicit Product Owner decisions and deferrals.
2. **Preserve original requirement references:** Never rename, delete, or orphan original roadmap/handover IDs (`OS-*`, `NOTIFY-*`, `WELFARE-*`, `PL-*`, `SEC-*`, `FIN-*`, `PEOPLE-*`, `AGE-*`, `B4D-*`, `P2P-*`).
3. **Never silently remove, reopen, or duplicate completed work:** Accepted completed items (`COMPLETE`) remain protected against unnecessary redevelopment; unresolved commitments remain active until `COMPLETE` (with acceptance evidence), explicitly `DEFERRED` by the Product Owner, or explicitly `WITHDRAWN` by the Product Owner.
4. **Keep deferred requirements visible:** Section 7 (Post-MVP) and Section 8 (Public Commercial Release) remain permanently tracked; never promote deferred items into MVP scope without explicit Product Owner approval.
5. **Supplement, do not replace:** New Product Owner requirements supplement previously agreed commitments unless the Product Owner explicitly changes or withdraws prior scope.
6. **Separate implementation from acceptance:** Never mark a requirement `COMPLETE` solely on automated validators or code inspection — use `IMPLEMENTED — NEEDS VERIFICATION` until Product Owner / live acceptance evidence is confirmed.
7. **Maintain standing release safeguards:** Retain the notification persistence verification check after every Academy plugin replacement and preserve all security, safeguarding, privacy, and financial integrity release gates.
