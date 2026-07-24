# Communications Architecture

**Source of truth:** `app/core/Communications/`
**Last verified:** 2026-07-24

---

## Overview

The Communications module provides email sending, announcement management, recipient snapshots, template management and delivery audit. Communications can be sent immediately or scheduled for future delivery.

---

## Domain Entities

| Entity | Class | Table |
|---|---|---|
| Communication | `Communication` | `communications` |
| Recipient | `CommunicationRecipient` | `communication_recipients` |
| Delivery | `CommunicationDelivery` | `communication_deliveries` |
| Template | `CommunicationTemplate` | `communication_templates` |
| Attachment | `CommunicationAttachment` | `communication_attachments` |
| Event | — | `communication_events` |

---

## Services

| Service | Responsibility |
|---|---|
| `CommunicationService` | Orchestrate send, schedule and delivery flows |
| `CommunicationRepository` | CRUD for communications and related entities |
| `CommunicationAudienceResolver` | Resolve recipient list from audience criteria |
| `CommunicationValidator` | Validate communication inputs |
| `CommunicationScheduler` | WP-Cron scheduling for deferred sends |
| `WordPressEmailSender` | WordPress `wp_mail()` adapter |

---

## Audience Resolution

`CommunicationAudienceResolver` supports the following audience types:

- **Role-based** — All people with a specific Club OS role (e.g. all parents, all coaches)
- **Team-based** — All members of a specific team
- **Season-based** — All members of a specific season

Recipients are snapshotted at send time into `communication_recipients` to preserve the audience at the point of sending.

---

## Scheduled Delivery

Communications can be scheduled for future delivery. The `CommunicationScheduler` registers a single WP-Cron event (`iexel_club_os_process_communication`) per scheduled communication. The event fires `CommunicationService::process_scheduled_communication()`.

---

## Delivery Audit

Every delivery attempt is recorded in `communication_deliveries` with status (sent, failed, bounced). The `communication_events` table records lifecycle events (created, scheduled, sent, cancelled).

---

## Status

**MVP Complete.** Core email sending, scheduling, templates and delivery audit are implemented. The `iexel_manage_communications` capability is declared but the Communications admin handler currently checks `iexel_manage_club_os`. This inconsistency is tracked in the Technical Debt Register.
