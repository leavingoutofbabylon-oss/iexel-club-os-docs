# Database Table Reference

**Source of truth:** `app/core/Database/DatabaseManager.php`
**Last verified:** 2026-07-24

---

## Table Prefix

All tables use the prefix `{wpdb->prefix}iexel_os_`. With the default WordPress prefix `wp_`, the `people` table is `wp_iexel_os_people`.

---

## Core Tables

### `activity_log`

Global activity log for all Club OS operations.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `user_id` | BIGINT UNSIGNED | WordPress user ID (0 for system) |
| `action` | VARCHAR(191) | Action key (e.g. `core_booted`, `person_created`) |
| `object_type` | VARCHAR(100) | Object type (e.g. `person`, `team`) |
| `object_id` | BIGINT UNSIGNED | Object ID |
| `message` | TEXT | Human-readable message |
| `metadata` | LONGTEXT | JSON metadata |
| `created_at` | DATETIME | UTC timestamp |

### `system_flags`

Key-value store for system flags and feature switches.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `flag_key` | VARCHAR(191) UNIQUE | Flag key |
| `flag_value` | TEXT | Flag value |
| `updated_at` | DATETIME | UTC timestamp |

---

## People Tables

### `people`

Core person records for all club members.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `club_id` | VARCHAR(50) | Club-assigned ID (e.g. `IEXEL-001`), NOT NULL, UNIQUE |
| `wp_user_id` | BIGINT UNSIGNED | Linked WordPress user ID, DEFAULT 0 |
| `first_name` | VARCHAR(100) | First name, NOT NULL |
| `last_name` | VARCHAR(100) | Last name, NOT NULL |
| `display_name` | VARCHAR(191) | Full display name, DEFAULT '' |
| `date_of_birth` | DATE | Date of birth, NULL |
| `email` | VARCHAR(191) | Email address, DEFAULT '' |
| `phone` | VARCHAR(100) | Phone number, DEFAULT '' |
| `address` | TEXT | Physical address, NULL |
| `profile_attachment_id` | BIGINT UNSIGNED | Profile photo attachment ID, NULL |
| `profile_focal_position` | VARCHAR(20) | Profile photo focal position, NOT NULL DEFAULT '50% 50%' |
| `status` | VARCHAR(50) | `active`, `inactive`, `suspended`, DEFAULT 'active' |
| `created_at` | DATETIME | UTC timestamp, NOT NULL |
| `updated_at` | DATETIME | UTC timestamp, NULL |

**Indexes:**
- `PRIMARY KEY (id)`
- `UNIQUE KEY club_id (club_id)`
- `KEY wp_user_id (wp_user_id)`
- `KEY email (email)`
- `KEY status (status)`

### `person_roles`

Roles assigned to people (player, parent, coach, etc.).

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `person_id` | BIGINT UNSIGNED | FK to `people.id` |
| `role_key` | VARCHAR(100) | Role key (e.g. `player`, `parent`, `coach`) |
| `status` | VARCHAR(50) | `active`, `inactive` |
| `created_at` | DATETIME | UTC timestamp |

### `person_relationships`

Family and guardian relationships between people.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `person_id` | BIGINT UNSIGNED | The person (e.g. child) |
| `related_person_id` | BIGINT UNSIGNED | The related person (e.g. parent) |
| `relationship_type` | VARCHAR(100) | `parent`, `guardian`, `billing_contact` |
| `is_billing_contact` | TINYINT(1) | Whether this is the billing contact |
| `created_at` | DATETIME | UTC timestamp |

---

## Teams Tables

### `teams`

Team records.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `name` | VARCHAR(255) | Team name |
| `age_group` | VARCHAR(50) | Age group (e.g. `U9`, `U11`) |
| `football_format` | VARCHAR(50) | Format (e.g. `5v5`, `7v7`, `11v11`) |
| `status` | VARCHAR(50) | `active`, `inactive` |
| `metadata` | LONGTEXT | JSON metadata |
| `created_at` | DATETIME | UTC timestamp |
| `updated_at` | DATETIME | UTC timestamp |

### `team_assignments`

Assignments of people to teams with roles.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `team_id` | BIGINT UNSIGNED | FK to `teams.id` |
| `person_id` | BIGINT UNSIGNED | FK to `people.id` |
| `assignment_role` | VARCHAR(100) | `player`, `head_coach`, `assistant_coach` |
| `status` | VARCHAR(50) | `active`, `inactive` |
| `season_id` | BIGINT UNSIGNED | FK to `seasons.id` (nullable) |
| `created_at` | DATETIME | UTC timestamp |
| `updated_at` | DATETIME | UTC timestamp |

---

## Seasons Tables

### `seasons`

Season records.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `name` | VARCHAR(255) | Season name (e.g. `2025/26`) |
| `start_date` | DATE | Season start date |
| `end_date` | DATE | Season end date |
| `is_current` | TINYINT(1) | Whether this is the current season |
| `status` | VARCHAR(50) | `active`, `archived` |
| `created_at` | DATETIME | UTC timestamp |
| `updated_at` | DATETIME | UTC timestamp |

### `team_seasons`

Canonical season links for teams.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `team_id` | BIGINT UNSIGNED | FK to `teams.id` |
| `season_id` | BIGINT UNSIGNED | FK to `seasons.id` |
| `status` | VARCHAR(50) | `active`, `archived` |
| `created_at` | DATETIME | UTC timestamp |

---

## Venues Table

### `venues`

Venue records for events.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `name` | VARCHAR(255) | Venue name |
| `address` | TEXT | Full address |
| `postcode` | VARCHAR(20) | Postcode |
| `map_link` | TEXT | Map URL |
| `created_at` | DATETIME | UTC timestamp |
| `updated_at` | DATETIME | UTC timestamp |

---

## Events Tables

### `events`

Event records (training, matches, tournaments).

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `title` | VARCHAR(191) | Event title, NOT NULL |
| `type` | VARCHAR(50) | `match`, `friendly`, `training`, `tournament`, NOT NULL DEFAULT 'training' |
| `team_id` | BIGINT UNSIGNED | FK to `teams.id`, NOT NULL DEFAULT 0 |
| `season_id` | BIGINT UNSIGNED | FK to `seasons.id`, NULL |
| `team_season_id` | BIGINT UNSIGNED | FK to `team_seasons.id`, NULL |
| `venue_id` | BIGINT UNSIGNED | FK to `venues.id`, NOT NULL DEFAULT 0 |
| `venue_name` | VARCHAR(191) | Venue name override, NOT NULL DEFAULT '' |
| `venue_address` | TEXT | Venue address override, NULL |
| `venue_postcode` | VARCHAR(20) | Venue postcode override, NOT NULL DEFAULT '' |
| `event_date` | DATE | Event date, NOT NULL |
| `start_time` | TIME | Start time, NULL |
| `end_time` | TIME | End time, NULL |
| `description` | TEXT | Event description, NULL |
| `banner_attachment_id` | BIGINT UNSIGNED | Event banner image, NULL |
| `banner_focal_position` | VARCHAR(20) | Banner focal position, NOT NULL DEFAULT '50% 50%' |
| `banner_responsive_media` | LONGTEXT | Responsive banner config, NULL |
| `status` | VARCHAR(50) | `scheduled`, `cancelled`, `completed`, NOT NULL DEFAULT 'scheduled' |
| `created_at` | DATETIME | UTC timestamp, NOT NULL |
| `updated_at` | DATETIME | UTC timestamp, NULL |

**Indexes:**
- `PRIMARY KEY (id)`
- `KEY type (type)`
- `KEY team_id (team_id)`
- `KEY venue_id (venue_id)`
- `KEY event_date (event_date)`
- `KEY status (status)`
- `KEY season_date_type (season_id, event_date, type, status)`
- `KEY team_season_date (team_season_id, event_date, status)`

### `event_audience`

Audience members for each event.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `event_id` | BIGINT UNSIGNED | FK to `events.id` |
| `person_id` | BIGINT UNSIGNED | FK to `people.id` |
| `audience_role` | VARCHAR(100) | Role in the audience |
| `created_at` | DATETIME | UTC timestamp |

### `attendance`

Attendance records for events.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `event_id` | BIGINT UNSIGNED | FK to `events.id` |
| `person_id` | BIGINT UNSIGNED | FK to `people.id` |
| `status` | VARCHAR(50) | `attended`, `absent`, `late` |
| `recorded_by` | BIGINT UNSIGNED | WordPress user ID |
| `created_at` | DATETIME | UTC timestamp |

### `event_availability`

Pre-event availability responses.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `event_id` | BIGINT UNSIGNED | FK to `events.id` |
| `person_id` | BIGINT UNSIGNED | FK to `people.id` |
| `status` | VARCHAR(50) | `available`, `unavailable`, `unknown` |
| `note` | TEXT | Optional note |
| `created_at` | DATETIME | UTC timestamp |
| `updated_at` | DATETIME | UTC timestamp |

---

## Registrations Table

### `player_registrations`

Player registration records.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `person_id` | BIGINT UNSIGNED | FK to `people.id` (nullable until approved) |
| `submitted_by` | BIGINT UNSIGNED | WordPress user ID of submitter |
| `status` | VARCHAR(50) | `draft`, `submitted`, `under_review`, `approved`, `rejected`, `withdrawn` |
| `form_data` | LONGTEXT | JSON form data |
| `reviewer_notes` | TEXT | Administrator review notes |
| `created_at` | DATETIME | UTC timestamp |
| `updated_at` | DATETIME | UTC timestamp |

---

## Match Mode Tables

### `formation_templates`

Formation template definitions.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `name` | VARCHAR(255) | Template name |
| `football_format` | VARCHAR(50) | `5v5`, `7v7`, `9v9`, `11v11` |
| `is_system` | TINYINT(1) | Whether this is a system template |
| `created_at` | DATETIME | UTC timestamp |

### `formation_template_slots`

Slot definitions for formation templates.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `template_id` | BIGINT UNSIGNED | FK to `formation_templates.id` |
| `position_key` | VARCHAR(50) | Position key (e.g. `GK`, `CB`, `ST`) |
| `display_order` | INT | Display order |

### `event_match_details`

Match details (score, result, opponent).

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `event_id` | BIGINT UNSIGNED UNIQUE | FK to `events.id` |
| `opponent` | VARCHAR(255) | Opponent name |
| `home_away` | VARCHAR(10) | `home`, `away`, `neutral` |
| `goals_for` | INT UNSIGNED | Goals scored |
| `goals_against` | INT UNSIGNED | Goals conceded |
| `result` | VARCHAR(10) | `win`, `loss`, `draw` |
| `metadata` | LONGTEXT | JSON metadata |
| `updated_at` | DATETIME | UTC timestamp |

### `event_match_selections`

Pre-match player selections.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `event_id` | BIGINT UNSIGNED | FK to `events.id` |
| `person_id` | BIGINT UNSIGNED | FK to `people.id` |
| `selection_status` | VARCHAR(50) | `selected`, `reserve`, `not_selected` |
| `shirt_number` | INT UNSIGNED | Shirt number (nullable) |
| `formation_slot_id` | BIGINT UNSIGNED | FK to `formation_template_slots.id` (nullable) |
| `created_at` | DATETIME | UTC timestamp |

### `event_match_lineups`

Match lineup metadata.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `event_id` | BIGINT UNSIGNED UNIQUE | FK to `events.id` |
| `formation_template_id` | BIGINT UNSIGNED | FK to `formation_templates.id` (nullable) |
| `submitted_at` | DATETIME | When lineup was submitted |
| `metadata` | LONGTEXT | JSON metadata |

### `event_match_incidents`

Match incidents (goals, cards, substitutions).

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `event_id` | BIGINT UNSIGNED | FK to `events.id` |
| `incident_type` | VARCHAR(50) | `goal`, `own_goal`, `yellow_card`, `red_card`, `substitution` |
| `person_id` | BIGINT UNSIGNED | FK to `people.id` (nullable) |
| `minute` | INT UNSIGNED | Match minute |
| `metadata` | LONGTEXT | JSON metadata |
| `created_at` | DATETIME | UTC timestamp |
| `is_undone` | TINYINT(1) | Whether this incident has been undone |

### `event_match_action_requests`

Queued match action requests for async processing.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `event_id` | BIGINT UNSIGNED | FK to `events.id` |
| `action_type` | VARCHAR(100) | Action type |
| `payload` | LONGTEXT | JSON payload |
| `status` | VARCHAR(50) | `pending`, `processed`, `failed` |
| `created_at` | DATETIME | UTC timestamp |

### `event_match_reports`

Post-match reports.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `event_id` | BIGINT UNSIGNED UNIQUE | FK to `events.id` |
| `report_text` | LONGTEXT | Match report text |
| `player_of_match_id` | BIGINT UNSIGNED | FK to `people.id` (nullable) |
| `submitted_by` | BIGINT UNSIGNED | WordPress user ID |
| `submitted_at` | DATETIME | UTC timestamp |

### `event_match_player_ratings`

Player ratings from match reports.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `event_id` | BIGINT UNSIGNED | FK to `events.id` |
| `person_id` | BIGINT UNSIGNED | FK to `people.id` |
| `rating` | TINYINT UNSIGNED | Rating (1–10) |
| `created_at` | DATETIME | UTC timestamp |

---

## Finance Tables

### `finance_accounts`

Finance accounts for tracking balances.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `person_id` | BIGINT UNSIGNED | FK to `people.id` |
| `balance` | DECIMAL(10,2) | Current balance |
| `created_at` | DATETIME | UTC timestamp |
| `updated_at` | DATETIME | UTC timestamp |

### `finance_invoices`

Invoice records.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `person_id` | BIGINT UNSIGNED | FK to `people.id` (invoice recipient) |
| `status` | VARCHAR(50) | `draft`, `issued`, `paid`, `overdue`, `cancelled` |
| `due_date` | DATE | Payment due date |
| `total_amount` | DECIMAL(10,2) UNSIGNED | Total invoice amount |
| `paid_amount` | DECIMAL(10,2) UNSIGNED | Amount paid |
| `notes` | TEXT | Invoice notes |
| `created_at` | DATETIME | UTC timestamp |
| `updated_at` | DATETIME | UTC timestamp |

### `finance_invoice_lines`

Line items for invoices.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `invoice_id` | BIGINT UNSIGNED | FK to `finance_invoices.id` |
| `description` | VARCHAR(500) | Line item description |
| `quantity` | DECIMAL(10,2) | Quantity |
| `unit_amount` | DECIMAL(10,2) UNSIGNED | Unit price |
| `total_amount` | DECIMAL(10,2) UNSIGNED | Line total |
| `created_at` | DATETIME | UTC timestamp |

### `finance_payments`

Payment records.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `person_id` | BIGINT UNSIGNED | FK to `people.id` |
| `amount` | DECIMAL(10,2) UNSIGNED | Payment amount |
| `payment_method` | VARCHAR(100) | Payment method |
| `payment_date` | DATE | Payment date |
| `reference` | VARCHAR(255) | Payment reference |
| `recorded_by` | BIGINT UNSIGNED | WordPress user ID |
| `created_at` | DATETIME | UTC timestamp |

### `finance_payment_allocations`

Allocations of payments to invoices.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `payment_id` | BIGINT UNSIGNED | FK to `finance_payments.id` |
| `invoice_id` | BIGINT UNSIGNED | FK to `finance_invoices.id` |
| `allocated_amount` | DECIMAL(10,2) UNSIGNED | Amount allocated |
| `created_at` | DATETIME | UTC timestamp |

### `finance_invoice_events`

Audit trail for invoice lifecycle events.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `invoice_id` | BIGINT UNSIGNED | FK to `finance_invoices.id` |
| `event_type` | VARCHAR(100) | Event type (e.g. `issued`, `paid`, `cancelled`) |
| `user_id` | BIGINT UNSIGNED | WordPress user ID |
| `metadata` | LONGTEXT | JSON metadata |
| `created_at` | DATETIME | UTC timestamp |

### `finance_billing_schedules`

Recurring billing schedule definitions.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `name` | VARCHAR(255) | Schedule name |
| `status` | VARCHAR(50) | `active`, `paused`, `archived` |
| `frequency` | VARCHAR(50) | `monthly`, `termly`, `annually`, `one_off` |
| `audience_criteria` | LONGTEXT | JSON audience criteria |
| `fee_rule_id` | BIGINT UNSIGNED | FK to `finance_fee_rules.id` |
| `next_run_date` | DATE | Next scheduled run date |
| `created_at` | DATETIME | UTC timestamp |
| `updated_at` | DATETIME | UTC timestamp |

### `finance_fee_rules`

Fee rule definitions for billing.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `name` | VARCHAR(255) | Fee rule name |
| `amount` | DECIMAL(10,2) UNSIGNED | Fee amount |
| `description` | TEXT | Fee description |
| `status` | VARCHAR(50) | `active`, `archived` |
| `created_at` | DATETIME | UTC timestamp |
| `updated_at` | DATETIME | UTC timestamp |

### `finance_discount_policies`

Discount policy definitions.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `name` | VARCHAR(255) | Policy name |
| `discount_type` | VARCHAR(50) | `percentage`, `fixed` |
| `discount_value` | DECIMAL(10,2) UNSIGNED | Discount value |
| `criteria` | LONGTEXT | JSON eligibility criteria |
| `status` | VARCHAR(50) | `active`, `archived` |
| `created_at` | DATETIME | UTC timestamp |

### `finance_billing_runs`

Billing run records.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `schedule_id` | BIGINT UNSIGNED | FK to `finance_billing_schedules.id` |
| `status` | VARCHAR(50) | `completed`, `failed`, `partial` |
| `run_at` | DATETIME | UTC timestamp |
| `total_invoices` | INT UNSIGNED | Total invoices generated |
| `total_amount` | DECIMAL(10,2) UNSIGNED | Total amount invoiced |

### `finance_billing_run_items`

Individual items from a billing run.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `run_id` | BIGINT UNSIGNED | FK to `finance_billing_runs.id` |
| `person_id` | BIGINT UNSIGNED | FK to `people.id` |
| `invoice_id` | BIGINT UNSIGNED | FK to `finance_invoices.id` (nullable if failed) |
| `status` | VARCHAR(50) | `success`, `failed`, `skipped` |
| `amount` | DECIMAL(10,2) UNSIGNED | Invoice amount |
| `error_message` | TEXT | Error message if failed |

---

## Club Projects Table

### `club_projects`

Club project records.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `title` | VARCHAR(255) | Project title |
| `summary` | TEXT | Project summary |
| `progress_percent` | INT UNSIGNED | Progress (0–100) |
| `status` | VARCHAR(50) | `planning`, `on_track`, `needs_attention`, `paused`, `completed` |
| `priority` | VARCHAR(50) | `low`, `normal`, `high`, `critical` |
| `category` | VARCHAR(100) | `facilities`, `ground`, `equipment`, `fundraising`, `events`, `governance`, `marketing`, `general` |
| `owner_person_id` | BIGINT UNSIGNED | FK to `people.id` (nullable) |
| `target_date` | DATE | Target completion date (nullable) |
| `display_order` | INT UNSIGNED | Sort order |
| `is_visible` | TINYINT(1) | Visible on Committee workspace |
| `is_archived` | TINYINT(1) | Archived flag |
| `created_at` | DATETIME | UTC timestamp |
| `updated_at` | DATETIME | UTC timestamp |

---

## Communications Tables

### `communications`

Communication records.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `subject` | VARCHAR(500) | Email subject |
| `body` | LONGTEXT | Email body (HTML) |
| `status` | VARCHAR(50) | `draft`, `scheduled`, `sent`, `cancelled` |
| `channel` | VARCHAR(50) | `email` |
| `audience_criteria` | LONGTEXT | JSON audience criteria |
| `scheduled_at` | DATETIME | Scheduled send time (nullable) |
| `sent_at` | DATETIME | Actual send time (nullable) |
| `created_by` | BIGINT UNSIGNED | WordPress user ID |
| `created_at` | DATETIME | UTC timestamp |
| `updated_at` | DATETIME | UTC timestamp |

### `communication_recipients`

Recipient snapshot for each communication.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `communication_id` | BIGINT UNSIGNED | FK to `communications.id` |
| `person_id` | BIGINT UNSIGNED | FK to `people.id` |
| `email` | VARCHAR(255) | Email at time of snapshot |
| `name` | VARCHAR(255) | Name at time of snapshot |
| `created_at` | DATETIME | UTC timestamp |

### `communication_deliveries`

Delivery attempts for each recipient.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `communication_id` | BIGINT UNSIGNED | FK to `communications.id` |
| `recipient_id` | BIGINT UNSIGNED | FK to `communication_recipients.id` |
| `status` | VARCHAR(50) | `sent`, `failed`, `bounced` |
| `attempted_at` | DATETIME | UTC timestamp |
| `error_message` | TEXT | Error if failed |

### `communication_templates`

Reusable communication templates.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `name` | VARCHAR(255) | Template name |
| `subject` | VARCHAR(500) | Default subject |
| `body` | LONGTEXT | Template body (HTML) |
| `created_at` | DATETIME | UTC timestamp |
| `updated_at` | DATETIME | UTC timestamp |

### `communication_attachments`

File attachments for communications.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `communication_id` | BIGINT UNSIGNED | FK to `communications.id` |
| `attachment_id` | BIGINT UNSIGNED | WordPress media attachment ID |
| `created_at` | DATETIME | UTC timestamp |

### `communication_events`

Lifecycle events for communications.

| Column | Type | Description |
|---|---|---|
| `id` | BIGINT UNSIGNED AUTO_INCREMENT | Primary key |
| `communication_id` | BIGINT UNSIGNED | FK to `communications.id` |
| `event_type` | VARCHAR(100) | `created`, `scheduled`, `sent`, `cancelled` |
| `user_id` | BIGINT UNSIGNED | WordPress user ID |
| `created_at` | DATETIME | UTC timestamp |
