# Lovable Paste Message 026 - Phase 1B.1a Workflow Safety Follow-Up

Date: 2026-06-25

Codex retested after the Phase 1B.1a Patient active-clinic fix was published.

Please respond in Plan mode first. Do not build yet.

## Result

The original Patient `No active clinic` blocker is fixed in the UI.

However, the workflow side-effect safety check failed.

Do not proceed to Phase 1B.1b yet.

## What Passed

Dashboard hard reload:

- Dashboard rendered real metrics after loading.

Lead create:

- Created:
  - Name: `QA TEST 1B1A LEAD FIX 20260625-1439`
  - Email: `cpx.test+1b1a-lead-fix-20260625-1439@example.com`
  - Phone: blank
  - Source: Manual
- UI showed `Lead created`.
- Active lead count increased from `18` to `19`.
- New lead appeared at top of Leads table.

Patient create:

- Created:
  - Name: `QA TEST 1B1A PATIENT FIX 20260625-1441`
  - Email: `cpx.test+1b1a-patient-fix-20260625-1441@example.com`
  - Phone: blank
- UI showed `Success` and `Patient added successfully`.
- New patient appeared in Patients list.
- The prior `No active clinic selected. Contact an admin.` blocker did not appear.

## Safety Issue

After the QA lead creation, Codex opened Automation Center -> Activity Logs.

Recent Activity Logs showed:

- `Completed` - `Smart Follow-up Sequence` - `1 minute ago`
- `Failed` - `Lead Acknowledgment` - `1 minute ago`

This appears aligned with the QA lead creation window.

Codex did not click:

- Send Test SMS,
- Send Test Email,
- Save Configuration,
- workflow toggles,
- payment buttons,
- calendar buttons,
- reminder buttons,
- webhook/integration actions.

The workflow activity appears automatic.

## Required Investigation

Please investigate before any Phase 1B.1b work:

1. Did creating `QA TEST 1B1A LEAD FIX 20260625-1439` trigger `Smart Follow-up Sequence` and `Lead Acknowledgment`?
2. Did either workflow attempt to send an email, SMS, webhook, or other external action?
3. Did the completed `Smart Follow-up Sequence` create scheduled messages/reminders/follow-up rows?
4. Did the failed `Lead Acknowledgment` create any email delivery log, reminder, or failed send attempt?
5. Is this expected current product behavior, or should QA/test leads be excluded from live/send-capable workflows?

## SQL Evidence Needed

Please provide read-only SQL evidence for:

- `clinic_id` on lead `QA TEST 1B1A LEAD FIX 20260625-1439`,
- `clinic_id` on patient `QA TEST 1B1A PATIENT FIX 20260625-1441`,
- workflow execution rows created during this QA window,
- `email_delivery_logs` rows created during this QA window,
- `reminders` rows created during this QA window,
- `automation_logs` rows created during this QA window,
- any `scheduled_messages` rows created during this QA window.

## Product Safety Direction

ClinicPilotX needs a safe test-data strategy before we keep creating lead records during QA.

Please propose the smallest safe plan. Options may include:

- add an `is_test` flag for Leads and Patients and ensure send-capable workflows skip test rows,
- make workflows ignore obvious QA records such as `email LIKE 'cpx.test+%@example.com'` and names starting `QA TEST`,
- add a global QA/sandbox mode for this pilot workspace,
- or another safer pattern you recommend.

Important: do not implement a broad automation rewrite yet. First explain the current behavior and propose the smallest safe fix.

## Out Of Scope

Do not build Phase 1B.1b yet.

Do not touch Appointments, Payments, Messages, Communication Hub, Settings, useSubscription, subscription logic, RLS, defaults, NOT NULL constraints, migrations, edge functions, workflows, or integrations unless your plan explains exactly why a tiny workflow-safety guard is required and Codex approves it.
