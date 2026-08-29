# Development Handover — 2026-08-29

**Supersedes:** no prior dated Development Handover document was found anywhere in this docs repository (exhaustively searched by filename and content) at the time this one was written. This is treated as the first document of its kind rather than a literal replacement of a "2026-08-20" file, which does not exist in this repository. If such a document exists elsewhere (a different location, a personal note, a separate system), reconcile it against this one and correct this line.

---

## DO NOT START NEW FEATURE DEVELOPMENT

This handover's resume point is **documentation/release-readiness work only**. The Internal Club Testing remediation programme is complete and integrated. The next controlled action is Release Readiness / v1.0 sign-off work (see below), not a new implementation batch.

---

## Current Git Baseline

- Plugin `main`: `b2b51eb`
- `origin/main`: `b2b51eb` (pushed 2026-08-29)
- Integrated branch: `feature/mvp-internal-testing-fixes` (57 commits, still present, no longer the active development base)
- Integration method: audited, GREEN-gated, **pure fast-forward** (`git merge --ff-only`) — no merge commit, no rebase, no squash, no force push
- Divergence at integration: `origin/main` 0 commits ahead, feature branch 57 commits ahead, merge-base == `origin/main`'s pre-integration HEAD (`5276042`)
- Docs repo (`iexel-club-os-docs`) branch: `main`, clean, unaffected by the plugin-repo integration (separate repository)

---

## Completed Internal Testing Remediation

The `feature/mvp-internal-testing-fixes` branch (now `main`) carried, among its 57 commits:

- SEC-001 through SEC-008 (canonical Team Season provisioning, grassroots play-up eligibility, event meet-time unification, committee event routing, event audience policy/flexible builder/privacy-safe RSVP, coach football event-scope hardening)
- The Completed Match Correction architecture (Batches 2A, 2B-1, 2B-2, and a combined end-to-end acceptance gate)
- Admin Sidebar Navigation Consolidation (ADM-001/002/003) and dark-surface text contrast (OS-029/FIN-028/PL-024)
- Secretary member-maintenance safeguards and person-bound registration/training-member flow fixes
- Canonical **Current Emergency Contact** management (Person-level current state, authoritative even when explicitly empty, exact-current-Season Registration fallback, unavailable as the final state)
- **Secretary-assisted password-reset completion alerts** (WordPress user-meta based, no schema, never stores a password/hash/token/URL, idempotent on `after_password_reset`, correct attribution, seven-day self-expiring eligibility window, fail-closed identity re-check)
- A final pre-merge validator/repository hygiene batch (see below)

Full detail: `SPRINTS.md`, section "Internal Club Testing Remediation & Final Pre-Merge Validator Hygiene".

---

## Final Release-Gate Result

- **Final clean-branch pre-merge release gate: GREEN.** Zero functional/security/schema/integration blocker identified. Two items of harmless validator drift and one pre-existing bare-CLI environmental limitation, both individually classified as non-blocking (detail below).
- **Post-integration sanity validation: PASS.** All 10 required validators green on the post-merge tree (Secretary Command Centre, Secretary Person Role Management, Secretary Events Management, Secretary Portal Account Linking, Secretary-Assisted Password Reset, Current Emergency Contact, Training Membership Domain, Workspace Priority Alert Scoping, Event Response Text Overflow, Treasurer Finance Configuration).
- `git diff --check` on the integrated range surfaced one pre-existing, non-content whitespace nit (trailing blank line at EOF in `app/core/Upgrade/ParentGuardianRelationshipReconciliation.php`) — not a conflict marker, not introduced by the integration itself (a fast-forward cannot alter file content).

---

## Known Non-Blocking Validator Debt

Recorded accurately — none of these are confirmed production defects; all were individually root-caused with direct source evidence:

- **`validate-prospect-training-conversion.php`** — harmless source-shape drift. An exact-literal assertion against `TeamSeasonService`'s `age_group` snapshot expression no longer matches after a legitimate refactor (extracted to a named variable, added `trim()` + `'Unspecified'` default for blank values). The eligibility-governing invariant (`AgeGroupKey::from()` normalization) remains independently proven by adjacent assertions in the same file.
- **`validate-committee-club-projects.php`** — a stale exact-literal assertion (`if($result->success){$this->metrics_cache?->invalidate();}`) no longer matches after a legitimate, already-committed `log_important_lifecycle_activity()` call (canonical ActivityLogger, self-guarded) was added inside the same success-gated block. The "cache refresh restricted to successful mutations" invariant still holds by direct inspection.
- **`validate-visual-foundation.php`** — a stale dependency-array assertion expects `public.css` enqueued with an empty dependency array. Production now correctly declares a `iexel-club-os-club-mark` load-order dependency (introduced by an already-committed, already-reviewed branding-controls feature), consistent with the identical pattern already used for `login.css`.
- **`validate-secretary-portal-account-linking.php`** — passes (`PASS: ... (63 assertions verified)`), but emits 6 non-fatal `stdClass could not be converted to int` PHP warnings. Cosmetic; does not affect the PASS result; worth a small future look.

None of these require production, schema, or version-constant changes to resolve — only validator-file hardening, following the same "structural proof, not exact-literal" pattern already applied across the rest of the suite.

---

## Bare-CLI mysqli Limitation

The standalone `php.exe` CLI binary used for running `tools/validate-*.php` from a terminal lacks the `mysqli` extension (confirmed via `php -m`), unlike Local's own site-serving PHP-FPM process for the same codebase, which has it enabled. This affects 29 of 119 validators that require a live WordPress/database bootstrap. This is a structural, environmental, long-standing CLI-only gap — **not evidence of a functional defect** — and does not block safe integration into `main`. It does mean: before final Release Readiness / v1.0 sign-off, DB-integrated validators should be run through Local's browser-accessible environment (or a dedicated disposable test database), not assumed passing from CLI-only evidence. Do not attempt to mock or fake mysqli to work around this.

---

## Accepted Canonical Product/Data Decisions (unchanged, preserve)

- **Registration** = immutable historical submitted snapshot.
- **Person** = canonical current member identity/contact state.
- **Current Emergency Contact** = Person-level current operational state; resolution order is current Person-level row (authoritative even when explicitly empty) → exact-current-Season Registration fallback → unavailable.
- **Medical & Safety** = current operational state, separate from Registration history.
- **Family** = canonical Person relationships.
- **Registered Registration** must resolve to a valid active Person before downstream operational/financial use.
- **Training Only** = a valid independent Training Membership state; must not itself imply Match Player eligibility or Team Assignment.
- Security/safeguarding/privacy-first, canonical Activity attribution, the Secretary Priority Actions vs. Priority Alerts distinction, the seven-day password-reset completion alert lifecycle, and existing role/workspace boundaries are all unchanged by this integration.
- Player Progress remains an embedded Player-specific Team Workspace experience (Player Home → Team Workspace → My Progress) — see `SPRINTS.md`'s "Player Progress — Canonical MVP Architecture Decision".

---

## Remaining Release Checklist Work

Per `RELEASE_CHECKLIST.md` (Pre-Release section), satisfied by this integration:
- All planned features for this release are merged to `main` — satisfied; no unmerged feature/fix branch was identified (all six other lingering local branch refs were independently confirmed as ancestors of `main`, i.e. already merged via prior history).
- New upgrade steps are added to `UpgradeRunner` if schema changed — satisfied; 31 registered steps, all referencing symbolic `UpgradeVersions::SCHEMA_VERSION`/`DATA_VERSION` constants, zero duplicate IDs.
- Clean-install and controlled-upgrade-matrix verification — already `[x]` in the checklist from prior work, unaffected by this integration.

**Not yet satisfied, and not addressed by this integration:**
- PHPCS coding-standard pass — not run this session (only `php -l` syntax lint was run).
- All known P1 bugs fixed — no bug tracker was consulted in this session; unverified either way.
- `IEXEL_CLUB_OS_VERSION` constant update — currently `0.2.10-dev` in `iexel-club-os.php`; not a release version, not bumped.
- `IEXEL_CLUB_OS_DB_VERSION` constant — this exact constant name was **not found** in the plugin source; the actual mechanism is `UpgradeVersions::SCHEMA_VERSION`/`DATA_VERSION` (WP options), currently `2026.08.8`/`2026.08.7`. Worth reconciling the checklist's terminology against the actual mechanism at some point — not done here (out of this task's scope).
- `CHANGELOG.md` — **severely out of date**, its most recent entry describes "Version 0.5.0"/"Upcoming (Version 0.6)" content (early People/Teams/Team Assignments modules) with none of the substantial subsequent feature work reflected. This was not addressed in this documentation-reconciliation pass — it is a large, separate undertaking, not one of the documents this task was scoped to update.
- Release-section items (release branch, tag, GitHub release, ZIP artefact) and Post-Release items — none started; these are release-process/operational steps, not code-related, and follow only after the above.

**None of the outstanding items above is a known MVP implementation code blocker.** They are release-process, packaging, and documentation-currency items — version/tag/changelog/PHPCS/DB-integrated-validation work — not unresolved product defects. The 2026-08-26 read-only MVP/Release Readiness reconciliation audit (recorded in `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` and `MASTER_DEVELOPER_GUIDE.md`) found no currently-known unresolved High/MVP implementation blocker, and this integration introduced no new one.

---

## Exact Next Recommended Controlled Action

Run the DB-integrated validator suite (the 29 mysqli-gated validators) through Local's browser-accessible WordPress environment (not the bare CLI) against a disposable/test database, to close the one genuine evidence gap this integration could not verify from CLI alone. In parallel or afterward: run PHPCS, decide and apply the `IEXEL_CLUB_OS_VERSION` bump for the target release, and begin the `CHANGELOG.md` reconciliation — all release-process work, not new feature development.
