# Permissions and Security Standards

**Applies to:** All admin pages, portal pages and request handlers in `iexel-club-os`
**Last verified:** 2026-07-24

---

## Overview

Every entry point into Club OS must enforce the correct capability and verify a nonce before processing any data.

---

## Admin Page Guard Pattern

Every admin page class must begin its `render()` method with a capability check:

```php
public function render(): void {
    if ( ! current_user_can( 'iexel_manage_finance' ) ) {
        wp_die( esc_html__( 'You do not have permission to access this page.', 'iexel-club-os' ) );
    }
    // ...
}
```

---

## Request Handler Guard Pattern

Every `admin_post_*` handler must:

1. Check POST method
2. Check capability
3. Verify nonce
4. Sanitise all inputs
5. Redirect after processing (PRG pattern)

```php
public function handle(): void {
    if ( 'POST' !== $_SERVER['REQUEST_METHOD'] ) {
        wp_die( 'Invalid request method.' );
    }
    if ( ! current_user_can( 'iexel_manage_finance' ) ) {
        wp_die( 'Permission denied.' );
    }
    if ( ! wp_verify_nonce(
        sanitize_text_field( wp_unslash( $_POST['iexel_nonce'] ?? '' ) ),
        'iexel_finance_create_invoice'
    ) ) {
        wp_die( 'Invalid nonce.' );
    }
    // Process...
    wp_safe_redirect( $redirect_url );
    exit;
}
```

---

## Portal Access Control

Portal pages use `MemberExperienceService` to determine the active experience role. Each portal page must check:

1. The user is logged in (`is_user_logged_in()`)
2. The user has a linked Person record
3. The user's active experience role has access to the requested section

The `PortalRouter` handles the top-level check; individual portal pages handle section-specific checks.

---

## Treasurer Role Restrictions

The `iexel_club_treasurer` role is intentionally restricted. It does not have `manage_options`, `activate_plugins`, `edit_plugins`, `edit_theme_options`, `list_users`, `create_users`, `edit_users`, `delete_users`, `promote_users` or `iexel_manage_club_os`. This prevents Treasurer users from accessing wp-admin beyond the Finance workspace.

Do not add these capabilities to the Treasurer role.

---

## Nonce Lifetime

All nonces use the default WordPress nonce lifetime (24 hours). Do not use custom nonce lifetimes.

---

## Redirect Safety

Always use `wp_safe_redirect()` for redirects within the same domain. Use `wp_redirect()` only when redirecting to an external URL that has been validated.

---

## SQL Injection Prevention

All database queries with user-supplied values must use `$wpdb->prepare()`. See [PHP Coding Standards](PHP_CODING_STANDARDS.md) and [Repository Standards](REPOSITORY_STANDARDS.md).

---

## XSS Prevention

All output must be escaped at the point of output. See [PHP Coding Standards](PHP_CODING_STANDARDS.md) for the escaping functions.

---

## File Upload Security

Entity media uploads use the WordPress media library (`wp_handle_upload()`). File type validation is enforced by WordPress. Do not accept file uploads outside the media library.

---

## Sensitive Data

The `people` table contains date of birth and contact information. The `finance_*` tables contain financial data. Access to these tables must be gated on the appropriate capability. Do not log sensitive field values in the activity log.
