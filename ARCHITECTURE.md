# IEXEL Club OS Architecture

## Purpose

IEXEL Club OS is a modular WordPress-based football club operating
system.

It is designed for grassroots clubs first, while remaining scalable for
academies, semi-professional clubs and professional organisations.

WordPress provides:

-   Authentication
-   Website content management
-   Plugin hosting
-   User accounts
-   Administrative infrastructure

Club OS provides:

-   Football operations
-   People and team management
-   Events and matchday
-   Rewards
-   Finance
-   Communications
-   Analytics
-   Integrations
-   AI-assisted workflows

------------------------------------------------------------------------

## Core Principles

-   Modular features
-   Clean separation of responsibilities
-   Reusable components
-   Configurable club settings
-   Feature toggles for advanced functionality
-   Repository-based database access
-   Page classes for complete screens
-   One source of truth for club data
-   Mobile-first user experience
-   Role-based permissions
-   Portal-first access for non-administrators
-   Upgrade existing components before creating duplicates

------------------------------------------------------------------------

## High-Level Architecture

``` text
WordPress
│
├── Authentication
├── User Accounts
├── Plugin Runtime
└── Website Content
    │
    ▼
IEXEL Club OS
│
├── Core
├── Business Engines
├── Portal
├── UI Framework
├── Repositories
├── Services
├── Modules
└── Integrations
```

------------------------------------------------------------------------

## Core Platform

### Application

Bootstraps Club OS and registers services, routes, permissions and
modules.

### Kernel

Provides central access to repositories and services such as:

-   People
-   Teams
-   Team Assignments
-   Events
-   Venues
-   Event Audience
-   Availability
-   Attendance
-   Weather
-   Branding
-   Permissions
-   Portal services

### Container

Manages shared application services.

### DatabaseManager

Creates and upgrades Club OS database tables.

### SettingsManager

Provides configurable club settings and defaults.

### ModuleManager

Registers and boots optional Club OS modules.

### ActivityLogger

Records important system actions.

### PermissionManager and Roles

Controls access for:

-   Website Administrator
-   Club Administrator
-   Coach
-   Parent / Guardian
-   Player
-   Committee Member
-   Volunteer

------------------------------------------------------------------------

## Business Engines

### People Engine

Handles:

-   Members
-   Players
-   Coaches
-   Parents
-   Volunteers
-   Staff
-   Relationships
-   WordPress user linking

### Teams Engine

Handles:

-   Teams
-   Age groups
-   Team formats
-   Team colours
-   Team profiles
-   Coach assignments
-   Player assignments

### Events Engine

Handles:

-   Training
-   Fixtures
-   Friendlies
-   Tournaments
-   Meetings
-   Presentations
-   Trials
-   Venues
-   Event audiences
-   Event status

### Availability Engine

Handles pre-event RSVP responses:

-   Available
-   Unavailable
-   Pending

Availability is separate from attendance.

### Attendance Engine

Handles what happened at the event:

-   Present
-   Late
-   Absent
-   Excused
-   Notes
-   Checked by
-   Checked at

### Matchday Engine

Uses events, audience, availability and attendance to provide:

-   Matchday Register
-   Bulk attendance actions
-   Live progress
-   Coach tools
-   Future player ratings
-   Goals and assists
-   Cards
-   Injuries
-   Match timeline

### Rewards Engine

Planned responsibilities:

-   Reward points
-   Achievements
-   Challenges
-   Leaderboards
-   Redemptions

### Finance Engine

Planned responsibilities:

-   Membership fees
-   Invoices
-   Payments
-   Payment status
-   Accounting integrations

### Communications Engine

Planned responsibilities:

-   Announcements
-   Team messages
-   Email
-   Push notifications
-   SMS
-   WhatsApp-related workflows

------------------------------------------------------------------------

## Portal Architecture

All non-administrative users should work inside Club OS rather than the
WordPress dashboard.

### Portal Routes

``` text
/club-os/
/club-os/events/
/club-os/events/{event_id}/
/club-os/events/{event_id}/attendance/
```

### Portal Users

-   Coaches
-   Parents
-   Players
-   Committee members
-   Volunteers

Only website administrators should normally require access to
`wp-admin`.

------------------------------------------------------------------------

## UI Architecture

Club OS uses a reusable component-based UI framework.

### Common Components

-   Button
-   Badge
-   StatCard
-   SummaryCard
-   SectionCard
-   CountdownCard

### Layout Components

-   TwoColumnLayout
-   SidebarStackLayout
-   MetricGrid
-   DashboardSection

### Event Components

-   EventHeroCard
-   EventInfoGrid
-   EventResponseActionsCard
-   CoachActionsCard
-   EventCountdownCard
-   EventWeatherCard
-   EventNotesCard
-   AvailabilityPanel
-   AttendanceSummaryCard
-   AttendanceHeroCard
-   AttendanceProgressCard
-   AttendancePlayerCard
-   AttendanceActionBar
-   AttendanceBulkActionsCard

### UI Rules

-   Reuse components instead of duplicating HTML.
-   Page classes compose components.
-   Components should contain presentation logic only.
-   Business logic belongs in repositories or services.
-   Midnight blue is the primary visual foundation.
-   Gold is reserved for important actions and emphasis.
-   Interfaces must be responsive and touch-friendly.

------------------------------------------------------------------------

## JavaScript Architecture

Current structure:

``` text
assets/js/
├── app.js
└── attendance.js
```

-   `app.js` initialises Club OS JavaScript modules.
-   `attendance.js` handles bulk attendance actions and live progress
    updates.

Future JavaScript should follow the same modular pattern.

------------------------------------------------------------------------

## Data Flow

``` text
Person
  ↓
Team Assignment
  ↓
Event Audience
  ↓
Availability / RSVP
  ↓
Attendance
  ↓
Statistics
  ↓
Rewards
  ↓
Dashboards
  ↓
AI Insights
```

------------------------------------------------------------------------

## Database Responsibility

Database operations must remain inside repository classes.

Examples:

-   PeopleRepository
-   TeamRepository
-   TeamAssignmentRepository
-   EventRepository
-   EventAudienceRepository
-   AvailabilityRepository
-   AttendanceRepository
-   VenueRepository

Pages and UI components should not execute direct database queries.

------------------------------------------------------------------------

## Development Rules

-   One feature per branch.
-   Commit after each stable milestone.
-   Open a pull request before merging into `main`.
-   Test before merging.
-   Delete completed feature branches after merge.
-   Avoid adding large methods to `AdminUI.php`.
-   Move full screens into `Pages`.
-   Move reusable presentation into `Components`.
-   Keep database access inside repositories.
-   Use services for reusable business logic.
-   Use `SettingsManager` for configurable behaviour.
-   Update the docs repository after each completed feature branch.
-   Check the Component Library before creating a new component.

------------------------------------------------------------------------

## Documentation Workflow

1.  Merge the code branch.
2.  Update `CHANGELOG.md`.
3.  Update `Roadmap.md`.
4.  Update `UI-UX/ComponentLibrary.md`.
5.  Update `Architecture.md` if responsibilities changed.
6.  Commit and push the docs repository.

------------------------------------------------------------------------

## Current Architectural Focus

The current focus is the Matchday Register and Attendance Engine.

Current completed flow:

``` text
Create Event
  ↓
Build Event Audience
  ↓
Player RSVP
  ↓
Coach Opens Matchday Register
  ↓
Mark Attendance
  ↓
Save Attendance
  ↓
Live Progress and Event Summary
```

### Next Priorities

-   Auto-save
-   Custom permission management
-   Match statistics
-   Coach workspace
-   Parent workspace
-   Rewards integration