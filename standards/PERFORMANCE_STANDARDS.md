# Performance Standards

**Applies to:** All PHP and frontend code in `iexel-club-os`
**Last verified:** 2026-07-24

---

## Overview

Club OS is a WordPress plugin. Performance must be considered in the context of a shared WordPress installation.

---

## Database Query Budget

| Context | Maximum queries per request |
|---|---|
| Admin list page | 10 |
| Admin detail page | 15 |
| Portal dashboard | 15 |
| Portal workspace section | 20 |
| Match Mode live page | 10 |

Queries that exceed these budgets must be reviewed and optimised.

---

## N+1 Query Prevention

Repository methods must use `IN` clause queries to fetch related records in bulk rather than issuing one query per record. The `IN` clause pattern is documented in [PHP Coding Standards](PHP_CODING_STANDARDS.md).

---

## Caching

The `ExecutiveDashboardService` caches its assembled data for 60 seconds using a WordPress transient. This is the canonical example of dashboard caching.

Expensive read operations (e.g. finance summary, statistics aggregation) should use transients with a maximum lifetime of 5 minutes.

All transients must be cleared when the underlying data changes.

---

## Asset Loading

Admin CSS and JS are only enqueued on Club OS admin pages. Portal CSS is only enqueued on portal pages. Do not enqueue assets globally.

---

## Autoloading

The plugin uses Composer autoloading. All classes under `app/core/` and `app/` are autoloaded. Do not use `require_once` for class files.

---

## Rewrite Rule Flushing

`flush_rewrite_rules()` is expensive. The `PortalRouter` uses the `iexel_club_os_rewrite_schema` option to avoid flushing on every request. Only flush when the rewrite rule schema changes or on plugin activation/deactivation.

---

## Match Mode

Match Mode is used on mobile devices with potentially poor network connectivity. The Match Mode page must:

- Load in under 3 seconds on a 4G connection
- Use minimal JavaScript
- Not make background AJAX requests more frequently than every 10 seconds
