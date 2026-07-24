# Club Projects Architecture

**Source of truth:** `app/core/Projects/`
**Last verified:** 2026-07-24

---

## Overview

The Club Projects module provides a project management surface for club committee members. Projects are visible on the Committee workspace and can be managed by users with the appropriate capabilities.

---

## Domain Entity: ClubProject

| Property | Type | Description |
|---|---|---|
| `id` | `int` | Auto-increment primary key |
| `title` | `string` | Project title |
| `summary` | `string` | Project summary |
| `progress_percent` | `int` | Progress (0–100) |
| `status` | `string` | One of: `planning`, `on_track`, `needs_attention`, `paused`, `completed` |
| `priority` | `string` | One of: `low`, `normal`, `high`, `critical` |
| `category` | `string` | One of: `facilities`, `ground`, `equipment`, `fundraising`, `events`, `governance`, `marketing`, `general` |
| `owner_person_id` | `int\|null` | Linked Person record (project owner) |
| `target_date` | `string\|null` | Target completion date |
| `display_order` | `int` | Sort order on workspace |
| `is_visible` | `bool` | Whether visible on Committee workspace |
| `is_archived` | `bool` | Whether archived |
| `created_at` | `string` | Creation timestamp |
| `updated_at` | `string` | Last update timestamp |

---

## Services

| Service | Responsibility |
|---|---|
| `ClubProjectService` | Project CRUD, lifecycle transitions, visibility, ordering |
| `ClubProjectRepository` | Database access for projects |
| `ClubProjectValidator` | Validate project inputs |

---

## Lifecycle Operations

| Operation | Method | Capability required |
|---|---|---|
| Create | `create_project()` | `iexel_create_club_projects` |
| Update | `update_project()` | `iexel_edit_club_projects` |
| Archive | `archive_project()` | `iexel_archive_club_projects` |
| Restore | `restore_project()` | `iexel_archive_club_projects` |
| Show on workspace | `show_on_workspace()` | `iexel_manage_club_project_visibility` |
| Hide from workspace | `hide_from_workspace()` | `iexel_manage_club_project_visibility` |
| Mark completed | `mark_completed()` | `iexel_edit_club_projects` |
| Reopen | `reopen_project()` | `iexel_edit_club_projects` |
| Reorder | `reorder_projects()` | `iexel_edit_club_projects` |

---

## Request Actions

All mutations are handled by `ClubProjectAdminRequestHandler` via `admin_post_iexel_club_project_{action}` hooks:

- `iexel_club_project_create`
- `iexel_club_project_update`
- `iexel_club_project_archive`
- `iexel_club_project_restore`
- `iexel_club_project_show`
- `iexel_club_project_hide`
- `iexel_club_project_complete`
- `iexel_club_project_reopen`
- `iexel_club_project_reorder`

---

## Dashboard Integration

The `CommitteeProjectsProvider` aggregates project data for the Committee workspace dashboard widget, including counts by status and priority.

---

## Status

**Complete.** Full project lifecycle, visibility management and ordering are implemented.
