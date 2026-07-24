# Routes and Entry Points

**Source of truth:** `app/core/Release/ReleaseRouteInventory.php`
**Last verified:** 2026-07-24

---

## Overview

Club OS has three categories of entry points:

1. **Admin pages** — WordPress `admin.php?page=iexel-club-os-*` URLs
2. **Portal routes** — Frontend `/club-os/*` URLs via WordPress rewrite rules
3. **Request actions** — `admin_post_*` and `wp_ajax_*` handlers for mutations

For the complete inventories, see:
- [`reference/ADMIN_MENU_REFERENCE.md`](../reference/ADMIN_MENU_REFERENCE.md)
- [`reference/PORTAL_ROUTE_REFERENCE.md`](../reference/PORTAL_ROUTE_REFERENCE.md)
- [`reference/REQUEST_ACTION_REFERENCE.md`](../reference/REQUEST_ACTION_REFERENCE.md)

---

## Admin Page URL Pattern

All admin pages are registered under the top-level menu slug `iexel-club-os`. The URL pattern is:

```
/wp-admin/admin.php?page={slug}
```

Where `{slug}` is one of the slugs listed in [`reference/ADMIN_MENU_REFERENCE.md`](../reference/ADMIN_MENU_REFERENCE.md).

---

## Portal URL Pattern

Portal URLs follow the pattern `/club-os/{section}/`. The `iexel_club_os_section` query var determines which page is rendered.

---

## Request Action Pattern

All mutation handlers use the WordPress `admin_post_*` hook pattern:

```
POST /wp-admin/admin-post.php
action=iexel_{module}_{operation}
```

Authentication-required actions use `admin_post_{action}`. Public actions (login, lost password) use `admin_post_nopriv_{action}`.

All handlers follow the guard pattern:
1. Check `$_SERVER['REQUEST_METHOD'] === 'POST'`
2. Check `current_user_can($capability)`
3. Check `check_admin_referer($nonce)`
4. Process the mutation
5. Flash a success or error message
6. Redirect back to the appropriate admin page

---

## AJAX Actions

| Action | Hook type | Handler |
|---|---|---|
| `iexel_registration_autosave` | `wp_ajax_` | `RegistrationPortalRequestHandler` |

---

## WP-Cron Actions

| Hook | Handler |
|---|---|
| `iexel_club_os_process_communication` | `CommunicationService::process_scheduled_communication()` |
| `iexel_club_os_process_billing_schedules` | `RecurringBillingService::process_due()` |
