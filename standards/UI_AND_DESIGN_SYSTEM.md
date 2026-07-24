# UI and Design System

**Source of truth:** `app/core/UI/Design/DesignTokens.php` and `assets/css/public.css`
**Last verified:** 2026-07-24

---

## Overview

Club OS uses a CSS custom property-based design system. All colours, spacing, typography and component styles are defined as CSS variables prefixed `--iexel-`.

---

## Design Tokens

The following CSS custom properties are defined in `:root` in `assets/css/public.css`:

### Colours

| Token | Default value | Purpose |
|---|---|---|
| `--iexel-primary` | `#1a56db` | Primary brand colour (overridden by club branding) |
| `--iexel-primary-dark` | `#1e429f` | Dark variant of primary |
| `--iexel-primary-light` | `#e8f0fe` | Light variant of primary |
| `--iexel-secondary` | `#6b7280` | Secondary / neutral |
| `--iexel-success` | `#057a55` | Success state |
| `--iexel-warning` | `#c27803` | Warning state |
| `--iexel-danger` | `#e02424` | Danger / error state |
| `--iexel-surface` | `#ffffff` | Card / surface background |
| `--iexel-background` | `#f9fafb` | Page background |
| `--iexel-border` | `#e5e7eb` | Border colour |
| `--iexel-text-primary` | `#111827` | Primary text |
| `--iexel-text-secondary` | `#6b7280` | Secondary / muted text |

### Typography

| Token | Default value | Purpose |
|---|---|---|
| `--iexel-font-family` | `'Inter', system-ui, sans-serif` | Body font |
| `--iexel-font-size-base` | `1rem` | Base font size |
| `--iexel-font-size-sm` | `0.875rem` | Small text |
| `--iexel-font-size-lg` | `1.125rem` | Large text |
| `--iexel-font-weight-normal` | `400` | Normal weight |
| `--iexel-font-weight-medium` | `500` | Medium weight |
| `--iexel-font-weight-bold` | `700` | Bold weight |

### Spacing

| Token | Default value | Purpose |
|---|---|---|
| `--iexel-spacing-xs` | `0.25rem` | Extra small spacing |
| `--iexel-spacing-sm` | `0.5rem` | Small spacing |
| `--iexel-spacing-md` | `1rem` | Medium spacing |
| `--iexel-spacing-lg` | `1.5rem` | Large spacing |
| `--iexel-spacing-xl` | `2rem` | Extra large spacing |

### Border Radius

| Token | Default value | Purpose |
|---|---|---|
| `--iexel-radius-sm` | `0.25rem` | Small radius |
| `--iexel-radius-md` | `0.5rem` | Medium radius |
| `--iexel-radius-lg` | `1rem` | Large radius |
| `--iexel-radius-full` | `9999px` | Pill / badge |

---

## Club Branding Override

The `BrandingService` injects a `<style>` block into the portal `<head>` that overrides `--iexel-primary`, `--iexel-primary-dark` and `--iexel-primary-light` with the club's configured brand colour. This allows each club to customise the portal colour scheme without modifying CSS files.

---

## Component Classes

The following CSS component classes are defined in `assets/css/public.css`:

| Class | Purpose |
|---|---|
| `.iexel-card` | Standard card container |
| `.iexel-btn` | Base button |
| `.iexel-btn--primary` | Primary action button |
| `.iexel-btn--secondary` | Secondary action button |
| `.iexel-btn--danger` | Destructive action button |
| `.iexel-badge` | Status badge |
| `.iexel-badge--success` | Success badge |
| `.iexel-badge--warning` | Warning badge |
| `.iexel-badge--danger` | Danger badge |
| `.iexel-table` | Data table |
| `.iexel-form-group` | Form field group |
| `.iexel-form-label` | Form label |
| `.iexel-form-input` | Text input |
| `.iexel-form-select` | Select input |
| `.iexel-alert` | Alert / notice block |
| `.iexel-alert--success` | Success alert |
| `.iexel-alert--warning` | Warning alert |
| `.iexel-alert--danger` | Danger alert |

---

## Admin CSS

The admin surface uses `assets/css/member-admin.css`. Admin styles follow the same token system but are scoped to wp-admin pages.

---

## Match Mode CSS

The Match Mode live surface uses `assets/css/match-mode.css`. This stylesheet is only enqueued on Match Mode portal pages.

---

## Do Not

- Do not use hardcoded colour values in PHP view files
- Do not use inline `style` attributes
- Do not add new CSS files without updating the enqueue list in `AdminUI` or the portal page class
- Do not modify `--iexel-*` token values in component CSS; override at the `:root` level only
