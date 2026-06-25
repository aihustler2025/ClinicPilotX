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

Status: **partial pass / evidence follow-up required**.

The live app still loads normally after the Phase 1B migration. No visible CRM regression was found in this pass. Read-only API checks show `clinic_id` is selectable on 20 of the 23 expected tables. The remaining 3 are internal chat tables blocked by the already-known RLS recursion on `internal_channel_members`, so Codex could not verify those columns through anonymous REST.

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

## What Codex Could Not Verify

Because the provided DOCX was the prior SQL-review document, not Lovable's actual completion output, Codex could not independently confirm from Lovable's report:

- exact pre-migration row counts,
- exact post-migration row counts,
- zero NULL `clinic_id` counts for all 23 tables,
- all 23 indexes,
- all 23 foreign keys,
- linter baseline comparison,
- whether Lovable's transaction guard passed exactly as planned.

## Recommendation

Do not approve the next build phase yet.

Next Lovable request should ask for:

1. the actual Phase 1B migration completion report,
2. pre-check output,
3. post-check output,
4. confirmation row counts did not change,
5. confirmation all 23 tables have zero NULL `clinic_id`,
6. confirmation indexes and FKs exist,
7. linter baseline comparison,
8. acknowledgement that internal chat RLS recursion remains a pre-existing known issue,
9. Phase 1B.1 planning only for app-level active clinic context and safe `clinic_id` stamping/filtering.
