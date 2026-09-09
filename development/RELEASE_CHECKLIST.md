# Release Checklist

**Last verified:** 2026-09-09

---

## Pre-Release

- [ ] All planned features for this release are merged to `main`
- [x] All known P1 bugs are fixed — the one P1 open at the start of the MVP Release Candidate cycle (Access-restricted portal branches returning HTTP 200 instead of 403) was repaired and independently re-verified in RC-03-R1/RC-03-CLOSE (plugin `main` `3ee4c92963e8721b5562aa3a64e3706f81a346dc`). Zero evidenced P0 or unresolved P1 remains as of that commit. This does not certify future work merged after this checkpoint.
- [ ] PHPCS passes with no errors
- [ ] All tests pass
- [ ] `IEXEL_CLUB_OS_VERSION` constant is updated in `iexel-club-os.php`
- [ ] `IEXEL_CLUB_OS_DB_VERSION` constant is updated if schema changed
- [ ] New upgrade steps are added to `UpgradeRunner` if schema changed
- [ ] `CHANGELOG.md` is updated with all changes for this release
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
- [ ] Update `ROADMAP.md` to mark completed items
- [ ] Update `MVP_STATUS.md` if this is the MVP release

---

## Hotfix Process

If a critical bug is found after release:

1. Create a hotfix branch from the release tag: `hotfix/{version}-{description}`
2. Fix the bug
3. Update the patch version number
4. Update `CHANGELOG.md`
5. Merge to `main` and the release branch
6. Tag and release as a patch version
