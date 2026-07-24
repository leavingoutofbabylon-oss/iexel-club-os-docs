# AI Developer Guide

**Last verified:** 2026-07-24

---

## Overview

This guide is specifically for AI coding assistants (e.g. Copilot, Cursor, Manus) working on the Club OS codebase. It provides the context and constraints needed to generate correct, safe and consistent code.

---

## Critical Constraints

1. **Never modify plugin source code** (`iexel-club-os` repository) unless explicitly instructed. Treat it as read-only unless the task is specifically a source code change.
2. **Never merge branches** unless explicitly instructed.
3. **Never push to `main`** directly. All changes go through pull requests.
4. **Never remove upgrade steps** from `UpgradeRunner`. They are idempotent and must remain for installations upgrading from older versions.
5. **Never add `manage_options` or `activate_plugins`** to the `iexel_club_treasurer` role.

---

## Architecture Patterns to Follow

When generating new code, follow these patterns:

### New Service

```php
namespace IexelClubOS\Core\{Module};

if ( ! defined( 'ABSPATH' ) ) { exit; }

class {Module}Service {
    public function __construct(
        private readonly {Module}Repository $repo,
        private readonly ActivityLogger $logger
    ) {}

    public function do_something( int $id ): bool {
        $result = $this->repo->update( $id, [ 'status' => 'done' ] );
        if ( $result ) {
            $this->logger->log( get_current_user_id(), '{module}_done', '{entity}', $id, "Done: #{$id}" );
        }
        return $result;
    }
}
```

### New Repository

```php
namespace IexelClubOS\Core\{Module};

if ( ! defined( 'ABSPATH' ) ) { exit; }

class {Module}Repository {
    private string $table;

    public function __construct(
        private readonly \wpdb $wpdb,
        private readonly DatabaseManager $db_manager
    ) {
        $this->table = $db_manager->table('{table_name}');
    }

    public function get_by_id( int $id ): ?array {
        return $this->wpdb->get_row(
            $this->wpdb->prepare( "SELECT * FROM `{$this->table}` WHERE id = %d", $id ),
            ARRAY_A
        );
    }
}
```

### New Admin Request Handler

```php
namespace IexelClubOS\Core\{Module};

if ( ! defined( 'ABSPATH' ) ) { exit; }

class {Module}AdminRequestHandler {
    public function __construct( private readonly Kernel $kernel ) {}

    public function register(): void {
        add_action( 'admin_post_iexel_{module}_{action}', [ $this, 'handle' ] );
    }

    public function handle(): void {
        if ( 'POST' !== $_SERVER['REQUEST_METHOD'] ) { wp_die( 'Invalid method.' ); }
        if ( ! current_user_can( 'iexel_manage_{module}' ) ) { wp_die( 'Permission denied.' ); }
        if ( ! wp_verify_nonce(
            sanitize_text_field( wp_unslash( $_POST['iexel_nonce'] ?? '' ) ),
            'iexel_{module}_{action}'
        ) ) { wp_die( 'Invalid nonce.' ); }

        // Process...

        wp_safe_redirect( admin_url( 'admin.php?page=iexel-club-os-{module}' ) );
        exit;
    }
}
```

---

## Where to Register Things

| Thing to add | Where to register |
|---|---|
| New service | `Kernel.php` (add accessor method) |
| New capability | `ClubRoleCapabilityRegistrar.php` + `ReleaseCapabilityInventory.php` |
| New admin page | `AdminUI.php` + `ReleaseRouteInventory.php` |
| New portal route | `PortalRouter.php` + `ReleaseRouteInventory.php` |
| New request handler | `Application.php` (in `register_request_handlers()`) |
| New database table | `DatabaseManager.php` + `ReleaseSchemaInventory.php` + `UpgradeRunner.php` |
| New module | `ReleaseModuleInventory.php` |

---

## Common Mistakes to Avoid

- Do not use `new ClassName()` inside service methods. Inject dependencies.
- Do not use `$_POST['key']` without `sanitize_text_field( wp_unslash( ... ) )`.
- Do not use `echo` in service or repository classes.
- Do not add `manage_options` to the Treasurer role.
- Do not skip the `ABSPATH` guard.
- Do not use `wp_die()` in service methods. Return `WP_Error` instead.
- Do not use `IN (1,2,3)` with string concatenation. Use the prepared `IN` clause pattern.
- Do not add a new table without a corresponding upgrade step.
- Do not add a new capability without adding it to `ReleaseCapabilityInventory`.

---

## Useful Source Files to Read First

Before generating code for a specific module, read:

1. The module's `*Service.php` for existing patterns
2. The module's `*Repository.php` for table structure
3. The module's `*AdminRequestHandler.php` for action names
4. `Kernel.php` for the service accessor pattern
5. `ReleaseRouteInventory.php` for existing route slugs
