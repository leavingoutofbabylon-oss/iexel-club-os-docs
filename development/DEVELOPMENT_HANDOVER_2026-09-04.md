# Development Handover — 2026-09-04

**Supersedes:** `DEVELOPMENT_HANDOVER_2026-09-03.md`. That document remains in the repository as a historical record of the point where Verified Historical Scorer Attribution v1 (CMC-002) had just landed and CMC-003 had not yet been started; this document carries the resume point forward.

---

## DO NOT START NEW FEATURE DEVELOPMENT WITHOUT READING THIS

**Match Hero Goal-Scorer Presentation (CMC-003)** — the item the prior handover recommended as "next" — **is now complete**, along with a live-eligibility correction, focused-action/half-width responsive polish, and a primary immersive module accent-top design-system consolidation delivered in the same arc. **Do not restart or re-scope any of this work.** See "Recently Completed" below and `SPRINTS.md` for full delivery detail.

There is currently **no new confirmed Pre-MVP product decision** to start next. See "Recommended Next Starting Point" at the end of this document.

---

## Current Git Baseline

- Plugin `main`: `5616f8befde1144800d991e3eb1496665a65526b` ("fix: unify branded trim on immersive modules")
- `origin/main`: `5616f8befde1144800d991e3eb1496665a65526b` (pushed)
- Working tree: clean at this checkpoint
- Docs repo (`iexel-club-os-docs`) branch: `main`, clean at `41b8f0f565cf8ecef2352ef0e91c15e87a8e66b9` immediately prior to this documentation checkpoint (a separate repository; this batch's own docs commit is not yet made)

Prior baseline (`DEVELOPMENT_HANDOVER_2026-09-03.md`): plugin `main` `2f3dcee`. Between `2f3dcee` and `5616f8b`, the plugin `main` history is (newest first):

```
5616f8b  fix: unify branded trim on immersive modules
54edcb2  fix: add branded trim to live match mode
0b8d21b  fix: polish match score hero responsive layout
ff73ae6  fix: align live goal eligibility with on-pitch state
b37de1c  feat: add match goal scorers to result heroes
2f3dcee  feat: add verified historical scorer attribution        (prior baseline)
7d3caa0  fix: make data quality recovery actions truthful         (already on main before 2f3dcee; not this session's work)
2cbae72  fix: use effective selection for historical match data   (already on main before 2f3dcee; not this session's work)
```

`2cbae72` and `7d3caa0` were already committed to `main` before the prior handover's `2f3dcee` baseline — they are part of the same CMC-002 historical-eligibility arc but were not individually called out in the prior handover. Both are now documented in `MASTER_DEVELOPER_GUIDE.md`'s "Verified Historical Scorer Attribution — Historical Eligibility Direction" and `SPRINTS.md`'s new "Historical eligibility and Data Quality correctness fixes" section.

---

## Recently Completed (since the 2026-09-03 handover)

### 1. Match Hero Goal-Scorer Presentation (CMC-003) — `b37de1c`

Club goal scorers now present beneath the Match score in familiar football-result style on both live Match Mode and completed-Match presentation, sourced from canonical active Match goal incidents only via `MatchGoalScorersCard`, shared verbatim across live Match Mode, the Coach completed-Event hero and the privacy-minimised participant Match Story. Ordinary Correct Match Record corrections and Verified Historical Scorer Attribution (CMC-002) both flow through automatically. A participant scorer-name bug (`for_event()` vs `active_for_event()` sourcing) was found and fixed in the same arc. Full detail: `SPRINTS.md`, "Match Hero Goal-Scorer Presentation (CMC-003)".

### 2. Live attribution eligibility correction — `ff73ae6`

Browser acceptance found the live Goal Scorer/Assist dropdowns missing an on-pitch Player with no Attendance row — a pre-existing rule violation surfaced by CMC-003 testing, not a CMC-003 regression. Fixed: a missing Attendance row no longer disqualifies an on-pitch Player; an **explicit** negative Attendance status still does; Available Bench Players remain ineligible until admitted/substituted on. Same eligibility projection serves both the read (dropdown) and write (server-side enforcement) paths.

### 3. Focused-action and half-width responsive polish — `0b8d21b`

The focused Goal Attribution score card no longer stretches to match a taller adjacent form; Team names now scale against the card/container's own width (not the viewport), fixing character-by-character breaks in narrow half-width layouts; the scorer list guarantees a Player name and minute never separate.

### 4. Primary immersive module accent-top consolidation — `54edcb2`, `5616f8b`

Match Mode's own cards, Match Recovery/Match Details (the shared collapsible disclosure — **Undo Last Goal was not removed, only its border treatment changed**), the main Events header, and the Matchday Hub hero now all use one reusable `.iexel-accent-top-module` CSS primitive for the club's runtime-configured Accent Colour top-edge treatment, instead of each carrying its own one-off left-rail rule. TeamEventForm, Matchday Hub's light operational grid cards, and every semantic/nested/unrelated surface remain deliberately untouched. See `MASTER_DEVELOPER_GUIDE.md`'s "Primary Immersive Module Accent Treatment" for the durable design rule. Full delivery detail: `SPRINTS.md`, "Primary Immersive Module Accent-Top Consolidation".

---

## Current Match Mode State

Match Mode remains an immersive dark football workspace; none of the above changed its business logic, permissions, data or database. Specifically preserved and re-verified throughout this arc:

- Live scorer/assist eligibility, score calculation, goal incident semantics.
- Substitution and goalkeeper-change logic.
- Match Recovery's collapsed-by-default behaviour and its Undo Last Goal/Substitution/Goalkeeper Change content.
- Completed-Match privacy (participant Match Story remains privacy-minimised).
- Historical attribution (Correct Match Record, Verified Historical Scorer Attribution).

---

## Historical Scorer / Recovery State

- **Historical Scorer Attribution v1 (CMC-002) is complete** — the exceptional Verified Historical Scorer Attribution pathway is an explicit authorised attestation, not ordinary correction; accepted candidate-discovery evidence is exact Event Audience **or** exact Event Attendance only — **never current Team roster, current Team assignment or Registration**. A verified attribution contributes exactly +1 goal and +1 appearance to that exact Player's Match history and must never fabricate start/substitute status, minutes, Attendance, rating, POTM or an assist. Only the exact verified active goal/scorer receives narrow provenance to suppress its specific outside-selection Data Quality warning.
- **Two correctness fixes landed in the same arc** (`2cbae72`, `7d3caa0`, already on `main` before the `2f3dcee` baseline): normal historical eligibility (`historically_eligible_players()`) now uses `effective_selection()` (Selection plus legitimate live-bench admissions), not raw saved Selection alone; Data Quality's recovery-action routing is now a truthful positive allowlist per destination, not a catch-all default to Match Report.
- **Deferred, unchanged, do not restart without separate approval:** Verified Historical Appearance, Verified Historical Assist Attribution, Historical Registration as candidate evidence, reliable effective-dated Team-assignment history, a longer-term unified historical-participation evidence model. See `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s "Historical Match Participation Evidence — Deferred Opportunities".

---

## Current Design-System State

The visual treatment colloquially called "gold" is architecturally the Club's runtime-configured **Accent Colour**:

```
Settings "Accent Colour" -> brand_accent -> --iexel-brand-accent -> --iexel-color-gold -> var(--iexel-gold)
```

`var(--iexel-gold)` is the token to use; never a hardcoded hex. The accepted primary/nested/form/semantic distinction, and the new `.iexel-accent-top-module` reusable primitive, are recorded durably in `MASTER_DEVELOPER_GUIDE.md`'s "Primary Immersive Module Accent Treatment" — do not duplicate that explanation here or re-derive it from source; read that section first.

This batch deliberately did **not** migrate the many already-working accent-top selectors (Team Events, Team Attendance/Statistics, Match Report, Correct Match Record, Event Detail) onto the new primitive — only the confirmed remaining gaps were closed. A future batch could consider that migration if it becomes worthwhile, but it is not currently scheduled.

---

## Known Technical Debt / Validator Caveats

- **Dev-fixture drift, not a product defect:** several DB-integrated Match Mode validators (`validate-match-mode-attendance-live-squad.php`, `validate-match-mode-player-actions.php`, `validate-match-substitution-attendance-eligibility.php`, `validate-live-bench-admission.php`, `validate-match-goal-live-eligibility.php`) assume Person 19 is a genuine current Team-1 Player; on this dev database Person 19 is currently a Team-6 Player. Predates the recent CSS/eligibility batches; produces the identical failure regardless of which of them is run. **Do not change production behaviour or seed data to silence this** — it needs a dev-database fixture correction, not a code change.
- **Stale "changed set" self-checks in some older validators:** `tools/validate-team-attendance-final-polish.php` and `tools/validate-team-workspace-overview-shell-polish.php` (among possibly others) include a `git status`/`git diff --stat` scope-guard hardcoded to their own original batch's expected file list. These fail whenever run against a clean, fully-committed tree, or during any later unrelated batch's uncommitted changes — confirmed by running `validate-team-workspace-overview-shell-polish.php` against a fully clean, committed tree and seeing it still report unrelated files (from `2cbae72`, itself long since committed) as "in the changed set." This is validator technical debt from how these self-checks were authored, not a regression signal. Treat any such failure as informational unless the specific listed files are genuinely part of your own current batch.
- **Known non-blocking validator debt carried forward unchanged** from the 2026-08-29 handover (`validate-prospect-training-conversion.php`, `validate-committee-club-projects.php`, `validate-visual-foundation.php`, `validate-secretary-portal-account-linking.php`) — see `SPRINTS.md`'s "Internal Club Testing Remediation & Final Pre-Merge Validator Hygiene" section.

---

## Deferred Work (unchanged, do not restart without approval)

- Historical Match Participation Evidence opportunities (Verified Historical Appearance, Verified Historical Assist, Registration-as-evidence, Team-assignment-history reliability, unified evidence model) — see above.
- The Release Readiness work described in `DEVELOPMENT_HANDOVER_2026-08-29.md` ("Remaining Release Checklist Work") remains outstanding and unaffected by any of the work in this handover.
- FIN-031 (Low priority, static caret-cursor visual bug — not reproducible in current source, needs fresh Product Owner reproduction) and OS-011 (Medium priority/Polish, Welfare concern-detail hierarchy — genuinely open, cosmetic/non-blocking) remain the only open MVP-scope roadmap items, neither currently promoted as the next batch. See `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s "Recommended next implementation batch" section.

---

## Recommended Next Starting Point

No new confirmed Pre-MVP product decision is currently open (CMC-003 was the last one, and it is now complete). Before selecting a new roadmap-labelled implementation batch:

1. Re-read `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s "Recommended next implementation batch" section for the current state of FIN-031/OS-011 and Release Readiness.
2. Consider whether Release Readiness sign-off work (per `MASTER_DEVELOPER_GUIDE.md`'s "Current Priority") should take precedence over further visual/UX polish.
3. If Product Owner review surfaces a new candidate item, prefer a small source-first verification step before implementing — the same approach that has repeatedly revealed items were already further along (or already complete) than the roadmap recorded (ADM-001/002/003, OS-029/FIN-028/PL-024, and this handover's own Events Card Consistency and Team Availability findings).

**Important "do not restart" notes:**
- Do not re-implement Match Hero Goal-Scorer Presentation (CMC-003) or its eligibility/responsive follow-ups — complete.
- Do not re-audit or re-implement the primary immersive module accent-top treatment for Team Events, Team Attendance/Statistics, Match Report, Correct Match Record or Event Detail — already correct from earlier work, confirmed unaffected by this arc.
- Do not treat Team Availability's header as a remaining gap — audited and confirmed already correctly treated.
- Do not treat Match Recovery or Undo Last Goal as missing or removed — both remain, only the disclosure's border treatment changed.
- Do not implement any of the deferred historical-recovery opportunities without a separate, dedicated approval.
