# Request 025 Phase 1B.1a Fix Retest

Date: 2026-06-25

Published app: `https://clinic-pilot-x.lovable.app`

## Scope Retested

Lovable reported the Phase 1B.1a active-clinic fix:

- moved `ClinicProvider` from `AppLayout` to wrap `Routes` in `src/App.tsx`,
- removed duplicate provider from `src/components/layout/AppLayout.tsx`,
- added active-clinic loading guards to `src/pages/Patients.tsx`,
- added matching loading guard to `src/components/leads/LeadFormDialog.tsx`,
- no RLS, migrations, defaults, edge functions, workflows, useSubscription, or other module changes.

## Result

Partial pass / follow-up required.

The original Patients `No active clinic` blocker is fixed in the UI.

However, the automation side-effect safety check failed: creating the QA lead produced new Automation Center workflow activity.

Do not proceed to Phase 1B.1b until the workflow safety behavior is explained and controlled.

## UI Retest

Dashboard:

- Hard reload completed.
- Dashboard rendered real metrics after loading.
- Dashboard showed the previous QA lead in Recent Leads.

Leads:

- `/leads` rendered.
- Before the retest, active leads showed `18`.
- Created safe QA lead:
  - Name: `QA TEST 1B1A LEAD FIX 20260625-1439`
  - Email: `cpx.test+1b1a-lead-fix-20260625-1439@example.com`
  - Phone: blank
  - Source: Manual
- Result:
  - UI showed `Lead created`.
  - Active lead count increased from `18` to `19`.
  - New row appeared at the top of the Leads table.

Patients:

- `/patients` rendered.
- Created safe QA patient:
  - Name: `QA TEST 1B1A PATIENT FIX 20260625-1441`
  - Email: `cpx.test+1b1a-patient-fix-20260625-1441@example.com`
  - Phone: blank
- Result:
  - UI showed `Success` and `Patient added successfully`.
  - New patient row appeared in the Patients list.
  - The previous `No active clinic selected. Contact an admin.` blocker did not appear.

## Safety Retest

Automation Center:

- Opened `/automation`.
- Workflows tab showed current plan `Professional` and `7 / 13 Active`.
- Opened Activity Logs.

Observed new/recent workflow activity:

- `Completed` - `Smart Follow-up Sequence` - `1 minute ago`
- `Failed` - `Lead Acknowledgment` - `1 minute ago`

This appears aligned with the new QA Lead creation window.

This means Codex cannot certify that the QA lead create path had no workflow side effects.

No send buttons, calendar buttons, payment buttons, workflow test buttons, or integration buttons were clicked by Codex.

## Backend Evidence Limitation

Codex still cannot independently verify authenticated SQL evidence from the browser session in this environment.

Lovable should provide SQL evidence for:

- the new Lead's `clinic_id`,
- the new Patient's `clinic_id`,
- workflow execution rows in the QA window,
- email delivery/reminder/automation logs in the QA window.

## Decision

Phase 1B.1a UI behavior is improved, but the overall QA is not fully clean because workflow safety is unresolved.

Next step: ask Lovable to investigate the workflow activity before any Phase 1B.1b build.
