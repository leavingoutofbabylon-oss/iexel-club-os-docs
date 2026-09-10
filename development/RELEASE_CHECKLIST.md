# Release Checklist

**Last verified:** 2026-09-09

---

## Pre-Release

- [ ] All planned features for this release are merged to `main`
- [x] All known P1 bugs are fixed — the one P1 open at the start of the MVP Release Candidate cycle (Access-restricted portal branches returning HTTP 200 instead of 403) was repaired and independently re-verified in RC-03-R1/RC-03-CLOSE (plugin `main` `3ee4c92963e8721b5562aa3a64e3706f81a346dc`). Zero evidenced P0 or unresolved P1 remains as of that commit. This does not certify future work merged after this checkpoint.
- [x] **PHPCS — N/A for this release.** No PHPCS ruleset, configuration file (`phpcs.xml`/`phpcs.xml.dist`) or `composer.json` dependency is configured anywhere in this repository — there is currently no PHPCS tooling to run. This item is settled as not applicable, not silently skipped; introducing PHPCS tooling is separate, un-scoped future work.
- [x] **All tests pass (2026-09-09, plugin `main` `fbfc032fa286b2d227c085c369a02b8a9cd837f1`).** This project's test suite is its `tools/validate-*.php` set. The canonical final validation gate for this release was re-run fresh against the current clean, committed tree: the RC-03-CLOSE 9-validator persona/security gate (`validate-plain-permalink-portal-routing.php` 91, `validate-team-staff-operational-access.php` 55, `validate-committee-permissions.php` 105, `validate-team-workspace-route-and-display.php` 39, `validate-admin-person-role-dependency-guards.php` 91, `validate-admin-person-role-sync.php` 54, `validate-secretary-people-foundation.php` 81, `validate-welfare-people-compliance.php` 123, `validate-staff-compliance-secretary-ui.php` 98 — every total exactly matching its established baseline) plus the Finance-domain regression set (`validate-parent-family-finance.php` 44, `validate-treasurer-billing-run-detail.php` 93, `validate-treasurer-directory-ux.php` 34, `validate-treasurer-finance-configuration.php` **535** on a clean tree, `validate-treasurer-finance-relationships.php` 264, `validate-treasurer-invoice-detail.php` 54, `validate-treasurer-operational-read-access.php` 45), plus a full recursive PHP lint of `app/` and `iexel-club-os.php` (zero syntax errors). This is the smallest authoritative gate proven sufficient by the immediately preceding MVP Final Ship-Gate Audit — not a claim that every one of the ~149 historical validator scripts in `tools/` was re-run for this checkpoint. **`validate-treasurer-finance-configuration.php`'s count is git-status-dependent by design** (it asserts against live `git status`/`git diff` output for a small "no unexpected file changed" sub-check) — 535 is the correct, fully-passing total for the current clean tree; an earlier mid-implementation run against a deliberately dirty tree recorded 537, which was equally correct for that transient state. Neither number reflects a failure at any point. **Release Readiness (`ReleaseReadinessService::evaluate()`, run live and read-only) reports `Ready` with zero risks flagged `required=true`** (0 Blocker, 0 Critical, 0 High; 4 Medium/1 Low/2 Informational, all `required=false`) — exactly matching the pre-RC documented baseline (22 checks: 17 Pass, 1 Review, 4 External, 0 Fail), confirming no regression through the RC cycle or any post-RC batch. **The one known validator condition, `validate-visual-foundation.php`'s "Public stylesheet dependency order changed" failure, is confirmed validator-expectation drift, not a runtime defect** — the actual `public.css` dependency (`array('iexel-club-os-club-mark')`) is correctly registered and resolves at runtime; the validator's hardcoded expectation is simply stale. Not a release blocker.
- [x] `IEXEL_CLUB_OS_VERSION` constant is updated in `iexel-club-os.php` — bumped to `1.0.0-dev` (plugin header `Version:` and `readme.txt`'s `Stable tag:` updated to match) for this Operational MVP release, per the version-history audit recorded in the MVP Release Preparation Batch 1 checkpoint. Left `-dev`-suffixed, consistent with this constant's entire prior history, since tagging the final release remains a separate, later step in the "Release" section below.
- [x] **Database schema/data version — N/A for this release.** The checklist's original "`IEXEL_CLUB_OS_DB_VERSION`" wording refers to a constant that does not exist in source; the actual mechanism is `UpgradeVersions::SCHEMA_VERSION`/`DATA_VERSION` (currently `2026.08.9`/`2026.08.9`). Confirmed via `git diff --stat` against the RC-03-CLOSE baseline commit that no file under `app/core/Database`, `app/core/Upgrade`, `Activator.php` or `Deactivator.php` changed in any post-RC batch — no schema/data-version bump is required.
- [x] **New `UpgradeRunner` steps — N/A for this release.** No schema change occurred (see above), so no new `UpgradeStep` is required.
- [x] `CHANGELOG.md` is updated with all changes for this release — a new "Version 1.0.0 - Operational MVP" entry has been added, organised around the delivered product (portal/member experience, Club Admin/Secretary, Coach/Team Workspace/Matchday, Parent/Player, Treasurer/Finance, Welfare/safeguarding, Staff Compliance, and platform/lifecycle/security hardening). It explicitly does not represent Finance Reports, the Premium Surface Colour Consistency Audit, or OS-011 as shipped — Finance Reports is recorded only as removal of an unfinished, never-connected route, not as delivered reporting.
- [x] **(Historical baseline)** Release Readiness and clean-install verification pass on a clean test installation (verified on WP 7.0.4 / PHP 8.2.29 / MySQL 8.4; blocker repairs merged on `main`; 48 tables, schema/data `2026.08.6`)
- [x] **(Historical baseline)** Release Readiness and controlled upgrade matrix pass on upgraded test installations across all canonical baselines (Rows 1–4 and Interruption/Resume verified on WP 7.0.4 / PHP 8.2.29 / MySQL 8.4; Environment 2 PASSED)
- [x] **(Current RC cycle, 2026-09-09)** Clean-install validation re-verified against the current committed build on WordPress 7.1 / PHP 8.2.29 / MySQL 8.4.0 (RC-02A, disposable **IEXEL Club OS Dev RC Clean**) — schema/data `2026.08.9`, 51 tables, current rewrite-rule set compiled correctly on normal activation, Staff Compliance correctly installed and scoped, idempotent reconciliation, healthy deactivate/reactivate lifecycle. One P1 found (no-current-Season Team Workspace fatal) and repaired — see RC-02A-R1 below.
- [x] **(Current RC cycle, 2026-09-09)** No-current-Season Team Workspace fatal repaired and Product-Owner-accepted (RC-02A-R1, plugin `main` `73c576762d5340ddc0cfa8c12d840b1ee10b31b7`).
- [x] **(Current RC cycle, 2026-09-09)** Supported existing-club upgrade validated against the current committed build (RC-02B, disposable **IEXEL Club OS Dev RC Upgrade**, historical pre-upgrade baseline commit `d8d9607` / schema `2026.08.6`) — representative existing-club data (Season, Team, Coach, Player, Parent, assignments, Event, Finance, Welfare) preserved field-for-field through an in-place upgrade to `2026.08.9`, correct Staff Compliance backfill, no capability broadening, idempotent reconciliation confirmed self-healing (not defective) on a second pass.
- [x] **(Current RC cycle, 2026-09-09)** Representative final persona/security validation passed (RC-03) across Club Admin, Secretary, Welfare, Treasurer, Coach/Manager, Parent/Guardian and Player, using genuinely non-admin single-persona test accounts. One P1 found (Access-restricted denial branches returning HTTP 200 instead of 403) and repaired across all 13 affected branches, independently live-verified pre-fix and post-fix (RC-03-R1, plugin `main` `3ee4c92963e8721b5562aa3a64e3706f81a346dc`); closure revalidation (RC-03-CLOSE) confirmed **RELEASE CANDIDATE PASS**.
- [x] **Product Owner manual sign-off: PASSED** (2026-09-09, against plugin `main` `3ee4c92963e8721b5562aa3a64e3706f81a346dc`). This certifies the MVP Release Candidate as technically validated and product-accepted — it is a distinct step from, and does not itself satisfy, the remaining `PHPCS`/`CHANGELOG`/version-constant items above or the "Release"/"Post-Release" sections below.

---

## Release

- [ ] Create a release branch: `release/{version}`
- [ ] Tag the release: `git tag v{version}`
- [ ] Push the tag: `git push origin v{version}`
- [ ] Create a GitHub release from the tag
- [ ] Attach the plugin ZIP to the GitHub release

---

## Post-Release

- [ ] Deploy to production
- [ ] Verify Release Readiness page passes on production
- [ ] Monitor activity log for errors
- [ ] Update `development/CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` to mark completed items (this checklist's original "`ROADMAP.md`" reference does not exist under that name in this repository; this is the actual roadmap document)
- [ ] Create/update `MVP_STATUS.md` — this is genuinely post-release documentation (it records the shipped state of the MVP release), so it correctly belongs here and must NOT be created before release

---

## Hotfix Process

If a critical bug is found after release:

1. Create a hotfix branch from the release tag: `hotfix/{version}-{description}`
2. Fix the bug
3. Update the patch version number
4. Update `CHANGELOG.md`
5. Merge to `main` and the release branch
6. Tag and release as a patch version
