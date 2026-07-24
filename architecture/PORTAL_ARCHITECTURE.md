# Portal Architecture

**Source of truth:** `app/core/Portal/PortalRouter.php`, `app/core/Experience/MemberExperienceService.php`
**Last verified:** 2026-07-24

---

## Overview

The Club OS member portal is a custom frontend surface mounted at `/club-os/`. It bypasses the active WordPress theme entirely and renders its own full-page HTML output.

---

## URL Structure

All portal URLs follow the pattern `/club-os/{section}/`. The portal is mounted at the WordPress root via custom rewrite rules registered on the `init` hook.

```
/club-os/                    ← Portal dashboard (role-dependent)
/club-os/login               ← Branded login page
/club-os/coach               ← Coach workspace
/club-os/treasurer           ← Treasurer dashboard
/club-os/finance/...         ← Finance workspace (Treasurer only)
/club-os/teams/{id}          ← Team workspace
/club-os/events/{id}         ← Event detail
/club-os/events/{id}/...     ← Event sub-pages (attendance, matchday, live, etc.)
```

See [`reference/PORTAL_ROUTE_REFERENCE.md`](../reference/PORTAL_ROUTE_REFERENCE.md) for the complete route inventory.

---

## Request Flow

1. WordPress processes the request and fires `template_redirect`.
2. `PortalRouter::render()` checks whether the request is a portal request via `is_portal_request()`.
3. If not a portal request, `render()` returns immediately and WordPress continues normally.
4. If it is a portal request, `PortalRouter` handles the entire response:
   a. If the section is `login`, render `PortalLoginPage` (unauthenticated users) or redirect to destination.
   b. If the upgrade is not complete, return a 503 maintenance page.
   c. If the user is not logged in, redirect to the login page with `redirect_to` parameter.
   d. Resolve the `MemberExperienceContext` via `MemberExperienceService::context()`.
   e. If context resolution fails, render an error page.
   f. Route to the appropriate workspace page based on `iexel_club_os_section` query var.

---

## Experience System

The `MemberExperienceService` resolves the current user's active experience context. The context includes:

- The user's active **experience role** (Parent, Player, Coach, Committee, Treasurer)
- The user's linked **Person record**
- The user's **team context** (for Coach and Player roles)
- The user's **child profiles** (for Parent role)
- Navigation items and quick actions for the active role

### Experience Roles

| Role key | Snapshot class | Primary workspace |
|---|---|---|
| `parent` | `ParentExperienceSnapshot` | `PortalParentDashboardPage` |
| `player` | `PlayerExperienceSnapshot` | `PortalPlayerDashboardPage` |
| `coach` | `CoachExperienceSnapshot` | `PortalCoachDashboardPage` |
| `committee` | `CommitteeExperienceSnapshot` | `PortalCommitteeDashboardPage` |
| `treasurer` | `TreasurerExperienceSnapshot` | `PortalTreasurerDashboardPage` |

### Profile Switching

Users with multiple linked roles (e.g. a parent who is also a committee member) can switch between experience profiles using `PortalProfileSwitcher`. The active profile is stored in the user's session and can be changed via the `iexel_member_experience_switch` admin_post action.

---

## Rewrite Rules

Portal rewrite rules are registered in `PortalRouter::add_rewrite_rules()` (called statically during activation) and re-registered on the `init` hook. The rules map URL patterns to WordPress query vars:

| Query var | Purpose |
|---|---|
| `iexel_club_os_portal` | Signals that this is a portal request |
| `iexel_club_os_section` | The section slug (e.g. `coach`, `finance`, `login`) |
| `event_id` | Event ID for event sub-pages |
| `team_id` | Team ID for team workspace |
| `person_id` | Person ID for person-scoped pages |
| `preview_player_id` | Player ID for statistics preview |

---

## Authentication Flow

The portal uses WordPress authentication. The `AuthenticationService` handles:

- **Login** — `PortalLoginPage` renders a branded login form. The `iexel_club_os_login` admin_post_nopriv action processes the form.
- **Logout** — The `iexel_club_os_logout` admin_post action logs the user out and redirects to the login page.
- **Lost password** — The `iexel_club_os_lost_password` admin_post_nopriv action initiates the WordPress password reset flow.
- **Redirect after login** — `AuthenticationService::destination_for_user()` determines the appropriate post-login destination based on the user's role.

---

## Portal Shell

All portal pages are wrapped in `PortalShell`, which renders:

- `PortalHeader` — Club branding, user name, profile switcher
- `PortalNavigation` — Role-specific navigation items
- `PortalMobileNavigation` — Mobile-optimised navigation
- Page content
- `PortalSection` wrapper for consistent spacing

---

## Admin Access Boundary

The `AdminAccessBoundary` class prevents non-Club-OS users from accessing wp-admin. It hooks into `admin_init` and redirects users who do not have at least one Club OS capability to the member portal. Users with only `upload_files` are also permitted.

The `iexel_club_treasurer` role has wp-admin access restricted to Finance pages only, enforced by removing `manage_options` and related capabilities.
