# PHP Coding Standards

**Applies to:** All PHP files under `app/core/` and `app/` in `iexel-club-os`
**Last verified:** 2026-07-24

---

## Overview

Club OS follows WordPress Coding Standards (WPCS) with the specific conventions documented here. All new code must pass PHPCS with the project's ruleset before merging.

---

## Namespace and Class Conventions

All classes under `app/core/` use the namespace `IexelClubOS\Core\{Module}`. Legacy classes under `app/` use `IexelClubOS\{Module}`.

```php
namespace IexelClubOS\Core\Finance;

class FinanceService {
    // ...
}
```

Class names use PascalCase. File names match the class name exactly (`FinanceService.php`).

---

## File Structure

Every PHP file begins with:

```php
<?php

namespace IexelClubOS\Core\{Module};

if ( ! defined( 'ABSPATH' ) ) {
    exit;
}
```

The `ABSPATH` guard is mandatory on every file.

---

## Dependency Injection

Services receive dependencies via constructor injection. The Kernel provides lazy-initialised instances. Never use `new` inside a service method; always inject or receive from the Kernel.

```php
public function __construct(
    private readonly PeopleRepository $people_repo,
    private readonly ActivityLogger $logger
) {}
```

---

## Database Access

All database access goes through repository classes. Direct `$wpdb` access is only permitted inside repository methods.

Use `$wpdb->prepare()` for all queries with user-supplied values. For `IN` clauses, use `implode(',', array_fill(0, count($ids), '%d'))` with a PHPCS suppression comment explaining the pattern is safe.

```php
// phpcs:ignore WordPress.DB.PreparedSQL.InterpolatedNotPrepared -- $placeholders is a safe integer placeholder string
$results = $wpdb->get_results(
    $wpdb->prepare(
        "SELECT * FROM {$this->table} WHERE id IN ({$placeholders})",
        ...$ids
    )
);
```

---

## Capability Checks

Every admin page and request handler must check the required capability before rendering or processing.

```php
if ( ! current_user_can( 'iexel_manage_finance' ) ) {
    wp_die( esc_html__( 'You do not have permission to access this page.', 'iexel-club-os' ) );
}
```

Portal pages use the `MemberExperienceService` to check experience-level access.

---

## Nonce Verification

Every form submission must include a nonce field and verify it in the handler.

```php
// In the form:
wp_nonce_field( 'iexel_club_project_create', 'iexel_nonce' );

// In the handler:
if ( ! wp_verify_nonce( sanitize_text_field( wp_unslash( $_POST['iexel_nonce'] ?? '' ) ), 'iexel_club_project_create' ) ) {
    wp_die( 'Invalid nonce.' );
}
```

---

## Input Sanitisation

All `$_POST`, `$_GET` and `$_REQUEST` values must be sanitised before use.

| Type | Function |
|---|---|
| Text strings | `sanitize_text_field()` |
| Textarea content | `sanitize_textarea_field()` |
| Email addresses | `sanitize_email()` |
| Integers | `(int)` or `absint()` |
| URLs | `esc_url_raw()` |
| HTML content | `wp_kses_post()` |

---

## Output Escaping

All output must be escaped at the point of output.

| Context | Function |
|---|---|
| HTML text | `esc_html()` |
| HTML attributes | `esc_attr()` |
| URLs | `esc_url()` |
| JavaScript | `esc_js()` |
| Translated strings | `esc_html__()`, `esc_attr__()` |

---

## Error Handling

Use `WP_Error` for recoverable errors in service methods. Throw `\Exception` or a domain-specific exception for unrecoverable errors. Never silently swallow exceptions.

---

## Constants

Plugin-level constants are defined in the main plugin file (`iexel-club-os.php`):

| Constant | Value |
|---|---|
| `IEXEL_CLUB_OS_VERSION` | Plugin version string |
| `IEXEL_CLUB_OS_PLUGIN_FILE` | Absolute path to main plugin file |
| `IEXEL_CLUB_OS_PLUGIN_DIR` | Absolute path to plugin directory |
| `IEXEL_CLUB_OS_PLUGIN_URL` | URL to plugin directory |
| `IEXEL_CLUB_OS_DB_VERSION` | Current database schema version |

---

## Internationalisation

All user-facing strings must use WordPress i18n functions with the text domain `iexel-club-os`.

```php
__( 'People', 'iexel-club-os' )
esc_html__( 'Add Person', 'iexel-club-os' )
```

---

## PHPCS Suppressions

PHPCS suppressions are permitted only for the following known patterns:

1. `IN` clause placeholder construction (see Database Access above)
2. Direct `$wpdb->query()` calls for DDL statements in `DatabaseManager`
3. `phpcs:ignore WordPress.Security.NonceVerification.Missing` on read-only GET handlers that do not mutate state

All suppressions must include an inline comment explaining why the suppression is safe.
