# Development Handover — 2026-09-03

**Supersedes:** `DEVELOPMENT_HANDOVER_2026-08-29.md`. That document remains in the repository as a historical record of the Internal Club Testing remediation integration; this document carries the resume point forward.

---

## DO NOT START NEW FEATURE DEVELOPMENT WITHOUT READING THIS

This handover's resume point is **documentation is current; the recommended next implementation batch is Match Hero Goal-Scorer Presentation (CMC-003)** — a confirmed Product Owner decision, explicitly classified **Pre-MVP / before Version 1 release**, not Post-MVP. See `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s "Match Hero Goal-Scorer Presentation" and "Recommended next implementation batch" sections before starting it.

---

## Current Git Baseline

- Plugin `main`: `2f3dcee4c8430a39a2e443614cfe8deea6e75dd8` ("feat: add verified historical scorer attribution")
- `origin/main`: `2f3dcee4c8430a39a2e443614cfe8deea6e75dd8` (pushed 2026-09-03)
- Working tree: clean at this checkpoint
- Docs repo (`iexel-club-os-docs`) branch: `main`, clean, unaffected by the plugin-repo work (separate repository)

Prior baseline (`DEVELOPMENT_HANDOVER_2026-08-29.md`): plugin `main` `b2b51eb`. Between `b2b51eb` and `2f3dcee`, the only work merged to plugin `main` is Verified Historical Scorer Attribution v1 (below) — a single controlled commit.

---

## Since the Last Handover: Verified Historical Scorer Attribution v1 (CMC-002)

Implemented, source-validated, browser-accepted, committed and pushed at `2f3dcee`. Full delivery detail: `SPRINTS.md`, section "Verified Historical Scorer Attribution v1 (CMC-002)". Durable architecture/product rules: `MASTER_DEVELOPER_GUIDE.md`, section "Verified Historical Scorer Attribution — Historical Eligibility Direction". Roadmap entry: `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`, Coach Workspace section and Consolidated review log (CMC-002).

In one sentence: an authorised Coach can now recover a genuine historical scorer on a completed Match's active Club goal, through an exceptional, evidence-backed pathway, only when Club OS's normal Tier-1 historical evidence (saved Selection + legitimate live-bench admission) is genuinely absent for that goal — and this is Player-specific and provenance-specific throughout, never a broadening of normal historical eligibility.

**Browser acceptance established:**
- A verified historical scorer can be recovered through the exceptional evidence-backed pathway.
- The Match score remains unchanged.
- The active goal incident receives the verified scorer.
- The Player receives the verified goal, one appearance, and Match-history inclusion.
- No starting/substitute status, minutes, Attendance, rating, POTM or assist is fabricated.
- The exact verified scorer no longer triggers the generic outside-selection Data Quality warning; the two genuine goalkeeper warnings remain.
- Player Match-card statistics remain Player-specific after a browser-acceptance crediting-leak regression was found and fixed (see `SPRINTS.md`).

**What this deliberately does not do** (do not let future work assume otherwise): it does not rewrite saved Match Selection, does not broaden `effective_selection()`, does not make Event Audience/Attendance normal scorer eligibility evidence, does not grant any other Audience/Attendance participant historical eligibility, does not implement a verified assist, and does not implement Verified Historical Appearance.

---

## Known Non-Blocking Validator Debt (carried forward, unchanged)

Unchanged since `DEVELOPMENT_HANDOVER_2026-08-29.md` — none resolved, none newly introduced by CMC-002:

- `validate-prospect-training-conversion.php` — harmless source-shape drift (see prior handover for detail).
- `validate-committee-club-projects.php` — stale exact-literal assertion; underlying invariant still holds.
- `validate-visual-foundation.php` — stale dependency-array assertion after a legitimate branding-controls change.
- `validate-secretary-portal-account-linking.php` — passes; non-fatal `stdClass` conversion warnings only.

None require production, schema or version-constant changes — validator-file hardening only.

## Known Data Reliability Debt (new — recorded during CMC-002)

- **Team-assignment history (`team_assignments.joined_on`/`left_on`) is not currently reliable for historical eligibility decisions.** A read-only audit conducted during CMC-002 found three materially different write paths and a confirmed real-data counter-example (a `joined_on` date recorded 13 days after a Match the same Person is independently evidenced to have attended). Do not use "ever assigned to this Team" as proof of Match-date eligibility anywhere. See `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s "Historical Match Participation Evidence — Deferred Opportunities" (item 4) for the full finding and the future work required before this can change.

---

## Accepted Canonical Product/Data Decisions (unchanged, preserve)

All decisions recorded in `DEVELOPMENT_HANDOVER_2026-08-29.md`'s equivalent section remain unchanged and are not repeated here. Additionally, from CMC-002:

- Normal historical scorer/assist correction on a completed Match remains Tier-1 evidence only (saved Selection + legitimate live-bench admission via `effective_selection()`). Event Audience and Attendance are not normal historical scorer eligibility evidence.
- Verified Historical Scorer Attribution is an exceptional, Player-specific, provenance-specific pathway — reachable only when Tier-1 is genuinely empty, never a substitute for it, and never broadened into general Match eligibility.

---

## Exact Next Recommended Controlled Action

**Match Hero Goal-Scorer Presentation (CMC-003)** — see `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`. This is a confirmed Product Owner decision, explicitly Pre-MVP / before Version 1 release. It has not been implemented or scaffolded. The Post-v1 deferred opportunities identified during CMC-002 (Verified Historical Appearance, Verified Historical Assist Attribution, Registration-as-candidate-evidence, Team-assignment-history reliability, a longer-term historical-participation evidence model) are explicitly **not** part of this next batch and should not be started without a separate, dedicated approval.

The Release Readiness work described in `DEVELOPMENT_HANDOVER_2026-08-29.md` ("Remaining Release Checklist Work") remains outstanding and unaffected by CMC-002; this handover does not supersede that section's content, only its "Current Git Baseline" and "Exact Next Recommended Controlled Action".
