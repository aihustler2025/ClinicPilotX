# ClinicPilotX Authenticated Platform Audit

Date: 2026-06-03

## Access Method

Codex used a dedicated Chrome QA browser with Playwright attached through local Chrome remote debugging.

The authenticated app was available at:

`https://clinic-pilot-x.lovable.app/dashboard`

## Confirmed Left Navigation

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

## First Verified Inventory

### Dashboard

Shows high-level CRM metrics, recent leads, lead source counts, appointment summaries, and revenue summary.

### Leads

Shows lead management with search, export, refresh, add lead, and status filters. Current visible totals included 13 total leads.

### Patients

Shows patient directory with search, export, add patient, status filter, and sort controls.

### Appointments

Shows 26 total appointments, list view, calendar view, date range, filters, export, and book appointment controls.

Calendar View opens correctly and shows a June 2026 calendar layout.

### Communication Hub

External Messages opens and shows unified inbox-style conversations across SMS, WhatsApp, and Messenger.

Internal Chat opens and shows sections for group channels, direct messages, and staff members. It currently shows a blank "Select a channel" state.

### Video Consultation

The module exists but currently shows "Coming Soon."

### Payments & Billing

Shows payment/invoice search, status filter, method filter, recent filter, new invoice, and export controls.

### Analytics & Reporting

Shows revenue, appointments, lead conversion, active staff, revenue trends, appointment trends, date range, and export controls.

### Staff Management

Shows staff management with add staff, role filter, and search. Visible users include `teambuzzooka@gmail.com` and `Kizha Kaye`.

### Automation Center

Shows workflows and activity logs.

Workflow categories include:

- Lead Intake
- Nurture
- Patient Engagement
- Financial
- Analytics

Activity Logs opens correctly and shows recent workflow executions, including multiple completed Appointment Confirmation runs.

### Auto-Assignment Rules

This page has a verified backend error.

The frontend tries to load `assignment_rules`, but Supabase returns:

`PGRST205: Could not find the table 'public.assignment_rules' in the schema cache`

This page needs Lovable/Supabase repair before it can be considered functional.

### Subscription

Shows current plan, available plans, and add-ons.

Potential issue: during authenticated navigation, the app sometimes displayed `Professional` and sometimes displayed `No Plan` for the same user/session. This may indicate a subscription state loading bug or inconsistent profile/subscription lookup.

### Settings

Tabs open correctly:

- General
- Notifications
- Integrations
- Profile
- Email Logs
- Audit Log

Settings Integrations lists Twilio, Facebook Messenger, Viber, Google Calendar, Stripe, and email test tools.

Email Logs exposes Resend webhook setup:

`https://imuyfbvsombbpgdgkhrb.supabase.co/functions/v1/resend-webhook`

### Profile

The main `/profile` navigation page currently shows "Coming Soon."

Settings > Profile is separate and shows user profile fields.

## Important Early QA Findings

1. Auto-Assignment Rules is broken because the expected `assignment_rules` table is missing or unavailable.
2. Subscription/plan display appears inconsistent between `Professional` and `No Plan`.
3. Video Consultation is not built yet.
4. Main Profile page is not built yet.
5. Internal Chat opens but appears empty until a channel or staff member exists/loads.
6. Settings Integrations exists but should not be tested with real sends until credentials, sandbox mode, and cost controls are confirmed.
7. Automation Activity Logs exist and show prior workflow executions, so this app has real workflow history to audit.

## QA Artifacts

Local screenshots and JSON captures were saved in:

`C:\Users\Rosstafari\Documents\CLINICPILOTX\qa-output\authenticated-audit`

Support scripts were created in:

`C:\Users\Rosstafari\Documents\CLINICPILOTX\scripts`

## Next Recommended Verification

1. Verify Supabase tables, RLS, and policies for all app modules.
2. Ask Lovable why `assignment_rules` is referenced but missing.
3. Ask Lovable why the same logged-in session sometimes shows `No Plan`.
4. Audit Automation Center workflow configs before clicking any workflow test/send buttons.
5. Investigate whether old n8n workflows still exist in Hostinger before recreating anything.

