# ClinicPilotX Authenticated Dashboard Module Audit

Date: 2026-06-11

## Scope

Codex connected browser control to the authenticated ClinicPilotX Lovable app and performed a read-only module sweep at:

`https://clinic-pilot-x.lovable.app`

This was a safe audit pass. No paid actions were clicked, no live credentials were entered, no sends/calls/payment links were triggered, and no destructive create/edit/delete actions were performed.

## Key Takeaways

- Browser control is working for the in-app browser, so repeatable click-by-click QA is now available on the laptop.
- The live dashboard is a substantial existing product, not a blank project.
- The current app appears to be driven by Lovable plus Supabase/Lovable Cloud style functions and secrets, not by direct frontend n8n references.
- Automation Center is present with workflow rows, plan gating, configure buttons, and activity logs.
- Local n8n remains useful for safe workflow prototyping and old-workflow review, but production workflow ownership must be decided after Lovable/Supabase architecture is confirmed.
- Do not trigger email/SMS/voice/payment test buttons until credential mode, sandbox mode, and client-test boundaries are confirmed.

## Safety Rules During Audit

Avoid clicking these until Ross explicitly approves the exact test:

- `Send Test Email`
- SMS/WhatsApp/Messenger send buttons
- voice/VAPI call buttons
- Stripe/payment link buttons
- subscription upgrade/downgrade/add-on buttons
- workflow activation buttons
- create/edit/delete/convert actions using real records

## Module Readiness Matrix

| Module | Verified UI State | Current Readiness | Notes |
| --- | --- | --- | --- |
| Dashboard | Loads behind login with metrics cards, upcoming appointments, leads by source, patient counts, follow-ups, revenue, recent leads. | Needs data-source verification | Metrics showed zeros even while other modules have records, so calculations/data filters need review. |
| Leads | Loads with 11 leads, status tabs, source/status/staff filters, search, export, refresh, and Add Lead. | Needs controlled CRUD test | Records and scoring/status UI exist. Test create/edit/convert/delete only with approved test data. |
| Patients | Loads with patient list, statuses, visit totals, revenue totals, search, filters, export, Add Patient. | Needs controlled CRUD test | Contains real/demo patient-looking data. Need verify record model and lead-to-patient linkage. |
| Appointments | Loads with 26 appointments, list view, calendar view, filters, export, Book Appointment, status counts. | Partially verified | Calendar view opens. Need controlled booking/edit/status/reminder/payment-request test. |
| Communication Hub | External Messages and Internal Chat tabs open. External inbox shows conversations; internal chat shows channel/staff selection state. | Partially verified | Prior RLS recursion concern still needs backend verification. Do not send messages yet. |
| Video Consultation | Route loads but shows `Coming Soon`. | Incomplete | Future module requirements need definition before build. |
| Payments & Billing | Loads invoices/payments with totals, filters, search, New Invoice, export. | Needs safe payment test plan | Do not create payment links or touch Stripe until sandbox/live credential status is confirmed. |
| Analytics & Reporting | Loads metrics, date range, charts/sections, export. | Needs validation | Shows zeros for current period; needs data aggregation verification against real module data. |
| Staff Management | Loads 2 staff records, roles/search, Add Staff Member, response/conversation summary. | Needs roles/permissions test | Verify staff invite/edit permissions and role boundaries with test users. |
| Automation Center | Loads Workflows and Activity Logs tabs. Shows current plan Professional and `7 / 13 Active`. | High-priority audit area | Workflows have Configure/Upgrade controls. Activity Logs show recent Appointment Confirmation executions. |
| Auto-Assignment Rules | Route opens but remains on `Loading assignment rules...`. | Broken / blocked | Consistent with missing or unavailable `assignment_rules` backend/schema support. |
| Subscription | Shows Current Plan: Professional, available plans, add-ons, downgrade/upgrade/add buttons. | Needs entitlement verification | Prior and current sweeps show inconsistent plan display in some contexts; do not click billing actions. |
| Settings | General, Notifications, Integrations, Profile, Email Logs tabs verified. | Partially verified | Integrations tab exposes credential placeholders and says credentials are managed via Lovable Cloud secrets. Audit Log tab needs retest. |
| Profile | Route loads but shows `Coming Soon`. | Incomplete | Main profile route differs from Settings > Profile, which shows read-only user profile fields. |

## Automation Center Findings

Workflow tab evidence:

- Current Plan shown as `Professional`.
- Active count shown as `7 / 13 Active` during the latest read-only audit.
- Visible workflow rows included Lead Intake, Multi-Channel Sync, AI Voice Agent - Inbound, Lead Scoring & Assignment, Facebook Messenger Bot, WhatsApp Business Integration, Lead Acknowledgment, Advanced Lead Nurture AI, AI Voice Agent - Outbound, and related follow-up/payment/reporting workflows.
- Some rows have `Configure`; some have `Upgrade`.

Activity Logs tab evidence:

- Activity Logs opens.
- Recent Workflow Executions table is present.
- Rows show completed `Appointment Confirmation` executions from about 15 days earlier with durations around 550-700ms.

Open concerns:

- Earlier audits referenced 19 workflow rows, while this authenticated UI pass shows `7 / 13 Active`. Lovable/Supabase must clarify whether this is plan-gated filtering, seeded data drift, or a bug.
- Subscription state has shown both `Professional` and `No Plan` in related audits. Entitlement logic must be verified before approving build work.
- Workflow configuration buttons were not opened in this pass to avoid accidental sends or credential exposure.

## Settings / Integration Findings

Verified tabs:

- General
- Notifications
- Integrations
- Profile
- Email Logs

Integrations tab shows configuration areas for:

- Twilio SMS/WhatsApp
- Facebook Messenger
- Viber
- Google Calendar email
- Stripe customer ID
- Email configuration test

Important UI copy says API credentials are managed securely via Lovable Cloud secrets and support/contact is needed to update them. Lovable must confirm exactly where secrets live and whether they are sandbox or live.

Email Logs tab shows:

- Resend webhook URL: `https://imuyfbvsombbpgdgkhrb.supabase.co/functions/v1/resend-webhook`
- Events: `email.sent`, `email.delivered`, `email.bounced`, `email.opened`, `email.clicked`
- Historical sent email rows, including appointment reminder-style subjects.

Audit Log tab was not successfully captured in this pass and needs retest.

## Immediate Next QA Pass

1. Open every Automation Center `Configure` panel without saving or sending, then document available settings.
2. Create a safe controlled test-data plan for Leads, Patients, Appointments, Payments, and Communication.
3. Ask Lovable to confirm project/backend/marketing-site details using handoff 003.
4. Confirm whether integrations are connected to sandbox credentials or live services.
5. Investigate `assignment_rules`, subscription/entitlement inconsistency, internal chat RLS, and public anon data exposure before any client-facing test.

