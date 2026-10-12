# IEXEL Club OS — Development Handover

**Date:** 2026-09-30
**Status:** Prospect Trial Period COMPLETE / ACCEPTED / COMMITTED ON PLUGIN MAIN; documentation reconciliation awaiting review

## 1. Current Development Position

The branded public Come and Try enquiry and Prospect Trial Period are complete and Product Owner accepted. The implementation was committed and pushed as `e5426be1741e207cdc3ac56f86cf1fbaa55a49c3` — `feat: add prospect trial period workflow`. Registration Packages, RP-B/RP-C, post-registration Package arrangements, Parent draft hardening, Guided Registration Conflict Resolution and Legacy Staff Registration Recovery remain complete. This handover supersedes older handovers' current-position and next-task recommendations; their historical acceptance evidence remains valid. Read `MASTER_DEVELOPER_GUIDE.md` for canonical rules, `../SPRINTS.md` for delivery evidence and `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` for remaining work.

## 2. Repository State at This Checkpoint

- Plugin `main`: HEAD and `origin/main` `e5426be1741e207cdc3ac56f86cf1fbaa55a49c3`; ahead/behind `0/0`; clean, nothing staged.
- Protected plugin stash: `stash@{0}: On global-navigation-system: Commit composer: 7/10/2026, 1:04:53 PM`, SHA `ed95f294a6ccccfbb48425903118abcc48d2a9ec`. Do not apply, pop, drop, clear or modify it.
- Docs `main`: HEAD and `origin/main` `b5255a1e7448c44fc2dd7f4e8be158d8fceaf960`; ahead/behind `0/0` at the start of this reconciliation. The three authoritative docs are being edited and this dated handover is new, all unstaged; no docs commit or push is authorized yet.
- Protected unrelated docs modification: `development/RELEASE_CHECKLIST.md`, modified and unstaged. SHA-256 `0B7EE2861A0605588F2DB55101DCBE91829C1C4E62167D5A1DD581CB85A501C5`; keep it outside the documentation checkpoint.

## 3. Completed Prospect Trial Period

The public Come and Try route presents a branded introductory enquiry and records explicit Prospect-level trial participation consent and, for youth, responsible-adult authority. Secretary can deliberately confirm evidence and current safety for historical enquiries, schedule independent dated sessions and set a review date. Assigned-Team Coach/Manager access is narrow: only active, ready Trialists for the exact Team, relevant bounded safety information, attendance outcomes and brief operational notes. The notes use the shared auto-grow control and a 500-character limit. Session and outcome history remains attached to the Prospect, distinct from canonical Event attendance.

`ProspectTrialService` enforces participation and permission rules; `ProspectTrialSessionRepository` stores the repeated visits. Schema version `2026.09.4` registers the new table and nullable evidence in clean-install SQL, upgrade steps and release inventories, without fabricating old consent or visit history. Trial participation itself creates no canonical Person, guardian relationship, Team Assignment, Registration, Finance record or fixture eligibility. Deliberate Prospect conversion uses the established TrainingMembership service, recommends the DOB/Season natural football age group and offers one-year-up only where eligible. Conversion preserves Prospect trial history and does not treat trial permission as unrestricted ongoing consent. Training Only remains separate from competitive Match Player eligibility.

## 4. Accepted Evidence and Verification Limits

Public youth enquiry/safeguarding, two distinct trial sessions with attended and did-not-attend outcomes, Secretary and Coach desktop/mobile workflows, operational-note auto-grow, Training Membership age-group recommendation and deliberate Training Only conversion passed Product Owner acceptance. A separate read-only conversion-integrity audit found one appropriate canonical Player, one Parent relationship, one active 2026/27 U7 Training Membership, preserved Prospect sessions and no unintended competitive, Finance or canonical Event attendance records. Disposable names and IDs are omitted here.

Final read-only regression: nine database-free validators passed **760 assertions**; PHP lint passed for all 21 changed PHP files; JavaScript syntax and `git diff --check` passed. Source integration, local installed schema and release inventories passed inspection. An independent fresh-install and upgrade execution was not performed in that final read-only audit.

Two unchanged tooling limitations are **not Trialist regressions**: `validate-training-membership-management.php` has an outdated source-literal assertion that excludes Training Membership candidates from Event audience options, although the previously committed Event Builder intentionally admits eligible Training Only Players to appropriate non-fixture audiences. The OS-wide auto-grow validator has a UTF-8 BOM parsing failure and requires explicit WordPress/database bootstrap; it was not run. Trialist note controls reuse the existing utility and passed browser acceptance. Do not silently report either validator as passing or repair them as part of this documentation task.

## 5. Remaining Work and Recommended Next Action

**Select the next approved MVP task after this documentation reconciliation; do not infer an implementation mandate from the backlog.** The direct Prospect-to-competitive Match Registration invitation (`ProspectLifecycle::INVITED_MATCH_REGISTRATION`) remains an open operational seam. Integration of Prospect trial visits with existing Team training sessions remains deferred; no canonical Event attendance bridge was delivered. Multi-club public-page branding remains future work. Preserve OS-011 Welfare Concern Detail hierarchy polish, validator/fixture hygiene, Internal Club Testing preparation, general Package amendments/upgrades, Person 176 orphaned assignment cleanup, `iexel-fee-rule-back` naming debt and the Premium Surface Colour Consistency Audit as previously documented candidates or deferred work; none is promoted here.

Release/deployment is a separate checklist gate. The earlier MVP Release Candidate and Registration integrity work remain accepted. Finance Reports is an intentionally removed unfinished scaffold requiring fresh product definition. Approved Fundraising architecture remains future phased work. Do not start a new development batch or alter protected Registration/Person/Finance reference data during this documentation checkpoint.

## 6. Private Encrypted Backup Vault Checkpoint (B4C.4–B4C.6)

A dedicated private encrypted backup vault has been provisioned and verified outside the Club OS repository to support upcoming release candidate backup and disaster-recovery workflows.

- **Vault Provisioning:** A dedicated 20 GiB virtual disk was initialized with GPT partitioning and formatted with an NTFS filesystem under the label `IEXEL_RC_VAULT`. The container is configured without persistent drive letters or automatic mounting.
- **Security & Encryption:** The volume underwent full-volume encryption using XTS-AES 256. Dual key protectors were established: a primary password protector and a secondary numerical recovery-password protector. Automatic unlocking is disabled, and recovery material is stored securely outside the vault.
- **Operational Verification:** The vault was independently verified, locked, and successfully unlocked using the primary password. Windows subsequently confirmed clean detachment (`Attached = False`), returning the container to an encrypted rest state.
- **Evidence & Scope Boundary:** The private backup vault is maintained strictly outside the Club OS repository and deployment environments. The container provisioning, encryption, and password-based unlock verification milestones (B4C.4–B4C.6) are complete. The final locked state immediately prior to detachment was not independently captured in shared output, and end-to-end backup and restore validation (populating, verifying, and restoring a complete site and database payload) has not yet been executed and remains an outstanding milestone. The vault is therefore not yet designated as an operational disaster-recovery solution.

## 7. Delivery Baseline Reconciliation (29 Commits Between 30 September and 9 October 2026; Commit 1342540 / Schema 2026.10.20)

Between 30 September 2026 (`e5426be1741e207cdc3ac56f86cf1fbaa55a49c3`) and 9 October 2026 (`134254095a9e8332d0bff4523b7275829c9a9873`), 29 plugin commits were implemented, tested, and integrated into plugin `main`, advancing the database schema version to `2026.10.20`. This section bridges the authoritative documentation to the actual delivered codebase baseline.

### 7.1 Reconciled Implementation Arcs

1. **Fundraising Domain (Phases F1-F5; Commits `745f8d4` to `6d6c457`; Schema `2026.10.01` to `2026.10.10`):**
   - **Team Appeals & Supporter Journey (F1):** Public appeal campaign pages (`/club-os/fundraising/appeals/{slug}/`), target meter, Gift Aid capture, team attribution, and direct donation checkout.
   - **Spot the Ball Flagship Competition (F2-F4):** Competition lifecycle management, adult panel coordinate sealing, normalized coordinate selection canvas (0.000000 to 1.000000), multi-entry cart, panel coordinate unsealing, Euclidean distance calculation, unique-winning-person tie breaking, and prize settlement bridge.
   - **Back My Game Supporter Subscriptions (F5):** Recurring micro-sponsorship and pledge agreements for teams and players, automated monthly collection schedule generator, payment attempt tracking, and Treasurer oversight.
   - **Domain Invariants:** Complete financial isolation via `FundraisingFinanceBridgeService` creating payments in `iexel_os_finance_payments` without invoice allocations (no pollution of member registration invoices or billing ledger allocations); strict safeguarding guarantees via `FundraisingShareAttributionPolicy` (youth share links restricted to authenticated canonical adult guardians; zero public child seller profiles or URLs; adult-authorized payments; minor prize routing to verified guardians). Phase F6 (Club Draw lottery) remains deferred future work.

2. **Hosted Online Payments & SumUp Checkout Foundation (Commits `be36f2e`, `f89087a`, `caab932`; Schema `2026.10.11` to `2026.10.13`):**
   - First-class payment gateway architecture integrating SumUp Hosted Checkout API.
   - Zero cardholder data touches Club OS servers (handled entirely on SumUp hosted checkout pages); idempotent session initiation with local reference (`COSPAY-...`).
   - Asynchronous webhook notifications (`/webhooks/sumup`) trigger direct server-to-server verification via `SumUpHostedCheckoutService::verify_checkout()`, validating merchant code, checkout ID, local reference, GBP currency, and exact minor amount.
   - Terminal payment states (`STATUS_SETTLED`, `STATUS_EXCEPTION`) enforce idempotency against replayed notifications, atomically invoking domain settlement services.

3. **Club Shop Domain (Batches 1-4A; Commits `6163554` to `a8c66c5`; Schema `2026.10.14` to `2026.10.19`):**
   - **Batches 1 & 2:** Product catalogue, SKU variants (size/colour), inventory stock tracking, member storefront (`/club-os/shop/`), and multi-item shopping cart.
   - **Batch 3:** Multi-item checkout supporting dual payment rails: SumUp hosted card checkout and offline Bank Transfer instructions.
   - **Batches 3A & 3B:** Post-upgrade baseline stabilization, admin session security closure, runtime baseline reconciliation, and bank transfer settlement reconciliation.
   - **Batch 4A:** Secretary order fulfillment dashboard (`/club-os/secretary/shop/orders/`), packing slip generation, and collection-oriented fulfillment lifecycle (`ordered` -> `preparing` -> `ready_for_collection` -> `collected`).

4. **Disposable Validator Safety Architecture & Test Isolation (Commit `1342540`):**
   - Framework establishing host, port, database identity, and structure guards (`ValidatorEnvironment::verify_disposable_target()`) to guarantee diagnostic tools cannot execute against production or non-disposable environments.

5. **AdminUI Route Inventory Parity (Commit `1342540`; Schema `2026.10.20`):**
   - Full audit and alignment of all 56 registered WordPress admin routes in `ReleaseRouteInventory::administrator()` with `AdminUI.php`, resolving orphaned and untracked menu slugs.

### 7.2 Acceptance Evidence Classification

The implementation and verification status across the 29 commits is classified according to established evidence standards:

- **Fundraising Appeals (F1):**
  - Public appeal supporter journey and donation checkout: **Implemented and merged; Automated validation passed (`tools/validate-fundraising-appeal.php`); Product Owner-reported walkthrough.**
  - Specific edge subflows without dedicated logs: **Acceptance evidence not located.**
- **Spot the Ball (F2-F4):**
  - Competition creation, interactive coordinate selection canvas, adult panel sealing, Euclidean distance calculation, unique-person tie-breaking: **Implemented and merged; Automated validation passed (`tools/validate-spot-the-ball-domain.php`, `tools/validate-spot-the-ball-adjudication.php`); Product Owner-reported walkthrough.**
  - Minor prize settlement execution: **Implemented and merged; Automated validation passed; Acceptance evidence not located.**
- **Back My Game (F5):**
  - Supporter agreements, recurring collection scheduling, payment request engine, Treasurer dashboard: **Implemented and merged; Automated validation passed (`tools/validate-treasurer-back-my-game-domain.php`); Product Owner-reported walkthrough.**
  - Automated monthly close cron execution: **Implemented and merged; Automated validation passed; Acceptance evidence not located.**
- **Hosted Online Payments & SumUp Checkout:**
  - Hosted checkout initiation, redirection, out-of-band verification, and webhook handling: **Implemented and merged; Automated validation passed (`tools/validate-sumup-hosted-checkout-foundation.php`, `tools/validate-online-payment-attempt-foundation.php`); Product Owner-reported walkthrough.**
- **Club Shop (Batches 1-3B):**
  - Merchandise catalog, SKU variants, cart, SumUp checkout, offline Bank Transfer instructions: **Implemented and merged; Documented manual acceptance.** Formal acceptance recorded in untracked Batch 3B reports (Order `ORD-000070` paid via Bank Transfer, receipt `PAY-012619`, stock decremented, and Treasurer reconciliation verified).
- **Club Shop Fulfilment (Batch 4A):**
  - Secretary order fulfillment dashboard, packing slips, collection status transitions: **Implemented and merged; Automated validation passed (`tools/validate-club-shop-batch-4a.php --database-free`, 130 assertions PASS); Documented manual browser acceptance artifact not located.**
- **Disposable Validator Safety Architecture:**
  - Guard framework and test isolation: **Implemented and merged; Automated validation passed (`tools/validate-validator-disposable-safety.php`, 368 assertions PASS).**
- **AdminUI Route Inventory Parity:**
  - Alignment of all 56 registered admin routes: **Implemented and merged; Automated validation passed (`tools/validate-admin-inventory-parity.php`, 56/56 routes PASS).**

### 7.3 Mobile Experience & WordPress Admin UX Walkthrough Closure

The Product Owner mobile and WordPress Admin walkthroughs have concluded across all eight workspaces. The review status is no longer "screenshots forthcoming" but is formally recorded as **UX walkthrough complete / provisionally accepted** across all eight surfaces, with five Mobile UX batches delivered on `main` (`28264dc` through `bf6df68`), MOB-008A implementation complete in the plugin working tree, and outstanding findings classified into Tier A/B/C/D for final MVP completion. See Section 8 for the full reconciliation.

### 7.4 Preserved Operational Boundaries & Repository Status

- **Private Encrypted Backup Vault:** The 20 GiB XTS-AES 256 vault (`IEXEL_RC_VAULT`, B4C.4–B4C.6) is detached and encrypted at rest outside the repository. End-to-end backup and restore validation (B4D payload population, verification, and restore) remains an outstanding milestone before operational DR designation.
- **Registration Discovery Seam:** The direct Prospect-to-competitive Match Registration invitation (`ProspectLifecycle::INVITED_MATCH_REGISTRATION`) remains an open operational seam.
- **Commercial & Architecture Boundaries:** General package amendments/upgrades remain deferred; multi-club branding remains future work; Finance Reports is an intentionally removed unfinished scaffold requiring fresh product definition; Club Draw (F6) remains future compliance-gated work.
- **Untracked Artifacts:** The 21 untracked historical plugin files remain strictly preserved, unmodified, and unstaged.
- **Protected Stashes:** Protected plugin stash `stash@{0}` remains preserved.
- **Plugin Repository State:** `c:\Users\leavi\Local Sites\iexel-club-os-dev\app\public\wp-content\plugins\iexel-club-os` is on branch `main` at commit `cdd9054efe7394297b4047f1cd59ba1335266d52` (YTH-001 committed and pushed; working tree clean for tracked files; 21 historical untracked files and `stash@{0}` intact).

---

## 8. MVP Mobile & WordPress Admin UX Walkthrough Reconciliation, Findings Register & Completion Plan

- **Date:** 2026-10-12
- **Plugin Baseline:** `cdd9054efe7394297b4047f1cd59ba1335266d52` on `main`, schema `2026.10.20` (YTH-001 committed and pushed to `origin/main`)
- **Docs Baseline:** `718b91374f778ee69edc9fac9abf595509e850e1` on `main`
- **Status:** UX Walkthroughs Complete / Provisionally Accepted across all 8 Workspaces; Authoritative MVP Completion Plan Established

### 8.1 Delivered Mobile UX Arc & Working Tree State

Between 9 October and 12 October 2026, seven Mobile and Safeguarding UX implementation batches were developed, validated, and integrated into plugin `main`:
1. **Batch 1 (`28264dc`):** MOB-005 — Coach lineup builder draft persistence and coach player access.
2. **Batch 2 (`bc5ab91`):** MOB-006 / MOB-007 — Coach lineup builder bulk attendance reliability and match status synchronization.
3. **Batch 3 (`4e259f9`):** MOB-009 / MOB-010 / MOB-011 — Football fixture card presentation unification across Parent and Coach hubs using `FixtureCardMatchup`, with responsive team-boundary heading wrapping.
4. **Batch 4 (`fa72493`):** MOB-008 — Parent Team Hub inline per-child RSVP controls and scroll position preservation via URL fragment targeting.
5. **Batch 5 (`bf6df68`):** MOB-001 — Parent invoice currency encoding repair (£ symbol correction).
6. **Batch 6 / MOB-008A & PRN-002 (`75c14aa`):** Parent Event Detail RSVP return navigation and Parent Priority Alerts 7-day rolling window & chronological ordering.
7. **Batch 7 / YTH-001 (`cdd9054`):** Club Shop Youth Purchasing Safeguarding — adult purchaser verification (`KNOWN_ADULT`), fail-closed policy, online checkout and bank transfer prevention, safe browse-only UI with safeguarding notice card.

**Committed and Pushed to Main (YTH-001, Commit `cdd9054`):**
- *YTH-001 (Club Shop Youth Purchasing Safeguarding):* Enforces strict adult purchasing controls in Club Shop. Prevents minor players (<18) and unverified-age users from placing orders, initiating SumUp online checkout, or selecting bank transfer across `ShopRequestHandler`, `ShopAccessPolicy`, `ShopService`, `ShopOnlinePaymentService`, and `ShopBankTransferService`. Preserves safe product browsing and size/price selection with an accessible safeguarding note card. Suppresses unpaid order reminders for youth members. Preserves adult player self-purchases and adult parent purchases for authorised children.
  - *Files:* 8 modified domain/UI files (`ShopAccessPolicy.php`, `ShopService.php`, `ShopOnlinePaymentService.php`, `ShopBankTransferService.php`, `PortalShopPage.php`, `PortalShopProductPage.php`, `ShopOrderPaymentPanel.php`, `ShopRequestHandler.php`), 1 updated test file (`tools/validate-club-shop-batch-4a-unit.php`), and 1 new validator (`tools/validate-club-shop-youth-safeguarding.php`, 61 assertions PASS).
  - *Validation & Git Status:* All automated test suites passed (61/61 on youth safeguarding, 130/130 on Batch 4A database-free, 41/41 on fundraising share links; PHP lint clean; `git diff --check` clean). Staged exactly 10 files and committed as `cdd9054efe7394297b4047f1cd59ba1335266d52`, pushed to `origin/main`. Working tree clean for tracked files; 21 untracked historical files and `stash@{0}` preserved.
  - *Audit Confirmations:* YTH-002 (Spot the Ball guardian authorization and prize routing) and YTH-003 (Youth fundraising appeal attribution via `FundraisingShareAttributionPolicy`) verified as existing safeguards by code audit, not newly implemented features.
  - *Manual Test Limitation:* Available youth Player persona in the local environment had no historical orders, so historical youth-order visibility in "My Orders" was not manually exercised in the browser (covered by automated test assertions).

**Committed and Pushed to Main (MOB-008A & PRN-002, Commit `75c14aa`):**
- *MOB-008A (Parent Event Detail RSVP Return Navigation):* Resolves incorrect redirection to Team Hub → Events when an RSVP is submitted from the standalone Event Detail view (`/club-os/parent/events/{id}/`), returning the user to the same event card.
  - *Files:* 4 modified files (`MemberPortalService.php`, `EventResponseActionsCard.php`, `PortalEventDetailPage.php`, `assets/css/public.css`) and 1 new validator (`tools/validate-parent-event-detail-rsvp-return.php`, 52 assertions PASS).
- *PRN-002 (Parent Priority Alerts RSVP Window):* Limits unanswered event RSVP action requests in the Parent / Guardian Priority Alerts feed to a rolling seven-day window (club timezone) and sorts them in ascending chronological order so imminent fixtures appear first.
  - *Files:* 2 modified files (`WorkspacePriorityAlertService.php`, `MemberExperienceService.php`) and 1 new validator (`tools/validate-parent-priority-alerts-rsvp-window.php`, 33 assertions PASS).
- *Validation & Git Status:* All automated test suites passed (52/52 on Event Detail RSVP return, 33/33 on Priority Alerts window, 138/138 on Priority Alert scoping, 68/68 on inline RSVP; PHP lint clean; `git diff --check` clean). Staged exactly 8 files and committed as `75c14aa9cb9d9b7d31c85aefd2a9778e02dd99e4`, pushed to `origin/main`. Working tree clean for tracked files; 21 untracked historical files and `stash@{0}` preserved.

### 8.2 Workspace Review Walkthrough Closure

The Product Owner completed walkthroughs across all eight operational surfaces. Each is recorded as **UX walkthrough complete / provisionally accepted**:
1. **Parent / Guardian:** Family hub, registrations, and finance validated. MOB-001 (£ currency), MOB-008 (inline RSVP), MOB-008A (return navigation), and PRN-002 (priority alerts 7-day RSVP window) accepted, committed, and pushed. Open items: PRN-001 (Parent RSVP button copy distinction) remains outstanding, and Back My Game visibility.
2. **Secretary:** Command Centre, People, Teams, Registrations, Venues, and Shop Fulfilment validated. Open items: Create Event selector modal mobile overflow (SEC-009) and operational settings separation (SET-001).
3. **Treasurer:** Billing, invoicing, payment allocations, fee rules, and Back My Game oversight validated. Open item: static caret browser artifact (FIN-031) awaiting PO confirmation to close.
4. **Committee:** Club overview, projects, and communications validated. Open items: data minimisation boundaries (excluding confidential welfare, individual invoices, and medical records) and club-wide communications approval gate.
5. **Coach / Manager:** Matchday Hub, lineup builder, match mode, completed match corrections, and training attendance validated. MOB-005–007 and MOB-009–011 accepted. Open items: upcoming event bulk responses and squad availability polish.
6. **Player:** Player Hub, Matchday journey, My Stats, and My Progress validated. Open items: youth commercial safeguarding invariants; My Stats breakdown and My Progress deep links open for polish.
7. **Welfare:** Safeguarding dashboard, concern lifecycle, welfare updates, and staff compliance validated. Open item: OS-011 Concern Detail card visual hierarchy polish.
8. **WordPress Admin:** Route parity and consolidation validated. Open items: SET-001 operational settings separation, `/wp-admin/` blank Fundraising route cleanup, and permanent technical support/recovery access retention invariant.

### 8.3 Reconciled Findings Register by Delivery Classification

#### Tier A — Release-Critical (Security, Safeguarding, Essential Workflows, Release Controls)
- **YTH-001 (Club Shop Youth Checkout):** Minor players (<18) and unverified-age users must not execute direct hosted credit/debit card checkout, bank transfer, or order creation without adult guardian authentication. (Resolved, verified 61/61 assertions PASS, committed and pushed as `cdd9054`). (Note: Local youth Player persona had no past orders, so historical youth-order visibility in My Orders was verified via automated test suite rather than manual browser walkthrough).
- **YTH-002 (Spot the Ball Minor Safeguarding):** Youth entry requires adult guardian authorization; minor prize settlements route strictly to verified adult guardians. (Existing safeguard verified by code audit).
- **YTH-003 (Youth Fundraising Attribution):** Public appeal sharing links attributing youth players require adult guardian issuance (`FundraisingShareAttributionPolicy`); zero public child seller profiles or URLs. (Existing safeguard verified by code audit).
- **COM-002 (Committee Data Minimisation):** General Committee views must strictly exclude confidential Welfare safeguarding notes, individual debtor ledgers / itemised family invoices, and registration medical records.
- **B4D (Private Encrypted Backup Vault):** Complete end-to-end payload population, verification, and restore of `IEXEL_RC_VAULT` to validate DR readiness before operational release.
- **MOB-008A (Parent Event Detail RSVP Return):** Ensure Event Detail RSVP submissions return to Event Detail rather than redirecting to Team Hub. (Resolved, verified 52/52 assertions PASS, committed and pushed as `75c14aa`).
- **ADM-006 (WordPress Admin Recovery Access Invariant):** `/wp-admin/` must remain permanently accessible for system administrators, technical support, database upgrades (`UpgradeRunner`), and recovery diagnostics.

#### Tier B — MVP Usability & Operational Improvements
- **SET-001 (Operational Settings Separation):** Separate operational configuration (season dates, age groups, club contacts) from Brand Studio into a dedicated settings tab for MVP.
- **ADM-005 (Fundraising Admin Menu Cleanup):** Investigate blank screen on `/wp-admin/admin.php?page=iexel-club-os-fundraising` and clean up route/menu.
- **SEC-009 (Create Event Selector Mobile Overflow):** Resolve mobile modal horizontal overflow in Create Event "Specific People" selector.
- **PRN-001 (Parent RSVP Wording Distinction):** Differentiate button copy between "Available for [Child]" and "I'm Available". (Remains OPEN).
- **PRN-002 (Parent Priority Alerts RSVP Window):** Unanswered event RSVP action requests are limited to a rolling seven-day window using the club's configured timezone and sorted in ascending chronological order so imminent fixtures appear first; verified with 33 assertions in tools/validate-parent-priority-alerts-rsvp-window.php. (Resolved, verified 33/33 assertions PASS, committed and pushed as `75c14aa`).
- **COM-001 (Committee Comms Approval Gate):** Require administrative sign-off for general committee members broadcasting club-wide messages.
- **CCH-001 (Coach Bulk Upcoming Event Responses):** Rapid bulk availability response tools for upcoming training/events in Coach Hub.
- **BMG-001 (Back My Game Supporter Visibility):** Clear supporter agreement and pledge status in Parent Hub.

#### Tier C — North Star Visual Polish
- **OS-011 (Welfare Concern Detail Hierarchy):** Differentiate Summary, Information, Timeline, and Activity History card weights on Concern Detail.
- **Coach Squad Availability Presentation Polish:** Visual polish for squad availability cards and response badges.
- **PL-026 (Player My Stats Match Breakdown):** Expandable match-by-match breakdown under season aggregates.
- **PL-027 (Player My Progress Match Report Links):** Contextual deep links from appearance milestones into completed Match Reports.
- **FIN-031 (Static Caret Visual Artifact):** Awaiting PO confirmation to formally close as client-side browser caret browsing.

#### Tier D — Post-MVP (Deferred Scope)
- Role-specific onboarding setup wizard and video training library.
- SET-003 / SET-004 modular multi-tier settings architecture (Grassroots, Academy, Semi-Pro, Pro, Custom).
- Full migration of operational CRUD away from WordPress Admin.
- Direct Prospect-to-competitive Match Registration invitation (`ProspectLifecycle::INVITED_MATCH_REGISTRATION`).
- General package amendments / upgrades post-registration.
- Club Draw (F6) statutory lottery engine.
- Notification attachment / image lightbox viewer (OS-031).
- Commercial licensing engine and Club OS Control Centre remote update server.
- Optional standalone club website theme.
- Standalone mobile app shells.
- Public demonstration environment with synthetic data and automated reset.
- Multi-club League OS platform architecture (~5-year horizon).
- FND-001: Campaign-specific family/player and team fundraising appeal attribution tokens with downloadable/scannable QR-code sharing, safeguarding, payment confirmation, refund handling, and avoidance of double-counting.

### 8.4 Operational Onboarding Workstream

Planned workstream for role-specific Club OS how-to guides covering 7 core roles:
- **Roles:** Secretary, Treasurer, Coach / Manager, Welfare Officer, Committee Member, Parent / Guardian, Player.
- **Standards:** Real verified workflows tested step-by-step; synthetic sample test data only; strictly zero member PII, payment data, or safeguarding case details.
- **Execution Boundary:** Guides are planned in this reconciliation; authoring and publication occur in a subsequent authorized batch. Setup wizard and video training library are Post-MVP.

### 8.5 Phased Implementation Sequence

Implementation will proceed in small, controlled, risk-ordered batches:
1. **Batch 1 — MOB-008A & PRN-002 Acceptance Closure, Commit & Push (COMPLETED):**
   - Product Owner accepted both fixes. Staged 8 files across MOB-008A and PRN-002. Automated test suites passed (52/52 on Event Detail RSVP return, 33/33 on Priority Alerts window, 138/138 on Priority Alert scoping, 68/68 on inline RSVP; PHP lint clean; `git diff --check` clean). Committed as `75c14aa9cb9d9b7d31c85aefd2a9778e02dd99e4` and pushed to `origin/main`.
2. **Batch 2 — Youth Safeguarding Purchasing Enforcement (COMPLETED — `cdd9054`):**
   - Enforce Club Shop youth checkout restrictions (block minor direct card payments, require adult guardian — YTH-001; resolved, verified 61/61 assertions PASS, committed and pushed as `cdd9054efe7394297b4047f1cd59ba1335266d52`). Spot the Ball guardian prize bridge (YTH-002) and Fundraising appeal attribution policy (YTH-003) verified as existing safeguards by code audit.
3. **Batch 3 — Committee Data Minimisation & Communications Approval Gate (RECOMMENDED NEXT BATCH):**
   - Filter out confidential welfare notes, individual invoice ledgers, and registration medical records from general Committee views (COM-002); implement approval requirement for club-wide broadcasts (COM-001).
4. **Batch 4 — SET-001 Operational Settings Separation & Admin Cleanup:**
   - Create dedicated operational settings surface for season dates, age groups, and contacts; investigate and clean up `/wp-admin/` blank Fundraising route (ADM-005).
5. **Batch 5 — Mobile Usability & Workflow Polish:**
   - Secretary Create Event Specific People modal mobile overflow fix (SEC-009); Parent RSVP wording differentiation ("Available for [Child]" vs "I'm Available" — PRN-001); Coach upcoming event bulk responses (CCH-001).
6. **Batch 6 — North Star Visual Polish:**
   - OS-011 Welfare Concern Detail visual card hierarchy; Coach squad availability styling; Player My Progress match report deep links (PL-027); Player My Stats breakdown (PL-026).
7. **Release Gate — Private Encrypted Backup Vault (B4D) & Release Checklist:**
   - End-to-end payload population, verification, and restore of `IEXEL_RC_VAULT`; execution of `RELEASE_CHECKLIST.md` release criteria.

### 8.6 Repository States & Safety Invariants

- **Plugin Repository (`iexel-club-os`):** HEAD `cdd9054efe7394297b4047f1cd59ba1335266d52` on `main`, up to date with `origin/main`. Working tree is completely clean for tracked files. The 21 untracked historical audit/patch files and protected `stash@{0}` remain strictly preserved and intact.
- **Docs Repository (`iexel-club-os-docs`):** Active target for documentation updates only. Branch `main` at commit `718b91374f778ee69edc9fac9abf595509e850e1`. No commits or pushes authorized; documentation changes remain unstaged for Product Owner review.

### 8.7 Three-Tier Deployment Pipeline Architecture

To transition safely from local development to production operations, Club OS defines a formal three-tier deployment pipeline:
1. **Tier 1 — Local Development (`iexel-club-os-dev`):**
   - Single-site LocalWP instance running PHP 8.2 and MySQL 8.0.
   - Used for initial implementation, unit/integration testing, automated validator suites, and preliminary browser walkthroughs.
2. **Tier 2 — Pre-Production / Update Rehearsal (`iexel-club-os-rc`):**
   - Clean, isolated environment mirroring production server specifications and runtime constraints.
   - Used to execute end-to-end rehearsal deployments, verify database schema upgrades via `UpgradeRunner`, test real payment gateway credentials, and validate encrypted backup vault creation and restoration procedures (B4D).
3. **Tier 3 — Live Club Operations (IEXEL FC Live):**
   - Production hosting environment running the live IEXEL FC installation.
   - Deployed strictly via release-gated procedures after Tier 2 sign-off, zero direct hot-patching.

### 8.8 Commercial Product Architecture & Package Boundaries

- **Customer vs Product Boundary:** IEXEL FC is independent customer club #1. The commercial entity produces and distributes Club OS as an independent software platform.
- **Core Product:** The self-hosted WordPress plugin (`iexel-club-os`) is the standalone, full-featured Club Operating System. It functions fully with any compliant WordPress theme.
- **Optional Premium Website Theme (Post-MVP):** An optional companion theme providing a public-facing club website and branding integration for grassroots clubs that do not have an existing web presence.
- **Universal Mobile App Access (Post-MVP):** Mobile app access (iOS / Android container shells) is universally included with every Club OS licence at no additional charge.

### 8.9 Post-MVP Commercial Licensing Architecture & Club OS Control Centre

- **Club OS Control Centre:** Centralised administrative platform for licence issuance, tenant telemetry, update distribution, and compliance monitoring.
- **Cryptographic Licence Verification:** Asymmetric key-pair licensing (RSA/ECDSA signed JWTs) validated locally in PHP without requiring continuous per-request phone-home connectivity.
- **Strict Data Minimisation:** The Control Centre never ingests, stores, or processes member personal data, player identities, medical notes, safeguarding cases, or transaction ledgers. Only anonymised licence metadata, active plugin version, and domain verification tokens are exchanged.
- **Restricted Data Access Mode:** If a club licence expires, administrative access to member records and GDPR data exports remains permanently functional in read-only / export mode. Member data is never held hostage.
- **Audited Time-Limited Support Access:** Any remote administrative assistance requires explicit, time-bounded, cryptographic authorization from the club's Data Protection Officer / Club Secretary.
- **Self-Hosted Security Model:** Recognises the practical boundaries of on-premise / self-hosted PHP execution, prioritising defense-in-depth and operational transparency.

### 8.10 Public Demonstration Environment & Long-Term League OS Horizon

- **Public Demonstration Environment (Post-MVP):** An isolated, ephemeral demonstration sandbox running with realistic synthetic demo data, automated hourly/daily resets, and restricted outbound messaging, enabling prospective clubs to experience all eight workspaces interactively.
- **Long-Term League OS Horizon (~5-Year Vision):** Multi-tenant platform architecture designed to coordinate league fixtures, cross-club transfers, referee assignments, disciplinary tracking, and competition tables across all participating member clubs.
