# Accessibility Standards

**Applies to:** All HTML output in `iexel-club-os`
**Last verified:** 2026-07-24

---

## Overview

Club OS targets WCAG 2.1 Level AA compliance for all portal and admin surfaces.

---

## Colour Contrast

All text must meet the WCAG 2.1 AA contrast ratio requirements:

- Normal text (below 18pt): minimum 4.5:1
- Large text (18pt or bold 14pt): minimum 3:1

The default design tokens are chosen to meet these requirements. When overriding with club branding colours, verify contrast ratios before deployment.

---

## Keyboard Navigation

All interactive elements (buttons, links, form fields) must be keyboard-accessible. Focus indicators must be visible. Do not remove the default browser focus outline without providing an equivalent.

---

## Form Labels

Every form input must have an associated `<label>` element with a `for` attribute matching the input's `id`. Do not use placeholder text as a substitute for labels.

---

## ARIA

Use ARIA attributes only when native HTML semantics are insufficient. Common patterns:

- `aria-live="polite"` for dynamic content updates (e.g. match score)
- `aria-label` for icon-only buttons
- `role="alert"` for error messages
- `aria-expanded` for collapsible sections

---

## Images

All meaningful images must have descriptive `alt` text. Decorative images must have `alt=""`.

---

## Tables

Data tables must use `<th>` with `scope="col"` or `scope="row"` for header cells.

---

## Match Mode

The Match Mode live surface is used on mobile devices on a football pitch. It must be fully operable with one hand and large touch targets (minimum 44x44px).
