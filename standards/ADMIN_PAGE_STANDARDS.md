# Admin Page Standards

**Applies to:** All admin page classes under `app/core/UI/Pages/`
**Last verified:** 2026-07-24

---

## Overview

All admin pages extend `BasePage` and are registered by `AdminUI`. Pages are responsible for capability checking, data resolution and HTML rendering.

---

## Class Structure

```php
class FinancePage extends BasePage {

    public function __construct( private readonly Kernel $kernel ) {}

    public function render(): void {
        if ( ! current_user_can( 'iexel_view_finance' ) ) {
            wp_die( esc_html__( 'Permission denied.', 'iexel-club-os' ) );
        }

        $data = $this->kernel->finance_service()->get_dashboard_data();

        include IEXEL_CLUB_OS_PLUGIN_DIR . 'app/core/UI/Views/finance/dashboard.php';
    }
}
```

---

## View Files

Admin page HTML is in view files under `app/core/UI/Views/`. View files are plain PHP templates. They receive data via variables extracted from the page class.

View files must escape all output. They must not contain business logic or database access.

---

## Navigation

The active menu item is highlighted by returning the correct menu slug from `AdminUI::get_current_page_slug()`. Hidden pages (e.g. edit forms) must specify their parent menu slug so the correct parent item is highlighted.

---

## Redirects After Mutations

Admin pages that process form submissions must follow the Post-Redirect-Get (PRG) pattern. After processing, redirect to the appropriate list or detail page using `wp_safe_redirect()`.

---

## Error and Success Messages

Use the WordPress admin notice pattern for feedback messages. Store the message in a transient keyed to the current user, then display and delete it on the next page load.

```php
// In the handler:
set_transient( 'iexel_admin_notice_' . get_current_user_id(), [
    'type'    => 'success',
    'message' => 'Invoice created successfully.',
], 30 );

// In the page:
$notice = get_transient( 'iexel_admin_notice_' . get_current_user_id() );
if ( $notice ) {
    delete_transient( 'iexel_admin_notice_' . get_current_user_id() );
    // render notice
}
```

---

## Asset Enqueuing

Admin CSS and JS are enqueued by `AdminUI::enqueue_assets()`. Assets are only enqueued on Club OS admin pages (checked via `$hook_suffix`). Do not enqueue assets globally.

The admin CSS file is `assets/css/member-admin.css`. The admin JS file is `assets/js/admin.js`.
