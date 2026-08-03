# UI and Design System

**Sources of truth:** `app/core/UI/Design/DesignTokens.php`, `app/core/Branding/BrandingService.php`, and `assets/css/design-system.css`
**Last verified:** 2026-08-03

---

## Status

### FOUNDATION AVAILABLE

The shared visual foundation provides semantic surfaces, safe on-brand foregrounds, product-owned functional states, typography roles, action contracts, geometry, elevation, workspace values, and compatibility aliases.

### PAGE MIGRATION PENDING

Production pages have not been redesigned or comprehensively migrated to these contracts. Existing page-specific selectors remain in `public.css` and `member-experience.css` until a separately approved migration batch. Do not claim visual consistency merely because the foundation exists.

### LIGHT PRIMARY COMPATIBILITY CORRECTION

The shared foundation now pairs legacy shared components with the semantic foreground owned by their actual surface. Portal header and selected-navigation controls use `on-primary`; light Coach dashboard cards use standard text; My Stats and shared team feature cards retain `on-dark`; and accent-backed badges use `on-accent`.

This is a bounded Batch 1 compatibility correction. It does not redesign the affected screens, migrate their markup, alter their responsive composition, or mark a production page as fully migrated.

---

## Product direction

Club OS is a premium football operating system. The visual rhythm should generally move through:

> dark identity or feature surface -> light operational surface -> dark feature or analytic surface -> light content cards

This is a compositional direction, not a requirement to make every page dark. Forms, schedules, tables, settings, and dense operational workspaces may remain light.

Midnight/navy establishes identity. Warm gold is restrained: use it for emphasis, selected moments, progress, and bounded brand accents. It must not replace warning, danger, or other functional meaning.

---

## Four-layer token architecture

### Layer 1 - club inputs

`BrandingService` validates saved settings and emits the configurable `--iexel-brand-*` properties:

- primary, secondary, and accent;
- page, card, text, and muted text;
- success, warning, and danger compatibility inputs;
- derived `on-primary`, `on-secondary`, and `on-accent` foregrounds.

These are inputs, not component styling instructions. Club settings do not own layout, spacing, typography hierarchy, interaction states, or accessibility behavior.

### Layer 2 - product semantics

`DesignTokens::css_variables()` maps validated inputs to Club OS-owned roles.

| Role | Canonical token examples |
|---|---|
| Identity surfaces | `--iexel-surface-identity`, `--iexel-surface-identity-strong`, `--iexel-surface-identity-secondary` |
| Operational surfaces | `--iexel-surface-page`, `--iexel-surface-card`, `--iexel-surface-muted`, `--iexel-surface-elevated` |
| Feature surface | `--iexel-surface-feature` |
| On-surface text | `--iexel-color-on-primary`, `--iexel-color-on-secondary`, `--iexel-color-on-accent`, `--iexel-color-on-dark` |
| Standard text | `--iexel-color-text`, `--iexel-color-text-muted` |
| Borders | `--iexel-border-standard`, `--iexel-border-subtle`, `--iexel-border-emphasis`, `--iexel-border-on-dark` |
| Focus/disabled | `--iexel-focus-ring`, `--iexel-disabled-*` |
| Functional status | `--iexel-status-{success,warning,danger,info}-{bg,border,text}` |

Consumers should select a semantic role before selecting a raw club input.

### Layer 3 - component aliases

Foundation component aliases bind semantic roles to reusable UI needs:

- hero, standard card, feature card, and metric card;
- primary, secondary, ghost, and danger actions;
- neutral, success, warning, danger, and info statuses;
- progress track/value;
- primary and accent data-visualisation series.

Component aliases are deliberately small. Add one only when it represents a reusable product contract, not a one-page preference.

### Layer 4 - compatibility aliases

Existing public names remain available while consumers migrate. This includes:

- `--iexel-color-primary`, `--iexel-color-navy-deep`, and `--iexel-color-gold`;
- `--iexel-color-on-anchor` and `--iexel-color-on-anchor-muted`;
- compact/card radius aliases and legacy small/medium names;
- standard/elevated shadow aliases and legacy small/medium/large names;
- portal aliases such as `--iexel-midnight`, `--iexel-navy`, `--iexel-gold`, `--iexel-ink`, and `--iexel-bg`.

Do not delete or rename compatibility tokens during page migration. Remove them only after repository-wide usage evidence and a separate approval.

---

## Ownership boundary

### Club-owned inputs

The club may configure approved colours and imagery through the existing settings and `BrandingService` path. Values are validated before CSS output. No arbitrary CSS or new theme-settings system is part of this foundation.

### Product-owned semantics

Club OS owns:

- layouts, workspaces, spacing, and responsive composition;
- typography roles and supported weights;
- component structure and action hierarchy;
- focus, hover, disabled, and error behavior;
- semantic success, warning, danger, and info treatment;
- contrast-safe foreground selection.

Saved success, warning, and danger settings still feed the legacy `--iexel-color-*` tokens for compatibility. New status components must use the product-owned `--iexel-status-*` contracts. A later settings migration should deprecate the functional colour fields, measure remaining legacy consumers, migrate them, and only then stop emitting the compatibility mapping. Existing saved data must not be silently ignored.

---

## Foreground contrast derivation

`BrandingService::contrast_foreground()` derives a validated foreground for primary, secondary, and accent colours.

1. Accept a validated three- or six-digit hexadecimal colour.
2. If invalid or missing, use the validated role fallback; if that is also invalid, use canonical primary `#071d49`.
3. Convert sRGB channels to linear values using the WCAG relative-luminance formula.
4. Calculate luminance with coefficients 0.2126, 0.7152, and 0.0722.
5. At luminance greater than `0.179`, emit `#000000`; otherwise emit `#ffffff`.

The output is always a validated hex colour. This is a deterministic contrast-safety foundation, not a claim that every existing page is WCAG certified.

---

## Surface contracts

Use identity surfaces for club/product anchoring and feature surfaces for deliberate dark emphasis. Use page, card, muted, and elevated surfaces for operational content.

Opt-in shared helpers are available:

- `.iexel-surface--identity`;
- `.iexel-surface--identity-strong` and `.iexel-surface--feature`;
- `.iexel-surface--card` and `.iexel-surface--elevated`;
- `.iexel-surface--muted`.

Do not apply surface helpers indiscriminately. A page should retain deliberate dark/light rhythm and readable on-surface text.

---

## Typography

The canonical family token preserves the existing local stack: `Inter, Arial, sans-serif`. No external font is loaded.

Semantic roles are:

| Role | Intended use |
|---|---|
| Display | Page/hero title |
| Section | Major section title |
| Card | Card or item title |
| Metric | High-salience numeric value |
| Body | Default reading text |
| Supporting | Metadata, explanations, and secondary copy |
| Label | Eyebrow, kicker, and compact uppercase label |

Foundation-supported weights are 600, 700, and 800. Existing 750/850/900 consumers remain compatible but should migrate deliberately rather than being mass-rewritten. Use the corresponding `.iexel-type-*` helper only where an approved component migration is underway.

---

## Radius and depth

| Role | Token | Use |
|---|---|---|
| Compact/control | `--iexel-radius-compact`, `--iexel-radius-control` | Inputs, compact buttons, small nested surfaces |
| Standard card | `--iexel-radius-card` | Operational cards and standard sections |
| Feature/hero | `--iexel-radius-large` | Identity and feature surfaces |
| Pill | `--iexel-radius-pill` | Statuses and bounded chips |

Use `--iexel-shadow-standard` for normal elevation and `--iexel-shadow-elevated` for deliberate feature depth. Do not create page-specific shadow ladders. Flat surfaces need no new elevation token; use `box-shadow: none` within the scoped component contract when required.

---

## Action hierarchy

The shared `.iexel-experience-button` contract defines:

- `.is-primary`: club primary background with derived `on-primary` text;
- `.is-secondary`: light/card background with primary border and text;
- `.is-ghost` or legacy `.is-text`: transparent low-emphasis action;
- `.is-danger`: product-owned red danger action, never gold;
- visible hover and focus states;
- explicit disabled and `aria-disabled` behavior.

The previous shared ambiguity came from competing gold and navy `.is-primary` rules plus a coach-specific selector. The foundation now owns one sufficiently scoped primary contract. Page-specific action selectors remain migration debt and must be reviewed page by page.

---

## Workspace and responsive strategy

Canonical opt-in workspace values are:

- application maximum: `1380px`;
- reading/data maximum: `1180px`;
- desktop gutter: `20px`;
- mobile gutter: `12px`.

`.iexel-workspace` and `.iexel-workspace--content` expose these values without changing existing pages.

Recommended responsive composition:

- decompose major wide grids around `1024px`;
- use primary stacking around `760/768px`;
- define mobile component behavior around `520px`;
- accept at `390px` and `360px` without creating new global breakpoints merely for those widths.

Breakpoints remain authored in media queries because CSS custom properties cannot be used directly in media-query conditions. Production page widths and existing media queries are unchanged in this foundation batch.

---

## Migration rules

When a page migration is approved:

1. Inventory the page's raw colours, radii, shadows, type values, and action selectors.
2. Map intent through product semantics, then component aliases.
3. Use safe on-surface foregrounds whenever a configurable club colour is a background.
4. Keep gold out of functional warning and danger meaning.
5. Prefer fewer, stronger card types and responsive recomposition.
6. Validate at desktop, 1024px, 768px, 520px, 390px, and 360px as relevant.
7. Retain compatibility aliases until all consumers are proven migrated.
8. Update this document only for real foundation or migration changes.

Do not mass-edit `public.css` or `member-experience.css`. Do not claim page migration until the specific page and its browser acceptance have been completed.
