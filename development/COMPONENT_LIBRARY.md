# Component Library

**Last verified:** 2026-07-24

---

## Overview

This document catalogues the reusable PHP component classes available in Club OS. These components are used in admin and portal view files.

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

Renders the incident feed (goals, cards, substitutions).

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

All dashboard widgets follow the Provider-Widget pattern. See [PROVIDER_AND_WIDGET_STANDARDS.md](../standards/PROVIDER_AND_WIDGET_STANDARDS.md) for the full pattern.

| Widget | Provider | Dashboard |
|---|---|---|
| `ExecutiveSummaryWidget` | `ExecutiveSummaryProvider` | Admin Executive Dashboard |
| `FinanceSummaryWidget` | `FinanceSummaryProvider` | Admin Executive Dashboard |
| `RecentActivityWidget` | `RecentActivityProvider` | Admin Executive Dashboard |
| `UpcomingEventsWidget` | `UpcomingEventsProvider` | Admin Executive Dashboard |
| `CommitteeProjectsWidget` | `CommitteeProjectsProvider` | Committee Workspace |
| `CoachTeamSummaryWidget` | `CoachTeamSummaryProvider` | Coach Workspace |
| `ParentChildSummaryWidget` | `ParentChildSummaryProvider` | Parent Workspace |
