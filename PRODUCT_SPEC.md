# ClinicPilotX Product Spec

Last updated: 2026-06-12

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
| Patients | Partially verified | Authenticated browser audit + controlled CRM QA | Patient list, statuses, visits/revenue, search/filter/export/Add Patient visible. Lead-to-patient conversion verified with dummy record. Patient editing still needs testing. |
| Appointments | Partially verified / issue found | Authenticated browser audit + controlled CRM QA | 26 appointments visible; list and calendar views open. Booking form lists converted patient and auto-fills contact info, but dummy booking attempt closed without visible success and did not show a new row. |
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

## Controlled CRM QA Notes - 2026-06-11

Verified lead lifecycle behavior:

- A manual dummy lead can be created.
- Lead search can isolate that dummy lead by name.
- Lead edit saves service/notes changes.
- Lead Details view opens and shows contact, service, notes, timeline, and action controls.
- Converting a lead to a patient creates a patient record with matching name, email, and phone.

Open product/engineering issues:

- Editing a lead's service/notes and creating later leads changed existing dummy lead status/temperature without an explicit status/temperature edit.
- The app intermittently displays `No Plan` where `Professional` is expected, while still showing protected CRM data.
- Appointment booking for a converted dummy patient did not visibly persist or confirm success.
- Leads `Show Converted` can display confusing count/table behavior and needs clear converted-lead handling.
- Leads export should support explicit export scope, current filters, statuses, date range, source, file type, column selection, estimated row count, and clear filenames.
- Leads manual creation should use a proper international phone input with country selector, digits-only typing, display formatting such as `+1 (555) 123-4567`, and normalized storage.
- Leads manual creation should use a searchable service selector with custom service entry and future clinic-specific service lists.
- Leads should be ready for future intake sources: chatbot, email inquiry parser, website contact forms, phone/voice assistant, manual entry, Facebook, Instagram, and referrals.
- Lead details should become the full record of the relationship, including communication history, uploaded photos/files, timeline activity, staff assignment, follow-up context, and conversion history.

These issues should be clarified or fixed before writing final customer-facing tutorials for lead conversion and appointment booking.

## Leads Published v2 QA - 2026-06-11

After Lovable's Leads improvement build was approved and published, Codex verified the following live behavior:

- Manual lead creation supports expanded lead intake fields: contact info, country-aware phone input, service selector, source, preferred contact, urgency, consent, and notes.
- Phone storage normalizes to E.164, verified with `+12135550199`.
- Service selection saved a catalog value, verified with `Botox`.
- Lead Details now has Overview, Timeline, Comms, Files, and Activity tabs.
- Timeline records created and edited events.
- Files tab is intentionally disabled for now and explains that future file/photo uploads require a storage backend.

Still incomplete:

- A notes-only lead edit changed the test lead temperature from `Cold` to `Hot`. Lead status stayed `NEW LEAD`, but temperature mutation on safe edits is not acceptable for final behavior.
- Invalid phone input needs a visible validation message.
- U.S./Canada display formatting should be improved toward `+1 (213) 555-0199`, while keeping normalized E.164 database storage.
- Export dialog still needs a clean retest after the blocking temperature issue is fixed.

## Leads v2 Fix QA - 2026-06-12

After Lovable's QA fix build was approved and published, Codex retested the live Leads workflow.

Verified final behavior for this pass:

- Invalid phone numbers block lead creation and show an inline validation message.
- Valid U.S. digits can be typed without punctuation and are accepted.
- Manual lead creation still normalizes stored phone data to E.164.
- Lead Details displays U.S./Canada-style phone formatting such as `+1 (213) 555-0199`.
- A newly created lead starts as `NEW LEAD` and `Cold`.
- Editing notes only no longer changes lead status or temperature.
- Timeline records both `Lead created` and `Lead edited` events.

Current Leads status:

- Leads v2 critical temperature mutation blocker is resolved for the tested create/edit path.
- Leads remains `Partially verified`, because export behavior, converted-lead filtering, patient/appointment continuation, and future intake-source readiness still need deeper QA.

Remaining Leads polish:

- The main Leads table still shows E.164 phone values such as `+12135550199`; detail formatting is fixed, but table formatting should be reviewed.
- Invalid-phone helper copy should ideally match the preferred display format.

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
