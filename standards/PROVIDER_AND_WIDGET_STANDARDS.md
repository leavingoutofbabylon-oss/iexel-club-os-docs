# Provider and Widget Standards

**Applies to:** All `*Provider.php` and `*Widget.php` classes under `app/core/`
**Last verified:** 2026-07-24

---

## Overview

The Provider-Widget pattern separates data retrieval (Providers) from rendering (Widgets). This pattern is used for all dashboard sections in both the admin Executive Dashboard and the Member Portal workspaces.

---

## Provider Conventions

A Provider is a PHP class that:

1. Receives its dependencies via constructor injection
2. Exposes a single public method (typically `get_data(): array`)
3. Returns a structured array of data for the corresponding Widget
4. Does not render any HTML

```php
class CommitteeProjectsProvider {
    public function __construct(
        private readonly ClubProjectRepository $project_repo
    ) {}

    public function get_data(): array {
        return [
            'projects' => $this->project_repo->get_visible_projects(),
            'total'    => $this->project_repo->count_visible(),
        ];
    }
}
```

---

## Widget Conventions

A Widget is a PHP class that:

1. Receives its data array (from the Provider) via constructor or method
2. Exposes a `render(): string` method that returns HTML
3. Does not access the database directly
4. Uses `esc_html()`, `esc_attr()` and `esc_url()` on all output

```php
class CommitteeProjectsWidget {
    public function render( array $data ): string {
        ob_start();
        // render HTML using $data
        return ob_get_clean();
    }
}
```

---

## Naming

| Class type | Naming pattern | Example |
|---|---|---|
| Provider | `{Domain}Provider` or `{Domain}DataProvider` | `CommitteeProjectsProvider` |
| Widget | `{Domain}Widget` | `CommitteeProjectsWidget` |

---

## Dashboard Registration

Dashboard Providers and Widgets are registered in the appropriate dashboard service (`ExecutiveDashboardService`, `CommitteeDashboardService`, etc.). The dashboard service calls each Provider, passes the data to the Widget, and assembles the rendered output.

---

## Caching

Providers that perform expensive queries should implement transient caching. The cache key must be prefixed `iexel_` and cleared when the underlying data changes.

The `ExecutiveDashboardService` caches its assembled data for 60 seconds. Individual Providers should not implement their own caching unless the data is particularly expensive to compute.
