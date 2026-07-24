# ADR-001: Workspace Architecture — Admin Surface and Member Portal

**Status:** Accepted
**Date:** 2025-01-01 (estimated)
**Last verified:** 2026-07-24

---

## Context

Club OS needs to serve two distinct audiences:

1. **Club administrators** (committee members, coaches, treasurers) who need a rich management interface
2. **Club members** (parents, players) who need a simple, mobile-friendly portal

WordPress's default admin interface is not suitable for non-technical club members. A dedicated frontend portal is required.

---

## Decision

Club OS implements two distinct surfaces:

1. **Admin Surface** — wp-admin pages registered under the `iexel-club-os` menu slug. Accessible to users with Club OS capabilities. Uses WordPress admin UI conventions.

2. **Member Portal** — A custom frontend surface at `/club-os/`. Uses WordPress rewrite rules to route requests to portal page classes. Provides role-based workspaces for five experience roles.

The two surfaces share the same backend services and database but have separate routing, rendering and CSS.

---

## Consequences

**Positive:**
- Clean separation of concerns between management and member-facing interfaces
- Portal can be styled independently of wp-admin
- Portal can be made mobile-friendly without affecting admin UI
- Treasurer role can have portal access without wp-admin access

**Negative:**
- Two rendering pipelines to maintain
- Portal pages must implement their own authentication and access control
- Rewrite rule management adds complexity

---

## Implementation

- Admin pages: `app/core/UI/Pages/` and `app/core/UI/AdminUI.php`
- Portal pages: `app/core/UI/Pages/Portal/` and `app/core/Portal/PortalRouter.php`
- Portal CSS: `assets/css/public.css`
- Admin CSS: `assets/css/member-admin.css`
