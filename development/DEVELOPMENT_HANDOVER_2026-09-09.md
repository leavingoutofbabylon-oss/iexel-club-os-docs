# Development Handover — 2026-09-09

**Supersedes:** `DEVELOPMENT_HANDOVER_2026-09-08C.md`. That document remains in the repository as a historical record of the point where Staff Compliance Batch D had just landed and no Release Candidate work had yet begun. This document carries the resume point forward through the complete MVP Release Candidate validation cycle.

---

## DO NOT START NEW FEATURE DEVELOPMENT WITHOUT READING THIS

Since the previous handover, three further commits have landed — all release-candidate defect repairs discovered and closed during a structured RC validation cycle, not new feature work:

- `a197abdd68d824890968ae0a5726e0cd0148273c` — "fix: correct portal success response status" (RC-01)
- `73c576762d5340ddc0cfa8c12d840b1ee10b31b7` — "fix: handle missing current season in team workspace" (RC-02A-R1)
- `3ee4c92963e8721b5562aa3a64e3706f81a346dc` — "fix: return forbidden status for restricted portal access" (RC-03-R1)

**The MVP Release Candidate validation cycle is now complete. Product Owner manual sign-off has PASSED.** See "MVP Release Candidate — Final Status" below.

**Do not restart or re-scope any of RC-01, RC-02A, RC-02A-R1, RC-02B, RC-03, RC-03-R1, or RC-03-CLOSE.** Do not invent an "RC-04." Do not treat this as production deployment — see "What this does and does not mean" below.

---

## Current Git Baseline

- Plugin `main`: `3ee4c92963e8721b5562aa3a64e3706f81a346dc` ("fix: return forbidden status for restricted portal access")
- Plugin status: **clean** — verified via `git status --short` returning nothing and `git rev-parse HEAD` matching the commit above; `origin/main` confirmed at the same commit
- Docs starting baseline for this reconciliation: `main` at `db1caebef423a212f01a686f4086a2837a674994` ("docs: record staff compliance expiry alerts"), clean — this reconciliation's own docs commit is not yet made; the Product Owner/lead developer will review before it is committed
- Prior plugin baseline (`DEVELOPMENT_HANDOVER_2026-09-08C.md`): `2bdd62e536beec27f0fec663db710efa93fb59e9`
- RC cycle checkpoints, in order:
  - RC-01 (portal successful-response HTTP-status correction): `a197abdd68d824890968ae0a5726e0cd0148273c`
  - RC-02A-R1 (no-current-Season Team Workspace fatal repair): `73c576762d5340ddc0cfa8c12d840b1ee10b31b7`
  - RC-03-R1 (Access-restricted HTTP-status correction): `3ee4c92963e8721b5562aa3a64e3706f81a346dc`

RC-02A, RC-02B and RC-03 themselves were validation-only tasks against disposable environments and made no plugin/docs commits of their own — their findings are recorded here and in `SPRINTS.md`, but the only git checkpoints they produced are the three repair commits above.

## Current Phase

**MVP Release Candidate technically validated; Product Owner manually signed off.** This is the phase transition this handover records. See "What this does and does not mean" below for the precise, non-speculative reading of that statement.

---

## MVP Release Candidate — Final Status

### What this does and does not mean

The current build (plugin `3ee4c92963e8721b5562aa3a64e3706f81a346dc`) has:

- **ZERO evidenced P0 release blockers**
- **ZERO evidenced unresolved P1 release blockers**
- **Product Owner manual sign-off: PASSED**

This means: **the MVP Release Candidate is technically validated and Product Owner accepted.** It does **not** mean Club OS has been deployed to production, that a release tag/branch has been cut, or that any of the `RELEASE_CHECKLIST.md` "Release"/"Post-Release" steps have occurred — those remain a distinct, separate project step and no evidence in this cycle claims otherwise. See `RELEASE_CHECKLIST.md` for the current state of that separate gate.

### The validation cycle, in order

1. **Targeted Release Readiness assessment** (pre-RC) — read-only audit; found no currently-known unresolved High/MVP implementation blocker; identified two P1-candidate leads that became RC-01 and RC-02A-R1's origin points (a systemic-looking missing `status_header(200)` on `PortalRouter`'s successful-render path, and a stale post-Batch-D install/upgrade re-validation gap).

2. **RC-01 — Portal successful-response HTTP-status correction.** Commit `a197abd`. `PortalRouter::render()` previously could reach its successful-render output with WordPress's earlier-resolved HTTP status (frequently a stale 404 carried over from degraded/plain-permalink rewrite resolution) still in effect, rather than an authoritative 200. Fixed by adding `ob_start(); status_header(200);` at the point a legitimate route begins rendering its success output, with `ob_end_flush()` at the true end of `render()` so any later, genuine `wp_die()`/`status_header()` call from a dispatched page or an explicit not-found branch can still correctly override the optimistic 200 before the buffer flushes. The final "Page not found" branch explicitly re-asserts `status_header(404)`. No authorization, capability, or workspace behaviour changed; the successful Welfare compliance response body was confirmed byte-identical before and after. Live HTTP-tested against real WordPress auth cookies: every legitimate route across Secretary, Welfare, Treasurer, Coach and Parent personas returned 200, while an unmatched section, an ineligible/nonexistent target Person, a wrong-persona request and an unauthenticated request all continued to return their original 404/403/400/302 — none were normalised to 200. `tools/validate-plain-permalink-portal-routing.php` extended 55 → 64.
   - **Important nuance preserved:** the original investigation observed that the long-lived normal Dev site's compiled `rewrite_rules` option was stale for some newer multi-segment routes. RC-02A subsequently proved this was **not** a systemic fresh-install defect — a true fresh activation correctly compiles the full current rewrite-rule set (confirmed: 106 `club-os` rules present, including the newer Secretary/Welfare People/Compliance routes, before any manual flush). The stale-rule condition is specific to a site not reactivated since those routes were added, a distinct and separate concern from anything RC-01 or RC-02A addressed, and remains relevant background for any future controlled-upgrade investigation rather than something fixed in this cycle.

3. **RC-02A — Clean-install validation.** Read-only-of-source validation task on a disposable **IEXEL Club OS Dev RC Clean** site (WordPress 7.1, PHP 8.2.29, MySQL 8.4.0, nginx — deliberately not downgraded to match the historical WP 7.0.4 reference). Confirmed: genuine clean WordPress baseline with no pre-existing Club OS state; normal `activate_plugin()` succeeds; schema/data version `2026.08.9`/`2026.08.9`; `UpgradeRunner` healthy and current across all 36 registered steps; Staff Compliance table installed correctly with the current capability model correctly scoped (no broadening); zero bogus credentials manufactured; administrative authority does not synthesize member identity (the unlinked default administrator resolves no member experience); 15 system formations, 129 formation slots; current rewrite rules compiled correctly on normal activation, including representative newer Secretary/Welfare nested routes; 3-pass reconciliation idempotent; deactivate/reactivate lifecycle healthy with no duplication.
   - **Table inventory note (P2, unfixed):** the actual live database contains **51** `iexel_os_*` tables; `DatabaseManager::CANONICAL_TABLES` currently enumerates **49**. The two extras (`current_emergency_contacts`, `event_match_live_bench_admissions`) are legitimate, correctly-created, correctly-populated tables simply missing from that inventory list, which feeds the plugin's own built-in Release Readiness table-count check. This is a tooling-completeness gap, not a schema defect, and remains open — **do not claim it is fixed.**
   - **One genuine P1 was found during this pass** — see RC-02A-R1 immediately below.

4. **RC-02A-R1 — No-current-Season Team Workspace fatal repair.** Commit `73c5767`. On a genuinely fresh installation, `SeasonRepository::create()` defaults every new Season to `is_current = 0` — the unremarkable, default state of any club's first Season before a Secretary/Admin explicitly marks one current. `TeamWorkspacePage::render()` passed `SeasonContext::season_id()`'s nullable `?int` result directly into `MemberPortalService::team_viewer_mode()`'s non-nullable `int $season_id = 0` parameter, producing an uncaught `TypeError` (HTTP 500) on `/club-os/teams/{id}/` whenever no Season was current. Root-caused and proven precisely by reproducing and resolving the fatal purely via test-data (`UPDATE seasons SET is_current = 1`), with zero code change to reproduce.
   - **Repair semantics (proven, not merely asserted):** `0` was already `team_viewer_mode()`'s own established safe "no explicit Season / resolve current" sentinel — when no current Season exists, `team_viewer_mode(..., 0)` already resolved to an empty (`''`) viewer mode rather than selecting any historical/arbitrary Season data; Team Workspace already contained a complete no-current-Season context/warning/empty-state architecture (`$has_context`, `$read_only`, the `missing_current_season` warning, `render_context_notices()`) that had simply never been reachable because the fatal occurred first. The repair normalized only the one confirmed call site: `$context->season_id() ?? 0`. No Season is automatically created. No Season is automatically made current. No historical Season fallback was introduced. Authorization did not broaden — Club Admin/Coach `'manager'` resolution still occurs before any Season check, unchanged.
   - **Product Owner manually accepted** the no-current-Season Team Workspace state (warning card visible, no current-season badge, coherent layout, verified at 320px/390px, no regression to the current-Season path).
   - The existing warning copy — "Season configuration warning" / "No canonical current Season is configured." — is unchanged and remains **minor future UX polish only, not a release blocker.**
   - `tools/validate-team-workspace-route-and-display.php` extended 29 → 39.

5. **RC-02A deferred latent finding (P2, unfixed, recorded only).** `TeamStatisticsService.php:203`, inside `authorisedPlayerHubTeam()`, contains a structurally identical unguarded `SeasonContext::season_id()` → `team_viewer_mode()` pattern to the one repaired above. It is **not independently reachable today**: its only two callers (`TeamWorkspacePage.php:486` and `:713-714`) already short-circuit on `$has_context` before ever invoking it, and `$has_context` is false in exactly the same no-current-Season state that would make `season_id()` null. It was **not** responsible for the RC-02A P1 and was **left deliberately untouched** by RC-02A-R1's narrow repair scope. Classify as deferred latent hardening debt / P2 unless a future caller reaches it without that guard.

6. **RC-02A closure revalidation.** Reconfirmed the RC-02A-R1 repair live on RC Clean: no-current-Season `/club-os/teams/{id}/` → HTTP 200 with the warning card, no fatal; current-Season path unaffected; both states verified with zero new PHP errors/warnings.

7. **RC-02B — Supported existing-club upgrade validation.** Read-only-of-source validation on a disposable **IEXEL Club OS Dev RC Upgrade** site. Chosen pre-upgrade baseline: commit `d8d9607` ("Add canonical completed match goal removal"), schema/data version `2026.08.6` — the last genuine commit at that exact version before the `2026.08.7` bump (confirmed via `git log -S` pickaxe search and adjacency to the version-bump commit with zero intervening commits), a genuine ancestor of Staff Compliance Batch A, and the established pre-Staff-Compliance state already referenced elsewhere in this documentation as the historical Environment 1/Environment 2 baseline.
   - A representative existing-club fixture was created at that baseline using only legitimate production writers: an active/current `2026/27` Season, a Team/TeamSeason, a Coach, a Player, a Parent relationship, Team assignments, an Event, an availability response, a Finance invoice/line, a Welfare concern, and a Player Operational Medical/Safety record.
   - The plugin files were then replaced in-place with the current committed build (no deactivation, no database reset) and the real production upgrade path invoked (`UpgradeAdminController`'s `UpgradeRunner::run('administrator')`, the same mechanism a real "Run Club OS database upgrade" admin-notice button triggers).
   - **Result:** schema/data reached `2026.08.9`/`2026.08.9`; all 36 current `UpgradeStep` invariants valid; Staff Compliance table created correctly with zero bogus credentials and the correct capability distribution (no broadening — identical to the clean-install distribution); every representative fixture record survived **field-for-field**, row-for-row; the current Season remained current; Team/Season continuity was preserved at both the database and rendering level (`Team Workspace` correctly resolved the same Team/Season post-upgrade); no automatic Season rollover; no duplicate TeamSeason; no silent data loss; no ownership reassignment.
   - **Idempotence nuance (self-healing behaviour confirmed, not a defect):** a second `UpgradeRunner` run, executed immediately after linking a new WP admin account to an existing Coach-assignment-holding Person (a state change introduced for smoke-testing, not part of the upgrade itself), correctly detected the resulting capability drift (`TeamStaffOperationalAccessBackfill::is_valid()` found the newly-linked, now-qualifying account lacked its direct assigned-Team capability) and correctly re-applied to repair it. A **third, genuinely clean run** with no intervening state change returned `already_current` with zero steps executed, as expected. This is the reconciliation architecture working exactly as designed — proof of self-healing, not an idempotence defect.

8. **RC-03 — Final representative persona validation.** A representative, not exhaustive, end-to-end pass across Club Admin, Secretary, Welfare, Treasurer, Coach/Manager, Parent/Guardian, Player, shared Messages/Events/Availability, Staff Compliance, sensitive-workspace boundaries, direct-route negative testing and representative HTTP-status testing, using genuinely single-persona non-admin test accounts throughout (to avoid the admin-capability-superset confound documented in prior RC work). Validated security behaviour included: administrative authority does not synthesize member identity; Secretary cannot enter Welfare-only routes and vice versa; Parent cannot access a non-linked child; Player cannot access another Player's data; a non-Finance persona cannot reach Treasurer routes; unauthorized Staff Compliance management is denied; an invalid/nonexistent target returns the correct error; an unauthenticated portal request redirects appropriately. **Do not describe RC-03 as an exhaustive re-test of every possible user journey** — it is the representative final RC pass, and it found the one P1 described next.

9. **RC-03 P1 → RC-03-R1 — Access-restricted HTTP-status correction.** Commit `3ee4c92`. RC-03 live-reproduced that a genuinely non-admin Coach/Manager with no valid assignment to an existing Team, requesting that Team's Workspace, received the correct "Access restricted" denial *content* but at **HTTP 200** rather than 403 — the same optimistic status RC-01 established for the successful-render path was leaking through this one unprotected denial branch. A narrow source-and-runtime audit of `PortalRouter.php` found the identical, unprotected pattern in **12 further** inline "Access restricted" denial branches sharing the same `can_manage_team()`/`can_view_team()`/`can_view_event()` shape (Event detail, Event Attendance, and ten Match-Mode/Event-management sections: matchday, live, report, correction, lineup, goal, substitution, goalkeeper, match-details, and audience/edit).
   - **Repair scope: all 13 branches, independently live-verified pre-fix and post-fix.** Each was deployed against the pristine pre-fix build (reproducing the HTTP 200 + "Access restricted" defect), then against the patched build (confirming HTTP 403 with the identical, unmodified denial body), with legitimate authorized access to the same 13 routes reconfirmed unaffected (200 throughout) and zero new PHP errors/warnings logged at any point.
   - **The production correction consisted only of thirteen explicit `status_header( 403 );` calls plus explanatory comments** — no denial content/markup changed, no authorization logic changed, no capability logic changed, no route matching changed, no CSS/UI copy changed.
   - **`PortalFinanceWorkspacePage::restricted()` was audited and deliberately left unchanged.** Every reachable Finance section already receives an authoritative `wp_die(...,403)` from `PortalRouter`'s own Finance gate before the page class is ever instantiated, and the underlying `iexel_club_treasurer` WP role grants `iexel_view_finance`, `iexel_manage_finance` and `iexel_manage_billing` together as one fixed, atomically-applied bundle — there is no real-world path to hold the first without the others, so its internal `restricted()` calls are genuinely unreachable via normal routing. Do not "fix" this without new evidence it is actually reachable.
   - `tools/validate-plain-permalink-portal-routing.php` extended 64 → 91 (the same file RC-01 had already extended to 64).

10. **RC-03-CLOSE — Closure revalidation.** Reconfirmed all 13 corrected branches live on the committed `3ee4c92` build: every denial → 403 with unchanged content and no data leakage; every authorized equivalent → 200; unauthenticated → existing redirect; invalid/nonexistent target → existing 400/404; unknown route → existing 404; all focused and regression validators passing at their established totals; zero new runtime errors. **Verdict: RELEASE CANDIDATE PASS.**

11. **Product Owner manual sign-off: PASSED.** Completed after RC-03-CLOSE, against the final `3ee4c92` build.

---

## Final Validator Evidence (current accepted totals)

| Validator | Total |
|---|---|
| `validate-plain-permalink-portal-routing.php` | 91/91 |
| `validate-team-staff-operational-access.php` | 55/55 |
| `validate-committee-permissions.php` | 105/105 |
| `validate-team-workspace-route-and-display.php` | 39/39 |
| `validate-player-season-journey.php` | 29/29 |
| `validate-player-season-stats.php` | 112/112 |
| `validate-staff-compliance-foundation.php` | 108/108 |
| `validate-staff-compliance-secretary-ui.php` | 98/98 |
| `validate-welfare-people-compliance.php` | 123/123 |
| `validate-welfare-workspace-batch1.php` | 118/118 |
| `validate-secretary-people-foundation.php` | 81/81 |
| `validate-secretary-mobile-responsive.php` | 138/138 |
| `validate-admin-person-role-dependency-guards.php` | 91/91 |
| `validate-admin-person-role-sync.php` | 54/54 |
| `validate-workspace-priority-alert-scoping.php` | 114/114 |
| `validate-welfare-dashboard-summary-sql.php` | 28/28 |

This list is **not** a claim that every repository validator is globally green — see "Known Technical Debt / Validator Caveats" below for known baseline/deferred validator debt that predates and is unrelated to this RC cycle and remains open.

---

## Known Current Staff Compliance State

Unchanged from `DEVELOPMENT_HANDOVER_2026-09-08C.md` — carried forward verbatim, since no RC-cycle commit touched Staff Compliance source:

- ✅ Staff Compliance canonical domain — **implemented**, `b5f006a6`.
- ✅ Secretary Staff Compliance management — **implemented**, `3352d300`.
- ✅ Restricted Welfare People/Person/Compliance projection — **implemented**, `cd871f3`.
- ✅ Secretary-vs-Welfare workspace mirror boundary — **implemented and proven live**, `cd871f3`.
- ✅ Compliance expiry alerts — **implemented**, `2bdd62e`.
- ✅ Re-confirmed structurally intact and correctly scoped across RC-02A (clean install), RC-02B (upgrade), and RC-03 (representative persona pass) — no Staff Compliance source was touched by any RC-cycle commit.
- **No further Staff Compliance batch is currently approved future direction.** Do not begin any of the previously-listed out-of-scope ideas (missing-compliance alerting, configurable threshold, qualification catalogue, notification-channel delivery, attachments, etc.) without a fresh, explicit Product Owner decision. **Do not invent a "Batch E."**

---

## Known Technical Debt / Validator Caveats

Carried forward unchanged from `DEVELOPMENT_HANDOVER_2026-09-08C.md`, plus RC-cycle-specific additions:

- **`DatabaseManager::CANONICAL_TABLES` 49-vs-51 inventory gap** (new, RC-02A) — actual live table count is 51; the constant lists 49; the two missing entries (`current_emergency_contacts`, `event_match_live_bench_admissions`) are legitimate tables simply absent from the inventory feeding the plugin's own Release Readiness table check. P2, tooling-completeness only. Not fixed.
- **`TeamStatisticsService.php:203` latent nullable-Season pattern** (new, RC-02A) — structurally identical to the repaired RC-02A-R1 defect but not independently reachable today (both its callers guard on `$has_context`). P2 deferred hardening debt. Not fixed.
- **CRLF source-validator methodology note** (new, RC-02A) — `git archive`-based export on a Windows host with `core.autocrlf=true` converts LF to CRLF, which caused one whitespace-literal validator (`validate-welfare-people-compliance.php`) to falsely fail when run against an *exported* copy while passing 123/123 against the canonical checkout. This is a validation-methodology note, not a source or runtime defect — future RC work should run source-literal validators against the canonical checkout, not a `git archive` export, on Windows hosts.
- No-current-Season warning copy ("Season configuration warning" / "No canonical current Season is configured.") — unchanged, minor future UX polish only, not a release blocker.
- **DevTools 404 status-code observation on the Welfare compliance destination page** — content renders and functions correctly; not investigated or fixed; genuinely open, deferred.
- **`tools/validate-current-emergency-contact.php`** — pre-existing, unrelated schema/data-version assertion failure, repeatedly re-confirmed via `git stash` across multiple prior batches to reproduce identically at baselines with none of the intervening work applied. Not caused by, and not repaired by, the RC cycle.
- Dev-fixture drift, not a product defect: several DB-integrated Match Mode validators assume Person 19 is a genuine current Team-1 Player; on the normal Dev database Person 19 is a Team-6 Player.
- **`tools/validate-team-events-badge-mobile-repair.php`** — pre-existing, unrelated breakpoint assertion failure (`.iexel-team-event-past-meta` at 480px).
- **`tools/validate-visual-foundation.php`** — pre-existing, unrelated `"Public stylesheet dependency order changed."` failure.
- **`validate-team-workspace-overview-shell-polish.php`** — a pre-existing, batch-specific git-status hygiene gate that hardcodes an already-committed historical batch's expected diff; it fails whenever *any* file is dirty in the working tree, independent of and unrelated to RC-cycle correctness (reconfirmed via `git stash` to fail identically on the untouched clean baseline). Not a regression, not fixed.
- **Person 176 orphaned Team Assignment** — an active `team_assignments` row referencing a `person_id` with no corresponding `people` row. Genuinely open; needs a dev-database data-integrity fix, not a code change.
- Secretary late-add `EventAudienceBuilder::add_attendee()`/`add_attendees_batch()` perform no eligibility validation of their own.
- Raw Team `age_group` string normalisation; Secretary's separate Event-creation architecture (no Cross-Team Duplicate); the `venue_mode` PHP warning; duplicated `public.css` rule blocks; the unused `EventRepository::duplicate()` method — all pre-existing, explicitly untouched.
- **FIN-031 (Treasurer/Secretary static-caret finding)** — positively classified as browser caret browsing, not a Club OS defect. No plugin change expected.

---

## Deferred / Post-MVP Work (unchanged unless noted, do not restart without approval)

- **Treasurer premium visual treatment** (pale-blue visual pass) — deferred, unchanged. Not a functional blocker.
- **Coach lineup formation-preservation enhancement** — deferred, unchanged.
- **Generic custom formation labels** — deferred, unchanged.
- **Same-context navigation friction** — deferred, unchanged.
- **OS-011** (Welfare Concern Detail hierarchy polish) — remains an open, approved-but-unpromoted MVP-scope polish item.
- The data-integrity items above (Person 176, raw `age_group` normalisation, Secretary late-add eligibility audit) — genuinely open data/validator hygiene items, not product features.
- **DevTools 404/status-code observation** — deferred technical debt, not investigated.
- **`TeamStatisticsService.php:203`, `CANONICAL_TABLES` 49-vs-51, CRLF validator methodology** — new deferred items from this RC cycle, see above.
- Historical Match Participation Evidence opportunities (Verified Historical Appearance, Verified Historical Assist, Registration-as-evidence, effective-dated Team-assignment history) — unchanged, Post-v1.
- **NEW — Guardian Link Role Synchronisation Audit** — see dedicated section below. **Audit/follow-up candidate only, not approved implementation direction.**

Do not restart completed workspace MVP sweeps (Internal Club Testing, Completed Match Correction, Admin Navigation Consolidation, dark-surface contrast, Welfare Workspace Workflows, Staff Compliance Batches A/B/C/D, or any of the RC-01/RC-02A-R1/RC-03-R1 repairs) — all remain complete as recorded here, in `MASTER_DEVELOPER_GUIDE.md`'s "Recently Completed", and in `SPRINTS.md`.

---

## NEW POST-RC FOLLOW-UP: Guardian Link Role Synchronisation Audit

**Classification: POST-RC workflow-integrity / onboarding audit candidate. NOT a release blocker. NOT an approved implementation batch.**

A Product Owner workflow observation, recorded here as an audit candidate only — no behaviour has been changed or decided.

**Observed current/manual workflow:** when manually linking a Person to a Player as Parent/Guardian, the Product Owner appears to need to give that Person the Parent role *first* before they become available/usable in the Guardian linking workflow.

**Product Owner's expected, more natural workflow:**
1. Find/select the Person while linking a Parent/Guardian to a Player.
2. Create the canonical Parent/Guardian → Child relationship.
3. Club OS automatically ensures the adult Person has the appropriate canonical Parent role/identity.
4. The user should not need to pre-assign the Parent role manually.

**A future audit (not started, not scoped as implementation) should determine:**

- A. Current behaviour of manual Guardian Links.
- B. Whether the Parent role is genuinely a prerequisite in the current implementation.
- C. Whether Registration/Prospect onboarding already creates both the parent/guardian relationship and the Parent role together.
- D. Whether Training Membership / youth onboarding already relies on the existing Guardian Links flow.
- E. Whether relationship creation should transactionally ensure the Parent role.
- F. Whether role removal should happen automatically when a link is removed.
- G. If role removal is considered, how to protect a Person who remains guardian to another Player.
- H. Whether the Parent role and the `parent_of`/`guardian_of` relationship must remain distinct domain concepts even if the UI eventually creates them atomically.
- I. Authorization/safeguarding implications.
- J. The canonical service/writer path to extend if a change is eventually approved.

**Product architecture principle to preserve — do not collapse this to simplify the UI:**

> RELATIONSHIP and ROLE are related but distinct concepts. The relationship answers "which child/Player is this adult linked to?" The role/identity contributes to "which Parent/Guardian experience may this Person receive?"

Any future change should extend the canonical People/relationship/role services (`PersonRelationshipRepository`, `PeopleRepository::add_role()`, `OperationalRoleAccessManager`) — never a parallel guardian-link mechanism.

---

## Post-RC Next Development Position

We are no longer in active Release Candidate defect closure. The next development work should be selected deliberately from the approved post-RC backlog / Product Owner priorities — this handover does not select one on its own authority.

Reviewing `SPRINTS.md`, `CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`'s "Recommended next implementation batch" section, and this handover together, the candidates are:

1. **OS-011** (Welfare Concern Detail hierarchy polish, Medium priority) — genuinely open, cosmetic/non-blocking.
2. **Person 176 orphaned Team Assignment** — a small, genuinely open dev-database data-integrity item, not a product feature.
3. **Guardian Link Role Synchronisation Audit** (new, this handover) — an audit, not an implementation batch; would need to run and report before any implementation is scoped.
4. The separate `RELEASE_CHECKLIST.md` "Release"/"Post-Release" gate (tagging, deployment) — a distinct project step from the technical/product validation this handover records, and not itself a development task.

**Product Owner/lead developer prioritisation is needed** to choose between these — none is unambiguously dominant per the authoritative docs. **Do not invent or begin a new implementation batch, an "RC-04," or a Staff Compliance "Batch E" from this handover's description alone.**

**Important "do not restart" notes:**
- Do not re-implement or re-scope RC-01, RC-02A-R1, or RC-03-R1 — all complete and closed.
- Do not re-open RC-02A, RC-02B, or RC-03 as if their findings were still pending — they are recorded above.
- Do not treat the Guardian Link Role Synchronisation Audit as a decided implementation direction — it is an audit candidate only.
- Do not re-implement any item listed as complete in earlier handovers — those documents' "do not restart" notes remain in force unchanged.
