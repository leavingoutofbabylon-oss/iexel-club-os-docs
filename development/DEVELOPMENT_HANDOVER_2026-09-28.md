# IEXEL Club OS — Development Handover

**Date:** 2026-09-28
**Status:** Post-Registration Package Arrangement Workflow Completed and Manually Accepted

## 1. Current Development Position
The Post-Registration Package Arrangement workflow has been fully implemented, automatically validated, manually accepted on desktop and mobile (320px viewports), committed, and pushed to `main` at `4285091daecf24214575a1c06c8ea86f33bdb0e1`.

This workflow provides a dedicated commercial mechanism for the Treasurer to arrange a Registration Package and optional Extra Charges for a player whose registration was completed without selecting a package (`package_id = null`). Crucially, the architecture preserves the immutable historical registration snapshot while establishing a distinct canonical post-registration arrangement domain linked idempotently to Finance.

## 2. Plugin Repository State
- **Branch:** `main`
- **Current HEAD & origin/main:** `4285091daecf24214575a1c06c8ea86f33bdb0e1`
- **Commit Subject:** `feat: add post-registration package arrangement workflow`
- **Preceding Layout Refinement Commit:** `1503291e8155d8fab12b321f0e7214c3caed7532` (`fix: refine arranged registration package detail layout`)
- **Ahead/Behind:** `0/0`
- **Working Tree:** Clean
- **Protected Stash:** Intact (`stash@{0}: On global-navigation-system: Commit composer: 7/10/2026, 1:04:53 PM`)

## 3. Documentation Repository State
- **Branch:** `main`
- **Pre-existing Working Tree Modification:** `development/RELEASE_CHECKLIST.md` (intentionally preserved untouched across documentation checkpoints).

## 4. Architectural Summary: Post-Registration Package Arrangement

### 4.1 Immutable Historical Snapshot Preserved
- The original registration record in `player_registrations` remains an unalterable historical audit record.
- For registrations completed without a package, `player_registrations.package_id` and `player_registrations.package_snapshot` remain strictly `NULL`.
- Under no circumstances does a post-registration arrangement rewrite or overwrite the historical registration fields.

### 4.2 Dedicated Canonical Domain
- Post-registration package arrangements live in their own first-class table: `registration_package_arrangements`.
- Schema features:
  - `id`: Primary key.
  - `registration_id`: Foreign key with `UNIQUE KEY uk_registration_id (registration_id)`.
  - `package_id`: Selected package ID.
  - `package_snapshot`: Serialized/JSON snapshot of the package at arrangement time.
  - `extras_snapshot`: Serialized/JSON snapshot of arranged extras.
  - `arranged_by_user_id`: WordPress user ID of the arranging Treasurer.
  - `arranged_at`: UTC timestamp of arrangement.
  - `invoice_id`: ID of the generated draft finance invoice.
- Entity class: `RegistrationPackageArrangement`.
- Repository: `RegistrationPackageArrangementRepository`.
- Service: `RegistrationPackageArrangementService`.

### 4.3 Persona and Security Boundaries
- **Treasurer Sole Authority:** Only users with `iexel_manage_billing` (Treasurers / Financial Administrators) can access the arrangement route `/club-os/treasurer/registrations/{id}/arrange-package/` and submit arrangements.
- **Secretary Read-Only Visibility:** Authorized Secretaries (`iexel_manage_registrations`) have contextual visibility of the arranged package in `PortalSecretaryRegistrationDetailPage`, but no arrange/edit actions or billing capabilities.
- **Parent Boundary:** Parents have no self-service arrangement route post-registration.
- **Registration Status Gate:** `RegistrationPackageArrangementService::can_arrange()` strictly requires status `'registered'`. Registrations in `'draft'`, `'submitted'`, `'information_requested'`, or `'approved'` cannot have a package arranged post-registration.

### 4.4 Pathway Eligibility and Commercial Applicability
The accepted Club OS commercial rule is:
1. Registration Packages have pathway applicability (`is_applicable_to`).
2. Extras/Add-ons attached to packages ALSO retain their own pathway applicability (`applies_to_pathway`).
3. An attached Extra is offered only when:
   - the package is eligible for the Registration pathway;
   - the Extra is attached to that package;
   - the Extra itself is eligible for that Registration pathway;
   - normal active/archive rules are satisfied.
4. This is intentional Treasurer-controlled behaviour:
   - *Confirmed LocalWP Example:* For Returning Player #303 (Reece Read), `Essential Player Package` is available; attached `Team Tracksuit` (eligible for Returning Player) is available; attached `Away Top` (restricted to New Player / Trialist Conversion) is correctly NOT offered.
   - If the Treasurer later wants Returning Players to be able to purchase `Away Top`, the Treasurer can enable Returning Player in the Extra Charge's existing "Applies to (Registration Pathways)" settings. No code change is required. Package/extra inheritance is not an unresolved issue.

### 4.5 Finance Handoff Integration
- When an arrangement with billable items is submitted, `RegistrationPackageArrangementService` delegates to Finance to generate an idempotent `Draft` invoice.
- The invoice uses `source_type = 'registration_post_package'` and `source_id = registration_id`.
- Line items are cleanly mapped from the arranged package and extra charges.
- The generated invoice follows standard Finance lifecycle management (Treasurer can review, adjust, issue, or collect).

### 4.6 Single Arrangement Scope
- The workflow supports exactly one package arrangement per registration completed without a package.
- Once arranged, the arrangement cannot be repeated or replaced via this workflow (`uk_registration_id` enforcement).
- General package amendments or upgrades for registrations that already have a package remain deferred.

## 5. Test & Manual Acceptance Evidence: Registration #303 (Reece Read)
- **Subject:** Registration #303 (`Reece Read`, Season 2026/27, Returning Player pathway).
- **Initial Historical State:** Status `Registered`, completed with no package chosen (`package_id = null`, `package_snapshot = null`).
- **Post-Registration Arrangement Applied:**
  - Arrangement ID: `#19`.
  - Selected Package: `Essential Player Package` (£60.00).
  - Selected Extra: `Team Tracksuit` (+£20.00).
  - Suppressed Extra: `Away Top` (+£20.00) — suppressed because pathway is Returning Player.
  - Total Arranged: £80.00.
  - Generated Invoice: `INV-001583` (Invoice ID `#1583`, Status: `Draft`).
- **UI & Presentation Acceptance:**
  - Historical panel confirms: "AT REGISTRATION: No package selected during registration."
  - Arranged panel confirms: "ARRANGED POST-REGISTRATION: Essential Player Package — £60.00 / Team Tracksuit +£20.00 / Total arranged £80.00 / Draft invoice INV-001583."
  - Desktop layout wrapping refined and verified (`1503291e8155d8fab12b321f0e7214c3caed7532`).
  - Mobile (320px) viewport verified for both the arrangement form and the registration detail display.

## 6. Automated Validation Evidence
- **Contract Validator (`validate-registration-post-package-arrangement-contract.php`):** 36/36 passed (100%).
- **Implementation Validator (`validate-registration-post-package-arrangement.php`):** 93 passed, 4 failed.
  - *Explanation of the 4 Failures:* These 4 failures are pre-browser-test test-fixture assertions that expect Registration #303 to have no arrangement and no invoice. Because Registration #303 was the explicit subject of the Product Owner's successful manual browser test (creating Arrangement #19 and Draft Invoice #1583), these 4 fixture-expectation failures are fully understood, expected, and accepted.
- **Non-Mutating Full Validator Suite:** 70/71 passed (the only failure being the above fixture assertions on #303).
- **Controlled Mutating Validators:** 5/5 passed.
- **PHP Linting:** All modified and new PHP files passed with zero syntax errors.
- **Git Whitespace (`git diff --check`):** Clean across all commits.

## 7. Protected Git Stash Warning
The `iexel-club-os` plugin repository contains a protected stash:
`stash@{0}: On global-navigation-system: Commit composer: 7/10/2026, 1:04:53 PM`
**DO NOT** apply, pop, drop, clear, or modify this stash.

## 8. Deferred Backlog & Candidates for Next Workstream
With RP-B, RP-C, and Post-RP all delivered, no single next implementation batch is dominant in the backlog. Candidates include:

1. **Prospect / Trialist Operational Seam Discovery (`ProspectLifecycle::INVITED_MATCH_REGISTRATION`):**
   - The enum/state exists in code, but there is not yet a completed operational UI/handler workflow for inviting a Prospect directly into competitive match registration.
   - This remains a legitimate future discovery candidate.
   - Strictly separate from package/extra applicability, which has already been resolved as intentional Treasurer-controlled behaviour where packages and attached extras each independently enforce pathway eligibility.
2. **Deferred General Package Amendments / Upgrades:**
   - Workflows to modify, upgrade, or re-arrange registrations that already possess an initial package selection.
3. **OS-011:**
   - Welfare Concern Detail visual hierarchy polish.
4. **Person 176:**
   - Orphaned Team Assignment data-integrity cleanup.
5. **`iexel-fee-rule-back` Naming Debt:**
   - Legacy CSS/template class renaming.
6. **Premium Surface Colour Consistency Audit:**
   - Visual harmonization across remaining administrative workspaces.

## 9. Recommended Next Action
Do not invent or start a new implementation batch. A Product Owner / lead developer selection is required to determine the next workstream.
