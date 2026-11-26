# Development Handover — Accelerated Batch 1 Closeout (`2026-11-26`)

> **Batch:** `ACCELERATED-BATCH-001` — Staff Compliance Notifications & Critical Safety Corrections
> **Status:** Accepted by Product Owner for Academy MVP Testing; Application Committed & Pushed
> **Date:** 2026-11-26
> **Authoritative Register:** `development/CLUB_OS_DEVELOPMENT_BACKLOG.md`

---

## 1. Confirmed Repository Checkpoints

### Application Repository
- **Worktree:** `c:\Users\leavi\Local Sites\iexel-club-os-dev\worktrees\notify001b2-ordinary-events`
- **Branch:** `feature/notify004a-adult-web-push`
- **Confirmed HEAD:** `3cbe92de0662c59a7ce10d307006f93ab2b911a5` (`feat: complete compliance reminders and MVP identity safeguards`)
- **Upstream Sync:** `0` ahead / `0` behind `origin/feature/notify004a-adult-web-push`
- **Staged Files:** `0`
- **Committed Scope:** Exact `27` accepted Batch 1 files (`4,934` insertions, `33` deletions), resolving all `11` previously pending `NOTIFY-COMPLIANCE-001` files.
- **Remaining Uncommitted Working Tree:** Only the `3` protected `NOTIFY-004B` diagnostic files (unchanged, unstaged).

### Documentation Repository
- **Repository:** `c:\Users\leavi\Local Sites\iexel-club-os-dev\app\public\wp-content\plugins\iexel-club-os-docs`
- **Branch:** `docs/registration-package-step-validation`
- **Prior HEAD:** `72ddaf4c191c33dc90d998064b1b1a0fc7c709aa` (updated by Batch 1 closeout commit covering ONLY `development/CLUB_OS_DEVELOPMENT_BACKLOG.md` and this handover)
- **Remaining Uncommitted Working Tree:** Only the `8` pre-existing unrelated documentation files (unchanged, unstaged).

---

## 2. Batch 1 Acceptance & Release Evidence

- **Delivered Requirements:**
  1. `NOTIFY-COMPLIANCE-001-FIX` — Officer Staff Compliance expiry reminders (`welfare_officer` canonical role fix, per-recipient durable expiry-lifecycle deduplication, atomic lease/heartbeat lock, WP-CLI `ScheduledTaskRunner` registration, permanent read-only browser preview).
  2. `WELFARE-NOTIFY-002` — Personal staff credential expiry reminders (separate default-OFF toggle, privacy-safe push routing to `/club-os/account/qualifications-compliance/`).
  3. `WELFARE-TEST-001` — Combined Staff Compliance notification validation and Academy acceptance.
  4. `PARENT-EXPERIENCE-001A` — P0 Parent Home multi-role active-persona registration scoping fix.
  5. `PEOPLE-MERGE-SAFETY-001` — P0 fail-closed server-side duplicate merge containment at `PersonMergeExecutor` & `PortalRouter` boundaries.
- **Accepted Academy Package (`r4`):**
  - **File:** `C:\Users\leavi\Local Sites\iexel-club-os-dev\worktrees\accelerated-batch-001-evidence\iexel-club-os-ACCELERATED-BATCH-001-r4-academy.zip`
  - **Size:** `7,327,306` bytes (`2,115` runtime files; `1,995` PHP files)
  - **SHA-256:** `1FA7D6A2F4285CBC693229A345204E133155A2964C90352316BEFDE54003CE67`
- **Automated Verification:**
  - `137/137` focused Batch 1 assertions passed (`validate-notify-compliance-001.php` `63/63`, `validate-welfare-notify-002.php` `33/33`, `validate-parent-experience-001a.php` `21/21`, `validate-people-merge-safety-001.php` `12/12`, `validate-compliance-preview-ui.php` `8/8`).
  - `validate-notify-update-persistence.php` (`12/12`), `validate-sched001b-cli-runner.php` (`18/18`), `14` regression suites, `9/9` PHP packaging integrity checks, `node --check assets/pwa/service-worker.js`, and `5/5` responsive Chrome viewports (`320px`, `360px`, `390px`, `412px`, `1280px`) passed.

---

## 3. Deferred Verifications & Known Acceptance Exceptions

The following **7 items remain explicitly open/unconfirmed** and must **never** be described as completed:

1. **Personal notification tap-through remains inconclusive** (Product Owner internet interruption during Academy test) — verify during subsequent Academy testing.
2. **Officer repeat-run manual deduplication was not explicitly confirmed** on Academy (automated deduplication & durable expiry-lifecycle pruning coverage passed).
3. **Temporary merge restriction notice was not observed** during manual Academy acceptance (server-side containment remains mandatory and enforced).
4. **Actual MySQL database concurrency validation remains outstanding** (local LocalWP MySQL service offline).
5. **Full duplicate merge execution repair (`PEOPLE-MERGE-001`) is deferred until after Academy MVP** — required before unrestricted commercial rollout.
6. **Restoration of both automatic compliance settings to OFF on Academy was requested but not explicitly confirmed** — do not claim completed.
7. **Temporary Welfare role configuration on Test Parent was used for acceptance** — do not silently alter Academy test account roles.

---

## 4. Protected Working-Tree Inventory (Must Remain Byte-Identical & Unstaged)

### Application Repository (`3` Protected `NOTIFY-004B` Diagnostic Files)
- `app/core/Events/EventNotificationVisibility.php` — `0F082C179222EF82D0573693B2630170D76A0F65B86AA1B70B9B6EB0C19E6896`
- `tools/validate-notify004b-tap-diagnostic.php` — `69AD1E94B6E288E3C65D46815C5CFCAF7FB23C47CADBBF771AB21D84CF4BC61D`
- `tools/validate-notify004b-tap-diagnostic-browser.cjs` — `CE69C929C27BF9DC976FBD629B9F8DD562675FB1D516BF9143C588882A0F3EEE`

### Documentation Repository (`8` Pre-Existing Uncommitted Files)
- `SPRINTS.md` — `30C33C61901C3EF48F6E0C253C17FA2F9411BD6300E86233C2A4105EB3B7DDFD`
- `development/CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` — `ACC228C549EF3015719D36B16571C07FFBC8CFF99D79770DF12631B7AFDD01EE`
- `development/CLUB_OS_MVP_TO_PRODUCTION_RELEASE_STRATEGY.md` — `71A1D174A717B01D1724A2755BCC82517C30657A4F1E6ACB1564ACDABB1CC7FF`
- `development/DEVELOPMENT_HANDOVER_2026-09-30.md` — `848DC8BBB3ACF4CBEF1B247C04FDB3B0CD7941559A89FE6FD8ABBE15CF0DEECA`
- `development/MASTER_DEVELOPER_GUIDE.md` — `1FFFE9A99101D4E31139B63D9B05E5D5A7CE47095324149BD874AEB807C79DE3`
- `development/RELEASE_CHECKLIST.md` — `5A2A14BEF859BD3E5317902562C168BCDD057C71BAEBA429F4B434A428BAAB46`
- `development/ACADEMY_PASSWORD_RESET_EMAIL_TESTING.md` — `32A816AE695AF8D1DFDF3A12021602A47654FBB5023FC9DB35F2A9A1EF2E32FF`
- `development/ACADEMY_REGISTRATION_PACKAGE_PROGRESSION_REPAIR_2026-10-22.md` — `B19E5997A3E688102CBAC9CF457ED8BEB7250B605F784456653E081A61B4BB94`

---

## 5. Product Owner Decisions Recorded (`2026-11-26`)

1. **`PEOPLE-DUPLICATE-PREVENTION-001`:** Defer full duplicate merge repair (`PEOPLE-MERGE-001`) until after Academy MVP (retaining active server-side containment `PEOPLE-MERGE-SAFETY-001`, duplicate detection, and safe review). Batch 4 audits and completes duplicate prevention across all canonical Person creation paths (youth registration, Guardian matching/reuse, sibling registration, staff creation, Secretary Add Person, account linking, imports); never auto-merge on shared contact details. Full merge repair + integrity validation remains required before unrestricted commercial rollout.
2. **`NOTIFY-SETTINGS-001` (Admin Rationalisation):** Include WordPress Notification Controls rationalisation in **Batch 6** — audit historical pilot controls, diagnostic utilities, obsolete experimental interfaces, and dependencies before removing anything; retain working settings, emergency pause, delivery diagnostics, safe testing, compliance preview, and safeguarding controls. (Member-facing grouped category preferences remain deferred to Post-MVP.)
3. **`DEPLOY-ENV-001`:** Conduct a read-only hosting environment inventory (Academy doc-root + hosting-home additions, scheduler, private storage, keys, config dependencies, historical diagnostics) classifying items as `required`/`automatable`/`historical`/`obsolete`/`unverified` for `iexelfc.co.uk`. Account for cPanel File Manager access with **no Terminal access**. Complete production installation docs before production deployment. Never delete files or expose secrets.
4. **`PRODUCT-PRINCIPLE-001`:** Binding product and engineering principle — **Minimal Administration. Maximum Engagement.** Applies across installation, configuration, club administration, and member experiences; retains explicit human oversight for safeguarding, identity, permissions, and finance; convenience never compromises security, privacy, integrity, or reliability. Exact proposed `MASTER_DEVELOPER_GUIDE.md` Engineering Rules insertion is recorded in `CLUB_OS_DEVELOPMENT_BACKLOG.md` §6.2 (without modifying the protected guide file).
5. **`SETUP-UX-001`:** Future audit and development workstream for guided installation/setup (reusing clean-install, DB-upgrade, System Status, and Release Readiness; environment checks, branding, initial season/team/membership config, essential services, readiness guidance; minimise manual SQL/PHP/WP-CLI/File Manager dependence; audit existing foundations first).

---

## 6. Accelerated Development Delivery Rules

- Operate autonomously within agreed batch scope; escalate only for material discrepancies, unexpected repository changes, security/safeguarding concerns, genuine unresolved product decisions, or failed essential validation.
- Deliver coherent batches as one validated Academy deployment ZIP with one concise acceptance checklist (always checking Web Push notification persistence after plugin ZIP replacement).
- Never claim interrupted, unconfirmed, or environment-blocked checks as completed.
- Preserve all protected working-tree files byte-for-byte unless explicitly authorised.

---

## 7. Next Active Implementation Batch: Accelerated Batch 2 — Parent & Welfare

- **Scope:**
  - `PARENT-EXPERIENCE-001B` — Second authorised Parent/Guardian Back My Game link access & safe link handling.
  - `PLAYER-PREVIEW-UX-001` — Preview Player Experience North Star visual parity (Regression A) & dedicated Exit Preview / Return to Parent View control (Regression B), meeting all 11 acceptance criteria while leaving the accepted actual Player workspace (`PL-021..025`) untouched.
  - `WELFARE-POLISH-001` — Welfare People pagination, touching `.iexel-experience-section` spacing, mobile/tablet polish & `OS-011` Concern Detail hierarchy.
  - Optional `BMG-001` (conditional on Decision D2).
- **Genuine Unresolved PO Decisions Before Starting Batch 2:**
  - **D1:** Back My Game multi-guardian link model (shared retrievable household link vs independent per-guardian links) and explicit "Adult verification required" notice for `AGE_UNKNOWN` 2nd Guardians.
  - **D2:** `BMG-001` supporter/pledge summary inclusion in Academy MVP vs deferral to Post-MVP.
- **Boundary:** Do **not** begin Batch 2 implementation until authorised.

---

## 8. Outstanding Documentation Reconciliation

- Insert the recorded `PRODUCT-PRINCIPLE-001` block (`CLUB_OS_DEVELOPMENT_BACKLOG.md` §6.2) into `development/MASTER_DEVELOPER_GUIDE.md` Engineering Rules once reconciliation of the `8` pre-existing uncommitted files in `iexel-club-os-docs` is explicitly authorised.
- Reconcile historical lag in `SPRINTS.md`, `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`, `RELEASE_CHECKLIST.md`, and `TECHNICAL_DEBT_REGISTER.md` during dedicated documentation housekeeping.
