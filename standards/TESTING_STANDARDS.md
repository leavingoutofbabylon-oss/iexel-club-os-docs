# Testing Standards

**Applies to:** All test files for `iexel-club-os`
**Last verified:** 2026-07-24

---

## Overview

Club OS uses PHPUnit for unit and integration tests. Tests are located in the `tests/` directory.

> **Note:** At the time of writing, the test suite is in its early stages. This document defines the standards for tests as they are written.

---

## Test Directory Structure

```
tests/
  unit/
    Core/
      Finance/
      People/
      ...
  integration/
    ...
  bootstrap.php
```

---

## Unit Tests

Unit tests test a single class in isolation. Dependencies are mocked using PHPUnit mock objects or a test double library.

```php
class FinanceServiceTest extends WP_UnitTestCase {

    public function test_create_invoice_returns_invoice_id(): void {
        $repo   = $this->createMock( FinanceRepository::class );
        $logger = $this->createMock( ActivityLogger::class );

        $repo->expects( $this->once() )
             ->method( 'create_invoice' )
             ->willReturn( 42 );

        $service = new FinanceService( $repo, $logger );
        $result  = $service->create_invoice( [ 'person_id' => 1, 'total_amount' => 50.00 ] );

        $this->assertSame( 42, $result );
    }
}
```

---

## Integration Tests

Integration tests test a service against a real (test) database. They use the WordPress test suite's database setup and teardown.

---

## Test Naming

Test methods are named `test_{method_name}_{scenario}_{expected_outcome}`.

```
test_create_invoice_with_valid_data_returns_invoice_id
test_create_invoice_with_missing_person_id_returns_wp_error
```

---

## Coverage Requirements

At MVP, the following modules require test coverage:

- `FinanceService` (invoice creation, payment recording, billing run)
- `SeasonPlanningService` (plan generation, approval, execution)
- `ClubRoleCapabilityRegistrar` (capability registration)
- `UpgradeRunner` (step execution, idempotency)

---

## Running Tests

```bash
cd iexel-club-os
composer install
./vendor/bin/phpunit
```

---

## Definition of Done for Tests

A test is considered done when:

1. It passes locally and in CI
2. It covers the happy path and at least one error path
3. It does not depend on external services or hardcoded data
4. It cleans up any data it creates
