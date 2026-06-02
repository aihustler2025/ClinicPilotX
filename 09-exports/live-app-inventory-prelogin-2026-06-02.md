# ClinicPilotX Live App Inventory - Pre-Login Pass

Date: 2026-06-02
URL: https://clinic-pilot-x.lovable.app
Lovable project ID: `8b4d9031-af8d-4faf-81d3-135c41ad73b7`
Lovable project URL: https://lovable.dev/projects/8b4d9031-af8d-4faf-81d3-135c41ad73b7
Lovable status from connector: `ready`, `agentFinished: true`

## Access Status

Codex does not yet have full authenticated access.

Every tested protected route redirects to the login page in a clean browser session. Routes tested by direct route render include:

- `/dashboard`
- `/leads`
- `/patients`
- `/appointments`
- `/communication-hub`
- `/video-consultation`
- `/payments`
- `/analytics`
- `/staff`

Observed login screen:

- Brand: ClinicPilot X
- Subtitle: AI-Powered CRM for Medical Clinics
- Login and Sign Up tabs
- Email field
- Password field
- Login button

Full click-by-click QA requires either a valid email/password or Ross logging Codex into the app in a browser session Codex can control.

## Backend Finding

The deployed app uses a standalone Supabase project as the primary backend:

- Supabase URL: `https://imuyfbvsombbpgdgkhrb.supabase.co`
- Supabase project ref: `imuyfbvsombbpgdgkhrb`
- Supabase Edge Function URL found: `https://imuyfbvsombbpgdgkhrb.supabase.co/functions/v1/resend-webhook`

The app also contains UI copy saying integration credentials are managed through Lovable Cloud secrets. Current interpretation:

- Database/auth/API layer: standalone Supabase project.
- Integration secrets: likely Lovable Cloud secrets or Lovable-managed server-side secret store.
- This must be confirmed by Lovable before build decisions.

## Navigation / Route Inventory From Deployed Bundle

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

### Auth / Utility

- Auth: `/auth`
- Recovery: `/recovery`

## Supabase Tables Referenced In App Bundle

The deployed app code references these tables:

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

## Read-Only Supabase Anon Inventory

Codex used the public anon key from the deployed bundle for read-only REST checks. No writes were performed. Sensitive row payloads were not dumped into this report.

| Table | Public anon result | Count / finding |
| --- | --- | --- |
| `addon_features` | Accessible | 6 rows |
| `appointments` | Accessible | 0 rows visible |
| `assignment_rules` | Error | 404, not found in schema cache |
| `audit_logs` | Accessible | 0 rows visible |
| `automation_logs` | Accessible | 0 rows visible |
| `call_logs` | Accessible | 0 rows visible |
| `clinic_subscriptions` | Accessible | 1 row |
| `conversation_notes` | Accessible | 0 rows visible |
| `conversations` | Accessible | 0 rows visible |
| `email_delivery_logs` | Accessible | 42 rows |
| `feature_entitlements` | Accessible | 68 rows |
| `internal_channel_members` | Error | 500, infinite recursion in RLS policy |
| `internal_channels` | Error | 500, infinite recursion in RLS policy |
| `internal_messages` | Error | 500, infinite recursion in RLS policy |
| `leads` | Accessible | 0 rows visible |
| `messages` | Accessible | 0 rows visible |
| `patients` | Accessible | 0 rows visible |
| `payment_items` | Accessible | 0 rows visible |
| `payments` | Accessible | 0 rows visible |
| `profiles` | Accessible | 0 rows visible |
| `quick_responses` | Accessible | 13 rows |
| `reminders` | Accessible | 0 rows visible |
| `scheduled_messages` | Accessible | 3 rows |
| `settings` | Accessible | 0 rows visible |
| `signatures` | Error | 404, not found in schema cache |
| `subscription_plans` | Accessible | 3 rows |
| `user_roles` | Accessible | 0 rows visible |
| `workflow_executions` | Accessible | 27 rows |
| `workflows` | Accessible | 19 rows |

## Security / Backend Risks Found Before Login

### High Priority: Public anon read access appears too broad

Several operational tables are readable with the anon role. This may be acceptable for public pricing tables such as `subscription_plans`, but it is not obviously acceptable for operational tables such as:

- `clinic_subscriptions`
- `email_delivery_logs`
- `scheduled_messages`
- `workflow_executions`
- `workflows`

Risk: these tables may reveal business, clinic, message, email, payment, or automation metadata to unauthenticated users.

### High Priority: Internal chat RLS recursion

The following tables return a 500 error:

- `internal_channel_members`
- `internal_channels`
- `internal_messages`

Error: `infinite recursion detected in policy for relation "internal_channel_members"`

Risk: internal chat may be broken for logged-in users, and the RLS policy is structurally unsafe.

### Medium Priority: App references tables not present in schema cache

The deployed bundle references:

- `assignment_rules`
- `signatures`

Both returned 404 from Supabase REST. This may mean migrations were not applied, table names changed, or these routes are partially built.

## Automation Center Inventory

The `workflows` table has 19 rows visible to anon. Safe summary fields showed these workflows:

| Workflow | Category | Trigger | Enabled | Required Plan | Execution Count | Last Executed |
| --- | --- | --- | --- | --- | --- | --- |
| Lead Scoring & Assignment | lead_intake | event | false | professional | 0 | null |
| Multi-Channel Sync | lead_intake | event | false | enterprise | 0 | null |
| Lead Acknowledgment | lead_intake | event | true | starter | null | 2025-11-14 |
| WhatsApp Business Integration | lead_intake | event | false | professional | 0 | null |
| AI Voice Agent - Inbound | lead_intake | event | false | enterprise | 0 | null |
| Facebook Messenger Bot | lead_intake | event | false | professional | 0 | null |
| Advanced Lead Nurture AI | nurture | event | false | enterprise | 0 | null |
| Smart Follow-up Sequence | nurture | schedule | true | professional | 0 | 2025-11-14 |
| AI Voice Agent - Outbound | nurture | manual | false | enterprise | 0 | null |
| Follow-up After Visit | nurture | schedule | true | starter | 0 | null |
| Follow-Up Sequences | patient_engagement | scheduled | true | professional | 0 | null |
| No-Show Recovery | patient-engagement | event | true | professional | 0 | null |
| Payment Receipt | payments | event | false | starter | 0 | null |
| Payment Reminder Sequence | payments | schedule | false | professional | 0 | null |
| Appointment Confirmation | reminders | event | true | starter | 21 | 2026-05-27 |
| Appointment Reminders | reminders | schedule | true | starter | 0 | null |
| Predictive Booking Suggestions | reminders | schedule | false | enterprise | 0 | null |
| Daily AI Briefing | reporting | schedule | false | enterprise | 0 | null |
| Weekly Performance Report | reporting | schedule | false | professional | 0 | null |

Interpretation: Automation Center is represented by real database rows and at least some execution logs. However, actual end-to-end automation behavior is not fully verified until authenticated UI access and controlled test records are available.

## Subscription / Pricing Inventory

Publicly visible plans:

- Starter: `$199/month`
- Professional: `$399/month`
- Enterprise: `$699/month`

Publicly visible add-ons:

- Ads Lead Capture (FB/IG): `$29/month`
- AI Voice Agent + Outbound Calls: `$39/month`
- Chatbot Knowledge Base: `$20/month`
- Multi-Clinic Dashboard: `$49/month`
- ReviewBoost Reputation Engine: `$29/month`
- WhatsApp Business Integration: `$19/month`

## Module Notes From Code Review

### Dashboard

Dashboard queries counts from `leads`, `appointments`, and `call_logs`, plus recent leads and upcoming appointments. It appears backend-backed, but live rendering is blocked by login.

### Leads

Code includes manual lead creation, edit/delete behavior, and conversion from lead to patient. Lead conversion inserts into `patients` and updates `leads` with `status: converted` and `patient_id`.

### Patients

Patient records are fetched from `patients`, especially active patients for appointment booking.

### Appointments

Appointments are fetched from `appointments`, sorted by `final_datetime`, and appear connected to patients, leads, payments, and reminders. There is likely a status workflow including scheduled, confirmed, checked-in, checked-out, cancelled, pending, and completed.

### Communication Hub

Code includes external and internal tabs:

- External Messages
- Internal Chat
- Group Channels
- Direct Messages

Backend tables include `conversations`, `messages`, `conversation_notes`, `internal_channels`, `internal_messages`, and `internal_channel_members`. Internal chat RLS recursion must be fixed before trusting this module.

### Video Consultation

Route exists: `/video-consultation`.

The deployed bundle does not contain obvious strings for:

- recording
- transcript
- AI notes
- consent
- HIPAA
- PIPEDA
- file upload specific to consultation

Interpretation: current video consultation is likely basic, placeholder, or incomplete compared with Ross's desired state-of-the-art consult room with consent, recording, transcript, AI summary, file/photo exchange, sign-off, and compliance controls.

### Payments & Billing

The app references `payments`, `payment_items`, `subscription_plans`, `clinic_subscriptions`, Stripe customer IDs, payment requests, and payment reminders. Real payment activation must not be done without Ross approval.

### Analytics & Reporting

Analytics page can export CSV and appears to calculate appointment/lead/conversion metrics. Needs authenticated visual QA and design improvement review.

### Staff Management

Staff page references profiles and roles including admin, doctor, and front_desk. Live behavior not verified.

### Settings / Integrations

Settings includes tabs for General, Notifications, Integrations, Profile, Email Logs, and Audit Log.

Integration UI includes Twilio, WhatsApp, Facebook Messenger, Viber, Google Calendar email, and Stripe customer ID. UI copy says API credentials are managed securely via Lovable Cloud secrets.

## Immediate QA Blocker

Need valid app login or authenticated session for `teambuzzooka@gmail.com` or another admin account. Without login, Codex cannot click through the left nav modules or test create/update/delete/persistence flows in the UI.

## Immediate Lovable Questions

1. Confirm whether this project uses standalone Supabase, Lovable Cloud, or both.
2. Confirm whether Supabase project `imuyfbvsombbpgdgkhrb` is the official backend.
3. Confirm whether public anon read access on operational tables is intentional.
4. Fix or explain the internal chat RLS recursion on `internal_channel_members`.
5. Explain missing schema-cache tables: `assignment_rules` and `signatures`.
6. Confirm which automations are real server-side workflows vs database-config placeholders.
7. Confirm whether email logs and workflow execution logs should be visible to unauthenticated users.
8. Confirm admin login account and role setup for Codex QA.
9. Confirm whether video consultation is placeholder/basic or already implemented somewhere not visible in current bundle.
