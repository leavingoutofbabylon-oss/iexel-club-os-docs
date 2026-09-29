# IEXEL Club OS — Development Handover

**Date:** 2026-09-29
**Status:** Registration Integrity COMPLETE / ACCEPTED / MERGED ON MAIN; documentation checkpoint awaiting review

## 1. Current Development Position

Registration Packages, RP-B, RP-C, post-registration Package arrangements, Parent draft identity/ownership hardening, Guided Registration Conflict Resolution and Legacy Staff Registration Recovery are complete. The two integrity workflows preserve Person-first Staff Registration, canonical Person + Season + pathway journeys and immutable commercial history. No next implementation batch is selected.

Read `MASTER_DEVELOPER_GUIDE.md` for canonical architecture, `../SPRINTS.md` for accepted delivery evidence and `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md` for remaining work. This handover supersedes older handovers' current-position/next-task recommendations; retain their historical acceptance evidence. In particular, RP-C and package/extra pathway applicability are completed, not pending product-definition tasks.

## 2. Repository State at This Checkpoint

- Plugin branch: `main`; HEAD and `origin/main`: `55ee697c796dbde93e481b45b5809422d7f3be0a`; ahead/behind `0/0`; clean, nothing staged.
- Latest commit: `55ee697c796dbde93e481b45b5809422d7f3be0a` — `feat: add legacy staff registration recovery`.
- Previous commit: `e303ca96234c8c2530aae776ea55914d3a5dc02d` — `feat: add guided registration conflict resolution`.
- Parent hardening: `67ac823` — `fix: enforce parent registration journey integrity`.
- Protected plugin stash: `stash@{0}: On global-navigation-system: Commit composer: 7/10/2026, 1:04:53 PM`; SHA `ed95f294a6ccccfbb48425903118abcc48d2a9ec`. Do not apply, pop, drop, clear or modify it.
- Docs branch: `main`; starting HEAD and `origin/main`: `5374f25936d0821d3dabd9d43dbd286c4f2cf074`; ahead/behind `0/0`. This checkpoint leaves three canonical docs modified and this handover untracked, all unstaged; no commit/push authorized.
- Pre-existing protected docs change: `development/RELEASE_CHECKLIST.md`, modified and unstaged. SHA256 `0B7EE2861A0605588F2DB55101DCBE91829C1C4E62167D5A1DD581CB85A501C5`; preserved separately from this checkpoint.

## 3. Completed Registration Package Architecture

- Foundation → RP-B (`c0936ed`): Step 5 Package/extras selection, independent pathway eligibility, immutable snapshots, settings-driven no-package policy, Parent attempt-token ownership and Staff Person-first selection. Information Requested is the controlled Parent correction/resubmission route; submitted choices are not silently overwritten.
- RP-C (`e8283e9`): Idempotent Registration → Finance Draft invoice handoff from the frozen commercial snapshot, with Treasurer visibility. No-package/zero-billable journeys do not create invoices. No automatic issuing, payments or checkout.
- Post-registration arrangements (`4285091`, layout `1503291`): Treasurer may arrange one initial package for a Registered journey completed without one. `RegistrationPackageArrangement` / `registration_package_arrangements` owns the separate immutable event; original `package_id`/`package_snapshot` remain NULL. Finance Draft handoff uses `registration_post_package`; Secretary is read-only. Package and attached extras each independently enforce pathway eligibility. General amendments/upgrades and Parent post-registration self-service remain deferred.
- Parent hardening (`67ac823`): Canonical child identity and authorized family ownership are retained; equivalent journeys resume safely and ambiguity fails closed. Staff recovery/conflicts do not relax those boundaries or Training Member/competitive participation requirements.

## 4. Complementary Integrity Workflows

**Guided conflicts:** More than one active Person + Season + pathway journey fails closed into Secretary discovery/comparison. Guided mutation supports exactly two existing-Person-linked Drafts with the same canonical key; mixed states/larger groups remain for club review. Deliberate survivor selection, reason (3–500 characters), confirmation, actor-bound stale checks and Person/child/Registration locking protect transactional resolution. Survivor unchanged; duplicate Withdrawn and retained, never deleted or merged; commercial snapshots intact. Mandatory survivor/duplicate/actor/reason/time audit failure rolls back. Resolved conflict leaves active surfaces, unrelated conflicts remain. Sensitive welfare data is not duplicated into comparison; contextual detail return preserves normal navigation.

**Legacy Staff recovery:** Only Secretary-origin, unlinked New Player Draft at Step 1, active Season, compatible Staff-editable state, no incompatible history, guardians or commercial selection. Deliberately select existing active Player → compare identity → reason/unchecked confirmation → trusted Secretary POST/nonce → locked stale/collision revalidation → atomic link/normalize FROM Person and New Player → Returning Player → mandatory audit → same Draft resumes. Person remains unchanged; no automatic matching/selection, Person creation, new/deleted Registration, guardian/commercial migration, Finance handoff, arbitrary DOB editing or Trialist Conversion recovery. Unsupported shapes fail closed.

Collision identity is the resulting Person + existing Season + Returning Player, including family Drafts and excluding Rejected/Withdrawn history: zero other active equivalents permits recovery; one rejects toward that journey; multiple reject into conflicts. Recovery cannot bypass conflict detection. These are not parallel generic migration tools.

Modern Staff first name/last name/DOB remain locked and canonical in People; authorized identity correction is `/club-os/secretary/people/{id}/edit/`. Ordinary save does not update Person identity. Final wizard wording: "This Registration is linked to the existing Club OS Person. Player identity details are managed in People."

## 5. Acceptance and Validation Baselines

Product Owner accepted desktop/mobile conflict comparison and detail navigation; disposable resolution kept survivor Draft, duplicate Withdrawn history and its commercial snapshot, then resumed the normal journey. Recovery desktop/320px search/comparison, centered narrow heading and shared autogrow reason (no horizontal resizing) passed. Actual browser recovery retained the same Registration, linked canonical Person, became Returning Player, left Person unchanged, audited once and had zero Finance/commercial effects. Picker searches Player name/Club OS ID, not internal Person database ID. Disposable IDs are not production requirements.

| Accepted evidence | Result |
|---|---|
| RP-B | 739/739 new assertions PASS; browser acceptance PASS |
| RP-C | 36 PASS / 0 FAIL |
| Guided conflicts | 108 PASS / 0 FAIL |
| Secretary Registration detail | 80 PASS / 0 FAIL |
| Legacy Staff recovery | 132 PASS / 0 FAIL |
| Registration draft ownership | 180 PASS / 0 FAIL |
| Training Member Registration | Previously accepted unrelated 99 PASS / 1 FAIL: "Return path accepts an arbitrary URL" |
| Post-package arrangement contract | 36/36 PASS |
| Post-package arrangement implementation | 93 PASS / 4 accepted fixture-baseline FAIL after successful browser arrangement on #303 |

The Training Member failure is not a recovery regression. Final literal Staff wording followed substantive validation; those validators were not rerun for copy alone. Earlier RP-B source/fixture caveats remain historical evidence, not new failures introduced by these batches. This documentation task performs no validators or database operations.

## 6. Protected Reference Data

- Henry James Registrations #304/#305 intentionally remain unresolved acceptance/reference data. Do not automatically resolve them or label them a product defect.
- Zayne Watt #558 demonstrated historical unlinked Staff Draft state; readonly DOB was intentional. At investigation no plausible canonical Player candidate existed; no recovery is claimed. If genuinely absent, create/verify the genuine Player through People before deliberate eligible recovery. Do not mutate #558 automatically or infer identity by surname.
- Accepted post-package arrangement evidence on #303 explains pre-browser validator fixture assumptions. Preserve its historical registration/arrangement/Finance evidence.
- Prior protected Registration, Person/family and Finance fingerprint checks were preserved through acceptance. This docs-only checkpoint does not query/re-fingerprint database state or authorize data repair.

## 7. Remaining Work and Recommended Next Action

**Reassess the next MVP batch from authoritative docs with the Product Owner/lead developer. Do not invent or start the next implementation task.** Supported candidates include:

- Prospect/Trialist invited Match Registration operational seam (`ProspectLifecycle::INVITED_MATCH_REGISTRATION`); separate from completed commercial pathway applicability.
- OS-011 Welfare Concern Detail hierarchy polish: cosmetic/non-blocking.
- Validator/fixture hygiene, especially post-package assertions tied to pre-browser #303 state; unrelated Training Member return-path baseline remains separately understood.
- Internal Club Testing preparation against the latest accepted build; do not restart completed testing/remediation or invent RC-04.
- Existing deferred general package amendments/upgrades, Person 176 orphaned assignment cleanup, `iexel-fee-rule-back` naming debt and Premium Surface Colour Consistency Audit retain their prior scope. None is promoted to the next task here.

Release/deployment remains a separate checklist gate. Finance Reports is a removed unfinished scaffold and requires fresh product definition; do not reopen its routing cleanup. Approved Fundraising architecture remains separate future phased work, not implemented by this checkpoint. Preserve prior completed-work and deferred-scope decisions.
