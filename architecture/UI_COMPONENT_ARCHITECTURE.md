# UI Component Architecture

**Source of truth:** `app/core/UI/`
**Last verified:** 2026-07-24

---

## Overview

Club OS uses a PHP-rendered component system. There is no JavaScript framework. All UI is server-rendered PHP that outputs HTML. JavaScript is used only for progressive enhancement (form autosave, live match mode interactions, drag-and-drop ordering).

---

## Directory Structure

```
app/core/UI/
├── AdminUI.php                    ← Admin menu registration and asset enqueuing
├── Components/
│   ├── Admin/                     ← Admin-specific components
│   │   ├── ClubProjectForm.php
│   │   ├── EntityMediaCard.php
│   │   ├── MediaField.php
│   │   ├── RegistrationAdminNavigation.php
│   │   ├── ResponsiveBannerField.php
│   │   └── SeasonAdminNavigation.php
│   ├── BillingScheduleForm.php
│   ├── Coach/                     ← Coach workspace components
│   ├── Common/                    ← Shared components
│   ├── Dashboard/                 ← Dashboard widgets
│   │   ├── ActivityWidget.php
│   │   ├── AlertsWidget.php
│   │   ├── ClubHealthWidget.php
│   │   ├── CommitteeGovernanceWidget.php
│   │   ├── CommitteeMajorEventsWidget.php
│   │   ├── CommunicationsWidget.php
│   │   ├── EventsWidget.php
│   │   ├── ExecutiveActivityWidget.php
│   │   ├── ExecutiveQuickActionsWidget.php
│   │   ├── FinanceWidget.php
│   │   ├── FrameworkWidget.php
│   │   ├── HeroWidget.php
│   │   ├── MemberHeroCard.php
│   │   ├── MetricWidget.php
│   │   ├── ProgressTrackingWidget.php
│   │   ├── QuickActionsWidget.php
│   │   ├── RecentActivityWidget.php
│   │   ├── RegistrationWidget.php
│   │   ├── SeasonWidget.php
│   │   └── StatsWidget.php
│   ├── DiscountPolicyForm.php
│   ├── Event/                     ← Event components
│   ├── FeeRuleForm.php
│   ├── FinanceAdminNavigation.php
│   ├── FinanceSelectors.php
│   ├── MatchMode/                 ← Match mode components
│   ├── MatchReport/               ← Match report components
│   ├── Matchday/                  ← Matchday hub components
│   ├── Navigation/                ← Navigation components
│   ├── Person/                    ← Person profile components
│   ├── Portal/                    ← Portal shell components
│   │   ├── EventCard.php
│   │   ├── EventHeroCard.php
│   │   ├── MemberHeroCard.php
│   │   ├── MemberQuickActionsCard.php
│   │   ├── PortalActionCard.php
│   │   ├── PortalDashboardLayout.php
│   │   ├── PortalDashboardWidget.php
│   │   ├── PortalEmptyState.php
│   │   ├── PortalHeader.php
│   │   ├── PortalMetricCard.php
│   │   ├── PortalMobileNavigation.php
│   │   ├── PortalNavigation.php
│   │   ├── PortalProfileSwitcher.php
│   │   ├── PortalSection.php
│   │   ├── PortalShell.php
│   │   ├── PortalStatusBadge.php
│   │   └── UpcomingEventsCard.php
│   ├── Statistics/                ← Statistics components
│   ├── Team/                      ← Team profile components
│   └── TeamEvents/                ← Team events components
├── Design/
│   └── DesignTokens.php           ← PHP design token constants
├── Layouts/
│   ├── DashboardSection.php
│   ├── MetricGrid.php
│   ├── PortalShellLayout.php
│   ├── SidebarStackLayout.php
│   └── TwoColumnLayout.php
└── Pages/                         ← All page classes (see reference/ADMIN_MENU_REFERENCE.md)
```

---

## Design Tokens

PHP design tokens are defined in `DesignTokens`:

| Token | Value |
|---|---|
| `RADIUS_SMALL` | `10px` |
| `RADIUS_MEDIUM` | `16px` |
| `RADIUS_LARGE` | `20px` |
| `SHADOW_SMALL` | `0 6px 18px rgba(0,0,0,.18)` |
| `SHADOW_MEDIUM` | `0 18px 45px rgba(0,0,0,.25)` |
| `SHADOW_LARGE` | `0 24px 60px rgba(0,0,0,.35)` |

CSS custom properties are defined in `assets/css/public.css` using `--iexel-*` naming.

---

## Page Classes

All admin and portal pages extend `BasePage`. Each page class is responsible for:

1. Checking the required capability
2. Resolving data from Kernel services
3. Rendering the page HTML

See [`reference/ADMIN_MENU_REFERENCE.md`](../reference/ADMIN_MENU_REFERENCE.md) for the full page inventory.

---

## Asset Enqueuing

Admin CSS and JS are enqueued by `AdminUI::enqueue_assets()` on the `admin_enqueue_scripts` hook. Assets are only enqueued on Club OS admin pages (checked via `$hook_suffix`).

Portal CSS is enqueued by the portal page classes on `wp_enqueue_scripts`.
