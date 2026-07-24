# ADR-002: Provider-Widget Pattern for Dashboard Sections

**Status:** Accepted
**Date:** 2025-03-01 (estimated)
**Last verified:** 2026-07-24

---

## Context

Dashboard pages in Club OS aggregate data from multiple domain services and render it as a collection of sections (widgets). Early implementations mixed data retrieval and rendering in a single class, making testing difficult and coupling the data model to the view.

---

## Decision

Dashboard sections are implemented using the Provider-Widget pattern:

- A **Provider** class retrieves and structures data from domain services. It has no rendering responsibility.
- A **Widget** class receives the structured data and renders HTML. It has no database access.

The dashboard service (e.g. `ExecutiveDashboardService`) orchestrates Providers and Widgets.

---

## Consequences

**Positive:**
- Providers can be unit-tested without rendering
- Widgets can be tested with mock data
- Data structure is explicit and documented
- Providers can be reused across multiple surfaces

**Negative:**
- More classes per dashboard section
- Requires discipline to keep Providers free of rendering logic

---

## Implementation

- Providers: `app/core/Dashboard/Providers/`, `app/core/UI/Components/Dashboard/`
- Widgets: `app/core/UI/Components/Dashboard/`, `app/core/UI/Components/Portal/`
- Standards: [PROVIDER_AND_WIDGET_STANDARDS.md](../standards/PROVIDER_AND_WIDGET_STANDARDS.md)
