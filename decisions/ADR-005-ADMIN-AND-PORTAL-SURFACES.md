# ADR-005: Dual Surface Strategy — Admin and Portal

**Status:** Accepted
**Date:** 2025-04-01 (estimated)
**Last verified:** 2026-07-24

---

## Context

As Club OS matured, it became clear that some functionality needed to be available on both the admin surface (for administrators) and the portal surface (for members). For example, Finance is managed by administrators in wp-admin but also needs to be accessible to Treasurers who should not have wp-admin access.

---

## Decision

Club OS implements a dual surface strategy for modules that need to serve both administrators and non-admin members:

1. The **admin surface** provides full management capabilities via wp-admin pages
2. The **portal surface** provides a role-appropriate view of the same data via the Member Portal

Both surfaces share the same backend services and repositories. The portal surface enforces access control via the `MemberExperienceService` and the experience role system.

The Treasurer role is the canonical example: it has a full Finance workspace at `/club-os/finance/` in the portal, but does not have wp-admin access.

---

## Consequences

**Positive:**
- Non-admin roles (Treasurer, Coach) can access their functionality without wp-admin
- Consistent data model across both surfaces
- Portal can be mobile-optimised independently

**Negative:**
- Some functionality is implemented twice (admin page + portal page)
- Access control logic must be maintained in both surfaces
- More routes and pages to manage

---

## Implementation

- Admin Finance: `app/core/UI/Pages/Finance/`
- Portal Finance: `app/core/UI/Pages/Portal/Finance/`
- Treasurer role: `ClubRoleCapabilityRegistrar.php`
- Portal routing: `app/core/Portal/PortalRouter.php`
