# ClinicPilotX Product Spec

Last updated: 2026-06-11

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

- Backend provider: evidence points to standalone Supabase project `imuyfbvsombbpgdgkhrb` plus Lovable-managed deployment/secrets, but Lovable must confirm the exact Lovable Cloud/Supabase relationship.
- Database schema: partially inferred from deployed app behavior and Supabase errors, but not fully verified.
- Auth provider and roles: Supabase auth is evidenced by deployed app behavior; role model still requires verification.
- Integrations: Automation Center and backend functions reference email, SMS, payment, AI, and appointment workflows; sandbox/live credential status must be confirmed before testing.
- Real data vs mock/demo data: partially assessed through authenticated QA, but still requires module-by-module verification.

## Architecture Direction - 2026-06-05

ClinicPilotX should treat Lovable Cloud/Lovable hosting/Supabase as the preferred production path before considering new paid backend or hosting platforms, because Ross already has Lovable package benefits.

Local n8n is approved only for review/testing/import of old workflow blueprints on the laptop. It must not become production infrastructure for commercial ClinicPilotX workflows unless Ross later approves a reliable hosting, monitoring, backup, security, and cost plan.

There may be two Lovable projects:

- Main ClinicPilotX CRM/dashboard.
- Separate partially built ClinicPilotX marketing website.

Do not assume they are merged. Lovable must clarify project IDs, URLs, GitHub connections, Supabase/backends, hosting status, and merge readiness before build decisions.

## Module Registry

First authenticated read-only module audit completed on 2026-06-11. See:

`09-exports/authenticated-dashboard-module-audit-2026-06-11.md`

| Module | Status | Evidence | Notes |
| --- | --- | --- | --- |
| Dashboard | Partially verified | Authenticated browser audit | Loads with dashboard metrics and sections, but metrics need data-source validation. |
| Leads | Partially verified | Authenticated browser audit | 11 leads visible with filters/search/export/Add Lead; CRUD and conversion need controlled test data. |
| Patients | Partially verified | Authenticated browser audit | Patient list, statuses, visits/revenue, search/filter/export/Add Patient visible; CRUD/linkage not yet tested. |
| Appointments | Partially verified | Authenticated browser audit | 26 appointments visible; list and calendar views open. Booking/editing/reminders need safe test plan. |
| Communication Hub | Partially verified | Authenticated browser audit | External Messages and Internal Chat tabs open; message sending not tested. |
| Video Consultation | Incomplete | Authenticated browser audit | Route shows `Coming Soon`. |
| Payments & Billing | Partially verified | Authenticated browser audit | Payment/invoice UI visible; payment link/Stripe flows not tested. |
| Analytics & Reporting | Partially verified | Authenticated browser audit | Reporting UI visible; values require validation against source data. |
| Staff Management | Partially verified | Authenticated browser audit | Staff list and role controls visible; permissions/invites not tested. |
| Automation Center | Partially verified / high priority | Authenticated browser audit | Workflows and Activity Logs tabs open; activity logs show completed Appointment Confirmation runs. |
| Auto-Assignment Rules | Broken / blocked | Authenticated browser audit | Route remains on `Loading assignment rules...`, consistent with missing/unavailable backend table. |
| Subscription | Partially verified | Authenticated browser audit | Professional plan UI visible; entitlement consistency still suspect. |
| Settings | Partially verified | Authenticated browser audit | General, Notifications, Integrations, Profile, Email Logs verified; Audit Log needs retest. |
| Profile | Incomplete | Authenticated browser audit | Main route shows `Coming Soon`. |

## Automation Center / n8n Blueprint Mapping

Old n8n workflow exports are reference blueprints only until imported into local n8n and reviewed. Keep all imported workflows inactive.

Initial known old workflow categories:

- Daily clinic/staff reporting.
- Email agent or email automation.
- Notifications.
- Outbound voice calling.
- Outbound reachout/follow-up.
- SMS messaging.
- VAPI inbound calling scenario.

Each workflow should be mapped to one of:

- Rebuild in Lovable/Supabase as app-native production automation.
- Retain as n8n orchestration only after a production-grade n8n plan is approved.
- Discard if obsolete or duplicated by current Automation Center behavior.

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
