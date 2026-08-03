# Component Library

**Last verified:** 2026-08-03

---

## Status

### FOUNDATION AVAILABLE

Club OS has reusable PHP components plus opt-in shared CSS contracts for surfaces, typography, actions, statuses, progress, and workspaces.

### PAGE MIGRATION PENDING

Existing production pages and page-specific components have not been redesigned by the Visual Foundation batch. A component being listed here does not mean every page uses its current semantic contract.

---

## Component rules

- Reuse an existing PHP component before creating a new one.
- Keep domain data resolution outside presentation components.
- Map visual intent through the four layers documented in [UI_AND_DESIGN_SYSTEM.md](../standards/UI_AND_DESIGN_SYSTEM.md).
- Use product-owned status and interaction semantics; never infer danger or warning from the club accent.
- Use derived on-surface foregrounds when a configurable club colour supplies a background.
- Preserve compatibility classes while consumers migrate.
- Do not add a component alias for a one-page style preference.

---

## Shared visual foundation

### Surfaces

The opt-in surface helpers are:

| Helper | Contract |
|---|---|
| `.iexel-surface--identity` | Primary identity surface with derived on-primary text |
| `.iexel-surface--identity-strong` | Strong identity surface with derived on-secondary text |
| `.iexel-surface--feature` | Dark feature/analytic surface |
| `.iexel-surface--card` | Standard operational card |
| `.iexel-surface--muted` | Muted nested surface |
| `.iexel-surface--elevated` | Elevated light surface |

Use these to support a deliberate dark/light rhythm. Do not convert entire operational pages to dark surfaces.

### Legacy shared-component compatibility

While page migration remains pending, `assets/css/design-system.css` owns the minimum surface/foreground correction for these existing shared selectors:

- portal header, brand, refresh, account summary, and selected navigation: identity surface plus adaptive `on-primary`;
- Coach Quick Actions, Priority Alerts, metrics, and empty states on light cards: standard text, with primary actions retaining adaptive `on-primary`;
- My Stats feature surfaces and shared team cards: feature/dark surface plus `on-dark` and `on-dark-muted`;
- accent-backed statistics and team badges: adaptive `on-accent`.

These mappings preserve existing PHP markup and layout. Do not copy them into page-specific palettes.

### Typography

| Helper | Role |
|---|---|
| `.iexel-type-display` | Page or hero title |
| `.iexel-type-section` | Section title |
| `.iexel-type-card` | Card title |
| `.iexel-type-metric` | Metric value |
| `.iexel-type-body` | Body copy |
| `.iexel-type-supporting` | Supporting/meta copy |
| `.iexel-type-label` | Eyebrow, kicker, or label |

The supported foundation weights are 600, 700, and 800. The family remains the existing local `Inter, Arial, sans-serif` stack; no external font is loaded.

### Actions

The base class is `.iexel-experience-button`.

| Modifier | Meaning |
|---|---|
| `.is-primary` | Highest-priority action, using club primary plus safe on-primary text |
| `.is-secondary` | Standard bordered alternative |
| `.is-ghost` | Low-emphasis transparent action |
| `.is-text` | Compatibility alias for the ghost treatment |
| `.is-danger` | Destructive or dangerous product-owned action |

Hover, focus, disabled, and `aria-disabled` states are part of the contract. Gold is an accent and must not be used as danger.

### Statuses and notices

`.iexel-experience-status` provides a neutral base. Use `.is-success`, `.is-warning`, `.is-danger`, or `.is-info` for product-owned meaning. Existing lifecycle aliases such as `.is-state-approved`, `.is-state-pending`, and `.is-state-failed` remain supported.

Saved club success/warning/danger colours continue to feed legacy colour aliases temporarily. New shared components must use `--iexel-status-*` roles. Removing the settings fields or legacy mapping requires a separate migration decision.

### Progress and data visualisation

Use `--iexel-component-progress-track` and `--iexel-component-progress-value` for shared progress treatments. Use `--iexel-component-data-primary` and `--iexel-component-data-accent` as the initial series aliases. Add further series only when a real reusable visualisation requires them; do not create page-local palettes in the foundation.

### Workspaces

`.iexel-workspace` provides the opt-in application maximum and gutter. Add `.iexel-workspace--content` for reading/data-focused content. Existing page widths are not migrated.

---

## Admin Components

### `AdminNoticeComponent`

Renders a WordPress admin notice.

```php
AdminNoticeComponent::render( 'success', 'Invoice created successfully.' );
AdminNoticeComponent::render( 'error', 'Failed to create invoice.' );
AdminNoticeComponent::render( 'warning', 'This action cannot be undone.' );
```

### `PaginationComponent`

Renders a pagination control for list pages.

```php
PaginationComponent::render( $current_page, $total_pages, $base_url );
```

### `PersonSearchComponent`

Renders a person search input with autocomplete.

```php
PersonSearchComponent::render( 'person_id', $selected_person_id );
```

### `TeamSelectComponent`

Renders a team select dropdown.

```php
TeamSelectComponent::render( 'team_id', $selected_team_id, $teams );
```

### `SeasonSelectComponent`

Renders a season select dropdown.

```php
SeasonSelectComponent::render( 'season_id', $selected_season_id, $seasons );
```

---

## Portal Components

### `ProfileSwitcherWidget`

Renders the experience role switcher for users with multiple roles.

```php
$widget = new ProfileSwitcherWidget( $experience_service );
echo $widget->render( $active_role, $available_roles );
```

### `PortalNavComponent`

Renders the portal navigation bar.

```php
PortalNavComponent::render( $active_section, $experience_role );
```

### `EventCardComponent`

Renders a single event card for event lists.

```php
EventCardComponent::render( $event, $show_team = true );
```

### `PersonAvatarComponent`

Renders a person's avatar (initials or uploaded image).

```php
PersonAvatarComponent::render( $person, $size = 'md' );
```

---

## Match Mode Components

### `MatchScoreboardComponent`

Renders the live scoreboard for Match Mode.

```php
MatchScoreboardComponent::render( $match_state );
```

### `MatchIncidentFeedComponent`

Renders the incident feed for goals, cards, and substitutions.

```php
MatchIncidentFeedComponent::render( $incidents );
```

### `FormationGridComponent`

Renders the formation grid for lineup management.

```php
FormationGridComponent::render( $formation_template, $selections );
```

---

## Dashboard Widgets

Dashboard widgets follow the Provider-Widget pattern. See [PROVIDER_AND_WIDGET_STANDARDS.md](../standards/PROVIDER_AND_WIDGET_STANDARDS.md).

| Widget | Provider | Dashboard |
|---|---|---|
| `ExecutiveSummaryWidget` | `ExecutiveSummaryProvider` | Admin Executive Dashboard |
| `FinanceSummaryWidget` | `FinanceSummaryProvider` | Admin Executive Dashboard |
| `RecentActivityWidget` | `RecentActivityProvider` | Admin Executive Dashboard |
| `UpcomingEventsWidget` | `UpcomingEventsProvider` | Admin Executive Dashboard |
| `CommitteeProjectsWidget` | `CommitteeProjectsProvider` | Committee Workspace |
| `CoachTeamSummaryWidget` | `CoachTeamSummaryProvider` | Coach Workspace |
| `ParentChildSummaryWidget` | `ParentChildSummaryProvider` | Parent Workspace |

---

## Future migration checklist

For each separately approved page migration:

1. Confirm whether an existing PHP component already represents the content.
2. Select semantic surface and typography roles.
3. Apply the shared action and status hierarchy.
4. Validate on-brand foreground contrast and focus visibility.
5. Recompose wide layouts near 1024px and stack near 760/768px where appropriate.
6. Validate component behavior near 520px and acceptance at 390px and 360px.
7. Retain legacy classes until all consumers are proven migrated.
8. Record the page as migrated only after manual browser acceptance.
