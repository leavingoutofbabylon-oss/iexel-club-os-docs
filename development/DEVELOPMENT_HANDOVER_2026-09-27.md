# Development Handover — 2026-09-27

**Supersedes:** `DEVELOPMENT_HANDOVER_2026-09-09D.md`. That document remains in the repository as a historical record of the Finance Reports Phantom Route Cleanup Batch 1 and the Post-RC Next Development Position at that point. **This document carries the resume point forward through the completed RP-B batch.**

---

## DO NOT START NEW FEATURE DEVELOPMENT WITHOUT READING THIS

Since the previous handover, one substantial development batch has landed — **RP-B**, a full product feature batch, not a post-RC follow-up and not a defect closure:

- `c0936eddafc1b7dc54e1bedf3453110cbaae984e` — "feat: establish registration packages selection, draft ownership, and secretary workflows (RP-B)"

**The MVP Release Candidate remains technically validated with Product Owner manual sign-off PASSED — this handover does not change that status.** See "MVP Release Candidate — Status (unchanged)" below. **Do not restart or re-scope any of RC-01, RC-02A, RC-02A-R1, RC-02B, RC-03, RC-03-R1, RC-03-CLOSE, Guardian Link Alignment Batch 1, Treasurer Premium Workspace Alignment Batch 1, Finance Reports Phantom Route Cleanup Batch 1, or RP-B.** Do not invent an "RC-04." Do not treat this as production deployment — see "What this does and does not mean" below.

---

## Current Git Baseline

- **Plugin `main`:** `c0936eddafc1b7dc54e1bedf3453110cbaae984e` ("feat: establish registration packages selection, draft ownership, and secretary workflows (RP-B)")
- **Plugin status:** **clean** — verified via `git status` returning nothing, `git rev-parse HEAD` matching the commit above, and local `main` confirmed identical to `origin/main`
- **Docs `main`:** `8da89afb9f22a168c3ed42d0eded1d0b542b5b2f` (pre-RP-B docs baseline; this documentation batch is not yet committed — the Product Owner/lead developer will review before it is committed)
- **Protected stash:** `stash@{0}: On global-navigation-system: Commit composer: 7/10/2026, 1:04:53 PM` — **must not be applied, popped, dropped or rewritten without explicit user approval**
- Prior plugin baseline (`DEVELOPMENT_HANDOVER_2026-09-09D.md`): `fbfc032fa286b2d227c085c369a02b8a9cd837f1`
- Post-RC checkpoints: Guardian Link Alignment Batch 1 (`29220cc0d6be03085c5096bf6bbe3af044d01741`), Treasurer Premium Workspace Alignment Batch 1 (`840369102b5b1d24f7701c7d2af3b325971fa824`), Finance Reports Phantom Route Cleanup Batch 1 (`fbfc032fa286b2d227c085c369a02b8a9cd837f1`), RP-B (`c0936eddafc1b7dc54e1bedf3453110cbaae984e`)

---

## Current Phase

**MVP Release Candidate technically validated; Product Owner manually signed off; four post-RC batches also complete — Guardian Link Alignment Batch 1, Treasurer Premium Workspace Alignment Batch 1, Finance Reports Phantom Route Cleanup Batch 1, and RP-B.** See "What this does and does not mean" below.

---

## MVP Release Candidate — Status (unchanged)

Nothing about the RC validation cycle's outcome has changed since the previous handover. The current build (plugin `c0936eddafc1b7dc54e1bedf3453110cbaae984e`) has:

- **ZERO evidenced P0 release blockers**
- **ZERO evidenced unresolved P1 release blockers**
- **Product Owner manual sign-off: PASSED** (against `3ee4c92`, still valid — the four subsequent post-RC batches are separately-completed follow-on work, not changes requiring re-sign-off of the RC itself)

### What this does and does not mean

This means: **the MVP Release Candidate is technically validated and Product Owner accepted, and four further post-RC batches have since been implemented, validated, committed and pushed.** It does **not** mean Club OS has been deployed to production, that a release tag/branch has been cut, or that any of the `RELEASE_CHECKLIST.md` "Release"/"Post-Release" steps have occurred — those remain a distinct, separate project step and no evidence in this cycle claims otherwise.

**For the full RC-01 → RC-03-CLOSE narrative, see `DEVELOPMENT_HANDOVER_2026-09-09.md` and `SPRINTS.md`'s "MVP Release Candidate Validation Cycle (RC-01 → RC-03-CLOSE)" section — unchanged. For the Guardian Link, Treasurer Premium Workspace, and Finance Reports narratives, see `DEVELOPMENT_HANDOVER_2026-09-09B.md`, `DEVELOPMENT_HANDOVER_2026-09-09C.md` and `DEVELOPMENT_HANDOVER_2026-09-09D.md` respectively — unchanged.**

---

## RP-B — Registration Packages Selection, Draft Ownership & Secretary Workflows (this handover's subject)

**Status: Complete.** Plugin `main` `c0936eddafc1b7dc54e1bedf3453110cbaae984e`. Full delivery detail is recorded in `SPRINTS.md`'s "Registration Packages Selection, Draft Ownership & Secretary Workflows (RP-B)" section; summarised here for resume-point purposes.

### Accepted Product & Architecture Decisions (What RP-B Delivered)

1. **Treasurer Registration Package Management:** Canonical package management surface exists at /club-os/finance/registration-packages/. Supports directory, create/edit, and active/archive/restore lifecycle, protected by iexel_manage_billing.
2. **Package Configuration:** Packages support images, Registration pathway/type applicability, and package ↔ Registration Extra/Add-on associations.
3. **Global Opt-out Policy:** "Allow registration without a package" is a global registration policy, *not* a per-package mandatory state.
4. **Historical Commercial Snapshot:** Step 5 selection creates an immutable JSON commercial snapshot. This snapshot is historical and remains independent of any later Treasurer catalogue edits.
5. **Submitted Lock:** Submitted commercial choices cannot be silently rewritten by background saves.
6. **Information Requested Correction Route:** "Request Information" is the controlled route for Parent correction before resubmission. A Parent correction/resubmission updates the snapshot while that lifecycle state permits it.
7. **Secretary Registration is Person-First:** Secretary Registration is NOT an alternative Person-creation route. It requires selecting an existing canonical Person.
8. **Missing-Player Route:** If the player cannot be found during Staff registration, the explicit deliberate journey is "Add them to People first." Person creation remains owned by the People workflow.
9. **Training Only Player Eligibility:** Eligible Training Only Players with canonical active Player identity can enter the Staff Registration journey. The Registration action itself does NOT create competitive participation (no Team Assignment, Match eligibility, or Finance obligation).
10. **Context & Authorisation Separation:** Parent and Staff contexts are explicitly isolated. Parent family shortcuts do not leak into Staff context, and Parent nonces do not authorise Staff writes.
11. **Duplicate Registration Protections:** Family-journey deduplication prevents concurrent active drafts for the same player.
12. **Shared Mobile Treatment:** Accepted narrow mobile presentation (including 320/360/390 views): step heading contained inside the white card; gold eyebrow/title centred; introductory sentence centred; functional form content naturally left-aligned. Parent and Staff share this treatment.
13. **Finance Isolation (Critical):** RP-B creates NO invoice, debt, billing schedule or Finance obligation.

### RP-B validation evidence

| Validator | Result |
|---|---|
| `validate-registration-draft-ownership.php` (new, 125 assertions) | PASS |
| `validate-registration-package-selection.php` (new, 135 assertions) | PASS |
| PHP lint — 33/33 PHP files | PASS |
| JS syntax | PASS |
| `git diff --check` | PASS (1 trailing-newline advisory at EOF — not a violation) |
| `validate-registration-existing-player-link.php` | 4/75 pre-existing baseline failures (obsolete single-nonce substring checks; not RP-B regressions) |
| `validate-registration-optional-fields.php` | 6/128 pre-existing baseline failures (whitespace-sensitive matching; not RP-B regressions) |
| `validate-secretary-registration-approval.php` | Pre-existing environment assumption (WP User fixture); not an RP-B regression |
| `validate-parent-card-info-request.php` | Pre-existing environment assumption (WP User fixture); not an RP-B regression |

**Total new assertions: 739 / 739 PASS.**

Real-browser acceptance: Henry James (Person 16), Real_player 11 (Person 205), Portal Youth Test (Person 136), Registrations 304 and 305 — all verified intact.

### Pre-existing validator baseline failures (not RP-B regressions)

The four failing assertions in `validate-registration-existing-player-link.php` match literal single-nonce strings that were superseded by the dual-context nonce architecture. They are pre-existing validator/source mismatches, not functional regressions. The six failures in `validate-registration-optional-fields.php` are whitespace-sensitive string matches on minified source — also pre-existing. Neither set represents an unresolved implementation defect.

---

## Deferred Work — Do Not Implement Without Approval

### RP-C — Finance Invoice/Debt Integration on Registration Completion

Finance integration is explicitly NOT part of RP-B. No invoice or debt record is created. When RP-C is eventually scheduled, it must:

- Route through `FinanceService` via an explicit, audited bridge — never direct insertion from registration handlers.
- Require an explicit Product Owner product definition of: which registration types trigger invoice creation, what line items are generated, how package/extras map to fee rules, and how existing billing schedules interact.
- Not be started from this handover's description alone.

### Secretary Package-After-Family Registration

A Secretary cannot currently take over a mid-journey parent-portal registration to complete the package-selection step on the family's behalf. The conflict/handoff UX is deferred.

### Prospect/Trialist Package Eligibility Audit

No package-eligibility rule for Prospect or Trialist registration types has been implemented or validated. The applicable package policy for these registration types requires Product Owner product definition before any implementation. **Do not invent Prospect/Trialist package eligibility rules from the RP-B implementation alone.**

---

## Known Technical Debt / Validator Caveats

Unchanged from `DEVELOPMENT_HANDOVER_2026-09-09D.md`, plus the RP-B pre-existing failures documented above. The full current list (unchanged items) from `DEVELOPMENT_HANDOVER_2026-09-09D.md` remains in force: the `CANONICAL_TABLES` 49-vs-51 gap, the `TeamStatisticsService.php:203` latent pattern, the CRLF validator-methodology note, the no-current-Season warning copy, the DevTools 404 observation, `validate-current-emergency-contact.php`, Person 19/Team 1 fixture drift, `validate-team-events-badge-mobile-repair.php`, `validate-visual-foundation.php`, `validate-team-workspace-overview-shell-polish.php`, Person 176 orphaned Team Assignment, Secretary late-add eligibility, raw `age_group` normalisation, FIN-031, `iexel-fee-rule-back` naming debt, and the Premium Surface Colour Consistency Audit.

The **Finance Reports route defect (FIN-033)** remains resolved by removal (from `DEVELOPMENT_HANDOVER_2026-09-09D.md`); do not re-open it.

---

## Post-RP-B Next Development Position

**No single next implementation batch is currently dominant in the authoritative backlog.** With the RC cycle, Staff Compliance A–D, Guardian Link Alignment Batch 1, Treasurer Premium Workspace Alignment Batch 1, Finance Reports Phantom Route Cleanup Batch 1, and RP-B all complete, the genuinely open remaining candidates are:

1. **OS-011** (Welfare Concern Detail hierarchy polish, Medium priority) — genuinely open, cosmetic/non-blocking.
2. **Person 176 orphaned Team Assignment** — small dev-database data-integrity item, not a product feature.
3. **`iexel-fee-rule-back` naming debt** — small, low-priority, cosmetic-to-code-quality only.
4. The **Premium Surface Colour Consistency Audit** — broader, larger, less-scoped; not currently promoted ahead of the smaller candidates.
5. The separate `RELEASE_CHECKLIST.md` "Release"/"Post-Release" gate (tagging, deployment) — a distinct project step, not itself a development task.
6. **RP-C** (Finance invoice/debt integration on registration completion) — requires Product Owner product definition before it can be scheduled as implementation work.
7. **Prospect/Trialist package eligibility audit** — requires Product Owner product definition.

**Product Owner/lead developer selection is needed** to choose among the genuinely open candidates — this handover states the accurate current position, it does not invent or authorise a priority. **Do not invent or begin a new implementation batch, an "RC-04," a new guardian or treasurer batch, RP-C, or a Prospect/Trialist package implementation from this handover's description alone.**

### Important "do not restart" notes

- Do not re-implement or re-scope RC-01, RC-02A-R1, RC-03-R1, Guardian Link Alignment Batch 1, Treasurer Premium Workspace Alignment Batch 1, Finance Reports Phantom Route Cleanup Batch 1, or RP-B — all complete and closed.
- Do not re-open RC-02A, RC-02B, or RC-03 as if their findings were still pending.
- Do not re-open the Guardian Link Role Synchronisation Audit — complete and recorded in `DEVELOPMENT_HANDOVER_2026-09-09B.md`.
- Do not re-open the Treasurer Premium Workspace Alignment — visual acceptance has PASSED, recorded in `DEVELOPMENT_HANDOVER_2026-09-09C.md`.
- Do not describe Finance Reports as an outstanding routing fix, a missing dispatcher case or a partially completed Reports page — it is a removed unfinished scaffold; a genuine capability is future product-definition work.
- Do not extend the Invoice Detail dark-record exception to any other Finance surface without a fresh, explicit Product Owner decision.
- Do not implement RP-C (Finance invoice/debt integration) without an explicit Product Owner product definition.
- Do not implement Prospect/Trialist package eligibility without an explicit Product Owner product definition.
- Do not re-implement any item listed as complete in earlier handovers — those documents' "do not restart" notes remain in force.
