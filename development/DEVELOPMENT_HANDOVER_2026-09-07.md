# Development Handover — 2026-09-07

**Supersedes:** `DEVELOPMENT_HANDOVER_2026-09-04.md`. That document remains in the repository as a historical record of the point where Match Hero Goal-Scorer Presentation (CMC-003) and the Primary Immersive Module Accent-Top Consolidation had just landed, with no new confirmed Pre-MVP product decision yet open. This document carries the resume point forward.

---

## DO NOT START NEW FEATURE DEVELOPMENT WITHOUT READING THIS

Six further commits have since landed and been accepted, covering Team Events/Attendance and Shared Messages month-disclosure navigation, Coach Workspace Batch B (Statistics chooser, inline availability editing, return-to-context), Live Match transient success notice auto-dismiss, and — the largest of the six — **Event Builder Productivity & Training Only Event Audience Eligibility**. **Do not restart or re-scope any of this work.** See "Recently Completed" below and `SPRINTS.md` for full delivery detail.

There is currently **no new confirmed Pre-MVP product decision** to start next. See "Recommended Next Starting Point" at the end of this document.

---

## Current Git Baseline

- Plugin `main`: `1c97ebbd55854ccc7343419acf498ec0fca8cfdf` ("feat: improve event builder productivity and audience eligibility")
- `origin/main`: `1c97ebbd55854ccc7343419acf498ec0fca8cfdf` (pushed, confirmed via fetch)
- Working tree: clean at this checkpoint
- Docs repo (`iexel-club-os-docs`) branch: `main`, clean at `ffc5f2bbf7b6786bf6620dc074530648253e5dc6` ("docs: reconcile post-match-mode development state") immediately prior to this documentation checkpoint — this batch's own docs commit is not yet made; the Product Owner/lead developer will review this reconciliation before it is committed

Prior baseline (`DEVELOPMENT_HANDOVER_2026-09-04.md`): plugin `main` `5616f8b`. Between `5616f8b` and `1c97ebb`, the plugin `main` history is (newest first):

```
1c97ebb  feat: improve event builder productivity and audience eligibility
fc9dc8a  feat: improve shared messages navigation and presentation
22a18fd  fix: auto-dismiss live match success notices
a9c5dc7  fix: close out coach workspace release readiness
e796f19  fix: polish coach workspace release readiness
082e418  feat: add month navigation to season history
5616f8b  fix: unify branded trim on immersive modules        (prior baseline)
```

---

## Recently Completed (since the 2026-09-04 handover)

### 1. Team Events & Attendance Month-Disclosure Navigation — `082e418`

Team Past Events and Completed Attendance Registers now group history by calendar month (latest month open, older months collapsed) via a new, small reusable `MonthDisclosureGrouping` helper, replacing the earlier fixed-batch-size "load more" disclosure. Upcoming Events is deliberately unaffected. Full detail: `SPRINTS.md`, "Team Events & Attendance Month-Disclosure Navigation".

### 2. Coach Workspace Release-Readiness Polish — `e796f19`

The Event Builder's Venue Type radios now use the same card-row visual language as the Audience Mode radios (resolves the roadmap's former "Venue Control Presentation" item — see `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`, now marked Complete). Matchday Selection cards gained an optional formation-code badge. Several other components received small, mechanical, presentation-only touch-ups. Full detail: `SPRINTS.md`, "Coach Workspace Release-Readiness Polish".

### 3. Coach Workspace Batch B — `a9c5dc7`

- A dedicated Statistics landing/Team chooser (`PortalCoachStatisticsChooserPage`) for a Coach/Manager who manages more than one Team.
- The former standalone "Update player availability" dropdown is replaced by an inline per-Player editor directly inside the existing Team Responses list — same canonical write path (`update_player_availability_as_coach()`), same eligibility source, new presentation entry point only.
- Event lifecycle actions and the new inline availability write now redirect back to the specific section the Coach just acted on (`ContextAnchor`), not the top of the page.

Full detail: `SPRINTS.md`, "Coach Workspace Batch B — Statistics Navigation, Inline Availability Editing & Return-to-Context".

### 4. Live Match Transient Success Notice Auto-Dismiss — `22a18fd`

A live Match Mode success notice now clears itself (and its query-string parameters) after ~5 seconds. Error/warning notices are never touched by this script, and the page remains fully correct if the script does not run. Full detail: `SPRINTS.md`, "Live Match Transient Success Notice Auto-Dismiss".

### 5. Shared Messages Month-Disclosure Navigation — `fc9dc8a`

The shared Messages/Club Announcements history now uses the same month-disclosure grouping as Team Events/Attendance (item 1 above) — same helper, same convention, latest month open. Individual conversation/announcement detail is not month-grouped. No unread counts, filtering, search or pagination were introduced. Full detail: `SPRINTS.md`, "Shared Messages Month-Disclosure Navigation".

### 6. Event Builder Productivity & Training Only Event Audience Eligibility — `1c97ebb`

The largest of the six, delivered across several Product Owner acceptance rounds:

- **Optional End Time**, **safe non-Match Duplicate Event** (including **cross-Team destination** re-authorisation and audience re-derivation), and **weekly independent recurring Events** (server-capped at 12, no recurrence-series entity) are now available in the Team Event Builder.
- **Training Only Players can now be deliberately included in appropriate Event audiences** — both "Current Team + Same Age Group Players" and "Selected Players" surface a clearly separated Training Only candidate group, sourced entirely from the canonical Training Membership record. **No Team Assignment is ever created for a Training Only Player** — this remains true throughout.
- **League/Fixture competitive eligibility is unchanged and unweakened.** Training Only candidates are excluded from the Fixture audience/selection path specifically; a Coach may deliberately admit a Training Only Player to an appropriate **Friendly** (the full downstream Match Selection/lineup/Live Match lifecycle then works normally for that legitimately-admitted Player); Tournament remains a plain Event workflow with no Match Selection/lineup path to reach at all.
- RSVP and Attendance both work correctly for a legitimately admitted Training Only recipient, via the existing canonical paths (no duplicate system introduced).
- A separate, unrelated bug (Selected Players' first row rendering a blank name) was found and fixed in the same batch using Club OS's existing `?? 'Player'` fallback convention — root-caused to a pre-existing orphaned `team_assignments` row (Person 176) with no corresponding `people` row, which remains an **open data-integrity follow-up**, not resolved by this batch.
- A genuine 320px responsive overflow bug in the new Training Only row was found (a classic flex `min-width: auto` + `white-space: nowrap` badge interaction) and fixed.

**Do not restart or re-implement any of the above.** Full, precise, source-verified delivery detail — including the exact Fixture/Friendly/Tournament rule, which must not be summarised as either "Training Only can never play Matches" or "Training Only is eligible for all Matches" — is in `SPRINTS.md`'s "Event Builder Productivity & Training Only Event Audience Eligibility" section, and in `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s Coach Workspace section (which also reconciles a now-superseded 2026-08-14 statement that Coach Training Only visibility was "NOT CURRENTLY VISIBLE").

---

## Current Training Only Product Rule (read this before touching Training Only anywhere)

Training Membership remains the **sole and canonical** representation of Training Only participation: Player identity + an active Training Membership + no active competitive Player Team Assignment. This model is unchanged by the recent work.

What **has** changed: Training Only Players are no longer invisible to authorised Coach Event-audience surfaces. Specifically:

- **Event audiences (Training, Tournament, Friendly):** a Training Only Player scoped to the relevant Team's current age group and Season may be deliberately included, via either "Current Team + Same Age Group Players" or "Selected Players". Inactive, previous-Season, wrong-age-group and fabricated Person IDs are all excluded. No Team Assignment is created merely to make this possible.
- **Fixture (League/competitive):** unchanged — normal competitive eligibility protections remain in full force. A Training Only Player is **not** eligible for a Fixture's audience/selection, and this cannot be bypassed by Event-audience UI changes.
- **Friendly:** an authorised Coach **may** deliberately select an otherwise-valid Training Only Player. This is event-specific participation eligibility, not a change to registration/competitive eligibility — it does not create a Team Assignment, does not change Training Membership status, and does not convert the Player to competitive registration.
- **Tournament:** currently a plain Event workflow (no Match Selection/lineup/Live Match path exists for it at all in current source) — Training Only participation here is governed entirely by ordinary Event-audience rules, same as Training.
- **Downstream Match lifecycle:** once a Training Only Player is legitimately selected into a Friendly's Match Selection, the existing saved-selection state (not a live re-check of registration status) carries them through lineup, Matchday Hub and Live Match — including Goal Scorer/Assist eligibility — exactly as for any other Player.

**Do not describe this as "Training Only can never play Matches."** **Do not describe this as "Training Only is eligible for all Matches."** Both are wrong. The precise rule is the type-aware distinction above.

---

## Current Coach Workspace State

Recently closed out (do not treat as remaining gaps):

- Dedicated Statistics navigation/Team chooser for multi-Team Coaches.
- Inline Team Responses availability editing (replacing the old standalone dropdown).
- Return-to-context redirects after Event lifecycle actions and inline availability writes.
- Live Match transient success notices auto-dismiss after ~5 seconds.
- Venue Type radio visual polish (former "Venue Control Presentation" roadmap item).
- Event Builder productivity (optional End Time, Duplicate/cross-Team Duplicate, weekly recurrence) and Training Only Event-audience support (see above).

**Not claimed as resolved:** this is not "every Coach technical-debt item resolved." See "Known Technical Debt / Validator Caveats" below and `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s Coach Workspace section for anything not listed here.

---

## Current Shared Messages State

- One shared, recipient-based Messages/Club Announcements experience remains canonical (per `MASTER_DEVELOPER_GUIDE.md`'s "Channel-Neutral Communications" rule) — no role-specific Messages store or second Communications architecture was introduced.
- Long announcement history now uses the same month-disclosure grouping as Team Events/Attendance: latest month opens, older months collapse.
- Individual conversation/announcement detail was **not** month-grouped.
- Announcement previews preserve meaningful text structure.
- Presentation uses the established premium midnight-navy/accent-top card language.
- **No new unread-state model, filtering, search or pagination was introduced.** Do not describe any of these as delivered.

---

## Known Technical Debt / Validator Caveats

- **Dev-fixture drift, not a product defect (carried forward unchanged from 2026-09-04):** several DB-integrated Match Mode validators assume Person 19 is a genuine current Team-1 Player; on this dev database Person 19 is currently a Team-6 Player. This also blocks `tools/validate-match-goal-live-eligibility.php` from running end-to-end even after this batch's own extension to it — confirmed via `git stash` that the failure predates and is unrelated to this batch's changes. The new Selected-Players/League-Friendly checks added to that file were verified correct in isolation (extracted and run standalone). **Do not change production behaviour or seed data to silence this** — it needs a dev-database fixture correction, not a code change.
- **`tools/validate-team-events-badge-mobile-repair.php`** has a separate, also pre-existing, unrelated breakpoint assertion failure (`.iexel-team-event-past-meta` at 480px) — confirmed via the same `git stash` technique to predate the Event Builder batch entirely.
- **Person 176 orphaned Team Assignment** — an active `team_assignments` row referencing a `person_id` with no corresponding `people` row (found while fixing the Selected Players blank-name bug). Genuinely open; needs a dev-database data-integrity fix, not a code change. The display-side symptom (a blank name) is fixed; the underlying orphaned record is not.
- **Secretary late-add `EventAudienceBuilder::add_attendee()`/`add_attendees_batch()`** perform no eligibility validation of their own (pre-existing, not introduced by this batch) — a candidate for a dedicated audit if that path is ever extended toward Training Only.
- **Raw Team `age_group` string normalisation** — regular-player same-age-group Team matching (`active_for_age_group()`) still does an exact string match, unlike Training Only matching (which correctly normalises via `AgeGroupKey`). Two Teams spelling the same age group differently would not currently match for the regular-player pool. Not addressed.
- **Secretary has a separate Event-creation architecture** (`PortalSecretaryEventAddPage.php`) that Cross-Team Duplicate was deliberately not built into — see `SPRINTS.md`'s Known debt section for that batch.
- **Stale "changed set" self-checks in some older validators** and **known non-blocking validator debt** — both carried forward unchanged from the 2026-09-04 handover (`validate-team-attendance-final-polish.php`, `validate-team-workspace-overview-shell-polish.php`, `validate-prospect-training-conversion.php`, `validate-committee-club-projects.php`, `validate-visual-foundation.php`, `validate-secretary-portal-account-linking.php`) — see `SPRINTS.md` for detail on each.
- Pre-existing, explicitly untouched items: the `venue_mode` PHP warning noted during SEC-008 acceptance; duplicated `public.css` rule blocks; the unused `EventRepository::duplicate()` method.

---

## Deferred Work (unchanged, do not restart without approval)

- Historical Match Participation Evidence opportunities (Verified Historical Appearance, Verified Historical Assist, Registration-as-evidence, Team-assignment-history reliability, unified evidence model) — unchanged since 2026-09-04.
- The Release Readiness work described in `DEVELOPMENT_HANDOVER_2026-08-29.md` ("Remaining Release Checklist Work") remains outstanding and unaffected by any of the work in this or the prior handover.
- FIN-031 and OS-011 remain the only open MVP-scope roadmap items, neither currently promoted as the next batch — unchanged since 2026-09-04. See `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s "Recommended next implementation batch" section.
- The data-integrity items in "Known Technical Debt" above (Person 176, raw age_group normalisation, Secretary late-add eligibility audit) are genuinely open but are data/validator hygiene items, not product features — do not silently fold them into a future feature batch without calling them out explicitly.

---

## Recommended Next Starting Point

No new confirmed Pre-MVP product decision is currently open. There is no already-authorised next implementation batch — **the next task should be selected from the remaining MVP/Release-Readiness priorities below, not invented.**

1. Re-read `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s "Recommended next implementation batch" section for the current state of FIN-031/OS-011 and Release Readiness.
2. Consider whether Release Readiness sign-off work (per `MASTER_DEVELOPER_GUIDE.md`'s "Current Priority") should take precedence over further visual/UX polish.
3. Consider whether the Person 176 data-integrity item (a dev-database fixture issue, not a product defect) warrants a small, separate, explicitly-scoped fix before it is forgotten.
4. If Product Owner review surfaces a new candidate item, prefer a small source-first verification step before implementing — the same approach that has repeatedly revealed items were already further along (or already complete) than the roadmap recorded.

**Important "do not restart" notes:**
- Do not re-implement optional End Time, Duplicate Event, cross-Team Duplicate, or weekly recurring Events — complete.
- Do not re-implement Training Only Event-audience support for either "Current Team + Same Age Group Players" or "Selected Players" — complete, and do not weaken the accompanying Fixture/League eligibility protection while doing so.
- Do not re-implement the Coach Statistics chooser, inline availability editing, or return-to-context redirects — complete.
- Do not re-implement Live Match transient success notice auto-dismiss — complete.
- Do not re-implement Team Events/Attendance or Shared Messages month-disclosure navigation — complete.
- Do not treat the former "Venue Control Presentation" roadmap item as outstanding — resolved.
- Do not restart or re-audit the primary immersive module accent-top treatment, Match Hero Goal-Scorer Presentation, or any Historical Scorer Attribution work — all remain complete from the prior handover, unaffected by this arc.
- Do not treat Person 176's orphaned record as anything other than a data-integrity follow-up — it is not a product feature gap and does not block any of the work described above.
