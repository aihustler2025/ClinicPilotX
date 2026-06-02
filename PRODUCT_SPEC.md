# ClinicPilotX Product Spec

Last updated: 2026-05-27

## Product Purpose

ClinicPilotX is a Buzzooka product for appointment-based and service businesses, including clinics, plastic surgery practices, dental clinics, med spas, beauty/wellness businesses, salons, and similar operators.

The product is intended to support real client testing and launch after the current Lovable build is audited, organized, verified, documented, and stabilized.

## Current Verification Status

The Lovable project is reportedly 70-80% complete, but no modules are considered verified yet in this official workspace.

Until the audit is complete, every major claim should be marked as one of:

- `Verified`: confirmed through direct evidence.
- `Claimed by Lovable`: stated by Lovable but not yet independently checked.
- `Mock/demo`: present but using mock, seed, placeholder, or demo data.
- `Incomplete`: partially present but not ready for real client testing.
- `Unknown`: not yet assessed.

## Product Areas To Audit

- Dashboard and analytics
- Admin panel
- User/staff portal
- Client/patient/customer-facing flows
- Appointment management
- Lead capture and CRM workflows
- Communication center
- Automations and reminders
- Calendar integrations
- Payment or subscription integrations
- AI/chatbot/voice workflows
- Settings, roles, and permissions
- Marketing website, only after core product functionality is itemized

## Backend To Audit

- Backend provider: unknown until Lovable responds.
- Database schema: unknown until Lovable responds.
- Auth provider and roles: unknown until Lovable responds.
- Integrations: unknown until Lovable responds.
- Real data vs mock/demo data: unknown until Lovable responds.

## Module Registry

No module is verified yet. Add modules here only after review and verification.

| Module | Status | Evidence | Notes |
| --- | --- | --- | --- |
| TBD | Unknown | Pending Lovable audit | Do not mark complete until verified. |

## Source Material Review - 2026-06-02

Ross provided old/source ClinicPilot documents from `D:\PROJECTS\CLINICPILOT X (Old)`. These were reviewed as reference material only. Review saved at `09-exports/source-material-review-2026-06-02.md`.

Durable concepts to carry forward into ClinicPilotX:

- AI-powered front desk and growth assistant for clinics and appointment-based service businesses.
- Unified lead capture across email, forms, chatbot, voice/phone, manual entry, social leads, and future messaging channels.
- Fast patient/prospect acknowledgments and staff alerts.
- Leads pipeline with source, status, qualification/classification, and follow-up tracking.
- Appointment request workflow that collects preferred times and supports staff-confirmed scheduling.
- Payment/deposit concept, with paid integrations requiring explicit approval before activation.
- Reminder, no-show, outgoing follow-up, review request, missed-call recovery, and voice assistant concepts.
- PriorityBook scoring/prioritization for high-value or time-sensitive requests.
- Automation Center with per-clinic settings for channels, timing, quiet hours, deposits, reminders, and scoring weights.

Architecture caveat: source docs often assume n8n plus Google Sheets. The current Lovable project must be audited before choosing or changing architecture. Do not assume the old stack is the right stack for the new official build.

## Live App Inventory - 2026-06-02 Pre-Login

Current deployed app: `https://clinic-pilot-x.lovable.app`
Lovable project ID: `8b4d9031-af8d-4faf-81d3-135c41ad73b7`
Backend evidence: standalone Supabase project `imuyfbvsombbpgdgkhrb`.

Current left-nav modules found in deployed bundle:

- Dashboard
- Leads
- Patients
- Appointments
- Communication Hub
- Video Consultation
- Payments & Billing
- Analytics & Reporting
- Staff Management
- Automation Center
- Auto-Assignment Rules
- Subscription
- Settings
- Profile

Status: module presence is verified from the deployed bundle, but live behavior is not yet verified because login is required. See `09-exports/live-app-inventory-prelogin-2026-06-02.md`.
