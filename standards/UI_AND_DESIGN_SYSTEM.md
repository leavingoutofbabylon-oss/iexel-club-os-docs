# UI and Design System

**Source of truth:** `app/core/UI/Design/DesignTokens.php` and `assets/css/public.css`
**Last verified:** 2026-07-24

---

## Overview

Club OS uses a CSS custom property-based design system. All colours, border radii and shadows are defined as CSS variables prefixed `--iexel-`. Spacing and typography values are generally hard-coded in the CSS rather than tokenised.

---

## Design Tokens

The following CSS custom properties are defined in `:root` in `assets/css/public.css`:

### Colours

| Token | Default value | Purpose |
|---|---|---|
| `--iexel-midnight` | `#06142f` | Darkest background / base |
| `--iexel-midnight-2` | `#0a1f49` | Elevated dark background |
| `--iexel-navy` | `#071d49` | Primary theme background |
| `--iexel-gold` | `#cba135` | Primary theme accent |
| `--iexel-gold-bright` | `#f2b31b` | Bright accent / interactive |
| `--iexel-white` | `#ffffff` | Pure white |
| `--iexel-text` | `#f8fafc` | Primary text |
| `--iexel-muted` | `#94a3b8` | Secondary / muted text |
| `--iexel-border` | `rgba(203, 161, 53, 0.35)` | Standard border |
| `--iexel-card` | `rgba(7, 29, 73, 0.92)` | Card background |
| `--iexel-success` | `#22c55e` | Success state |
| `--iexel-danger` | `#ef4444` | Danger / error state |
| `--iexel-warning` | `#f59e0b` | Warning state |

### Border Radius & Shadows

The `DesignTokens` PHP class (`app/core/UI/Design/DesignTokens.php`) defines the following constants used in PHP view files:

| Constant | Value |
|---|---|
| `DesignTokens::RADIUS_SMALL` | `10px` |
| `DesignTokens::RADIUS_MEDIUM` | `16px` |
| `DesignTokens::RADIUS_LARGE` | `20px` |
| `DesignTokens::SHADOW_SMALL` | `0 6px 18px rgba(0,0,0,.18)` |
| `DesignTokens::SHADOW_MEDIUM` | `0 18px 45px rgba(0,0,0,.25)` |
| `DesignTokens::SHADOW_LARGE` | `0 24px 60px rgba(0,0,0,.35)` |

---

## Club Branding Override

The `BrandingService::css_variables()` method injects a `<style>` block into the portal `<head>` that maps the club's configured brand palette to `--iexel-brand-*` tokens:

- `--iexel-brand-primary`
- `--iexel-brand-secondary`
- `--iexel-brand-accent`
- `--iexel-brand-page`
- `--iexel-brand-card`
- `--iexel-brand-text`
- `--iexel-brand-muted`
- `--iexel-brand-success`
- `--iexel-brand-warning`
- `--iexel-brand-danger`

This allows each club to customise the portal colour scheme without modifying CSS files.

---

## Component Classes

The following CSS component classes are defined in `assets/css/public.css`:

| Class | Purpose |
|---|---|
| `.iexel-button` | Base button |
| `.iexel-button-primary` | Primary action button |
| `.iexel-button-secondary` | Secondary action button |
| `.iexel-button-active` | Active state button |
| `.iexel-button-danger-active` | Active danger button |
| `.iexel-badge` | Status badge |
| `.iexel-badge-success` | Success badge |
| `.iexel-badge-warning` | Warning badge |
| `.iexel-badge-danger` | Danger badge |
| `.iexel-badge-info` | Info badge |
| `.iexel-badge-gold` | Gold badge |
| `.iexel-avatar` | Person avatar |
| `.iexel-breadcrumb` | Breadcrumb navigation |
| `.iexel-breadcrumb-item` | Breadcrumb item |
| `.iexel-breadcrumb-separator` | Breadcrumb separator |

---

## Admin CSS

The admin surface uses `assets/css/member-admin.css`. Admin styles follow the same token system but are scoped to wp-admin pages.

---

## Match Mode CSS

The Match Mode live surface uses `assets/css/match-mode.css`. This stylesheet is only enqueued on Match Mode portal pages.

---

## Do Not

- Do not use hardcoded colour values in PHP view files; use CSS variables or `DesignTokens` constants
- Do not use inline `style` attributes
- Do not add new CSS files without updating the enqueue list in `AdminUI` or the portal page class
- Do not modify `--iexel-*` token values in component CSS; override at the `:root` level only
