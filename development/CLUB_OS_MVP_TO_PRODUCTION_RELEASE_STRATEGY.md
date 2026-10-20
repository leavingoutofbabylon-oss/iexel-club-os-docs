# Club OS MVP to Production Release Strategy

**Current programme decision: 21 October 2026.** Product Owner approved the two-track strategy below following PLAN02-B03. This records direction and gates; it does not authorise implementation, hosting access, installation, integration enablement or deployment. Individual batch, write, acceptance and Git approvals remain separate.

This document owns the current programme sequence and milestone checklist. The [Master Developer Guide](MASTER_DEVELOPER_GUIDE.md) remains binding for architecture and Engineering Rules. Use [Sprints](../SPRINTS.md) for delivery history and the [Experience Review and Roadmap](CLUB_OS_EXPERIENCE_REVIEW_AND_ROADMAP.md) for issue IDs and experience direction. Their dated historical snapshots remain valid for the builds they describe; older “current”, “open” or “Ready” statements do not supersede this checkpoint.

## 1. Current baseline and readiness

Plugin branch: `integration/mvp-rc-01`.

Confirmed committed/pushed baseline: `5c911e89a67ae75afecce5e6d62a226bde7731e2`. Local, tracking and live origin matched at the B03 assessment checkpoint. Integration is ten linear commits ahead of `main` at `20afe2981cfd9672cb2f0ef0d384f117b4e1f3cc`; nothing has been merged by this documentation batch. Reverify alignment before a later implementation or release operation.

|Accepted batch|Commit|Accepted outcome|
|---|---|---|
|PLAN02-B01, including FIX01/FIX02|`a7502acd0b5d2a2b41b2444b7e049154ff5c8803`|Club Configuration, separate Brand Studio, draft-only Season presentation, canonical age-policy guidance, atomic contact save/audit, MySQL 8.4 transaction compatibility, pre-output Fundraising redirect, trusted Secretary recovery documentation|
|PLAN02-B02|`5c911e89a67ae75afecce5e6d62a226bde7731e2`|Correct child/self RSVP wording; bounded own-team Coach bulk availability Review/Save; individual corrections; stale-state, audit and football-data protections|

B01/B02 are complete and Product Owner accepted. Do not reopen them as missing implementations. Their scoped coverage exceptions remain in section 7. Earlier HME, account-security, People, navigation, Registration, Training Membership and Welfare acceptances remain preserved.

Source header/runtime version is `1.0.0-dev`; expected schema is `2026.10.21`, data `2026.10.4`. These identify the candidate, not a new database inspection or final release version. Native support/recovery remains available through WordPress Admin under its existing authority; the retained original-site hold is not a production permission model.

**First hosted-test installation: CHANGES REQUIRED.** Resolve case-sensitive portability and prove exact-candidate clean activation/first-run access, target isolation and recovery before installation approval. Remaining visual work and conditional Pay-to-Play do not all have to precede the first restricted fictional test.

**Fresh production launch: not yet certified.** Approved MVP scope, security, safeguarding, premium North Star acceptance, exact-release certification, recovery and Product Owner release sign-off remain required. Historical feature acceptance is not deployment authority.

## 2. Reconciliation and scope control

B03 reconciled **214 requirements**, **51 outstanding MVP actions** and **38 certification areas**. The remaining actions comprise **35 Required** and **16 Polish**. Counts are register rows, not defects, development batches or a completion percentage.

|Disposition in the original register|Count|
|---|---:|
|Completed and accepted implementations/procedures|100|
|Previously accepted retired/superseded directions|2|
|Original post-MVP scope retained|61|
|Implemented, awaiting scoped certification|8|
|Product Owner decisions|3|
|MVP visual/experience actions|2|
|Release, operational and validator assurance|38|
|Total|214|

The reduction from 56 to 51 closes `ADM-005`, `SET-001`, `CP-GOV-BOOT`, `PRN-001` and `CCH-001` through accepted B01/B02 evidence. Acceptance of the recovery procedure does not establish a completed disaster-recovery exercise or fresh linked-officer onboarding. `CP-INT` retains its final-artifact/main-promotion gate even though publishing the integrated branch is complete.

The source-backed portability finding `B03-PORT-01`, first-run verification tasks and conditional Pay-to-Play decisions are supplemental; do not silently inflate or replace the 214-row denominator. The 38 certification areas remain the evidence framework. Passing a feature test does not certify an entire area.

Private evidence, retained outside both repositories: `PLAN02-B03-complete-roadmap-to-fresh-production-launch.md`, `PLAN02-B03-214-requirement-lineage.md`, `requirements-214-b03-reconciled.json`, `PLAN02-B03-outstanding-action-register.md`, `outstanding-actions-51.json` and `certification-matrix-38-b03-overlay.json`, in the `plan02-b03-20261021` evidence set. They retain every original ID, scope, evidence and acceptance criterion. They are not plugin production assets or public documentation attachments. This strategy summarises them without rewriting the private evidence.

## 3. Approved parallel tracks

|Track|Responsibilities|Evidence and handoff|
|---|---|---|
|Product Development|Complete remaining approved MVP workflows, any explicitly approved Pay-to-Play work, and premium North Star improvements. Develop, review and validate locally; obtain acceptance and commit/push approval for bounded batches.|Reviewed source revision, exact scope, focused tests, safe synthetic evidence, manual acceptance and disclosed exceptions|
|Release Engineering|Establish the isolated hosted test site as early as safety/install readiness permits; produce reproducible versioned packages; verify installation/upgrades, hosting, recovery, privacy and operational controls.|Artifact manifest/hash/revision, environment/configuration identity, snapshots, migration/preservation evidence and role/browser certification|

The tracks are coordinated, not serial completion of every product improvement before any hosted testing. Release Engineering may proceed while independent product work continues locally. Changes affecting permissions, schema, financial eligibility, communications, shared UI or onboarding require an impact review and relevant hosted retesting. Neither track may silently change the other's scope or waive its gates.

Normal candidate flow:

1. Develop and validate locally on the approved branch and owned test targets.
2. Review source, integrity/security evidence and Product Owner acceptance; separately approve commit/push.
3. Build a reproducible versioned package from an approved committed tree. Record commit, package version, file manifest and checksum. Do not zip the dirty workspace or include untracked artifacts, secrets, backups, local guards, dumps or test datasets.
4. Preserve a recoverable hosted-test database/files/configuration checkpoint and its fictional fixture/audit baseline.
5. Deploy that package through the controlled plugin lifecycle; run canonical activation or upgrade as applicable, followed by required integrity, role, transport and presentation checks.
6. Preserve fictional hosted-test data across controlled upgrades. Do not reset or reseed it routinely to hide upgrade defects. Approve any intentional fixture change separately and account for it explicitly.
7. Record acceptance against the exact candidate; promote only approved artifacts through the final release gate.

Do not edit live hosted plugin source as the normal development process, enable unreviewed candidate auto-updates or treat hosting as an uncontrolled development environment. A failed upgrade requires containment and assessed recovery; reverting plugin files alone may not undo schema/data changes. No deployment is authorised by recording this flow.

## 4. Fresh installation and first-run journey

Both the hosted test and [iexelfc.co.uk](https://iexelfc.co.uk/) receive **fresh Club OS installations**. The designated hosted rehearsal website is [ixlfootballacademy.co.uk](https://ixlfootballacademy.co.uk/), subject to ownership, isolation and public-content preflight. No host specification or existing-content safety has yet been verified.

- Hosted test uses entirely fictional identities, safeguarding cases, invoices and football records, with no live provider credentials or deliverable contact details.
- Production receives new real club records through supported workflows after explicit release approval. There is **no database migration from original LocalWP or hosted test to production**. Do not copy synthetic users, credentials, fixtures, audits or private guards into production.
- Fresh Club OS data does not mean the existing WordPress websites are empty or disposable. Preserve public content, policies, existing users, integrations and backups; obtain approval for the exact installation target.
- Retained-data upgrade certification still matters: preserve fictional hosted-test data between candidate upgrades and test supported retained synthetic baselines, idempotency, interruption/resume, lock release and rollback. Fresh installation is not an exemption from safe future updates.

The exact first-run acceptance journey must prove: legitimate trusted WordPress Administrator → canonical active official Person → unique Member Linking and capability projection → first Secretary through authorised full administration → club identity/contacts → deliberate Season/current-state setup → Teams/Team Seasons and staff assignments → Players/guardians/relationships → Registration/Training Membership → fictional football/finance/communications journeys and all authorised personas.

The source provides the existing People, Member Linking, Season and operational workflows; there is no demonstrated requirement for an MVP setup wizard. The complete current-artifact journey from empty club data is unverified. WordPress Administrator, Club Administrator, canonical Secretary, Player, family relationship, Training Membership and competitive assignment are distinct facts. Do not bypass their dependencies with SQL grants or fabricated roles. Explicitly review Person creation's role defaults; an official must not accidentally become a Player. No-current-Season pages must render safe guidance without inventing a current Season.

## 5. Earliest safe hosted-installation gate

### B03-PORT-01: Linux case-sensitive autoload blocker

The committed loader in `iexel-club-os.php` builds `app/Core/Application.php` and `app/Core/Activator.php` from the namespaces. Git stores `app/core/Application.php` and `app/core/Activator.php`. This is a confirmed source-level mismatch that blocks normal loading on a case-sensitive Linux filesystem; Windows masks it. It predates B01/B02. A Linux runtime failure has not been reproduced and the intended hosting OS/filesystem remains unknown.

Require a separately approved bounded correction and full affected class/include/asset case inventory, then exact-package loading and activation on a disposable case-sensitive target. Do not claim it fixed, rename the architecture speculatively or assume a Composer classmap currently compensates for it.

Before first hosted installation, verify all of the following:

- Exact host ownership/target, HTTPS, restricted test access and noindex; independent WordPress filesystem, database/user, uploads, cache, configuration and temporary paths. No links to original LocalWP or production.
- Chosen supported WordPress/PHP/database versions and plugins/theme/permalink/cache compatibility. Source declares WordPress 6.7 and PHP 8.2 minima; retained native evidence covers MySQL 8.4. Do not certify untested higher versions or MariaDB by assumption.
- Case-compatible reproducible candidate, exact clean activation, canonical tables/indexes/capabilities/versions/rewrites, empty history, no residual upgrade lock and first linked-official/no-current-Season proof. Activation also reconciles schedulers and performs AI-table setup; inspect all side effects.
- Durable controls before activation for WordPress cron, host/CLI scheduling, financial and communication jobs, payment transports and attachment cleanup. A single WP-Cron switch or PHP prepend file is not a host-level sandbox.
- Outbound HTTP/email/payment denial or explicitly verified capture/sandbox routing, no external relay or live secrets, and private logs. Do not copy the failed original SQL-firewall architecture into the production plugin.
- Consistent restorable database/files/configuration checkpoint, protected custody, owned recovery target and containment/rollback procedure. Include existing website content where applicable.
- Approved essential security/install test gate and explicit permission for the hosted installation, bounded fictional writes and inspection.

The minimum safe hosted test may precede unfinished BMG/Player/P2P/visual work if those paths are clearly incomplete or unavailable and do not run unsafe operations. This is not production acceptance. Do not delay it for unrelated post-MVP features.

## 6. Product Development programme

### Remaining operational MVP

Retain the complete 51-action ledger. Immediate functional/experience decisions include `BMG-001` private own-child/team supporter/status visibility, `PL-026` finite acceptance of existing per-match statistics, `PL-027` authorised completed-report links and `CP-DONE-TARGETS` acceptance. Preserve family/youth privacy, staff-note restrictions and historical facts. BMG remains within its recorded scope unless the Product Owner explicitly excludes it; no job/payment enablement follows from a read summary.

Reproduce `SEC-009` long-name picker overflow, `OS-011` concern-detail hierarchy and `CP-DEBT-SHOP-CARD` before changing code. `FIN-031` awaits confirmation of browser caret browsing rather than a speculative application fix. Retain `CP-COACH-UX`, `CP-VAL-HERO-VERIFY` and `CP-VAL-EVENT-VERIFY` as current-build acceptance work. Do not duplicate accepted B01/B02 behaviour or label every open assurance row a software defect.

### Pay-to-Play: policy and v1.0 scope still conditional

The proposed U6–U16 2026/27 programme reuses existing Registration/consent, Finance, eligibility, Communications and audit foundations. It is not fully approved, implemented or certified. In particular, no automatic suspension or account/Person-role removal may substitute for an approved participation decision. Existing competition-age rules remain separate.

|Decision ID|Policy/software contract still requiring explicit approval|
|---|---|
|P2P-01|Authoritative annual policy/version, guardian/adult acceptance and retained actor/time/document evidence|
|P2P-02|Normally seven-day invoice due rule, trigger, timezone and exceptions|
|P2P-03|Formal Treasurer notice/initiation, service evidence, support route and wording|
|P2P-04|Fourteen-day minimum before a permitted human suspension decision; no automatic sanction|
|P2P-05|Payment arrangements, hardship/safeguarding exceptions and hold/review authority|
|P2P-06|Grievance/appeal postponement, resolution authority and timer treatment|
|P2P-07|Independent authorised approval, proposed Treasurer/Secretary maker-checker, conflicts and no self-approval|
|P2P-08|Configurable training, matches or both; effective participation state and all enforcement boundaries|
|P2P-09|Formal approval of the IEXEL default effect; “both” is not yet an installed/approved default|
|P2P-10|Coach sees neutral eligibility only, never debt, appeal, hardship or family details|
|P2P-11|Continued family account/invoice/support access and exact-child privacy|
|P2P-12|Approved, audited, idempotent reinstatement with historical evidence preserved|

If confirmed for v1.0: P2P-D1 policy/authority/state/privacy design → P2P-D2 annual acceptance/notice/holds/approval/audit → P2P-D3 eligibility/reinstatement → P2P-D4 native concurrency/failure, privacy, authenticated and manual acceptance. Each has its own approved scope and commit checkpoint. If excluded, record an explicit launch policy/disposition; do not silently defer or promote it.

### Premium North Star programme

Finish the agreed v1.0 quality bar across Club Administrator, Secretary, Treasurer, Welfare, Committee, Coach/Manager, Parent/Guardian and Player. Reuse midnight-blue/club-accent tokens, established shell/cards/controls, football identity and intentional administrative/immersive distinctions. No uncontrolled shell redesign or global colour rewrite.

|Group|Finite acceptance scope|
|---|---|
|NS-A shared/admin/finance|Configuration/Brand Studio hierarchy and separation; Brand Studio's recorded 9px mobile overflow; WordPress notices inside the hero; dense guidance and BMG grouping; Secretary picker; finance/Shop states and shared feedback/focus|
|NS-B football/family|Coach availability and touch/keyboard controls, long names/opponents, Event Detail/team management, Parent cramped View rows and child context, Player statistics/Progress/Targets and approved completed-report links|
|NS-C Welfare/Committee|Current concern-detail hierarchy, confidential minimal summaries, permitted aggregates/Projects, empty states and final eight-role consistency|

Inspect desktop 1280/1366/1440px and mobile 320/375/390px, intermediate responsive boundaries, contrast, keyboard/focus/labels, touch, dates/statuses, unknown facts, loading/error/conflict/success, confirmations and destructive actions. Essential unreadable/unusable or privacy failures block affected production journeys; approved pre-production North Star targets can follow the first hosted install. Retain explicit post-MVP refinements without silently lowering the v1.0 bar.

## 7. Release Engineering, safeguarding and certification

Use the existing 38-area matrix, recording source/artifact, target, exact expected effects, observed data visibility and acceptance. Distinguish pure offline, isolated filesystem, native database, authenticated and manual tests. Do not run original-path WordPress loaders, weaken assertions or add overlapping old test counts into a new certificate.

Required gates include:

- `CP-CERT-INSTALL`: current package clean installation, empty onboarding and canonical identity/role projection.
- `CP-CERT-UPGRADE`: retained fictional data, historical/football protections, invoice indexes including `uq_invoice_source`, expected schema/data, interruption/idempotency and no loss of attachments.
- `CP-CERT-ROLES`: real persona authority, protected account/native/REST roles, People/Registration/Training Membership integrity, Welfare/Committee/Coach/family data minimisation and negative object-access controls.
- `CP-CERT-PERF` and `CP-NS`: representative target-host performance/assets/errors and accepted desktop/mobile experience; no speculative caching.
- `B4D`, `CP-REC-RPO`, `CP-REC-OFFSITE`, `CP-REC-KEYS`: consistent recovery payload, independently retrievable protected custody, restore proof, named ownership and acceptable data-loss/outage limits.
- `CP-OPS-CRON`, `CP-OPS-EMAIL`, `CP-OPS-PAYMENT`, `CP-OPS-RETENTION` and `CP-COMPLIANCE-FUND`: deliberate job/queue/provider/competition/retention decisions, sandbox tests and staged real-operation approval; no catch-up storm or opportunistic cleanup.
- `CP-HOST-ACADEMY`, `CP-HOST-PROD`, `CP-INT`, `CP-DOC`, `CP-GUIDES` and `CP-RELEASE`: host/public-content compatibility, truthful guides, exact certified tree/version/package/main/tag, explicit deployment authority and monitored rollback.

Youth or unknown-age communications retain the safest canonical safeguards; no unsupervised adult-to-youth private channel. Coaches receive only authorised operational football/safety data, ordinary Committee receives minimised aggregates, and Welfare/private financial/family records retain their separate boundaries. Historical results do not create Back My Game financial achievements. No dataset import, UI change or hosting decision relaxes those rules.

Outstanding assurance retained explicitly:

- Parent/Player upcoming Event Detail Seen receipts: R4B's four positive/seven negative checks and manual acceptance remain incomplete. Approve the exact receipt/audit/write manifest; do not assume a GET is free of business effects.
- Three historical intercepted R4B HTTP attempts remain individually unattributed. T2-R1 captured none and was inconclusive. Any further diagnostic needs separate approval, redacted evidence and outbound blocking; no blanket update-check exception.
- B02 tamper-response body/internal classification was not independently retained, although the no-write outcome was verified. Obtain exact approved negative-case response evidence on an owned disposable target.
- B02 browser session/tab cleanup could not be independently confirmed; require operator cleanup/exclusive test arrangements and disclose visibility limits.
- B01 accepted absent inactive/unprivileged native Administrator runtime fixtures and draft/completed Season screenshots. Its capability-based contact policy and existing linked Club Administrator Fundraising override remain unchanged. Add approved fixtures or document accepted equivalent evidence/residual risk for release; do not invent new permissions.
- B02 mixed self/child invitation and receipt-producing Event Detail edges plus minor Coach/Parent mobile polish remain scoped acceptance items.
- Five known baseline age-validator warnings and selected legacy harness defects remain classified. `CP-VAL-AUTHNAV`, `CP-VAL-PAYER`, `CP-VAL-FAMILY`, `CP-VAL-FIN-KERNEL`, `CP-VAL-STB`, `CP-VAL-SAFE`, `CP-VAL-TARGET` and `CP-VAL-REG` identify critical coverage selection, not authority to run every validator.

## 8. Coordinated phases and next five batches

|Phase|Product Development and Release Engineering handoff|
|---|---|
|A readiness/decisions|Freeze remaining scope, P2P/BMG decisions, visual punch list, host/custodian and portability correction contract|
|B early hosted test|Exact package, case-sensitive clean-install/onboarding evidence, isolated fictional target and recoverable approved installation|
|C remaining MVP|Local bounded implementations and critical validation; promote accepted candidates to hosted test with retained fictional data|
|D conditional Pay-to-Play|Approved policy/design before implementation; affected finance/football certification follows it|
|E North Star|Shared/admin/finance, football/family and Welfare/Committee acceptance; may overlap independent engineering work|
|F integrated club acceptance|Realistic fictional onboarding, Registration, training/match, finance/comms, eight personas and negative privacy cases|
|G final assurance|Exact artifact install/upgrade/recovery, host safety, operating ownership, guides, security/safeguarding and release sign-off|
|H fresh production|Preserve existing public site; approved fresh plugin installation, new real club onboarding and gradual authorised opening|

The next five are proposed bounded batches, not implementation approvals. Critical validator work may run alongside N1/N2; minimum safety evidence must precede installation. Conditional P2P design may be prioritised after N1 if v1.0 inclusion is ratified.

### B03-N1 — Fresh onboarding, portability and hosting contract

References: `B03-PORT-01`, `CP-CERT-INSTALL`, `CP-HOST-ACADEMY`, residual `CP-GOV-BOOT` verification, recovery decisions and `BMG-001`. Verify host specs/custodian, first linked official, all case-sensitive loading/include/asset paths and exact correction/safety manifest. Expected components: bootstrap/Activator, existing roles/People/linking/Season flows and release packaging. Main risks are privilege bootstrap, wrong target and public-content loss. Exit: approved contract and separately authorised case-sensitive disposable correction/proof. No runtime or code operation follows automatically; freeze exact files and commit approval for any implementation.

### B03-N2 — Reproducible candidate and first isolated hosted install

References: `CP-CERT-INSTALL`, `CP-HOST-ACADEMY`, `CP-CERT-PERF`, `CP-RELEASE`, `B03-PORT-01`. After N1 gates: essential safe tests, canonical empty install/first-run, exact package manifest/hash, hosted holds and recovery, then approved fictional installation/smoke. Existing lifecycle/inventories/assets are the components; no casual new framework. Stop on unsafe activation schedules, egress, target ambiguity or state loss. Exit: exact-candidate hosted acceptance and recovery evidence; no main promotion or production deployment.

### B03-N3 — Release-critical validator reliability

References: `CP-VAL-AUTHNAV`, `CP-VAL-PAYER`, `CP-VAL-FAMILY`, `CP-VAL-FIN-KERNEL`, `CP-VAL-STB`, `CP-VAL-SAFE`, `CP-VAL-TARGET`, `CP-VAL-REG`; directly needed `CP-VAL-VERSIONS`, `CP-VAL-CANCEL`, `CP-VAL-DELEGATION` prerequisites. Freeze exact validator files and targets. Correct only fixture/loader/contracts, retain meaningful negatives and all other debt; no production-rule weakening. Offline/disposable/native execution has separate safety authority. Exit: trustworthy selected coverage, independent unsafe-case failures, PO residual-risk review and separate bounded validator commit approval.

### B03-N4 — Private family/Player workflow closure

References: `BMG-001` unless explicitly excluded, `PL-026`, `PL-027`, `CP-DONE-TARGETS`, scoped `CP-CERT-ROLES` and B02 evidence. Reuse canonical BMG reads, Parent page, Player Progress/history/report permissions. Agree supporter disclosure and remaining statistics scope before code. Test two-family/youth/preview isolation, genuine empty/active/revoked/closed states and completed reports; no GET charges/collections or staff-detail leak. Receipt tests require their own manifest and transport gate. Exit: scoped source/security tests and desktop/mobile acceptance, then separate explicit commit approval; split test groups if their write authority differs.

### B03-N5 — Shared North Star and administrative experience finish

References: `CP-NS`, `SEC-009`, `FIN-031`, `CP-DEBT-SHOP-CARD`, B01/B02 visual exceptions. Freeze a reproduced finite punch list; use existing shared controls/cards and scoped page/CSS patterns for Configuration/Brand Studio/finance/Secretary. No permission/navigation redesign or global CSS sweep. Accept before/after desktop/mobile, focus/keyboard/touch/contrast and unchanged data boundaries; prepare remaining NS-B/NS-C groups separately. Exit: Product Owner screenshot/manual acceptance and separately approved exact-file commit.

These are the first five, not the whole programme. B03's rough 10–18 controlled-batch envelope without P2P, with approximately 4–6 additional if the full policy workflow enters v1.0, is low-confidence planning, not dates or measured progress. Re-estimate after host/first-run and the finite visual/policy contracts.

## 9. Milestone checklist

Maintain ID, owner, status, candidate/package, evidence and Product Owner decision. The parallel strategy is approved; individual scope decisions, technical proofs and deployment permissions below remain open. No milestone is newly certified by this documentation update.

- [ ] M01 Remaining register, BMG/P2P inclusion and finite v1.0 visual scope approved; strategy approval alone does not settle these decisions.
- [ ] M02 Host/content/OS/runtime/plugin/cache/TLS/access and initial custodian contract verified.
- [ ] M03 `B03-PORT-01` correction accepted; exact package passes case-sensitive loading and asset checks.
- [ ] M04 Essential safe tests and clean activation/first linked official/no-current-Season journey pass.
- [ ] M05 Isolated fictional hosted target, blocked jobs/transports and independent recovery verified; installation approved.
- [ ] M06 First hosted installation/smoke recorded against immutable candidate; no real data or integrations.
- [ ] M07 Remaining BMG/Player functionality accepted or explicit approved scope disposition recorded.
- [ ] M08 P2P ratified and certified if included; otherwise explicit launch policy/disposition recorded.
- [ ] M09 Shared/admin/finance North Star punch list accepted, including B01 exceptions.
- [ ] M10 Football/family and Welfare/Committee North Star, 320px, keyboard/touch/contrast accepted.
- [ ] M11 Transport/R4B receipt manifest, four positives/seven negatives/manual and B02 tamper evidence closed or formally disposed with justified equivalent evidence; no blanket exemptions.
- [ ] M12 All eight personas and integrated club journeys pass required positive/negative/privacy cases on exact candidate.
- [ ] M13 Clean installation, retained-data upgrade, idempotency/interruption/lock/index/attachment and owned native concurrency/failure evidence accepted.
- [ ] M14 Host restoration, off-device custody/keys/RPO-RTO, retention and named operational owners accepted.
- [ ] M15 Current documentation and seven tested role guides plus Administrator setup/recovery guidance accepted; this document does not certify the entire five-draft programme complete.
- [ ] M16 Final version/package/hash, scope/exceptions, required tests and main/tag/release approval complete.
- [ ] M17 Existing production public content/integrations backed up and preserved; fresh Club OS installation explicitly approved.
- [ ] M18 Linked real officials, teams/Season, Players and families entered through supported workflows; access, jobs/email/payments/cleanup enabled only in approved monitored stages.

## 10. Decisions still required and preservation

Product Owner decisions: exact hosting target/access/public-content boundary and initial custodian; bounded portability correction/test scope; BMG launch/privacy; authoritative Pay-to-Play policy and v1.0 inclusion/governance/default effect; finite North Star pages/states; minimum critical validation and residual-risk dispositions; backup cadence/retention/RPO-RTO, independent custody/keys; named cron/communications/payment/cleanup owners. Later gates require exact fictional fixture/technical-write/receipt/diagnostic budgets, accepted release/main/tag/package, production installation and staged real-operation approval. Recording the strategy grants none of these permissions automatically.

Post-MVP work retains its recorded classification. Assistant Secretary protected-role approval governance (`ADM-004`), richer Team Health, rewards/analytics, wizard/videos, broader settings, WordPress independence/multi-club productisation, theme/app/licensing and League OS do not silently become production blockers. Bringing any forward requires explicit scope approval.

Original LocalWP `Q06FAQ8HY` remains stopped and untouched, retaining its marker/guards, historical result #100098, invoices, attachments, uploads and recovery evidence. Preserve synthetic `g_vIVpiAuS`, both RC environments, existing fixtures/audits, zero Seen-receipt baseline, 21 protected artifacts, stash and documentation drafts. Current database preservation is not newly certified by a documentation task; no database, WordPress, service or hosting operation is authorised here.

The [historical Handover](DEVELOPMENT_HANDOVER_2026-09-30.md) and [Release Checklist](RELEASE_CHECKLIST.md) remain preserved with their original evidence and pending drafts. Their older current-state text is superseded by this strategy for programme status only; Engineering Rules and accepted safety/authority boundaries remain binding. No release checklist tick or old roadmap score supplies current deployment permission.
