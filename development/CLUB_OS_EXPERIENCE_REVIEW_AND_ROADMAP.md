# IEXEL Club OS Experience Review and Roadmap

Role-based product review, MVP priorities, post-MVP roadmap and future club profiles

## Executive summary

Club OS has reached the stage where the core architecture is strong and the main remaining work is product refinement: role identity, workflow completeness, navigation, visual consistency, accessibility and selective pre-MVP engagement features.

## Workspace scores

| Workspace | Score | Summary |
|---|---:|---|
| Settings / Brand Studio | 9.5/10 | Premium, visual and approachable. Best treated as Brand Studio, with separate operational and system settings. |
| Coach Workspace | 9/10 | The strongest operational experience. Matchday Hub, team workspace, statistics and lineup builder are standout features. |
| Welfare Workspace | 9/10 | Strong safeguarding workspace with concern management, medical overview and emergency information. |
| Committee Workspace | 9/10 | Clear oversight and decision-making experience. Needs fuller operational CRUD because committee users should not depend on wp-admin. |
| Treasurer Workspace | 8.5–9/10 | Feels like a real finance workspace with invoices, payments, billing schedules and bulk family billing. |
| Admin Experience | 8.5/10 | Powerful and comprehensive, but navigation is crowded and long-term role separation needs refinement. |
| Parent Workspace | 8/10 | Solid family hub with events, registrations and communications. Finance and selected-child context need improvement. |
| Player Workspace | 6/10 current | Functionally stable, but needs a stronger identity centred on motivation, progress, achievement and belonging. |

## Role identity

- **Committee:** Run the club.
- **Welfare:** Protect people and keep the club safe and compliant.
- **Coach:** Manage and develop the team.
- **Treasurer:** Run and sustain the club’s finances.
- **Parent:** Stay informed and manage children.
- **Player:** Experience motivation, progress and belonging.
- **Administrator:** Maintain and configure the Club OS platform, not perform every sensitive operational role.

## MVP priorities

- **Global:** Move Quick Actions directly below each workspace hero, using the Coach dashboard as the reference pattern.
- **Global:** Fix blue-on-blue and other low-contrast text through shared design tokens.
- **Global:** Standardise displayed dates to DD-MM-YYYY or DD/MM/YYYY consistently across Club OS.
- **Committee:** Remove duplicate Home / Club Overview navigation.
- **Committee:** Improve registration summary metrics with total registrations, registered this month, awaiting approval and outstanding actions.
- **Committee:** Provide operational create/edit/archive flows for club events, communications and projects because committee users cannot use wp-admin.
- **Coach — complete:** Capture opponent, competition and match location during match-event creation.
- **Coach — complete:** Show authorised emergency contacts in Matchday Hub.
- **Coach:** Open Directions in a new tab without replacing Club OS.
- **Coach — complete:** Allow bench/substitute selection in Lineup Builder and persist it into Matchday Hub and substitution controls.
- **Parent — complete:** Fix selected-child context so an U8 child cannot see an U7 next event, and deliver Parent All-Children event identity + multi-child RSVP.
- **Parent:** Improve Team Hub text contrast.
- **Parent — complete:** Fix selected-child context so an U8 child cannot see an U7 next event, and deliver Parent All-Children event identity + multi-child RSVP.
- **Parent:** Improve Team Hub text contrast.
- **Parent — complete:** Provide a real Finance page with invoice detail and payment history — delivered in Parent Family Finance & Invoice Detail.
- **Notifications:** Improve attachment/image viewing so users can close and return without relying on the browser Back button.
- **Treasurer — complete:** Provide invoice view/edit/cancel/archive or void actions and a proper invoice detail route — delivered in Treasurer Finance MVP.
- **Treasurer — complete:** Allow Treasurer role to manage fee rules and discount policies inside Club OS — delivered in Treasurer Fee Rules & Discount Policies management.
- **Player:** Create a real My Stats page based on the coach player-statistics experience, limited to the logged-in player.
- **Player:** Expand My Season with progress, form, attendance, milestones and next achievement.
- **Player:** Add a lightweight pre-MVP engagement feature such as weekly challenges or personal targets.
- **Admin:** Reorganise the Club OS sidebar into grouped sections and hide route-only detail pages.

## Consolidated review log

| ID | Area | Finding | Type | Priority | Release |
|---|---|---|---|---|---|
| OS-001 | Committee | Duplicate Home and Club Overview navigation | Bug/UX | High | MVP |
| OS-002 | Committee | Registration panel needs stronger operational metrics | UX | High | MVP |
| OS-003 | Committee | Quick Actions should move near the top | UX | High | MVP |
| OS-004 | Committee | Create/edit/archive club events, communications and projects — delivered in Secretary Events, Communications & Command Centre | Resolved workflow | Complete | Sprint 30/32 |
| OS-005 | Committee | Improve dashboard visual hierarchy — delivered in Secretary Command Centre & Portal Navigation | Visual | Complete | Sprint 30 |
| OS-006 | Committee | Projects card feels isolated | Visual | Low | Post-MVP |
| OS-008 | Welfare | Quick Actions should move near the top | UX | High | MVP |
| OS-009 | Welfare | Add edit/archive lifecycle for concerns; deletion heavily restricted | Workflow | Medium | Post-MVP |
| OS-010 | Welfare | Expand into broader compliance workspace | Future feature | Medium | Post-MVP |
| OS-011 | Welfare | Strengthen concern detail hierarchy | Visual/UX | Medium | Polish |
| OS-012 | Welfare | Make directory filters more compact | Visual | Low | Post-MVP |
| OS-016 | Coach | Capture match configuration during event creation — delivered in Portal Event Builder & Secretary Events Management | Resolved gap | Complete | Sprint 30 |
| OS-017 | Coach | Emergency contacts missing from Matchday Hub — exact-season authorised projection delivered | Resolved gap | Complete | MVP Experience Polish |
| OS-018 | Coach | Directions opens in same browser tab | Bug | High | MVP |
| OS-019 | Coach | Some pages use different visual language | Consistency | Medium | Polish |
| OS-020 | Coach | Priority alerts dominate dashboard | UX | Medium | Polish |
| OS-025 | Coach | Bench players could not be selected or shown in Matchday Hub — saved substitute flow delivered | Resolved bug | Complete | MVP Experience Polish |
| OS-027 | Parent | Dates displayed in ISO format | Consistency | Medium | MVP |
| OS-028 | Parent | Selected child sees event from wrong team — selected-child event scoping, Player Preview, and Parent All-Children multi-child RSVP delivered | Resolved bug | Complete | Sprint 31 |
| OS-029 | Parent | Team Hub has blue-on-blue text | Accessibility | High | MVP |
| OS-030 | Parent | Finance experience is too limited — Parent Family Finance workspace, invoice detail & payment history delivered | Resolved gap | Complete | Sprint 33 |
| OS-031 | Notifications | Image attachments lack an in-app close/viewer experience | UX | Medium | MVP polish |
| FIN-027 | Treasurer | Invoices cannot be viewed, edited, cancelled, archived or voided properly — Treasurer invoice lifecycle delivered | Resolved gap | Complete | Sprint 33 |
| FIN-028 | Treasurer | Blue-on-blue text on billing pages | Accessibility | High | MVP |
| FIN-029 | Treasurer | Cannot create/edit/archive fee rules — Portal Fee Rules management delivered | Resolved gap | Complete | Sprint 33 |
| FIN-030 | Treasurer | Cannot create/edit/archive discount policies — Portal Discount Policies management delivered | Resolved gap | Complete | Sprint 33 |
| FIN-031 | Treasurer | Text shows caret as though editable | Visual bug | Low | MVP polish |
| PL-021 | Player | My Season has too much unused space and weak engagement | UX | High | MVP |
| PL-022 | Player | My Stats is only a minimal dashboard section | Missing experience | Critical | MVP |
| PL-023 | Player | Quick Actions should move near the top | UX | High | MVP |
| PL-024 | Player | Blue-on-blue text | Accessibility | High | MVP |
| ADM-001 | Admin | Sidebar navigation is too long | UX | High | MVP |
| ADM-002 | Admin | Route-only pages appear as sidebar destinations | UX | High | MVP |
| ADM-003 | Admin | Operational dashboards appear in admin navigation | UX/Architecture | Medium | MVP polish |
| ADM-004 | Admin | Long-term sensitive-role approval workflow | Security/Governance | High | Post-MVP |
| SET-001 | Settings | Current page is primarily a Brand Studio, not a full Settings area | Information architecture | High | MVP |
| SET-002 | Settings | Add image positioning, zoom and focal-point controls | Visual tool | Medium | Post-MVP |
| SET-003 | Settings | Create separate Club, System and Experience Settings areas | Information architecture | High | Post-MVP |
| SET-004 | Settings | Add club-profile defaults: Grassroots, Academy, Semi-Pro, Professional and Custom | Platform feature | High | Post-MVP |

## Detailed workspace direction

### Committee Workspace

- **Committee Workspace & Native Operations (complete):** Club OS-native management of club events, Club Projects CRUD, Committee Communications, Audience Builder v2, and live executive dashboard metrics are fully delivered (`Sprint 30`).
- Keep the premium hero and core dashboard structure.
- Use Club Overview as the sole landing tab.
- Move Quick Actions directly below the hero or alerts.
- Add richer registration metrics.

- **Welfare Experience Foundation (complete):** Role-aware safeguarding workspace, concern dashboard, concern directory, concern detail, status/priority lifecycle, optimistic revision control, activity timeline, and access isolation delivered (`Sprint 29`).
- Keep the concern dashboard, concern directory, concern detail, medical overview and emergency contacts.
- Move Quick Actions higher.
- Post-MVP, expand beyond concern management into DBS, safeguarding, first-aid and qualification compliance.
- Prefer archive over delete for safeguarding records; permanent deletion should be highly restricted and policy-controlled.

### Coach Workspace

- Preserve the Matchday Hub, Team Workspace, statistics and lineup builder design.
- Emergency-contact projection and bench selection are complete; match setup during event creation and external directions remain open.
- Use the Coach dashboard as the reference pattern for Quick Actions placement.
- Do not redesign the immersive dark team and match workspaces merely to make every page identical.

### Front-end Player Profile Workspace — Player Profile A

**Status (updated 2026-08-14):** Implementation and LocalWP manual acceptance complete; pending intentional commit. The existing partial route `/club-os/teams/{TEAM_ID}/players/{PERSON_ID}/` was hardened rather than replaced, preserving Team Hub → Squad → View Player. It remains read-only and private/no-store/noindex.

**Team Staff Operational Access Reconciliation prerequisite (source complete; core LocalWP manual acceptance passed):** Assignment-driven account provisioning gives a linked active Coach, Manager or Assistant Coach the narrow existing `iexel_manage_assigned_team` capability when the active Person has at least one active staff assignment on an active Team and active TeamSeason in the current active Season. LocalWP acceptance proved Manager access to U7 GOLD, Coach access to U8 GOLD and denial for an unrelated Team without broad all-Team access. The capability remains only Layer A.

- Player Profile authorization now proves linked active actor identity, Coach operational experience, `iexel_manage_assigned_team`, exact active route Team, exact active current TeamSeason and exactly one qualifying active `coach`, `manager` or `assistant_coach` assignment. A linked active Club Admin may use the established `iexel_manage_club_os` override. Preview and ordinary Secretary/Parent/Player/Treasurer/Welfare/Committee access are denied; Secretary continues at `/club-os/secretary/people/{PERSON_ID}/`.
- The target must be an active Person with active Player identity and exactly one active Player assignment on that exact Team/current TeamSeason. Training Only, former, inactive, missing, registered-but-unassigned, stale and duplicate/corrupt targets fail closed.
- One immutable authorized scope feeds a unified Player Profile snapshot. The minimum identity projection contains name, Club ID, avatar/initials, derived age, age group, Team and Season; exact DOB never enters rendered HTML, client state or URLs. Current assignment and current-Season Registration status are read-only and minimal.
- Guardian contact is shown only for positively known youth Players and is limited to name, neutral relationship ordering and telephone. Adult and age-unknown guardian cards are omitted. Emergency contact reuses `EmergencyContactService` for the exact current Season and remains visually separate.
- Current Operational Medical & Safety uses a dedicated non-Season Person-level singleton (`player_operational_medical_safety`) and never falls back to historical Registration. Admin and active Secretary users with `iexel_manage_registrations` own the protected current-state editor. Authorized current-Team Coach, Manager and Assistant Coach users receive only the four bounded current fields read-only. Registration stays immutable; only allergies and medication may seed prospectively on the first exact transition to `registered` when no current row exists. `medical_notes` and `emergency_information` never seed, existing Players are not bulk backfilled, and an explicit all-empty current row remains authoritative so historical declarations cannot reappear.
- Welfare concern existence/data and Finance data are absolutely excluded. No medical data is added to lists, directories, statistics, attendance, communications, client storage, analytics or activity logs. Attendance, statistics and Player Journey expansion remain deferred to Player Profile B.

**LocalWP acceptance update (2026-08-14):** Assigned Coach and Manager access, the Assistant Coach assignment architecture, exact assigned-Team authorization, cross-Team denial, Training Only isolation and the complete Player Profile A read model passed manual acceptance. The Secretary current Medical & Safety workflow, explicitly empty state and assigned-Team Coach read-only projection also passed. Registration testing proved seeding occurred only at the final `registered` transition: allergies and medication seeded where appropriate, historical medical notes and emergency information did not, and an existing current row was not overwritten. The persisted Training Member Registration type remained authoritative through successful submission. Responsive Player Workspace acceptance passed at 600px, 390px and 360px, and the intended private/no-store/no-cache/noindex response headers were verified. The final pre-commit audit found no functional MVP blocker. The accumulated batch remains pending intentional commit.

**Current Operational Medical & Safety status (updated 2026-08-14):** Schema, migration registration, canonical repository/service, Secretary Person Profile card, focused server-rendered edit route, prospective Registration seed hook and current-only Player Profile projection are implementation complete and have passed LocalWP manual acceptance. The entity is not Season-specific and stores one current row per Person. Emergency Contact remains separate as who to contact; Welfare/safeguarding and Finance remain separate domains. Sensitive routes are private/no-store/no-cache/noindex, and audit events record metadata/changed field names only. Intentional commit is still pending.

### Parent Workspace

- Keep dashboard, registrations, events and announcements.
- **Selected-Child & All-Children Event Scoping (complete):** Parent selected-child scoping (OS-028), Player Preview scoping, and All-Children event child identity (avatars/initials, per-child status) with independent multi-child RSVP on Event Detail are fully delivered.
- **Parent Family Finance (complete):** Family Finance workspace, invoice detail experience, child attribution, and payment allocation history are fully delivered.
- Improve notification attachments with an in-app viewer/lightbox.
- Post-MVP, evolve communications into richer posts, galleries, match reports and generated club content.

### Treasurer Workspace

- Keep the dedicated finance identity, payment recording, bulk family invoicing and billing schedules.
- **Treasurer Finance MVP (complete):** Invoice lifecycle management (draft, issue, cancel), payment recording & allocations, Fee Rules, and Discount Policies are fully delivered inside Club OS.
- Post-MVP, add reporting, exports, reconciliation and payment integrations.

### Player Workspace

- Reframe the workspace around motivation, progress, achievement and belonging.
- Create a full My Stats experience based on coach-visible player statistics.
- Expand My Season with attendance, form, progress bars, milestones and next achievement.
- Add lightweight challenges or competitions before MVP where feasible.
- Post-MVP, add rewards, XP, coach pointers, league tables, development journeys and team challenges.
- **Player Communications & Safeguarding Roadmap:**
  - Player Messages / Club News is part of the intended Player Experience; activation is gated by safeguarding controls.
  - Youth players may receive appropriate Club OS communications with linked guardian visibility/oversight supported.
  - Adult/senior players receive normal player communications without inheriting youth guardian rules.
  - Retain one canonical `Player` role with age/safeguarding classification beneath it (`Known Youth`, `Known Adult`, `Age Unknown`).
  - `Age Unknown` receives safeguarding-restricted behaviour until DOB/classification is resolved.
  - Club OS Communications are recipient-neutral and reusable across authorized experiences.
  - Support for adult/senior players and grassroots/semi-pro adult clubs remains part of long-term product direction.

### Admin Experience

- Keep admin focused on platform maintenance, system configuration and canonical records.
- Group sidebar navigation into Dashboard, People, Football, Seasons, Registrations, Finance, Communications, Welfare and System.
- Hide Person Profile, Team Profile and other route-only pages from the sidebar.
- Post-MVP, separate WordPress administrator power from automatic access to sensitive operational data.

### Settings and Brand Studio

- Rename or separate the current visual page as Brand Studio.
- Create separate Club Settings, System Settings and Experience Settings over time.
- Post-MVP, add image movement, crop, zoom and focal-point controls.
- Add club-profile defaults for Grassroots, Academy, Semi-Professional, Professional and Custom.

### Training Membership pathway roadmap

**Batch 2C source status (updated 2026-08-13):** Implementation remains pending LocalWP manual acceptance. Secretary People surfaces derive current Training Only status from active current-Season TrainingMemberships; a dedicated Training Members directory/detail supports operational filters and lifecycle management; and youth creation routes immediately into the existing Guardian Links workflow. Batch 2D-B1 normalises the canonical identity model so Prospect and direct Training entry now create a Player Person plus TrainingMembership atomically, without competitive assignment or account side effects. Coach/Manager Training Only visibility remains **NOT CURRENTLY VISIBLE** because authorised Coach surfaces are Team Assignment/Event-audience based.

**Batch 2D-A accepted status (2026-08-12):** The atomic Match Player → Training Only transition and Match Event ownership repair are implemented and have passed LocalWP manual acceptance. The Secretary Person Profile uses one transaction to revalidate the active Person, retained Player role, current Season, every active competitive Player assignment, Team/TeamSeason chains, TrainingMembership state and saved Match selections; it then ends every target-Season assignment and starts the canonical TrainingMembership. The Player role, linked account, Registration, Guardian/family relationships, Finance, historical assignments and historical Match/statistics records remain unchanged. Saved not-started lineups block until the Player is removed, live Matches require a terminal state, and terminal history does not block. Fixture/Friendly ownership is canonical through Event `team_id`, `season_id` and `team_season_id`; malformed scheduled Matches are repairable through the Secretary UI only after Match-state and saved-lineup compatibility checks, with the audience rebuilt from the exact TeamSeason roster. Current self Player Experience ceases naturally when no active competitive assignment remains. Historical-only Player Experience and Parent Preview changes remain incomplete and explicitly deferred.

**Batch 2D-B1 accepted status (2026-08-13):** Final acceptance passed and the implementation is merged on `main`. The reciprocal Secretary-controlled participation transitions preserve canonical Player identity, enforce Training Only/competitive assignment exclusivity, and require exactly one current `registered` Registration for Training → Match Player. Current/historical roster and statistics presentation and the responsive Training Members mobile filters also passed acceptance.

**Batch 2D-B2 accepted status (2026-08-13):** Implementation and LocalWP happy-path manual acceptance are complete, and the batch is merged on `main`. Training Member detail resolves the canonical current-Season Registration state and starts, resumes or views the existing Registration lifecycle without creating a parallel form. New drafts reuse the existing Person and current TrainingMembership Season, preserve terminal history, fail closed on contradictory active rows and return to the Training Member for the B1 competitive handoff once Registered. Acceptance verified that one existing Person progressed through Draft, Submitted and Registered into one compatible current Team Assignment while retaining the Registration, family links and historical Training Membership, with one current Team Hub roster entry. No account, Finance or Event mutation is introduced.

Training Membership is the one canonical representation of Training Only participation. `Player` is the canonical football-participant Person identity, not competitive eligibility. Training Only is Player + active current TrainingMembership + no active competitive Player Team Assignment; Match Player requires a valid current competitive assignment and the applicable Registration state. Youth uses an explicit supported TeamSeason U-group, while DOB-classified adults use the schema-compatible `senior` key. Player role alone must not create account access, Registration, Team assignment, Event audience, lineup or Match eligibility.

- **2B — Prospect → Training Only:** Manual acceptance passed under the prior identity model. Batch 2D-B1 now ensures canonical Player identity during the same atomic conversion while retaining Training-only participation: no Team Assignment, Registration, account or Match eligibility is created.
- **2C — Training Membership Visibility & Secretary Management:** Source implementation complete; pending LocalWP manual acceptance. Secretary visibility, direct Player-identity Training creation, re-entry and end/archive management use the canonical TrainingMembership domain. Coach/Manager visibility remains assignment-based and was not broadened.
- **2D-A — Atomic Match Player → Training Only Transition:** Implemented; LocalWP manual acceptance passed; pending commit. All current-Season competitive Player assignments end with canonical history-preserving lifecycle semantics, one active TrainingMembership starts through the transaction-safe domain boundary, and non-terminal saved lineups fail closed. Player role, account and Registration are retained. The accepted Match Event ownership repair prevents Team-less Fixtures/Friendlies and safely repairs malformed scheduled Match ownership without rewriting completed history.
- **2D-B1 — Registered-only Training Only → Match Player:** Final acceptance passed; merged on `main`. The Secretary Training Member detail requires exactly one current Person-linked `registered` Registration and a compatible active current TeamSeason, defensively ensures Player identity, creates a new regular active Player assignment episode, ends the TrainingMembership and writes one safe orchestration event in one transaction. Registration, account, family, Finance, Event audiences and history remain unchanged.
- **2D-B2 — Secretary-native Registration setup:** Final acceptance passed; merged on `main`. The Training Member workspace owns the safe entry into the canonical Registration wizard for the existing Player/current Season, with state-based resume/view behavior and a Registered handoff back to B1. No duplicate Person, account, Finance or Event side effects; the accepted B1 handoff creates one canonical current Team Assignment and preserves Training Membership history.
- **Historical experience:** Not implemented. Historical-only former Player Experience, Parent Preview policy changes and a new Training Member portal remain separate future work.

The three Training Only entry paths—Prospect conversion, Secretary direct creation and an existing Match Player transition—must converge on the same TrainingMembership service/domain. Training Only is not a mandatory step before Match Player: a later bounded pathway may invite a Prospect directly into competitive registration and assignment.

Post-MVP planning retains Taster/Trial invitations, Secretary communications to the Prospect contact, configurable Secretary/reply-to addressing and eventual role-authorized club mailbox integration. These communication capabilities are not Operational MVP blockers and must continue to reuse the channel-neutral Communications architecture.

## Future club profiles

### Grassroots

- Parent, Player, Coach, Committee, Welfare and Treasurer workspaces
- Registrations, events, attendance, availability, finance and communications
- Simple defaults and fewer advanced fields

### Academy

- Everything in Grassroots
- Player development plans, assessments, coach feedback and training programmes
- Scouting notes, development milestones and richer analytics

### Semi-Professional

- Everything in Academy where required
- Squad numbers, contracts, match bonuses and staff hierarchies
- More advanced finance, compliance and performance reporting

### Professional

- Medical, analysis, recruitment, media and contract departments
- Transfers, agents, multi-team structures and advanced permissions
- Deeper performance data and operational governance

### Custom

- Feature-by-feature module control
- Custom role terminology and workspace naming
- Custom defaults, labels, workflows and visible modules

## Recommended document role

Use this as a living product review and roadmap document in the repository, for example:

`development/CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md`

It should sit alongside `MASTER_DEVELOPER_GUIDE.md` and `SPRINTS.md`:

- `MASTER_DEVELOPER_GUIDE.md` remains the architecture and engineering source of truth.
- `SPRINTS.md` records implementation history and approved delivery phases.
- This document records product experience decisions, MVP gaps and future workspace direction.

## Product statement

> Committee runs the club. Welfare protects the club. Coaches develop the players. Treasurers sustain the club. Parents support the players. Players experience the journey. Administrators maintain the platform.
