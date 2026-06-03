# ClinicPilotX Platform Investigation

Date: 2026-06-03
URL: https://clinic-pilot-x.lovable.app
Lovable project ID: `8b4d9031-af8d-4faf-81d3-135c41ad73b7`
Supabase project ref: `imuyfbvsombbpgdgkhrb`

## Executive Summary

Codex attempted to use the authenticated in-app browser session that Ross prepared, but the browser-control connector fails in the Windows sandbox with a runtime setup crash. Because of that, Codex still cannot perform click-by-click authenticated UI QA from the logged-in in-app tabs.

However, Codex performed a deeper backend/deployed-code investigation using:

- Lovable project connector metadata
- Deployed app HTML and JavaScript bundle
- Headless Chrome unauthenticated route snapshots
- Read-only Supabase anon REST checks
- Public workflow/config summary extraction
- GitHub connector checks

This audit is substantial but not complete. It should be treated as a strong pre-authenticated technical inventory, not final product QA.

## Current Access State

### Working

- Lovable connector can resolve the project by ID and confirms status `ready`.
- Deployed app is reachable at `https://clinic-pilot-x.lovable.app`.
- Deployed app bundle can be inspected.
- Supabase anon REST checks can be performed read-only.
- GitHub connector can inspect known repositories.

### Not Working Yet

- In-app browser automation cannot connect to the authenticated browser session because the browser plugin runtime crashes.
- Headless Chrome is not logged into the app and redirects protected routes to `/auth`.
- Codex cannot yet click-test left-navigation modules, forms, buttons, or authenticated workflows.

## Backend Architecture Finding

The app uses standalone Supabase for DB/auth/API:

- Supabase URL: `https://imuyfbvsombbpgdgkhrb.supabase.co`
- Supabase project ref: `imuyfbvsombbpgdgkhrb`
- Supabase auth calls in bundle: `getSession`, `getUser`, `onAuthStateChange`, `signInWithPassword`, `signOut`, `signUp`
- Supabase realtime channels in bundle:
  - `appointments-changes`
  - `assignment-rules-changes`
  - `conversations`
  - `leads-changes`
  - `messages`
  - `online-staff`

The UI also says some API credentials are stored in Lovable Cloud secrets. Current interpretation:

- Database/auth/realtime/storage: standalone Supabase.
- Some secrets/functions: likely Supabase Edge Functions and/or Lovable Cloud secrets.
- This must be confirmed directly by Lovable or by source/project settings.

## Edge Functions / Server Actions Found In Bundle

The deployed app calls these functions:

- `ai-assistant`
- `ai-suggestions`
- `auto-assign-leads`
- `calculate-lead-score`
- `create-payment-link`
- `send-email`
- `send-sms`
- `test-workflow-message`
- `workflow-appointment-confirmation`

External function URL also found:

- `https://imuyfbvsombbpgdgkhrb.supabase.co/functions/v1/resend-webhook`

Implication: Automation Center is not only static UI. Some real backend functions exist or are expected to exist. Testing must be done carefully because `send-email`, `send-sms`, `create-payment-link`, and workflow test actions may create real external effects.

## n8n Finding

No literal `n8n` references were found in the deployed frontend bundle.

Current evidence suggests the live Lovable app is wired around Supabase tables and Supabase/Lovable functions, not direct frontend calls to n8n webhooks.

Recommendation: do not reinstall n8n immediately. First verify what the existing Supabase Edge Functions do. If n8n is needed later, use it as an external orchestration layer for selected workflows, not as an assumed replacement for existing backend logic.

Official n8n docs note that Docker is recommended for self-hosting, but n8n recommends Cloud for users who do not want to manage infrastructure. Production self-hosting needs proper security, persistence, and scaling. Queue mode is the production scaling path, and SQLite is not recommended for queue mode.

Sources:

- https://docs.n8n.io/hosting/installation/docker/
- https://docs.n8n.io/hosting/scaling/queue-mode/
- https://docs.n8n.io/hosting/configuration/task-runners/

## GitHub State

The official one-word GitHub repo still does not exist through the connector:

- `aihustler2025/ClinicPilotX`: not found

Known old repo still exists:

- `aihustler2025/clinicpilot-x`
- Public
- Admin/push permissions available
- Treat as old/reference-only unless Ross explicitly redirects.

The official new project memory remains local on D drive until a new GitHub repo is created/connected.

## Deployed Navigation Inventory

From the deployed bundle, the app contains these routes/modules:

### CRM

- Dashboard: `/dashboard`
- Leads: `/leads`
- Patients: `/patients`
- Appointments: `/appointments`

### Communication

- Communication Hub: `/communication-hub`
- Video Consultation: `/video-consultation`

### Finance / Insights

- Payments & Billing: `/payments`
- Analytics & Reporting: `/analytics`

### Admin / Operations

- Staff Management: `/staff`
- Automation Center: `/automation`
- Auto-Assignment Rules: `/auto-assignment`
- Subscription: `/subscription`
- Settings: `/settings`
- Profile: `/profile`

## Supabase Table Inventory From App Bundle

Tables referenced by the deployed app:

- `addon_features`
- `appointments`
- `assignment_rules`
- `audit_logs`
- `automation_logs`
- `call_logs`
- `clinic_subscriptions`
- `conversation_notes`
- `conversations`
- `email_delivery_logs`
- `feature_entitlements`
- `internal_channel_members`
- `internal_channels`
- `internal_messages`
- `leads`
- `messages`
- `patients`
- `payment_items`
- `payments`
- `profiles`
- `quick_responses`
- `reminders`
- `scheduled_messages`
- `settings`
- `signatures`
- `subscription_plans`
- `user_roles`
- `workflow_executions`
- `workflows`

Tables with insert/update/delete/upsert behavior in the deployed app:

### Insert

- `appointments`
- `assignment_rules`
- `audit_logs`
- `conversation_notes`
- `internal_channel_members`
- `internal_channels`
- `internal_messages`
- `leads`
- `messages`
- `patients`
- `payment_items`
- `payments`
- `quick_responses`
- `scheduled_messages`
- `user_roles`

### Update

- `appointments`
- `assignment_rules`
- `conversation_notes`
- `conversations`
- `leads`
- `messages`
- `patients`
- `payments`
- `profiles`
- `quick_responses`
- `scheduled_messages`
- `settings`
- `workflows`

### Delete

- `assignment_rules`
- `conversations`
- `leads`
- `messages`
- `patients`
- `quick_responses`
- `scheduled_messages`
- `user_roles`

### Upsert

- `internal_channel_members`

## Supabase Storage Finding

The app references Supabase storage bucket:

- `signatures`

Used for uploading signature/logo assets in settings/profile-style configuration.

## Public Anon RLS / Security Findings

Read-only anon checks showed some public accessibility.

### Likely OK To Be Public If Intended

- `subscription_plans`: 3 rows
- `addon_features`: 6 rows

These may be acceptable if they power public pricing/plan UI.

### Needs Review

- `clinic_subscriptions`: 1 row visible
- `email_delivery_logs`: 42 rows visible
- `feature_entitlements`: 68 rows visible
- `quick_responses`: 13 rows visible
- `scheduled_messages`: 3 rows visible
- `workflow_executions`: 27 rows visible
- `workflows`: 19 rows visible

These tables may contain operational or business metadata. Confirm whether anon read access is intentional. If not, tighten RLS before client testing.

### RLS Bug

These tables return a Supabase 500 error:

- `internal_channel_members`
- `internal_channels`
- `internal_messages`

Error:

`infinite recursion detected in policy for relation "internal_channel_members"`

This likely breaks internal chat/group messaging and should be fixed before communication-module QA.

### Schema Mismatch / Missing Tables

The deployed app references these tables, but anon REST says they are not in the schema cache:

- `assignment_rules`
- `signatures`

Possible explanations:

- Migrations missing or not applied.
- Table names changed.
- RLS/schema exposure issues.
- Frontend was deployed ahead of backend migration.

Needs Lovable/Supabase verification.

## Automation Center Inventory

19 workflow rows are present in `workflows`.

### Enabled Workflows

- Lead Acknowledgment
- Smart Follow-up Sequence
- Follow-up After Visit
- Follow-Up Sequences
- No-Show Recovery
- Appointment Confirmation
- Appointment Reminders

### Disabled But Active/Configured Rows

- Lead Scoring & Assignment
- Multi-Channel Sync
- WhatsApp Business Integration
- AI Voice Agent - Inbound
- Facebook Messenger Bot
- Advanced Lead Nurture AI
- AI Voice Agent - Outbound
- Payment Receipt
- Payment Reminder Sequence
- Predictive Booking Suggestions
- Daily AI Briefing
- Weekly Performance Report

### Workflows With Config UI In Bundle

- Lead Acknowledgment
- Appointment Reminders
- Appointment Confirmation
- Payment Receipt
- Follow-Up Sequences
- No-Show Recovery
- Smart Follow-up Sequence
- Payment Reminder Sequence

### Workflows Without Config UI In Bundle

- Lead Scoring & Assignment
- Multi-Channel Sync
- WhatsApp Business Integration
- AI Voice Agent - Inbound
- Facebook Messenger Bot
- Advanced Lead Nurture AI
- AI Voice Agent - Outbound
- Follow-up After Visit
- Predictive Booking Suggestions
- Daily AI Briefing
- Weekly Performance Report

## Automation Safety Notes

Do not casually click test buttons in Automation Center until we create a controlled test plan. Deployed code contains test-send behavior through `test-workflow-message`, `send-email`, `send-sms`, and payment-link generation.

Safe QA sequence should be:

1. Confirm if Twilio/Resend/Stripe/VAPI credentials are real or sandbox.
2. Confirm test recipient numbers/emails.
3. Disable production sends or switch to sandbox mode.
4. Run one workflow at a time with recorded inputs/outputs.
5. Verify logs without exposing client data.

## Module-by-Module Current Understanding

### Dashboard

Backend-backed metrics from `leads`, `appointments`, and `call_logs`. Needs logged-in visual QA.

### Leads

Frontend appears to support lead creation, edit, delete, manual entry, source/status, lead scoring, auto-assignment, and conversion to patient. Needs logged-in CRUD/persistence QA.

### Patients

Frontend supports patient records and active-patient selection for appointment booking. Needs logged-in CRUD/persistence QA.

### Appointments

Frontend supports appointment creation/update, statuses, appointment confirmation workflow invocation, reminders, payments, and patient/lead linking. Needs logged-in safe test plan.

### Communication Hub

Frontend supports external messages, internal chat, conversations, messages, notes, quick responses, AI suggestions, and channel send behavior for SMS/WhatsApp/Messenger/Viber. Internal chat likely blocked by RLS recursion until fixed.

### Video Consultation

Route exists. Deployed bundle does not show evidence of advanced consult features such as consent, transcript, recording, AI notes, file/photo transfer, HIPAA/PIPEDA language, or sign-off. Treat as incomplete until authenticated UI proves otherwise.

### Payments & Billing

Frontend references payment records/items, Stripe customer ID, payment links, payment requests, payment receipt workflow, and payment reminder sequence. Must not test live payment actions until sandbox/credentials are confirmed.

### Analytics & Reporting

Frontend supports date ranges and CSV export. Needs logged-in UI/design QA. Ross wants a cleaner, more advanced visual experience.

### Staff Management

Frontend references profiles, user roles, admin/doctor/front_desk roles, staff search/filter, add staff, and user role management. Needs logged-in role QA.

### Auto-Assignment Rules

Route exists and app references `assignment_rules`, but table appears missing from schema cache. Likely incomplete or migration mismatch.

### Settings / Profile

Includes clinic configuration, notifications, integrations, profile, email logs, audit logs, test email, signature/logo upload, Google Calendar email, Stripe customer ID, and secure placeholders for Twilio/WhatsApp/Messenger/Viber credentials.

## Recommended Development Breakdown

### Phase 0 - Access and Source of Truth

- Create/connect official GitHub repo `ClinicPilotX`.
- Get Codex controllable admin access to the app.
- Confirm Lovable project's GitHub/source connection.
- Confirm Supabase organization/project ownership and billing.

### Phase 1 - Security and Backend Integrity

- Review and fix public anon RLS exposure.
- Fix internal chat RLS recursion.
- Resolve missing `assignment_rules` and `signatures` schema/table issues.
- Confirm Edge Function secrets and sandbox/live status for Stripe/Twilio/Resend/VAPI.

### Phase 2 - Core CRM QA

- Dashboard QA.
- Leads CRUD, scoring, assignment, conversion.
- Patients CRUD.
- Appointments CRUD/status/reminders/payment request with sandbox only.

### Phase 3 - Communication Hub QA

- External conversations/messages.
- Quick responses.
- AI suggestions.
- Internal channels/direct messages after RLS fix.
- Channel integrations only after sandbox confirmation.

### Phase 4 - Automation Center QA

- Inventory each workflow config.
- Determine real vs placeholder workflows.
- Test one safe workflow at a time.
- Decide whether Supabase Edge Functions are enough or whether n8n should be introduced.

### Phase 5 - Premium/Future Modules

- Video Consultation architecture and compliance.
- Analytics redesign and animation polish.
- Subscription/add-ons packaging.
- Marketing site later.

## n8n Recommendation

Do not reinstall n8n as the first move. Current deployed evidence points to Supabase Edge Functions and workflow tables as the existing automation system.

If n8n is needed later, recommended options:

- n8n Cloud for fastest setup and least server maintenance.
- Self-hosted Docker n8n only if Ross wants to manage hosting/security or if a dedicated VPS/container host is selected.
- Avoid resurrecting unknown old Hostinger state; build fresh and document credentials/domains/secrets properly.

## Immediate Blockers

1. Codex still needs controllable authenticated app access for UI QA.
2. Official GitHub repo `ClinicPilotX` still does not exist through connector.
3. Need Lovable/Supabase confirmation on backend architecture and secrets.
4. Need safe sandbox plan before testing messaging/payment/voice automation.
