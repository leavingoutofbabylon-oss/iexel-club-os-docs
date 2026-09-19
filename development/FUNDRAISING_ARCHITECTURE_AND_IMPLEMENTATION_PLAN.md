# IEXEL Club OS — Fundraising Architecture & Implementation Specification

**Status:** Approved Product Architecture (Implementation Pending)  
**Version:** 1.1.0  
**Author:** Antigravity Architecture & Core Engineering  
**Date:** 2026-09-19  
**Target Domain:** `app/core/Fundraising/`  
**Applicable Releases:** F1 through F6 (Post-MVP Operational Roadmap — Planned, Not Implemented)  

---

## 1. Product Objective

Fundraising is established as a new first-class operating capability of IEXEL Club OS. Grassroots football clubs rely heavily on community fundraising to finance equipment (such as portable training goals and match balls), facility maintenance, floodlight improvements, tournament travel, match kits, and life-saving equipment (such as automated external defibrillators).

Historically, grassroots clubs have relied on fragmented third-party crowdfunding platforms, paper raffle sheets, or bolted-on web forms that create severe operational issues:
- Financial proceeds sit outside canonical club accounts and require tedious manual spreadsheet reconciliation;
- Youth player identities are frequently exposed on public "child seller" pages, creating safeguarding and data-privacy vulnerabilities;
- Secretary and Treasurer volunteers lack unified visibility into campaign health, received funds, and payment processing fees;
- Member families face disconnected user experiences outside their normal Club OS portal.

The objective of the **Fundraising Domain** is to deliver a native, secure, transparent, and football-centric fundraising ecosystem inside Club OS. It unifies:
1. **Secretary / Admin Campaign Operations:** Intuitive campaign setup, asset curation, adjudication workflows, and auditable status management;
2. **Treasurer Financial Oversight:** Transparent visibility into gross collected funds, gateway fees, prize liabilities, and net club proceeds, connecting directly with Club OS Finance primitives without polluting standard player membership invoices;
3. **Member Participation:** An engaging, responsive **Member Fundraising Hub** where parents, adult players, coaches, committee members, and supporters can back club appeals or enter skill competitions;
4. **Interactive Skill Competitions:** A flagship **Spot the Ball** experience engineered with independent adult panel adjudication, auditable immutable target sealing, device-independent normalized coordinates, and an auditable Euclidean distance results engine;
5. **Safeguarding & Data Minimisation:** Strict boundaries ensuring youth players are protected, child seller profiles are prohibited, and parental payment authorization is mandatory.

---

## 2. Scope

The scope of this architecture and implementation plan covers the complete domain model, operational workflows, UI experiences, database storage, and development phases for Club OS Fundraising:

- **Campaign Foundation:** A unified campaign model supporting multiple distinct fundraiser types, a robust finite-state lifecycle, and role-based visibility.
- **Campaign Types Accommodated:**
  1. *Fundraising Appeal:* Target-driven direct contributions (e.g., New Training Goals Fund).
  2. *Sponsored Challenge:* Activity-based team challenges (e.g., 100 Goals Challenge, Penalty Shootout).
  3. *Spot the Ball:* Flagship interactive skill/judgement competition featuring independent panel adjudication, immutable target sealing, touch-assisted positioning, and mathematical tie-breaking.
  4. *Club Draw:* Future compliance-gated campaign type (strictly deferred until regulatory review).
- **User Surfaces:**
  - *Member Fundraising Hub:* Mounted at `/club-os/fundraising/` within the canonical portal shell.
  - *Secretary Management Console:* Mounted at `/club-os/secretary/fundraising/` and mirrored in wp-admin.
  - *Treasurer Financial Dashboard:* Mounted at `/club-os/treasurer/` and `/club-os/finance/fundraising/`.
  - *Independent Judging Surface:* Secure, blinded coordinate submission for designated adult judges.
- **Core Computational Engines:**
  - Normalized sub-pixel coordinate translation ($0.000000$ to $1.000000$) invariant to screen size, device pixel ratio, or orientation.
  - Documented adjudication derivation methodology.
  - Auditable immutable target sealing before public participation opens.
  - High-precision Euclidean distance results calculation.
  - Deterministic unique-person tie-breaking with zero-penny-loss monetary remainder distribution.
- **Finance Integration:**
  - Clean separation between fundraising orders and standard membership billing.
  - Authoritative payment confirmation boundary interfacing with `iexel_os_finance_payments` without altering existing invoice `PaymentAllocation` semantics.
  - Financial ledger reconciliation supporting gross, fee, prize, and net accounting.
- **Implementation Phasing:** Controlled, incremental delivery across phases F1 through F6. Runtime functionality does not yet exist; F1 has not yet begun.

---

## 3. Non-Goals

To preserve architectural integrity and avoid technical debt, the following items are explicitly declared as **Non-Goals**:

1. **No Bolted-on Third-Party Plugins:** We will not install or wrap third-party WordPress crowdfunding plugins (e.g., GiveWP, WooCommerce, WP Crowdfunding) or embed external widgets.
2. **No Ordinary Invoices for Fundraising Entries:** We will not create standard club invoices (`iexel_os_finance_invoices`) for individual fundraising contributions or competition entries. Purchasing competition tickets is not a membership debt.
3. **No Polymorphic Payment Allocations:** We will not modify the existing invoice-bound `PaymentAllocation` entity or table (`iexel_os_finance_payment_allocations`) to link polymorphically to fundraising orders.
4. **No Public Child Seller Profiles:** We will not build public-facing youth player fundraising profiles, individual child donation URLs, or public leaderboards featuring children's names and amounts raised.
5. **No Premature Chance Draws at Launch:** We will not implement or activate Club Draw (lottery/raffle) functionality during MVP. Paid chance-based draws require prior regulatory review and compliance approval.
6. **No Gambling / Casino Visual Aesthetics:** We will not implement spinning wheels, casino slot animations, flashing neon banners, or speculative gambling tropes. The UI must remain a restrained, premium midnight-blue football experience centered on community achievement.
7. **No Secretary Historical Ball Clicking:** The Spot the Ball winning target must never be set by the Secretary clicking where the ball happened to be in the original match photo. Spot the Ball is legally structured as a skill and judgement competition based on independent adult adjudication.
8. **No Prize Splitting Per Winning Entry:** Prize shares in Spot the Ball ties are strictly allocated per **unique winning participant/person**, never per entry. A single person with multiple entries at the winning distance receives one prize share.
9. **No Floating-Point Financial Calculations:** All financial calculations, fee deductions, and prize distributions must strictly use integer pence ($1.00 = 100\text{p}$). Floating-point values (`float`, `double`) are strictly prohibited in financial paths.
10. **No Lossy Viewport Coordinate Storage:** Storing client CSS pixel coordinates or viewport-relative points is strictly prohibited. All coordinates must be normalized relative to native source dimensions.
11. **No Gift Aid Prerequisite for F1 Appeal:** Gift Aid will not be treated as an F1 prerequisite or assumed applicable to all fundraising transactions; it is deferred to a dedicated future compliance review.

---

## 4. Repository Architecture Findings

Inspection of the active codebase (`iexel-club-os` at checkpoint `a3990c8` and `iexel-club-os-docs`) establishes the architectural baselines that Fundraising must extend:

1. **System & Version Baseline:**
   - Current release baseline: `0.2.10-dev`.
   - PHP runtime requirement: PHP 8.2+.
   - WordPress baseline: WordPress 6.7+ / 7.0+.
   - Database manager: `IEXEL\ClubOS\Core\Database\DatabaseManager`, managing 51 canonical tables with prefix `$wpdb->prefix . 'iexel_os_'`.
2. **Identity & People Architecture:**
   - Canonical individual identity is rooted in `IEXEL\ClubOS\People\PeopleRepository` (`iexel_os_people.id`, canonical `person_id`).
   - WordPress users link to People via `iexel_os_people.user_id` managed by `UserLinkManager`.
   - Administrative authority never creates member identity (*Fail-closed identity boundary*).
   - Family relationships are maintained in `iexel_os_person_relationships` (`guardian` $\leftrightarrow$ `player`).
3. **Finance Domain Primitives & Boundary:**
   - Source: `app/core/Finance/`.
   - Currency amounts are strictly stored as integer pennies (`amount` in `Payment`, `InvoiceLine`).
   - `Payment` entity (`iexel_os_finance_payments`) supports methods: `'cash'`, `'card'`, `'bank_transfer'`, `'standing_order'`, `'direct_debit'`, `'online_payment'`, `'other'`.
   - Existing `PaymentAllocation` (`iexel_os_finance_payment_allocations`) strictly binds `payment_id` to `invoice_id`. This is an established financial invariant that must not be altered into a polymorphic structure.
   - Fundraising requires an explicit, auditable bridge between fundraising orders and canonical payments (e.g. via `FundraisingOrder.payment_id` or a dedicated fundraising payment association table), without altering existing invoice allocation semantics.
4. **Database Migration & Upgrade Pipeline:**
   - Schema and data migrations are governed by `IEXEL\ClubOS\Core\Upgrade\UpgradeRunner`.
   - Every database change is wrapped in an `UpgradeStep` contract evaluating preconditions, idempotent application, and post-flight validation.
   - `DatabaseManager::install()` and specialized schema installers manage DDL execution via `dbDelta()`.
5. **Audit & Logging Framework:**
   - Handled by `IEXEL\ClubOS\Core\Activity\ActivityLogger` inserting into `iexel_os_activity_log`.
   - Structured payload: `user_id`, `action`, `object_type`, `object_id`, `message`, and JSON `metadata`.
6. **Media & File Storage Conventions:**
   - `CommunicationAttachmentPolicy` defines allowed MIME types (`image/jpeg`, `image/png`, `image/webp`), size limits, and path containment within WordPress uploads.
   - Attachments link to WordPress media IDs (`attachment_id`).
7. **Portal Routing & UI Design System:**
   - Routed through `IEXEL\ClubOS\Core\Portal\PortalRouter` matching rewrite rules under `/club-os/`.
   - Strict HTTP response status integrity: buffered rendering must invoke explicit `status_header(403)` or `status_header(404)` on denial paths.
   - Styling relies on the midnight-blue palette, gold accent trim (`.iexel-accent-top-module`, `var(--iexel-gold)`), and shared experience layout components (`.iexel-experience-hero`, `.iexel-experience-section`, `.iexel-experience-metrics`).

---

## 5. Domain Model

The Fundraising domain is modeled around high-cohesion, loosely-coupled entities:

```
+-------------------------------------------------------------------------+
|                           FundraisingCampaign                           |
|-------------------------------------------------------------------------|
| id: int (PK)                                                            |
| campaign_type: string (appeal | sponsored_challenge | spot_the_ball | draw) |
| title: string                                                           |
| slug: string (unique)                                                   |
| purpose_category: string (equipment|facilities|pitch|kit|tour|general)  |
| summary: string                                                         |
| description: text                                                       |
| target_amount: ?int (pence)                                             |
| currency: string (GBP)                                                  |
| status: string (draft|ready|live|closed|settled|completed|archived)     |
| starts_at: ?datetime                                                    |
| ends_at: ?datetime                                                      |
| created_by_person_id: int (FK -> people.id)                             |
| visibility: string (public|club_members|team_only)                      |
| target_team_id: ?int (FK -> teams.id)                                   |
| rules_and_terms: text                                                   |
| created_at / updated_at: datetime                                       |
+-------------------------------------------------------------------------+
       | 1                                               | 1
       |                                                 |
       | 0..1 (type = spot_the_ball)                     | 0..*
       v                                                 v
+------------------------------------------+    +----------------------------------+
|          SpotTheBallCompetition          |    |         FundraisingOrder         |
|------------------------------------------|    |----------------------------------|
| id: int (PK)                             |    | id: int (PK)                     |
| campaign_id: int (FK)                    |    | order_reference: string (unique) |
| source_image_id: int (media PK)          |    | campaign_id: int (FK)            |
| competition_image_id: int (media PK)     |    | payer_person_id: int (FK)        |
| image_width: int                         |    | participant_person_id: int (FK)  |
| image_height: int                        |    | gross_amount: int (pence)        |
| entry_price: int (pence)                 |    | fee_amount: int (pence)          |
| max_entries_per_person: int              |    | net_amount: int (pence)          |
| adjudication_method: string              |    | payment_status: string           |
| target_x: ?decimal(7,6)                  |    | payment_method: string           |
| target_y: ?decimal(7,6)                  |    | payment_id: ?int (FK -> payments)|
| target_sealed_at: ?datetime              |    | completed_at: ?datetime          |
| target_sealed_by: ?int (FK -> people.id) |    | created_at: datetime             |
| prize_type: string (fixed|percentage)    |    +----------------------------------+
| prize_amount: int (pence)                |       | 1                | 1
+------------------------------------------+       |                  |
       | 1                   | 1                   | 0..*             | 0..* (Appeal)
       | 0..*                | 0..1                v                  v
       v                     v              +-------------------+  +-------------------+
+---------------------+ +-----------------+ | FundraisingEntry  |  |  Contribution     |
|SpotTheBallJudgement | |SpotTheBallResult| |-------------------|  |-------------------|
|---------------------| |-----------------| | id: int (PK)      |  | id: int (PK)      |
| id: int (PK)        | | id: int (PK)    | | order_id: int (FK)|  | order_id: int(FK) |
| competition_id: int | | competition_id  | | entrant_person_id |  | donor_person_id   |
| judge_person_id: int| | winning_distance| | entry_number: int |  | amount: int(pence)|
| judged_x: dec(7,6)  | | tied_count: int | | coord_x: ?dec(7,6)|  | is_anonymous: bool|
| judged_y: dec(7,6)  | | prize_pool: int | | coord_y: ?dec(7,6)|  | donor_name: string|
| judged_at: datetime | | prize_per_person| | status: string    |  | message: ?text    |
+---------------------+ | remainder_pence | +-------------------+  +-------------------+
                        | settled_at: dt  |
                        +-----------------+
                               | 1
                               | 1..*
                               v
                        +-------------------------------+
                        |    SpotTheBallPrizeAllocation |
                        |-------------------------------|
                        | id: int (PK)                  |
                        | result_id: int (FK)           |
                        | recipient_person_id: int (FK) |
                        | winning_entry_id: int (FK)    |
                        | prize_share_pence: int        |
                        | remainder_awarded_pence: int  |
                        | payout_status: string         |
                        +-------------------------------+
```

---

## 6. Campaign Lifecycle

The campaign lifecycle is governed by an explicit Finite State Machine (FSM). Arbitrary state jumps are rejected.

```
       [ Create ]
           |
           v
       +-------+         Passes Preflight
       | Draft | ----------------------------------> +-------+
       +-------+                                     | Ready |
           ^                                         +-------+
           | Edit / Revoke                               |
           +---------------------------------------------+
                                                         | Target Sealed (Spot the Ball)
                                                         | Start Time Reached (Appeal)
                                                         | Publish Action
                                                         v
                                                     +------+
                                                     | Live |
                                                     +------+
                                                         |
                                 +-----------------------+-----------------------+
                                 |                                               |
                                 | Scheduled `ends_at` Reached                   | Manual Admin Close
                                 v                                               v
                                                     +--------+
                                                     | Closed |
                                                     +--------+
                                                         |
                                                         | Calculate Result Engine (Spot the Ball)
                                                         | Review & Finalise (Appeal)
                                                         v
                                                    +---------+
                                                    | Settled |
                                                    +---------+
                                                         |
                                                         | Prizes Disbursed / Net Funds Transferred
                                                         v
                                                   +-----------+
                                                   | Completed |
                                                   +-----------+
                                                         |
                                                         | Admin Archive
                                                         v
                                                   +----------+
                                                   | Archived |
                                                   +----------+
```

### Lifecycle State Definitions & Transition Guards

| State | Permitted Operations | Entry Guards / Invariants |
|---|---|---|
| **Draft** | Edit details, upload images, assign judges, delete draft. | Initial state upon campaign creation. |
| **Ready** | Preview campaign, assign/execute judging, seal target. | Requires: title, description, valid dates, target amount, rules acceptance. |
| **Live** | Accept public/member entries, process contributions, view progress. | Preconditions: For **Spot the Ball**, `target_sealed_at IS NOT NULL`. Target coordinates and competition image are completely immutable. |
| **Closed** | Prevent new orders/entries; calculate distances and identify winners. | Reached when `ends_at` is passed or Secretary executes manual close. No further entries accepted. |
| **Settled** | Publish winners, review prize allocations, confirm financial reconciliation. | Preconditions: For **Spot the Ball**, `SpotTheBallResult` calculated and audited. For **Appeal**, final financial totals verified. |
| **Completed** | Full campaign review, financial ledger closed, summary visible. | Preconditions: All prize payouts authorized/settled by Treasurer; net proceeds recorded. |
| **Archived** | Read-only historical audit inspection. | Campaign closed to all active mutations. Retained indefinitely for club records. |

---

## 7. Campaign Types

The architecture explicitly defines four campaign archetypes:

### 1. Fundraising Appeal
- **Objective:** Pure donation/target campaign without competition or chance elements.
- **Examples:** *New Portable Training Goals Fund*, *Pitch Defibrillator Appeal*, *Under-14 Barcelona Tour Travel Fund*.
- **Mechanism:** Fixed preset donation tiers (£5, £10, £25, £50, £100) or custom amounts. Real-time visual progress thermometer showing percentage and amount raised. Optional donor wall with public recognition or full anonymity.
- **Safeguarding:** Pure club/team-level tracking. No individual youth player contribution metrics.
- **F1 Scope:** Works fully without Gift Aid. (Gift Aid is an optional future compliance enhancement, not an F1 prerequisite).

### 2. Sponsored Challenge
- **Objective:** Activity-driven athletic challenges where club members collect sponsorships.
- **Examples:** *100 Goals in a Month*, *Sponsored Penalty Shootout*, *5km Team Fun Run*.
- **Mechanism:** Activity metrics logged at the squad/team level or individual level under parental oversight. Fixed sponsorship pledges or per-unit pledges (e.g., £0.50 per penalty scored).
- **Safeguarding:** **Strict prohibition against public child profiles.** Donors sponsor the team or the child via a private family link managed by the parent. No public child leaderboard.

### 3. Spot the Ball (Flagship Experience)
- **Objective:** High-engagement interactive skill/judgement competition.
- **Mechanism:** Participants inspect a prepared football match photo with the ball removed. Using touch or mouse, participants place a marker where their skill and judgement tell them the center of the ball should be.
- **Legal Character:** Structured strictly as a skill/judgement competition under Section 14 of the UK Gambling Act 2005. Target location is determined by a panel of independent adult judges and sealed before competition launch.
- **Result:** The participant whose confirmed entry is closest to the sealed adjudicated target via Euclidean distance wins the advertised prize.

### 4. Club Draw (Strictly Deferred & Compliance-Gated)
- **Objective:** Future chance-based prize draw family.
- **Status:** **Planned, not implemented.** Not approved for runtime implementation yet.
- **Architecture Position:** The software architecture anticipates a future Club Draw family, but does **not** encode a predetermined statutory small-society-lottery implementation, local-authority registration route, or statutory promoter model. Before F6 can be considered, the club's specific operating structure, applicable jurisdiction, draw mechanics, and required licensing/registration must be explicitly reviewed and approved by the Product Owner and club leadership.

---

## 8. Role & Permission Matrix

To maintain strict operational boundaries, Fundraising introduces granular capabilities extending `ClubRoleCapabilityRegistrar`:

```php
iexel_manage_fundraising        // Create, edit, configure, publish, close campaigns (Secretary, Admin)
iexel_view_fundraising_admin    // Read-only access to campaign management surfaces (Committee, Admin)
iexel_adjudicate_spot_the_ball  // Designated adult judge: submit target coordinates only (Judge)
iexel_settle_fundraising_prizes // Authorize and disburse prize funds (Treasurer, Admin)
iexel_view_fundraising_finance  // Financial reporting, gross/fee/net visibility (Treasurer, Committee)
iexel_participate_fundraising   // Enter competitions, make appeal donations (Parent, Adult Player, Coach)
```

### Granular Matrix by Persona

| Persona | View Hub | Enter / Donate | Create / Edit Campaign | Judge Spot the Ball | Calculate / Publish Results | Settle Prizes | Reconcile Finance |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **Club Admin** | Yes | Yes | Yes | Yes (if assigned) | Yes | Yes | Yes |
| **Secretary** | Yes | Yes | Yes | No (segregation) | Yes | No (segregation) | Read-only |
| **Treasurer** | Yes | Yes | Read-only | No | Read-only | **Yes** | **Yes** |
| **Committee** | Yes | Yes | Read-only | No | Read-only | No | Read-only |
| **Designated Judge** | Yes | No (comp. excluded)| No | **Yes (isolated)** | No | No | No |
| **Parent / Guardian** | Yes | **Yes (for family)**| No | No | No | No | No |
| **Adult Player** | Yes | **Yes (self)** | No | No | No | No | No |
| **Youth Player (<18)**| Yes | No (browse only)| No | No | No | No | No |
| **Team Coach** | Yes | Yes | No | No | No | No | No |

*Note on Welfare:* Welfare officers have no automatic operational or financial access to fundraising prize settlements or monetary records unless a specific safeguarding case warrants it under existing safeguarding capabilities. Financial oversight remains restricted to Treasurer and Club Admin.

---

## 9. Identity Model

Fundraising strictly adheres to the canonical Club OS People identity model rooted in `iexel_os_people.id` (`person_id`).

### Actor Separation

A single transaction involves distinct actors who must never be conflated:
1. **`payer_person_id` (The Payer):** The legally capable adult responsible for the financial transaction. In youth football, this is almost always the Parent/Guardian.
2. **`participant_person_id` (The Entrant/Beneficiary):** The individual in whose name the entry or challenge is recorded (e.g., the youth player whose squad is benefiting).
3. **`organizer_person_id` (The Campaign Manager):** The Secretary or Club Official creating and executing the campaign.
4. **`judge_person_id` (The Adjudicator):** The verified adult individual providing independent coordinate estimates.
5. **`winner_person_id` (The Prize Recipient):** The individual entitled to the prize. If the winning entry belongs to a youth player, prize settlement follows the approved guardian/safeguarding settlement workflow, routing legal payout to the verified linked guardian (`payer_person_id` / linked guardian in `iexel_os_person_relationships`).

---

## 10. Safeguarding Model

Safeguarding children and vulnerable adults is a core engineering requirement:

1. **Zero Child Seller Pages:**
   - Third-party platforms encourage children to have public personal fundraising links with profile pictures and individual totals. This is explicitly prohibited in Club OS.
   - Campaign progress is reported at the Club or Team level only.
2. **Data Minimisation on Public Surfaces:**
   - Donor walls and supporter tickers must never display youth player full names or ages publicly.
   - Donor attribution displays adult names (e.g., *"The Stevens Family"*, *"David S."*) or *"Anonymous"*.
   - A toggle `is_anonymous` is provided during checkout.
3. **Minor Payment Protection:**
   - Youth player accounts (<18) are prohibited from initiating paid financial transactions or purchasing competition entries directly.
   - The UI guides youth players to notify their linked parent/guardian.
4. **Prize Settlement Safeguards:**
   - Cash prizes are not disbursed directly to minors. Where a youth player’s entry wins Spot the Ball, prize settlement follows the approved guardian safeguarding workflow, routing the payout to the verified linked guardian with Treasurer authorization. Financial information remains restricted to financial roles; Welfare involvement occurs only if an established safeguarding requirement specifically justifies it.
5. **Direct Object Access Isolation:**
   - Entrants can only view their own coordinates and receipts.
   - Judges cannot inspect entrants' coordinates or other judges' submissions before their own workflow is complete.
   - Unsealed competition targets are hidden from all non-admin users.

---

## 11. Compliance Architecture

Grassroots football fundraising operates under UK statutory frameworks. Club OS provides the architectural tools to ensure clubs operate consistently and auditably:

### Regulatory Boundaries

```
+---------------------+-------------------------------+-----------------------------------+
| Campaign Type       | Classification                | Status / Regulatory Gate          |
+---------------------+-------------------------------+-----------------------------------+
| Fundraising Appeal  | Voluntary Donations / CASC     | Lawful. No gambling licence req.  |
| Spot the Ball       | Gambling Act 2005, Section 14 | Prize Competition (Skill-based).  |
|                     | (Skill, Judgement & Knowledge)| Requires genuine skill barrier &  |
|                     |                               | independent panel adjudication.   |
| Sponsored Challenge | Voluntary Sponsorship         | Lawful. No gambling licence req.  |
| Club Draw (Deferred)| Compliance-Gated Family       | Planned, NOT implemented. Model,  |
|                     |                               | jurisdiction & licensing pending. |
+---------------------+-------------------------------+-----------------------------------+
```

### Spot the Ball Skill & Judgement Criteria
Under Section 14 of the UK Gambling Act 2005, prize competitions requiring genuine skill, judgement, or knowledge are distinct from lotteries and do not require gambling operating licences.

Club OS supports this operational model via:
- **Independent Adult Adjudication:** Target position is derived from the collective judgement of designated adult judges evaluating visual cues, rather than the historical location where the ball was removed.
- **Auditable Immutable Sealing:** The derived target is permanently locked and audited before public competition entries open.
- **Published Methodology & Rules:** Detailed competition rules and derivation methodology are published and versioned before entries open.

---

## 12. Finance & Payment Boundary

A primary architectural rule of Club OS is: **Fundraising transactions are NOT ordinary club invoices.**

```
               [ Member / Parent Checkout ]
                            |
                            v
                 +----------------------+
                 |   FundraisingOrder   |
                 +----------------------+
                            |
           +----------------+----------------+
           |                                 |
           v                                 v
[ Online Card Gateway ]             [ Manual Bank / Cash ]
   (e.g., Stripe Webhook)               (Treasurer Entry)
           |                                 |
           +----------------+----------------+
                            |
                            v
              +----------------------------+
              | Authoritative Confirmation |
              +----------------------------+
                            |
         +------------------+------------------+
         |                                     |
         v                                     v
+-----------------------------+       +-----------------------------+
|   iexel_os_finance_payments |       |   FundraisingOrder/Entry    |
|-----------------------------|       |-----------------------------|
| id: int                     |       | payment_status: 'completed' |
| person_id: payer_person_id  |       | entries: 'confirmed'        |
| amount: gross_pence         |       +-----------------------------+
| method: 'card'|'bank_trans' |                      |
| reference: 'FR-ORD-000123'  |                      |
+-----------------------------+                      |
         ^                                           |
         | (Explicit Fundraising Payment Linkage)    |
         +-------------------------------------------+
         | (e.g. FundraisingOrder.payment_id or      |
         |  dedicated association table)             |
         |                                           |
         | *Existing Invoice PaymentAllocation       |
         |  semantics remain completely unchanged*   |
```

### Key Architectural Boundaries

1. **No Invoicing Overhead:** Invoices (`iexel_os_finance_invoices`) represent contractual club fees and membership debts. Fundraising entries are discretionary consumer purchases. Generating invoices for £2 competition entries would pollute player financial ledgers, distort debt reporting, and corrupt billing schedules.
2. **No Polymorphic Payment Allocations:** Existing `PaymentAllocation` records link payments to invoices (`invoice_id`). Club OS will NOT convert this into a polymorphic allocation structure. Instead, Fundraising maintains its own explicit, auditable link to canonical payments (e.g., via `FundraisingOrder.payment_id` or a dedicated `iexel_os_fundraising_order_payments` table). F1 must inspect the live Finance implementation before finalising this bridge.
3. **Payment Reusability:** When money is authoritatively confirmed, a canonical `Payment` record is created in `iexel_os_finance_payments` with the payer's `person_id`.
4. **Treasurer Campaign Reconciliation:** The Treasurer Workspace provides a dedicated Fundraising reconciliation view tracking:
   - **Gross Receipts:** Total money received into club accounts.
   - **Gateway Fees:** Transaction fees deducted by card processors.
   - **Prize Liabilities & Disbursements:** Cash prizes committed vs paid.
   - **Net Club Proceeds:** Retained surplus available for club football expenditure.

---

## 13. Fundraising Appeal Architecture

The Fundraising Appeal is the simplest campaign family, designed for delivery in Phase F1.

### Operational Features
- **Campaign Configuration:** Goal target (£), start/end dates, purpose category, narrative, photo banner.
- **Contribution Tiers:** Preset button grid (£5, £10, £25, £50, £100) with custom amount entry.
- **Gift Aid Position:** **Deferred.** F1 Appeal MVP works fully without Gift Aid. Gift Aid eligibility is not universal (many fundraising activities or gifts with donor benefits are ineligible), and no declaration checkbox will be introduced until club CASC/charity eligibility and contribution qualifying rules are specifically verified as a future enhancement.
- **Public Supporter Wall:** Displays donor name, donation date, amount (optional), and donor message (e.g., *"Good luck with the new goals! The Smith Family"*).
- **Real-Time Progress:** Live calculation of percentage achieved and remaining balance.

---

## 14. Spot the Ball Management Architecture

Spot the Ball management follows a strict sequence of operational gates:

```
[ Step 1: Campaign Setup ]
- Define title, entry price (e.g. £2.00 / 200p), maximum entries per person, closing date.
- Choose prize structure: Fixed Cash (e.g., £250.00) or Percentage Pool (e.g., 50% of gross entries).

[ Step 2: Source & Competition Media ]
- Upload original high-resolution match photo (containing real ball).
- System stores original image in a protected, non-public directory.
- Upload prepared competition photo (ball cleanly edited out).
- System extracts and locks source dimensions: `image_width`, `image_height`, `aspect_ratio`.

[ Step 3: Independent Adjudication ]
- Secretary designates a panel of verified adult judges (e.g., Committee members, coaches, senior officials).
- Judges receive access to the blinded adjudication console.
- Each judge inspects the competition image and records their expert target position.
- Judges cannot view other judges' submissions or participant entries.

[ Step 4: Derivation & Sealing ]
- System derives the consensus target position $(x_t, y_t)$ using the published, deterministic adjudication methodology.
- Secretary reviews derivation audit evidence.
- Secretary confirms sealing: System records coordinates, timestamp, author, and locks the campaign into `Ready`.
- Target coordinates are permanently locked.

[ Step 5: Live Competition ]
- Campaign opened to members. Entries accepted. Target coordinates remain hidden from all entrants and UI until results publication.
```

---

## 15. Spot the Ball Judging & Sealing Model

### Adjudication & Target Derivation

- **Independent Adult Adjudication:** Designated adult judges independently submit coordinates $(x_i, y_i)$ in normalized units $0 \le x_i, y_i \le 1$.
- **Panel Integrity:** Judges submit coordinates through an isolated workflow. A judge cannot inspect other judges' submissions before their own submission is complete, and cannot see participant entries at any time. The panel size must be sufficient to establish a credible expert consensus (the exact panel sizing and derivation algorithm will be evaluated and selected during F2).
- **Deterministic Derivation:** The target position $(x_t, y_t)$ is derived using a documented, deterministic methodology (such as panel centroid or geometric median) fixed before entries open.

### Auditable Target Sealing

F2 must implement an auditable immutable target-sealing mechanism that guarantees the target cannot be altered once entries open:
- At minimum, the sealing mechanism preserves:
  1. Canonical derived coordinates;
  2. Adjudication inputs and judge evidence records;
  3. Precise sealing timestamp;
  4. Campaign/competition identity;
  5. Audit log entry (`spot_the_ball_target_sealed`);
  6. Hard database lock preventing post-seal mutation.
- **Commitment Scheme:** If a public commitment/reveal mechanism is desirable, F2 may design an appropriate cryptographic commitment scheme during implementation. However, raw target coordinates must **never** be exposed prior to official results publication.

---

## 16. Spot the Ball Entry & Order Model

### Participant Entry Journey

1. **Selection:** Participant opens the Spot the Ball campaign in the Member Hub.
2. **Entry Batch:** Participant chooses how many entries to play (e.g., 3 entries at £2.00 = £6.00).
3. **Interactive Coordinate Selection:**
   - For each entry (Entry 1, Entry 2, Entry 3), the member interacts with the canvas.
   - A crosshair marker appears on click/touch.
   - Touch placement is supported on mobile devices with touch-assisted magnification and fine-adjustment nudging to ensure ergonomic accuracy. (Exact magnification scale and step sizes are F3 UX implementation decisions).
4. **Draft Persistence:** Unsubmitted coordinates are held in browser session memory or a draft order.
5. **Checkout & Payment:** Order is submitted to `FundraisingOrderService`. Payer completes payment.
6. **Confirmation & Locking:** Upon payment confirmation, entries are marked `'confirmed'`. Confirmed coordinates are immutable.

---

## 17. Coordinate Model

### The Normalized Coordinate Invariant

Browser viewport pixels, CSS rendered dimensions, device pixel ratios (Retina/High-DPI), and mobile responsive layouts vary wildly between devices. Storing screen coordinates (e.g., `left: 342px; top: 180px`) causes total failure when evaluated on different screen sizes.

Club OS uses a **Normalized Coordinate Model**:

$$x_{\text{norm}} = \frac{X_{\text{click}} - X_{\text{image\_origin}}}{W_{\text{image\_rendered}}}, \quad y_{\text{norm}} = \frac{Y_{\text{click}} - Y_{\text{image\_origin}}}{H_{\text{image\_rendered}}}$$

- **Range:** $0.000000 \le x_{\text{norm}}, y_{\text{norm}} \le 1.000000$.
- **Storage Precision:** Sufficient fixed precision must be preserved. `DECIMAL(7,6)` (precision to $1 / 1,000,000$th of the image dimension) is the recommended candidate representation, with exact persistence precision to be confirmed against image handling requirements during F2.

---

## 18. Result Calculation

When the competition closes, the results engine calculates the distance from each confirmed entry to the sealed target.

### Euclidean Distance Formula

For an entry $j$ with coordinates $(x_j, y_j)$ and sealed target $(x_t, y_t)$:

$$d_j = \sqrt{(x_j - x_t)^2 + (y_j - y_t)^2}$$

- Distance is computed in PHP using standard 64-bit IEEE floating point arithmetic with full precision, stored as `DECIMAL(10,8)`.
- The entry with the minimum distance $d_{\min} = \min_{j} d_j$ is the winning entry.
- **Tie Threshold:** Exact closest-distance ties are determined using canonical stored precision. Two entries $A$ and $B$ are considered tied if:
  $$|d_A - d_B| < 10^{-7}$$

---

## 19. Tie / Prize Splitting Rules & Deterministic Penny Remainder

The Product Owner has approved an explicit, non-negotiable rule for competition ties:

> **Rule:** If multiple entries tie for the closest distance from the adjudicated target, the prize is divided equally between the tied **winning PARTICIPANTS (unique persons)**, NOT per winning entry.

### Invariant Principles
1. Winner calculation uses canonical unrounded distance.
2. Ties are determined using canonical stored precision.
3. One person cannot receive multiple tie shares because multiple entries from that person share the winning distance.
4. All prize amounts use integer pence.
5. Deterministic remainder allocation ensures: $\sum \text{Prize Shares} == \text{Advertised Prize}$ exactly.

### Example Scenario
- Advertised Prize: **£300.00** ($30,000\text{p}$).
- Winning Distance: Exactly $0.042185$.
- Entries matching winning distance:
  - Alice: Entry #12 ($d = 0.042185$) and Entry #15 ($d = 0.042185$).
  - Ben: Entry #44 ($d = 0.042185$).
- **Resolution:**
  - Unique winning persons = 2 (Alice, Ben).
  - Alice does **not** get 2 shares. Alice gets 1 share.
  - Result: Alice receives £150.00 ($15,000\text{p}$); Ben receives £150.00 ($15,000\text{p}$).

### Deterministic Zero-Penny-Loss Remainder Algorithm

When integer money cannot be divided equally without fractional pence, the software must never lose or create pennies.

Let:
- $P_{\text{total}}$ = Total prize amount in integer pence (e.g., £100.00 = $10,000\text{p}$).
- $K$ = Number of unique winning persons (e.g., $K = 3$).

1. **Calculate Base Share:**
   $$S_{\text{base}} = \lfloor P_{\text{total}} / K \rfloor = \lfloor 10000 / 3 \rfloor = 3333\text{p } (£33.33)$$
2. **Calculate Remainder Pence:**
   $$R = P_{\text{total}} - (S_{\text{base}} \times K) = 10000 - (3333 \times 3) = 10000 - 9999 = 1\text{p}$$
3. **Deterministic Allocation of Remainder:**
   - The competition rules published before launch define the deterministic remainder ordering.
   - Proposed algorithm: Sort the $K$ winning persons deterministically by their **earliest confirmed winning entry timestamp** (`confirmed_at` ASC, then `entry_id` ASC).
   - The first $R$ participants in this deterministic sequence receive:
     $$S_i = S_{\text{base}} + 1\text{p } (£33.34)$$
   - The remaining $K - R$ participants receive:
     $$S_i = S_{\text{base}} (£33.33)$$
4. **Invariant Check:**
   $$\sum_{i=1}^{K} S_i = R \times (S_{\text{base}} + 1) + (K - R) \times S_{\text{base}} = P_{\text{total}}$$
   Zero pennies are lost or created. The outcome is 100% deterministic, auditable, and transparent.

---

## 20. Audit Requirements

Every sensitive action in the Fundraising lifecycle generates an immutable log entry via `ActivityLogger`:

| Action Key | Object Type | Object ID | Metadata Recorded |
|---|---|---|---|
| `fundraising_campaign_created` | `fundraising_campaign` | `campaign_id` | `title`, `type`, `target_amount`, `created_by` |
| `fundraising_campaign_published` | `fundraising_campaign` | `campaign_id` | `published_at`, `starts_at`, `ends_at` |
| `fundraising_campaign_closed` | `fundraising_campaign` | `campaign_id` | `closed_at`, `reason` ('scheduled' \| 'manual') |
| `spot_the_ball_judge_submitted`| `spot_the_ball_comp` | `competition_id` | `judge_person_id`, `judged_at` (coordinates hidden in log) |
| `spot_the_ball_target_sealed` | `spot_the_ball_comp` | `competition_id` | `sealed_by`, `adjudication_method`, `sealed_at` |
| `fundraising_order_completed` | `fundraising_order` | `order_id` | `payer_person_id`, `gross_amount`, `payment_method` |
| `fundraising_entry_confirmed` | `fundraising_entry` | `entry_id` | `participant_person_id`, `order_id` |
| `spot_the_ball_result_calc` | `spot_the_ball_comp` | `competition_id` | `winning_distance`, `tied_count`, `prize_pool` |
| `spot_the_ball_result_publish` | `spot_the_ball_comp` | `competition_id` | `published_at`, `winner_ids` |
| `fundraising_prize_settled` | `spot_the_ball_prize` | `allocation_id` | `recipient_person_id`, `amount`, `treasurer_person_id` |
| `fundraising_order_refunded` | `fundraising_order` | `order_id` | `refunded_amount`, `reason`, `authorized_by` |

---

## 21. Member Fundraising Hub UX

The Member Fundraising Hub is integrated directly into the member portal at `/club-os/fundraising/`.

### Visual Hierarchy & Styling
- **Page Header:** Canonical `.iexel-experience-hero` displaying the club badge, header *"Club Fundraising"*, and supporting copy *"Back club appeals and enter competitions to support grassroots football."*
- **Active Campaign Grid:** Rendered using `.iexel-os-card` cards featuring:
  - Purpose badge (e.g., *"Equipment"*, *"Tour"*).
  - Campaign photo / banner with gold accent top edge (`.iexel-accent-top-module`).
  - Progress bar showing percentage raised and target.
  - Call-to-action button: `.iexel-button-primary` (*"Support the Appeal"* or *"Play Spot the Ball"*).
- **Interactive Spot the Ball Canvas:**
  - Responsive container constraining image aspect ratio.
  - Pan and zoom capabilities.
  - Touch-assisted magnification loupe on mobile touch.
  - Crosshair pins for each active entry with distinct visual markers (Entry 1 = Gold, Entry 2 = Blue, Entry 3 = Cyan).
- **Post-Result Reveal:**
  - Highlighting the club's collective achievement: *"Together the club raised £1,420 for new training goals."*
  - Interactive overlay displaying the adjudicated target position alongside winning player markers.

---

## 22. Secretary / Admin UX

Mounted at `/club-os/secretary/fundraising/` and mirrored in wp-admin (`admin.php?page=iexel-club-os-fundraising`).

### Information Architecture
- **Overview Strip:** KPI summary tiles (`.iexel-experience-metric`) showing:
  - *Active Campaigns*
  - *Total Raised This Season*
  - *Pending Adjudications*
  - *Awaiting Settlement*
- **Campaign Management Table:** Sortable list by Status, Type, Title, Target, Raised, and End Date.
- **Campaign Creation & Media Wizard:**
  - Multi-step form with tabbed stages: *1. Basics* $\rightarrow$ *2. Assets & Image Prep* $\rightarrow$ *3. Rules & Prizes* $\rightarrow$ *4. Adjudication Setup*.
  - Protected media upload for original photo; client-side image review before saving.
- **Judging & Sealing Console:**
  - Status indicators for each assigned judge (Pending / Submitted).
  - Target calculation preview (visible only to authorized Secretary/Admin).
  - One-click sealing action with confirmation modal.
- **Results & Publishing Console:**
  - Automated distance calculation upon competition closure.
  - Verification panel listing closest entries, tie detection, and penny remainder breakdown.
  - Action to publish results to the Member Hub.

---

## 23. Treasurer Reporting UX

Mounted at `/club-os/treasurer/` and `/club-os/finance/fundraising/`.

### Financial Ledger Integration
- **Fundraising Revenue Breakdown:**
  - *Gross Collected:* Total money received across all active and completed campaigns.
  - *Processing Fees:* Estimated or reconciled gateway fees.
  - *Prize Liabilities:* Cash prizes won, broken down by *Settled / Paid* and *Pending Payment*.
  - *Net Club Surplus:* Final net funds generated for the club's equipment or project funds.
- **Order Reconciliation Table:** Filterable table linking `FundraisingOrder` references with `iexel_os_finance_payments` and bank statement transactions.
- **Prize Settlement Authorization:** Interactive action allowing the Treasurer to approve and disburse prize shares to verified winners/guardians.

---

## 24. Security & Privacy Considerations

1. **CSRF Protection:** Every state mutation requires a cryptographically valid WordPress nonce (`wp_create_nonce()`, `check_admin_referer()`).
2. **Access Control Enforcement:** Capability checks (`current_user_can()`) are performed at the request handler layer and re-verified at the domain service layer.
3. **Protected Image Storage:** The original match image (containing the ball) is stored in a private directory with an `.htaccess` rule blocking direct HTTP access, served only through an authenticated PHP proxy for authorized judges.
4. **Coordinate Confidentiality:** Entrant coordinates are private data. The API will never return other players' coordinates while a competition is `Live` or `Closed` prior to official results publication.
5. **Rate Limiting:** Entry submission and payment checkout endpoints are rate-limited per user/IP to prevent brute-force coordinate placement or payment probing.

---

## 25. Proposed Database & Storage Model

The Fundraising schema introduces canonical tables created via `DatabaseManager` using standard WordPress collation:

### Table 1: `iexel_os_fundraising_campaigns`
```sql
CREATE TABLE {$wpdb->prefix}iexel_os_fundraising_campaigns (
    id BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
    campaign_type VARCHAR(32) NOT NULL, -- appeal, sponsored_challenge, spot_the_ball, club_draw
    title VARCHAR(191) NOT NULL,
    slug VARCHAR(191) NOT NULL,
    purpose_category VARCHAR(64) NOT NULL, -- equipment, facilities, pitch, kit, tour, welfare, general
    summary VARCHAR(255) NOT NULL,
    description LONGTEXT NOT NULL,
    target_amount INT(11) UNSIGNED DEFAULT NULL, -- in integer pence
    currency VARCHAR(3) NOT NULL DEFAULT 'GBP',
    status VARCHAR(32) NOT NULL DEFAULT 'draft', -- draft, ready, live, closed, settled, completed, archived
    starts_at DATETIME DEFAULT NULL,
    ends_at DATETIME DEFAULT NULL,
    created_by_person_id BIGINT(20) UNSIGNED NOT NULL,
    visibility VARCHAR(32) NOT NULL DEFAULT 'club_members', -- public, club_members, team_only
    target_team_id BIGINT(20) UNSIGNED DEFAULT NULL,
    rules_and_terms LONGTEXT DEFAULT NULL,
    created_at DATETIME NOT NULL,
    updated_at DATETIME NOT NULL,
    PRIMARY KEY  (id),
    UNIQUE KEY uq_slug (slug),
    KEY idx_status_visibility (status, visibility),
    KEY idx_created_by (created_by_person_id),
    KEY idx_target_team (target_team_id)
) {$charset_collate};
```

### Table 2: `iexel_os_fundraising_orders`
```sql
CREATE TABLE {$wpdb->prefix}iexel_os_fundraising_orders (
    id BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
    order_reference VARCHAR(64) NOT NULL, -- FR-ORD-000001
    campaign_id BIGINT(20) UNSIGNED NOT NULL,
    payer_person_id BIGINT(20) UNSIGNED NOT NULL,
    participant_person_id BIGINT(20) UNSIGNED NOT NULL,
    gross_amount INT(11) UNSIGNED NOT NULL, -- in integer pence
    fee_amount INT(11) UNSIGNED NOT NULL DEFAULT 0, -- in integer pence
    net_amount INT(11) UNSIGNED NOT NULL, -- in integer pence
    payment_status VARCHAR(32) NOT NULL DEFAULT 'pending', -- pending, completed, failed, refunded
    payment_method VARCHAR(32) NOT NULL DEFAULT 'card', -- card, bank_transfer, cash, account_credit
    external_reference VARCHAR(191) DEFAULT NULL,
    payment_id BIGINT(20) UNSIGNED DEFAULT NULL, -- FK to iexel_os_finance_payments
    completed_at DATETIME DEFAULT NULL,
    created_at DATETIME NOT NULL,
    PRIMARY KEY  (id),
    UNIQUE KEY uq_order_ref (order_reference),
    KEY idx_campaign_status (campaign_id, payment_status),
    KEY idx_payer (payer_person_id),
    KEY idx_participant (participant_person_id),
    KEY idx_payment_id (payment_id)
) {$charset_collate};
```

### Table 3: `iexel_os_fundraising_entries`
```sql
CREATE TABLE {$wpdb->prefix}iexel_os_fundraising_entries (
    id BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
    order_id BIGINT(20) UNSIGNED NOT NULL,
    campaign_id BIGINT(20) UNSIGNED NOT NULL,
    participant_person_id BIGINT(20) UNSIGNED NOT NULL,
    entry_number INT(11) UNSIGNED NOT NULL DEFAULT 1,
    coord_x DECIMAL(7,6) DEFAULT NULL, -- normalized 0.000000 to 1.000000
    coord_y DECIMAL(7,6) DEFAULT NULL, -- normalized 0.000000 to 1.000000
    status VARCHAR(32) NOT NULL DEFAULT 'pending_payment', -- pending_payment, confirmed, voided
    created_at DATETIME NOT NULL,
    confirmed_at DATETIME DEFAULT NULL,
    PRIMARY KEY  (id),
    KEY idx_order (order_id),
    KEY idx_campaign_status (campaign_id, status),
    KEY idx_participant (participant_person_id)
) {$charset_collate};
```

### Table 4: `iexel_os_fundraising_contributions`
```sql
CREATE TABLE {$wpdb->prefix}iexel_os_fundraising_contributions (
    id BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
    order_id BIGINT(20) UNSIGNED NOT NULL,
    campaign_id BIGINT(20) UNSIGNED NOT NULL,
    donor_person_id BIGINT(20) UNSIGNED NOT NULL,
    amount INT(11) UNSIGNED NOT NULL, -- in integer pence
    is_anonymous TINYINT(1) NOT NULL DEFAULT 0,
    donor_display_name VARCHAR(191) DEFAULT NULL,
    message TEXT DEFAULT NULL,
    created_at DATETIME NOT NULL,
    PRIMARY KEY  (id),
    KEY idx_order (order_id),
    KEY idx_campaign (campaign_id),
    KEY idx_donor (donor_person_id)
) {$charset_collate};
```

### Table 5: `iexel_os_spot_the_ball_competitions`
```sql
CREATE TABLE {$wpdb->prefix}iexel_os_spot_the_ball_competitions (
    id BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
    campaign_id BIGINT(20) UNSIGNED NOT NULL,
    source_image_id BIGINT(20) UNSIGNED NOT NULL,
    competition_image_id BIGINT(20) UNSIGNED NOT NULL,
    image_width INT(11) UNSIGNED NOT NULL,
    image_height INT(11) UNSIGNED NOT NULL,
    entry_price INT(11) UNSIGNED NOT NULL, -- in integer pence (e.g. 200 = £2.00)
    max_entries_per_person INT(11) UNSIGNED NOT NULL DEFAULT 10,
    adjudication_method VARCHAR(64) NOT NULL DEFAULT 'adjudication_panel',
    target_x DECIMAL(7,6) DEFAULT NULL,
    target_y DECIMAL(7,6) DEFAULT NULL,
    target_sealed_at DATETIME DEFAULT NULL,
    target_sealed_by BIGINT(20) UNSIGNED DEFAULT NULL,
    prize_type VARCHAR(32) NOT NULL DEFAULT 'fixed_cash', -- fixed_cash, percentage_pool
    prize_amount INT(11) UNSIGNED NOT NULL DEFAULT 0, -- in integer pence
    prize_pool_percentage DECIMAL(5,2) DEFAULT NULL,
    created_at DATETIME NOT NULL,
    updated_at DATETIME NOT NULL,
    PRIMARY KEY  (id),
    UNIQUE KEY uq_campaign (campaign_id),
    KEY idx_sealed (target_sealed_at)
) {$charset_collate};
```

### Table 6: `iexel_os_spot_the_ball_judgements`
```sql
CREATE TABLE {$wpdb->prefix}iexel_os_spot_the_ball_judgements (
    id BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
    competition_id BIGINT(20) UNSIGNED NOT NULL,
    judge_person_id BIGINT(20) UNSIGNED NOT NULL,
    judged_x DECIMAL(7,6) NOT NULL,
    judged_y DECIMAL(7,6) NOT NULL,
    confidence_notes VARCHAR(255) DEFAULT NULL,
    judged_at DATETIME NOT NULL,
    PRIMARY KEY  (id),
    UNIQUE KEY uq_comp_judge (competition_id, judge_person_id),
    KEY idx_competition (competition_id)
) {$charset_collate};
```

### Table 7: `iexel_os_spot_the_ball_results`
```sql
CREATE TABLE {$wpdb->prefix}iexel_os_spot_the_ball_results (
    id BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
    competition_id BIGINT(20) UNSIGNED NOT NULL,
    winning_distance DECIMAL(10,8) NOT NULL,
    total_eligible_entries INT(11) UNSIGNED NOT NULL,
    total_unique_participants INT(11) UNSIGNED NOT NULL,
    tied_winner_count INT(11) UNSIGNED NOT NULL DEFAULT 1,
    prize_pool_total INT(11) UNSIGNED NOT NULL, -- in integer pence
    share_per_winner INT(11) UNSIGNED NOT NULL, -- in integer pence
    remainder_pence INT(11) UNSIGNED NOT NULL DEFAULT 0, -- in integer pence
    calculated_at DATETIME NOT NULL,
    published_at DATETIME DEFAULT NULL,
    published_by BIGINT(20) UNSIGNED DEFAULT NULL,
    PRIMARY KEY  (id),
    UNIQUE KEY uq_competition (competition_id)
) {$charset_collate};
```

### Table 8: `iexel_os_spot_the_ball_prizes`
```sql
CREATE TABLE {$wpdb->prefix}iexel_os_spot_the_ball_prizes (
    id BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
    result_id BIGINT(20) UNSIGNED NOT NULL,
    recipient_person_id BIGINT(20) UNSIGNED NOT NULL,
    winning_entry_id BIGINT(20) UNSIGNED NOT NULL,
    prize_share_pence INT(11) UNSIGNED NOT NULL, -- base share
    remainder_awarded_pence INT(11) UNSIGNED NOT NULL DEFAULT 0, -- 1p if awarded
    total_payout_pence INT(11) UNSIGNED NOT NULL, -- share + remainder
    payout_status VARCHAR(32) NOT NULL DEFAULT 'pending', -- pending, approved, paid, waived
    payout_reference VARCHAR(64) DEFAULT NULL,
    settled_at DATETIME DEFAULT NULL,
    settled_by BIGINT(20) UNSIGNED DEFAULT NULL,
    PRIMARY KEY  (id),
    KEY idx_result (result_id),
    KEY idx_recipient (recipient_person_id),
    KEY idx_entry (winning_entry_id)
) {$charset_collate};
```

---

## 26. Services, Repositories & Components to Reuse

To maintain architectural cohesion, Fundraising reuses established Club OS components:

1. **`IEXEL\ClubOS\Core\Database\DatabaseManager`:** Reused for table name resolution (`$db->table('fundraising_campaigns')`) and DDL installation.
2. **`IEXEL\ClubOS\Core\Upgrade\UpgradeRunner`:** Reused for registering sequential, idempotent database upgrades.
3. **`IEXEL\ClubOS\People\PeopleRepository`:** Reused for person name formatting, identity validation, and linking WordPress users.
4. **`IEXEL\ClubOS\Core\Relationships\PersonRelationshipRepository`:** Reused to verify guardian-child relationships and enforce safeguarding.
5. **`IEXEL\ClubOS\Core\Finance\FinanceService`:** Reused to record incoming payments in `iexel_os_finance_payments` without altering invoice allocation semantics.
6. **`IEXEL\ClubOS\Core\Activity\ActivityLogger`:** Reused for transactional audit trails.
7. **`IEXEL\ClubOS\Core\Communications\CommunicationAttachmentPolicy`:** Reused for validating uploaded campaign images.
8. **`IEXEL\ClubOS\Core\Branding\BrandingService`:** Reused for club colors and badge presentation.
9. **`IEXEL\ClubOS\Core\Portal\PortalRouter` & `PortalShellLayout`:** Reused for portal routing and shell layout.
10. **Design System:** `.iexel-experience-hero`, `.iexel-experience-section`, `.iexel-experience-metrics`, `.iexel-os-card`, `.iexel-accent-top-module`, and `var(--iexel-gold)`.

---

## 27. Proposed New Classes & Components

All new code is namespaced cleanly under `IEXEL\ClubOS\Core\Fundraising\`:

### Domain Entities
- `FundraisingCampaign` — Core campaign entity.
- `FundraisingOrder` — Checkout order entity.
- `FundraisingEntry` — Individual competition/challenge entry.
- `FundraisingContribution` — Appeal donation record.
- `SpotTheBallCompetition` — Competition rules and coordinate configuration.
- `SpotTheBallJudgement` — Single judge coordinate submission.
- `SpotTheBallResult` — Final winning distance, tie count, and prize pool.
- `SpotTheBallPrizeAllocation` — Payout record for each unique winning participant.

### Repositories
- `FundraisingCampaignRepository` — Campaign CRUD and status queries.
- `FundraisingOrderRepository` — Order persistence and payment linkage.
- `FundraisingEntryRepository` — Entry coordinate storage and retrieval.
- `SpotTheBallRepository` — Competition, judging, result, and prize queries.

### Services & Engines
- `FundraisingCampaignService` — Campaign lifecycle state transitions and rules validation.
- `FundraisingOrderService` — Order checkout, fee calculation, and payment activation.
- `SpotTheBallJudgingService` — Blinded judging capture and consensus target calculation.
- `SpotTheBallSealingService` — Immutable target locking and sealing evidence capture.
- `SpotTheBallDistanceEngine` — High-precision Euclidean distance calculation.
- `SpotTheBallTieBreakService` — Unique-person grouping and deterministic penny remainder allocation.
- `FundraisingFinanceBridgeService` — Interfacing orders with `FinanceService` and canonical payment ledgers without mutating invoice allocations.

### UI & Page Controllers
- `PortalMemberFundraisingHubPage` — Frontend portal Member Hub at `/club-os/fundraising/`.
- `PortalSpotTheBallPage` — Interactive canvas game and entry placement.
- `PortalFundraisingAppealPage` — Appeal donation page with progress tracker.
- `PortalSecretaryFundraisingPage` — Secretary campaign management console.
- `PortalTreasurerFundraisingPage` — Treasurer fundraising reconciliation dashboard.

---

## 28. Validator & Test Strategy

To prevent regressions and ensure mathematical accuracy, Fundraising will introduce automated CLI validator suites under `tools/`:

1. **`validate-fundraising-campaign-lifecycle.php`:**
   - Validates all valid FSM transitions (`Draft` $\rightarrow$ `Ready` $\rightarrow$ `Live` $\rightarrow$ `Closed` $\rightarrow$ `Settled` $\rightarrow$ `Completed`).
   - Asserts that invalid jumps (e.g., `Draft` $\rightarrow$ `Live` without sealing) throw domain exceptions.
2. **`validate-spot-the-ball-judging-and-sealing.php`:**
   - Asserts that multiple judge coordinates compute correct derived targets.
   - Verifies target coordinates cannot be altered once sealed.
   - Verifies target coordinates remain hidden from unauthenticated and member queries before official results publication.
3. **`validate-spot-the-ball-distance-engine.php`:**
   - Tests Euclidean distance calculation against known mathematical test vectors.
   - Tests sub-pixel precision on normalized bounds.
   - Tests boundary conditions ($0.0, 0.0$ and $1.0, 1.0$).
4. **`validate-spot-the-ball-tie-and-penny-remainder.php`:**
   - Tests exact-tie detection with epsilon $10^{-7}$.
   - Asserts unique-person prize division: Alice with 2 winning entries and Ben with 1 winning entry split the prize 50/50.
   - Tests £100.00 split among 3 winners: asserts exactly £33.34, £33.33, £33.33 allocated based on earliest entry timestamp.
   - Asserts $\sum \text{Shares} = \text{Total Prize}$ across 1,000 randomized test cases.
5. **`validate-fundraising-safeguarding-and-privacy.php`:**
   - Verifies youth players cannot initiate orders directly.
   - Verifies child names and profiles are absent from public/member responses.
   - Verifies entrant coordinates are hidden before results publication.
6. **`validate-fundraising-finance-boundary.php`:**
   - Asserts fundraising orders do NOT create records in `iexel_os_finance_invoices`.
   - Asserts existing `iexel_os_finance_payment_allocations` semantics are unchanged.
   - Verifies `Payment` records are created in `iexel_os_finance_payments` with correct integer pence amounts.

---

## 29. Migration & Upgrade Strategy

Database changes will be delivered as sequential `UpgradeStep` contracts in `UpgradeRunner`:

```php
// Step 1: Core Fundraising Tables (F1)
new UpgradeStep(
    '2026_09_fundraising_core_schema',
    'schema',
    UpgradeVersions::SCHEMA_VERSION,
    'Create canonical fundraising campaigns, orders, entries, and contributions tables.',
    fn() => $this->database->install_fundraising_core_schema(),
    fn(): bool => $this->database->fundraising_core_schema_valid()
),

// Step 2: Spot the Ball Tables (F2)
new UpgradeStep(
    '2026_09_spot_the_ball_schema',
    'schema',
    UpgradeVersions::SCHEMA_VERSION,
    'Create Spot the Ball competition, judging, results, and prize allocation tables.',
    fn() => $this->database->install_spot_the_ball_schema(),
    fn(): bool => $this->database->spot_the_ball_schema_valid()
),

// Step 3: Capability Backfill (F1)
new UpgradeStep(
    FundraisingCapabilityBackfill::ID,
    'data',
    UpgradeVersions::DATA_VERSION,
    'Provision fundraising management capabilities for existing Secretaries, Admins, and Treasurers.',
    fn() => ( new FundraisingCapabilityBackfill( new Kernel() ) )->apply(),
    fn(): bool => ( new FundraisingCapabilityBackfill( new Kernel() ) )->is_valid()
)
```

---

## 30. Development Phases F1–F6

Delivery is structured into 6 controlled, testable batches:

```
+-------------------------------------------------------------------------------+
| F1: Fundraising Domain Foundation & Appeal MVP                                |
| - Core entities, DB tables, permissions, lifecycle FSM                        |
| - Secretary management shell (/club-os/secretary/fundraising/)                |
| - Member Fundraising Hub shell (/club-os/fundraising/)                        |
| - Fundraising Appeal campaign type (Donations, Target, Supporter Wall)        |
| - Non-polymorphic FundraisingOrder -> FinanceService payment recording bridge |
+-------------------------------------------------------------------------------+
                                        |
                                        v
+-------------------------------------------------------------------------------+
| F2: Spot the Ball Management & Judging                                        |
| - SpotTheBallCompetition entity and configuration                             |
| - Protected source media handling & competition image preparation             |
| - Blinded adult judge console & consensus target calculation                  |
| - Auditable immutable target sealing                                          |
+-------------------------------------------------------------------------------+
                                        |
                                        v
+-------------------------------------------------------------------------------+
| F3: Spot the Ball Member Experience                                           |
| - Interactive HTML5 canvas / touch coordinate selection                       |
| - Touch-assisted magnification & fine-adjustment controls                     |
| - Multi-entry workflow (Entry 1, 2, 3 pin management)                         |
| - Order checkout & payment confirmation boundary                              |
+-------------------------------------------------------------------------------+
                                        |
                                        v
+-------------------------------------------------------------------------------+
| F4: Spot the Ball Results Engine & Settlement                                 |
| - Euclidean distance calculation engine                                       |
| - Unique-person tie-breaking and deterministic penny remainder distribution   |
| - Member results reveal UX & winner presentation                              |
| - Treasurer prize settlement & financial reconciliation dashboard             |
+-------------------------------------------------------------------------------+
                                        |
                                        v
+-------------------------------------------------------------------------------+
| F5: Sponsored Challenges                                                      |
| - Team-based activity challenges (100 Goals, Penalty Shootout)                |
| - Squad progress aggregation                                                  |
| - Private family sponsorship links (zero public child profiles)               |
+-------------------------------------------------------------------------------+
                                        |
                                        v
+-------------------------------------------------------------------------------+
| F6: Club Draw (Compliance-Gated Family)                                       |
| - Future chance-based campaign family                                         |
| - Permitted ONLY after legal, regulatory & operating model review & approval   |
+-------------------------------------------------------------------------------+
```

---

## 31. Acceptance Criteria for Each Phase

### Phase F1: Foundation & Appeal MVP
- [ ] Database upgrade installs core tables idempotently.
- [ ] Capabilities registered and assigned to Secretary, Club Admin, Treasurer, and Parent roles.
- [ ] Secretary can create, edit, publish, and close a Fundraising Appeal.
- [ ] Member Hub displays active appeals with accurate percentage progress bars.
- [ ] Member/Parent can submit a donation with custom or preset tiers.
- [ ] Authoritative payment creates an `iexel_os_finance_payments` record with integer pence amount.
- [ ] An appeal order does **not** create a row in `iexel_os_finance_invoices`.
- [ ] Existing `iexel_os_finance_payment_allocations` semantics remain completely unmodified.
- [ ] Supporter wall respects anonymity toggle; youth players are not publicly profiled.

### Phase F2: Spot the Ball Management & Judging
- [ ] Original image with ball is protected from public web access.
- [ ] Secretary can configure entry price, prize structure, and assign adult judges.
- [ ] Assigned judges can log in and submit coordinates in a blinded interface.
- [ ] System derives consensus coordinate via published, deterministic methodology.
- [ ] Target sealing records immutable timestamp, author, and prevents post-seal mutation.
- [ ] Sealing is blocked if any assigned judge has not submitted.
- [ ] Target coordinates cannot be modified once campaign is `Ready` or `Live`.
- [ ] Target coordinates remain hidden from all non-admin users before official publication.

### Phase F3: Spot the Ball Member Experience
- [ ] Canvas renders competition image responsively across mobile (320px) to desktop (4K).
- [ ] Touch on mobile renders magnification loupe avoiding finger obstruction.
- [ ] Crosshairs place accurately with fine-adjustment controls.
- [ ] Normalized coordinates ($0.000000$ to $1.000000$) match native image features on all devices.
- [ ] Multi-entry checkout allows placing distinct pins for Entry 1, 2, and 3.
- [ ] Unpaid entries remain `pending_payment`; payment confirmation transitions them to `confirmed`.
- [ ] Other entrants' coordinates are invisible in browser network responses.

### Phase F4: Spot the Ball Results Engine & Settlement
- [ ] Distance engine calculates Euclidean distance with $10^{-8}$ precision.
- [ ] Ties within stored precision group by unique winning person.
- [ ] A participant with 2 winning entries receives only 1 prize share.
- [ ] Remainder pence are distributed deterministically by earliest entry timestamp without penny loss.
- [ ] Results page displays community achievement, winning distance, and target reveal.
- [ ] Cash prize payouts for minors follow the approved guardian settlement workflow.
- [ ] Treasurer dashboard displays gross collected, fees, prizes, and net surplus.

### Phase F5: Sponsored Challenges
- [ ] Squad challenges track cumulative metrics (e.g., 100 goals).
- [ ] Zero public child URLs or search-engine-indexed child donation pages.
- [ ] Sponsors donate via private family links authenticated or linked to known guardians.

### Phase F6: Club Draw (Compliance-Gated)
- [ ] Blocked until club completes formal regulatory, legal, and operational review.
- [ ] Operating model and statutory compliance route explicitly approved before development begins.

---

## 32. Open Compliance & Product Gates

Before code implementation commences for specific phases, the following gates must be formally satisfied:

1. **Gate 1: Spot the Ball Skill Competition Legal Policy (Pre-F2):**
   - Confirmation that the independent panel adjudication and published rules meet Section 14 criteria under the UK Gambling Act 2005.
2. **Gate 2: Payment Provider Selection (Pre-F3):**
   - Decision on whether online card payments will interface with an existing Stripe account (using Stripe Elements / Checkout) or an alternative provider, adhering to the provider abstraction in `FinanceAccount`.
3. **Gate 3: Gift Aid Eligibility & Contribution Scope (Deferred Enhancement):**
   - Detailed review of club CASC/charity status and qualification criteria for specific contribution types before introducing Gift Aid features.
4. **Gate 4: Club Draw Operating Model & Regulatory Route (Pre-F6):**
   - Comprehensive legal/compliance review establishing the applicable jurisdiction, club operating model, draw mechanics, and required registrations/licences before Phase F6 can be considered.

---

## 33. Explicit Deferred & Post-MVP Items

The following features are intentionally excluded from the initial implementation and deferred to future releases:

1. **Club Draw Runtime Implementation:** Strictly deferred to Phase F6 pending regulatory operating model approval.
2. **Gift Aid Support:** Deferred until club CASC/charity eligibility and contribution qualifying rules are specifically reviewed.
3. **Automated Recurring Lottery Subscriptions:** Recurring direct debits for weekly/monthly draws.
4. **Merchandise & eCommerce Shop:** Selling club scarves, kits, or beanies (belongs in a future Club Shop module, not Fundraising).
5. **Peer-to-Peer Social Leaderboards:** Individual public child leaderboards (rejected for safeguarding).
6. **Multi-Currency Processing:** Club OS Fundraising strictly operates in British Pounds (`GBP` / integer pence). Multi-currency processing is deferred.
