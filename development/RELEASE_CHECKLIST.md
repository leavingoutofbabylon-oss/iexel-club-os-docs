# Release Checklist

**Last verified:** 2026-08-15

---

## Pre-Release

- [ ] All planned features for this release are merged to `main`
- [ ] All known P1 bugs are fixed
- [ ] PHPCS passes with no errors
- [ ] All tests pass
- [ ] `IEXEL_CLUB_OS_VERSION` constant is updated in `iexel-club-os.php`
- [ ] `IEXEL_CLUB_OS_DB_VERSION` constant is updated if schema changed
- [ ] New upgrade steps are added to `UpgradeRunner` if schema changed
- [ ] `CHANGELOG.md` is updated with all changes for this release
- [x] Release Readiness and clean-install verification pass on a clean test installation (verified on WP 7.0.4 / PHP 8.2.29 / MySQL 8.4; blocker repairs merged on `main`)
- [x] Release Readiness and controlled upgrade matrix pass on upgraded test installations across all canonical baselines (Rows 1–4 and Interruption/Resume verified on WP 7.0.4 / PHP 8.2.29 / MySQL 8.4; Environment 2 PASSED)

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
