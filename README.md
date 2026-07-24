# IEXEL Club OS — Architecture Pack

**Version:** 0.2.10-dev  
**Schema version:** 2026.07.2  
**Branch:** `docs/architecture-pack`

---

## What is Club OS?

IEXEL Club OS is a proprietary WordPress plugin that provides a complete football club operating system for IEXEL F.C. It runs on WordPress 6.7+ with PHP 8.2+ and delivers two distinct surfaces:

- A **wp-admin management surface** for club administrators, coaches, welfare officers and treasurers.
- A **frontend member portal** at `/club-os/` providing role-based workspaces for parents, players, coaches, committee members and treasurers.

The plugin is entirely self-contained. It has no Composer runtime dependencies beyond WordPress itself.

---

## Purpose of this Repository

This repository (`iexel-club-os-docs`) is the authoritative documentation source for the IEXEL Club OS Architecture Pack. It is maintained on the `docs/architecture-pack` branch and must not be merged to `main` until a formal documentation release is approved.

The source code repository (`iexel-club-os`) is the implementation source of truth. Where any document conflicts with source code, the source code is correct and the document must be updated.

---

## Where Developers Should Start

| Goal | Start here |
|---|---|
| Understand the system | [`architecture/SYSTEM_OVERVIEW.md`](architecture/SYSTEM_OVERVIEW.md) |
| Understand the module map | [`architecture/MODULE_MAP.md`](architecture/MODULE_MAP.md) |
| Understand the database | [`reference/DATABASE_TABLE_REFERENCE.md`](reference/DATABASE_TABLE_REFERENCE.md) |
| Understand permissions | [`reference/CAPABILITY_REFERENCE.md`](reference/CAPABILITY_REFERENCE.md) |
| Understand admin pages | [`reference/ADMIN_MENU_REFERENCE.md`](reference/ADMIN_MENU_REFERENCE.md) |
| Understand portal routes | [`reference/PORTAL_ROUTE_REFERENCE.md`](reference/PORTAL_ROUTE_REFERENCE.md) |
| Write code | [`development/MASTER_DEVELOPER_GUIDE.md`](development/MASTER_DEVELOPER_GUIDE.md) |
| Use an AI agent | [`development/AI_AGENT_GUIDE.md`](development/AI_AGENT_GUIDE.md) |
| Understand MVP status | [`roadmap/MVP_STATUS.md`](roadmap/MVP_STATUS.md) |
| Understand technical debt | [`reference/TECHNICAL_DEBT_REGISTER.md`](reference/TECHNICAL_DEBT_REGISTER.md) |

---

## Authoritative Documents

The following documents are the canonical references for their respective domains. All other documents must link to these rather than duplicating content.

| Domain | Authoritative document |
|---|---|
| System architecture | [`architecture/SYSTEM_OVERVIEW.md`](architecture/SYSTEM_OVERVIEW.md) |
| Module inventory | [`architecture/MODULE_MAP.md`](architecture/MODULE_MAP.md) |
| Database schema | [`reference/DATABASE_TABLE_REFERENCE.md`](reference/DATABASE_TABLE_REFERENCE.md) |
| Capabilities and roles | [`reference/CAPABILITY_REFERENCE.md`](reference/CAPABILITY_REFERENCE.md) |
| Admin menu slugs | [`reference/ADMIN_MENU_REFERENCE.md`](reference/ADMIN_MENU_REFERENCE.md) |
| Portal routes | [`reference/PORTAL_ROUTE_REFERENCE.md`](reference/PORTAL_ROUTE_REFERENCE.md) |
| Request actions | [`reference/REQUEST_ACTION_REFERENCE.md`](reference/REQUEST_ACTION_REFERENCE.md) |
| Module status | [`reference/MODULE_STATUS.md`](reference/MODULE_STATUS.md) |
| Technical debt | [`reference/TECHNICAL_DEBT_REGISTER.md`](reference/TECHNICAL_DEBT_REGISTER.md) |
| MVP status | [`roadmap/MVP_STATUS.md`](roadmap/MVP_STATUS.md) |
| Architecture decisions | [`decisions/README.md`](decisions/README.md) |

---

## How AI Agents Should Use These Docs

See [`development/AI_AGENT_GUIDE.md`](development/AI_AGENT_GUIDE.md) for the full AI agent workflow.

**Key rules for AI agents:**

1. Read [`architecture/SYSTEM_OVERVIEW.md`](architecture/SYSTEM_OVERVIEW.md) and [`architecture/MODULE_MAP.md`](architecture/MODULE_MAP.md) before any implementation task.
2. Verify every class, table, capability and route against the source code before documenting or implementing.
3. Do not invent modules, tables, capabilities or completed features.
4. Clearly distinguish Complete, MVP Complete, In Progress, Partial, Placeholder, Planned, Post-MVP and Deprecated.
5. Do not modify plugin source code when working in this repository.
6. Commit documentation changes only to `docs/architecture-pack`.

---

## Implemented vs Planned Features

This documentation uses the following status classifications, derived from source code inspection:

| Status | Meaning |
|---|---|
| **Complete** | Fully implemented, tested and production-ready |
| **MVP Complete** | Implemented to MVP standard; known gaps documented |
| **In Progress** | Partially implemented; active development |
| **Partial** | Structural code exists; significant functionality missing |
| **Placeholder** | Directory or class exists; no functional implementation |
| **Planned** | Documented in roadmap or inventory; not yet started |
| **Post-MVP** | Intentionally deferred after Release 1.0 |
| **Deprecated** | Legacy code retained for compatibility; no new consumers |

The [`reference/MODULE_STATUS.md`](reference/MODULE_STATUS.md) document provides the complete status register for all modules.

---

## Document Structure

```
README.md                          ← This file
architecture/                      ← System and module architecture
standards/                         ← Coding, database and UI standards
development/                       ← Developer guides and workflows
reference/                         ← Authoritative inventories and registers
roadmap/                           ← MVP status and future versions
decisions/                         ← Architecture Decision Records (ADRs)
release/                           ← Changelog, release notes and candidate plan
```

---

## Discrepancies with Source Code

Any discrepancy between this documentation and the source code must be recorded in [`reference/TECHNICAL_DEBT_REGISTER.md`](reference/TECHNICAL_DEBT_REGISTER.md) under the "Documentation Discrepancy" category. The source code is always correct.
