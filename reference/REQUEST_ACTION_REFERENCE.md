# Request Action Reference

**Source of truth:** `app/core/Release/ReleaseRouteInventory.php` and all `*RequestHandler.php` files
**Last verified:** 2026-07-24

---

## Overview

Club OS mutations are handled via WordPress `admin_post_*` hooks (authenticated) and `admin_post_nopriv_*` hooks (unauthenticated). One AJAX action is registered for autosave.

All handlers follow the guard pattern: check POST method, check capability, check nonce.

---

## Authentication Actions

| Hook | Handler | Capability |
|---|---|---|
| `admin_post_iexel_club_os_login` | `AuthenticationRequestHandler` | Public (nopriv) |
| `admin_post_nopriv_iexel_club_os_login` | `AuthenticationRequestHandler` | Public |
| `admin_post_iexel_club_os_logout` | `AuthenticationRequestHandler` | Authenticated |
| `admin_post_nopriv_iexel_club_os_lost_password` | `AuthenticationRequestHandler` | Public |

---

## People and Relationships Actions

| Hook | Handler | Capability |
|---|---|---|
| `admin_post_iexel_add_person_relationship` | `PersonRelationshipRequestHandler` | `iexel_manage_people` |
| `admin_post_iexel_remove_person_relationship` | `PersonRelationshipRequestHandler` | `iexel_manage_people` |
| `admin_post_iexel_set_billing_contact` | `PersonRelationshipRequestHandler` | `iexel_manage_people` |
| `admin_post_iexel_entity_lifecycle` | `EntityLifecycleAdminRequestHandler` | `iexel_manage_people` |

---

## Team Assignment Actions

| Hook | Handler | Capability |
|---|---|---|
| `admin_post_iexel_team_assignment_create` | `TeamAssignmentAdminRequestHandler` | `iexel_manage_club_os` |
| `admin_post_iexel_team_assignment_update` | `TeamAssignmentAdminRequestHandler` | `iexel_manage_club_os` |
| `admin_post_iexel_team_assignment_delete` | `TeamAssignmentAdminRequestHandler` | `iexel_manage_club_os` |

---

## Branding and Media Actions

| Hook | Handler | Capability |
|---|---|---|
| `admin_post_iexel_branding_save` | `BrandingAdminRequestHandler` | `iexel_manage_club_os` |
| `admin_post_iexel_entity_media_save` | `EntityMediaAdminRequestHandler` | `iexel_manage_club_os` |

---

## Finance Actions

All Finance actions use the pattern `admin_post_iexel_finance_{action}`.

| Action suffix | Capability |
|---|---|
| Invoice CRUD | `iexel_manage_finance` |
| Payment recording | `iexel_record_payments` |
| Billing schedule CRUD | `iexel_manage_billing` |
| Fee rule CRUD | `iexel_manage_billing` |
| Discount policy CRUD | `iexel_manage_billing` |

---

## Communications Actions

| Hook | Handler | Capability |
|---|---|---|
| `admin_post_iexel_save_communication` | `CommunicationAdminRequestHandler` | `iexel_manage_club_os` |
| `admin_post_iexel_communication_action` | `CommunicationAdminRequestHandler` | `iexel_manage_club_os` |
| `admin_post_iexel_communication_template` | `CommunicationAdminRequestHandler` | `iexel_manage_club_os` |

---

## Club Projects Actions

All Club Projects actions use the pattern `admin_post_iexel_club_project_{action}`.

| Action | Capability |
|---|---|
| `create` | `iexel_create_club_projects` |
| `update` | `iexel_edit_club_projects` |
| `archive` | `iexel_archive_club_projects` |
| `restore` | `iexel_archive_club_projects` |
| `show` | `iexel_manage_club_project_visibility` |
| `hide` | `iexel_manage_club_project_visibility` |
| `complete` | `iexel_edit_club_projects` |
| `reopen` | `iexel_edit_club_projects` |
| `reorder` | `iexel_edit_club_projects` |

---

## Member Experience Actions

| Hook | Handler | Capability |
|---|---|---|
| `admin_post_iexel_member_experience_switch` | `MemberExperienceRequestHandler` | Authenticated |

---

## Registration Actions

| Hook | Handler | Capability |
|---|---|---|
| `wp_ajax_iexel_registration_autosave` | `RegistrationPortalRequestHandler` | Authenticated |
| Portal registration submit | `RegistrationPortalRequestHandler` | Authenticated |

---

## WP-Cron Actions

| Hook | Processor |
|---|---|
| `iexel_club_os_process_communication` | `CommunicationService::process_scheduled_communication()` |
| `iexel_club_os_process_billing_schedules` | `RecurringBillingService::process_due()` |

---

## Nonce Naming Convention

All nonces follow the pattern: `iexel_{module}_{operation}_{optional_id}`

Examples:
- `iexel_club_project_create`
- `iexel_club_project_update_{id}`
- `iexel_club_project_archive_{id}`
- `iexel_branding_save`
- `iexel_team_assignment_create`
