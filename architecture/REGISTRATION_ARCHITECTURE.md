# Registration Architecture

**Source of truth:** `app/core/Registrations/`
**Last verified:** 2026-07-24

---

## Overview

The Registrations module manages the player registration workflow for both administrators and families. Parents can submit registrations through the portal; administrators review and approve them.

---

## Registration Lifecycle

| Status | Description |
|---|---|
| `draft` | Started but not submitted |
| `submitted` | Submitted by parent, awaiting review |
| `under_review` | Being reviewed by administrator |
| `approved` | Approved; player is active |
| `rejected` | Rejected by administrator |
| `withdrawn` | Withdrawn by parent |

---

## Domain Entities

| Entity | Class | Table |
|---|---|---|
| Player registration | `PlayerRegistration` | `player_registrations` |

---

## Services

| Service | Responsibility |
|---|---|
| `PlayerRegistrationService` | Registration CRUD and lifecycle transitions |
| `PlayerRegistrationValidator` | Validate registration inputs |
| `PlayerRegistrationRepository` | Database access for registrations |
| `ParentRegistrationPortalService` | Portal-specific registration workflow for parents |

---

## Portal Registration Flow

1. Parent navigates to `/club-os/register` or clicks "Register a player" in their dashboard.
2. `PortalRegistrationWizardPage` renders a multi-step registration form.
3. Autosave is supported via the `iexel_registration_autosave` wp_ajax action, processed by `RegistrationPortalRequestHandler`.
4. On submission (both save draft and final submit), `PortalRegistrationWizardPage::handle_request()` processes the normal portal POST flow and updates the `PlayerRegistration` record.
5. Administrator reviews the submission in the Review Queue admin page.
6. Administrator approves or rejects the registration.

---

## Status

**MVP Complete.** Administrator and family registration workflows are implemented. The review queue, approval and rejection flows are operational.
