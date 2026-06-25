# Request 021 Phase 1B Migration QA - 2026-06-25

## Scope

Lovable was approved to run the reviewed Phase 1B migration:

- add nullable `clinic_id` to 23 existing tenant/data tables,
- backfill existing rows to the pilot clinic,
- add indexes and foreign keys,
- avoid NOT NULL, defaults, RLS rewrites, app code changes, Settings changes, integrations, workflows, sends, payments, and calendar actions.

Ross reported Lovable completed the work and published.

Important note: the attached DOCX labeled `CLINICPILOT LOVABLE TO CODEX 25.docx` extracted as the prior Request 024 exact SQL review document, not as the actual completion/post-check report. Codex therefore performed live UI QA and read-only API shape checks, but still needs Lovable to provide the actual migration evidence output.

## Result

Status: **pass for the tested Phase 1B migration scope**.

The live app still loads normally after the Phase 1B migration. No visible CRM regression was found in this pass. Lovable's actual completion evidence confirms all 23 expected tables received `clinic_id`, all existing rows were backfilled, row counts were unchanged, and the planned indexes/FKs exist.

## Live App Smoke QA

Verified after publish:

- Dashboard loads and shows real metrics:
  - `Total Leads 20`
  - `Conversion Rate 15%`
  - `Revenue (MTD) $0`
  - Recent Leads populated
- Leads loads and shows `17` active pipeline leads.
- Patients loads with populated patient records.
- Appointments loads and shows `29 total appointments`.
- Payments loads with invoices/payment rows.
- Communication Hub loads with External Messages and conversation list.
- Automation Center loads and shows `Professional` plus `7 / 13 Active`.
- Settings loads and still renders the Settings form.
- No `No Plan` state observed.
- No visible permission-denied/missing-table/settings errors observed in the checked routes.

No live send, workflow, payment, calendar, integration, SMS, email, WhatsApp, Messenger, Viber, Telegram, or voice action was triggered.

## Read-Only API Shape Check

Codex checked whether `clinic_id` is selectable through Supabase REST using the deployed app's anon key.

Tables returning HTTP 200 for `select=clinic_id&limit=1`:

- leads
- patients
- appointments
- payments
- payment_items
- messages
- conversations
- conversation_notes
- call_logs
- lead_activity
- reminders
- scheduled_messages
- scheduled_confirmations
- workflows
- workflow_executions
- automation_logs
- audit_logs
- email_delivery_logs
- services
- quick_responses

Tables that could not be verified through anon REST because of the known internal chat RLS recursion:

- internal_channels
- internal_messages
- internal_channel_members

Observed error:

`infinite recursion detected in policy for relation "internal_channel_members"`

This internal chat issue was previously observed before Phase 1B and remains a separate follow-up item.

## Lovable Completion Evidence Received

Ross later provided the correct Lovable completion response. Lovable reported:

- Exactly one clinic exists: `Dr. Colin Hong (Pilot)`.
- All 23 tenant tables have `clinic_id`.
- All 23 tenant tables have `0` NULL `clinic_id` rows.
- 23 `idx_<table>_clinic_id` indexes exist.
- 27 total FKs to `public.clinics` exist, including the 23 new tenant-table FKs plus 4 pre-existing clinic membership/subscription FKs.
- Linter returned 26 warnings, all pre-existing permissive-RLS findings unrelated to Phase 1B.
- No RLS policies, app code, edge functions, workflows, Settings rows, sends, payments, calendars, webhooks, or integrations were touched.

Row counts reported unchanged:

| Table | Before | After |
| --- | ---: | ---: |
| leads | 20 | 20 |
| patients | 28 | 28 |
| appointments | 29 | 29 |
| payments | 16 | 16 |
| payment_items | 0 | 0 |
| messages | 37 | 37 |
| conversations | 8 | 8 |
| conversation_notes | 0 | 0 |
| call_logs | 0 | 0 |
| lead_activity | 6 | 6 |
| reminders | 41 | 41 |
| scheduled_messages | 3 | 3 |
| scheduled_confirmations | 18 | 18 |
| workflows | 19 | 19 |
| workflow_executions | 58 | 58 |
| automation_logs | 28 | 28 |
| audit_logs | 5 | 5 |
| email_delivery_logs | 45 | 45 |
| services | 10 | 10 |
| quick_responses | 13 | 13 |
| internal_channels | 3 | 3 |
| internal_messages | 0 | 0 |
| internal_channel_members | 3 | 3 |

## Codex Verification Limitations

Read-only REST checks confirmed `clinic_id` is selectable on 20 of 23 tables. The 3 internal chat tables could not be checked through anonymous REST because of the known pre-existing RLS recursion on `internal_channel_members`. Lovable's completion evidence states those 3 tables did receive `clinic_id` and retained unchanged row counts.

## Recommendation

Phase 1B can be treated as complete for the approved additive migration scope.

Next step: ask Lovable for **Phase 1B.1 planning only** for app-level active clinic context, safe `clinic_id` stamping on new inserts, and read filtering. Do not approve app-code build until Lovable provides exact files, sequencing, QA, and rollback.
