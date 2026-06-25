# Request 026 Phase 1B.1a Safety Patch QA

Date: 2026-06-25

Published app: `https://clinic-pilot-x.lovable.app`

## Scope Tested

Lovable reported Phase 1B.1a safety patch was applied:

- `is_test` added to Leads and Patients.
- Existing QA rows backfilled.
- Lead Acknowledgment trigger short-circuits for QA/test leads.
- Smart Follow-up trigger short-circuits for QA/test leads.
- `workflow-lead-acknowledgment` edge function has request-body and DB re-check guards.
- `workflow-smart-follow-up` edge function has DB re-check guard.
- Lead and Patient create forms auto-flag QA rows.

## Result

Pass for live UI and Automation Center Activity Logs QA.

The prior workflow side-effect issue did not reproduce after the safety patch.

## Baseline Before QA

Automation Center -> Activity Logs was checked before creating new QA records.

Newest workflow rows before the test:

- `Completed` - `Smart Follow-up Sequence` - about 5 hours ago
- `Failed` - `Lead Acknowledgment` - about 5 hours ago

No fresh seconds/minutes-old workflow rows existed before the test.

## QA Lead Created

Created through the Leads UI:

- Name: `QA TEST SAFETY 20260625-A`
- Email: `cpx.test+safety-A@example.com`
- Phone: blank
- Source: Manual

Observed:

- UI showed `Lead created`.
- Active Leads count increased from `19` to `20`.
- New lead appeared at the top of the Leads table.

## QA Patient Created

Created through the Patients UI:

- Name: `QA TEST SAFETY PT 20260625-A`
- Email: `cpx.test+safety-pt-A@example.com`
- Phone: blank

Observed:

- UI showed `Success` and `Patient added successfully`.
- New patient appeared in the Patients list.

## Activity Logs After QA

After creating both QA records, Codex waited briefly and reopened Automation Center -> Activity Logs.

Newest workflow rows remained:

- `Completed` - `Smart Follow-up Sequence` - about 5 hours ago
- `Failed` - `Lead Acknowledgment` - about 5 hours ago

No new workflow rows appeared for:

- Lead Acknowledgment,
- Smart Follow-up Sequence,
- Appointment Confirmation,
- or any other visible workflow.

This confirms the prior visible workflow side-effect did not recur in the live UI/Activity Logs path.

## Smoke Test

Codex also smoke-rendered:

- Dashboard
- Leads
- Patients
- Appointments
- Payments
- Communication Hub
- Automation Center
- Settings

All checked routes rendered.

Console note:

- One existing dialog accessibility warning was observed:
  - `Warning: Missing Description or aria-describedby={undefined} for {DialogContent}.`
- No fatal console error was observed during the smoke pass.

## Backend Evidence Limitation

Codex could not independently run authenticated SQL from this browser environment.

Lovable's reported migration/SQL evidence is accepted for the DB-level `is_test` and `clinic_id` assertions, while Codex independently verified the user-facing create flows and visible Activity Logs behavior.

## Decision

Phase 1B.1a can be treated as passed for the tested scope.

Next recommended step: request a Plan-mode Phase 1B.1b proposal for active-clinic stamping on Appointments and Payments only, with no new live-send/payment/calendar behavior.
