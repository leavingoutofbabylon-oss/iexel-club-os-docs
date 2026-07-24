# Version 2.0 Planning

**Target:** 3–6 months after Version 1.0
**Last verified:** 2026-07-24

---

## Overview

Version 2.0 is the platform expansion release. It introduces new modules, multi-club support and payment gateway integration.

---

## Planned Modules

### Rewards Module

Implement the `iexel_manage_rewards` capability:

- Points-based rewards system for players
- Reward categories (attendance, goals, assists, fair play)
- Reward redemption
- Leaderboard widget for portal

**Status:** Placeholder capability declared; no implementation

---

### Multi-Club Support

Allow a single Club OS installation to manage multiple clubs:

- Club selector in admin and portal
- Per-club data isolation
- Per-club branding

**Effort:** Large
**Risk:** Significant architectural change; requires careful planning

---

### Payment Gateway Integration

Integrate with a payment gateway (e.g. Stripe, GoCardless):

- Online invoice payment via portal
- Direct Debit setup for recurring billing
- Payment confirmation and reconciliation

**Effort:** Large

---

### Mobile App

A React Native mobile app for club members:

- Push notifications for events and communications
- Match Mode on mobile
- Attendance check-in via QR code

**Effort:** Large

---

### Advanced Statistics and Reporting

- Season-level statistics aggregation
- Comparative statistics across seasons
- Exportable reports (PDF, CSV)
- Statistics widgets for portal

---

### Public Club Website Integration

- Public-facing club website pages (fixtures, results, squad)
- Integration with WordPress theme
- SEO-friendly URLs

---

## Architecture Considerations for 2.0

Multi-club support will require:

1. A `clubs` table and `club_id` foreign key on all domain tables
2. A `ClubContext` service injected into all repositories
3. Per-club capability scoping
4. Per-club branding and settings

This is a significant architectural change and should be planned as a dedicated spike before implementation.
