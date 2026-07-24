# Finance Architecture

**Source of truth:** `app/core/Finance/`
**Last verified:** 2026-07-24

---

## Overview

The Finance module provides invoice management, payment recording, billing schedules, fee rules, discount policies and automated billing runs. It is accessible to users with `iexel_view_finance` or higher finance capabilities.

---

## Domain Entities

| Entity | Class | Table |
|---|---|---|
| Invoice | `Invoice` | `finance_invoices` |
| Invoice line | `InvoiceLine` | `finance_invoice_lines` |
| Payment | `Payment` | `finance_payments` |
| Payment allocation | `PaymentAllocation` | `finance_payment_allocations` |
| Finance account | `FinanceAccount` | `finance_accounts` |
| Invoice event | — | `finance_invoice_events` |
| Billing schedule | `BillingSchedule` | `finance_billing_schedules` |
| Fee rule | `FeeRule` | `finance_fee_rules` |
| Discount policy | `DiscountPolicy` | `finance_discount_policies` |
| Billing run | `BillingRun` | `finance_billing_runs` |
| Billing run item | `BillingRunItem` | `finance_billing_run_items` |

---

## Services

| Service | Responsibility |
|---|---|
| `FinanceService` | Invoice and payment CRUD, allocation, reporting |
| `RecurringBillingService` | Process due billing schedules, generate invoices |
| `BillingAudienceResolver` | Resolve billing audience from schedule criteria |
| `ResponsibleBillingContactResolver` | Determine billing contact for a person |
| `FinanceValidator` | Validate invoice and payment inputs |
| `BillingScheduleValidator` | Validate billing schedule inputs |
| `FeeRuleValidator` | Validate fee rule inputs |
| `DiscountPolicyValidator` | Validate discount policy inputs |

---

## Billing Run Flow

1. `WordPressBillingScheduler` fires `iexel_club_os_process_billing_schedules` on an hourly WP-Cron schedule.
2. `RecurringBillingService::process_due()` queries all active billing schedules due for processing.
3. For each schedule, `BillingAudienceResolver` resolves the billing audience.
4. `BillingPreview` is generated showing candidates and amounts.
5. Invoices are generated for each candidate via `FinanceService`.
6. A `BillingRun` record is created with all `BillingRunItem` results.

---

## Portal Finance Workspace

The Treasurer experience provides a full Finance workspace at `/club-os/finance/`. Sub-sections:

| Path | Purpose |
|---|---|
| `/club-os/finance` | Finance dashboard |
| `/club-os/finance/invoices` | Invoice list |
| `/club-os/finance/invoices/new` | New invoice |
| `/club-os/finance/invoices/bulk` | Bulk invoice creation |
| `/club-os/finance/payments` | Payment list |
| `/club-os/finance/outstanding` | Outstanding balances |
| `/club-os/finance/billing-schedules` | Billing schedule management |
| `/club-os/finance/billing-schedules/new` | New billing schedule |
| `/club-os/finance/billing-schedules/edit` | Edit billing schedule |
| `/club-os/finance/fee-rules` | Fee rule management |
| `/club-os/finance/discount-policies` | Discount policy management |
| `/club-os/finance/billing-runs` | Billing run history |
| `/club-os/finance/reports` | Finance reports |

---

## Request Actions

All Finance mutations are handled by `FinanceAdminRequestHandler` via `admin_post_iexel_finance_{action}` hooks.

---

## Status

**MVP Complete.** Core invoice, payment and billing schedule workflows are implemented. Export functionality (`iexel_export_finance`) is declared but not yet implemented.
