# Portal Workspace Standards

**Applies to:** All portal page classes under `app/core/UI/Pages/Portal/`
**Last verified:** 2026-07-24

---

## Overview

The Member Portal is the frontend surface at `/club-os/`. It provides role-based workspaces for five experience roles: Parent, Player, Coach, Committee and Treasurer.

---

## Experience Role Routing

The `PortalRouter` resolves the active experience role from `MemberExperienceService` and routes to the correct workspace page. Each workspace page is responsible for its own access check.

---

## Portal Page Structure

```php
class PortalCoachDashboardPage extends BasePortalPage {

    public function __construct( private readonly Kernel $kernel ) {}

    public function render(): void {
        if ( ! $this->kernel->member_experience_service()->has_active_experience( 'coach' ) ) {
            wp_safe_redirect( home_url( '/club-os/' ) );
            exit;
        }

        $data = $this->kernel->coach_workspace_service()->get_dashboard_data();

        include IEXEL_CLUB_OS_PLUGIN_DIR . 'app/core/UI/Views/portal/coach/dashboard.php';
    }
}
```

---

## Portal View Files

Portal HTML is in view files under `app/core/UI/Views/portal/`. View files are plain PHP templates. They must escape all output and must not contain business logic.

---

## Portal CSS

Portal CSS is in `assets/css/public.css`. CSS custom properties (design tokens) are defined in `:root` and prefixed `--iexel-`. Do not use inline styles or hardcoded colour values.

---

## Profile Switcher

The profile switcher component is rendered on every portal page for users with multiple experience roles. It is provided by `ProfileSwitcherWidget` and submits to `admin_post_iexel_member_experience_switch`.

---

## Portal Login Page

The portal login page at `/club-os/login` uses the club's branding (logo, primary colour) from `BrandingService`. It must not expose the WordPress admin login URL.

---

## Treasurer Workspace

The Treasurer workspace at `/club-os/finance/` mirrors the admin Finance surface. It is accessible only to users with the `iexel_club_treasurer` WordPress role and the `iexel_view_finance` capability. The Treasurer role does not have wp-admin access.
