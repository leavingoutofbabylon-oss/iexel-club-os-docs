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
