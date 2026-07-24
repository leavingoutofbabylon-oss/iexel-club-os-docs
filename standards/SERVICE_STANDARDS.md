# Service Standards

**Applies to:** All `*Service.php` classes under `app/core/`
**Last verified:** 2026-07-24

---

## Overview

Services contain business logic and orchestrate operations across repositories. They do not contain database access code directly.

---

## Naming

Service classes are named `{Domain}Service` (e.g. `FinanceService`, `SeasonPlanningService`). Each service is responsible for a single domain.

---

## Constructor

Services receive all dependencies via constructor injection. Dependencies are typed and declared `private readonly`.

```php
public function __construct(
    private readonly FinanceRepository $finance_repo,
    private readonly ActivityLogger $logger,
    private readonly PeopleRepository $people_repo
) {}
```

---

## Return Types

Service methods must declare return types. Use `?Type` for nullable returns. Use `WP_Error` for recoverable errors. Use `void` for operations that do not return a value.

---

## Activity Logging

Any operation that creates, modifies or deletes a domain entity must log to the activity log via `ActivityLogger`.

```php
$this->logger->log(
    get_current_user_id(),
    'finance_invoice_created',
    'finance_invoice',
    $invoice_id,
    "Invoice #{$invoice_id} created for person #{$person_id}"
);
```

---

## Transactions

For operations that modify multiple tables atomically, use `$wpdb->query('START TRANSACTION')` and `$wpdb->query('COMMIT')` with a `ROLLBACK` on failure. The `SeasonPlanningService::execute_plan()` method is the canonical example.

---

## Caching

Services may use WordPress transients for read-heavy data. Transient keys must be prefixed `iexel_` and must be cleared when the underlying data changes.

The `ExecutiveDashboardService` uses a 60-second transient (`iexel_exec_dashboard_data`). This is the maximum permitted cache lifetime for dashboard data.

---

## No Direct Output

Services must never echo, print or call `wp_die()`. All error conditions must be returned as `WP_Error` or thrown as exceptions.
