# Request 024 Phase 1B.1a Active Clinic QA

Date: 2026-06-25

Published app: `https://clinic-pilot-x.lovable.app`

## Scope Tested

Lovable reported Phase 1B.1a built:

- `src/hooks/useActiveClinic.tsx`
- `src/components/layout/AppLayout.tsx`
- `src/components/leads/LeadFormDialog.tsx`
- `src/pages/Patients.tsx`

Approved scope was limited to active clinic hook/provider plus `clinic_id` stamping for new Leads and Patients inserts.

## Result

Failed / follow-up required.

Leads creation works from the UI.

Patients creation is blocked by the new active clinic guard.

Do not proceed to Phase 1B.1b yet.

## QA Details

Dashboard smoke:

- Hard reload completed.
- Dashboard rendered with real metrics.
- Sidebar navigation rendered.
- No visible `No Plan`, Settings, auth, or missing-table error.

Leads:

- `/leads` rendered.
- Before the test, active leads showed `17`.
- Add Lead modal opened.
- Blank email + blank phone failed current form validation with `Either email or phone must be provided`.
- Retried with safe QA email:
  - Name: `QA TEST 1B1A LEAD 20260625-1255`
  - Email: `cpx.test+1b1a-lead-20260625-1255@example.com`
  - Phone: blank
  - Source: Manual
- UI showed `Lead created`.
- Leads total increased from `17` to `18`.
- New row appeared at the top of the Leads table.

Patients:

- `/patients` rendered with existing patient cards.
- Add Patient modal opened.
- Blank email + blank phone failed current form validation with `Either email or phone must be provided`.
- Retried with safe QA email:
  - Name: `QA TEST 1B1A PATIENT 20260625-1258`
  - Email: `cpx.test+1b1a-patient-20260625-1258@example.com`
  - Phone: blank
- UI blocked creation with:
  - `No active clinic`
  - `No active clinic selected. Contact an admin.`
- Reloaded `/patients`, waited, reopened Add Patient, and retried:
  - Name: `QA TEST 1B1A PATIENT RETRY 20260625-1303`
  - Email: `cpx.test+1b1a-patient-retry-20260625-1303@example.com`
  - Phone: blank
- Same `No active clinic` blocker repeated.

Console:

- No fatal console error captured.
- Only visible warning was an existing dialog accessibility warning:
  - `Warning: Missing Description or aria-describedby={undefined} for {DialogContent}.`

Backend check limitation:

- Codex could not verify the new test Lead `clinic_id` through anon REST from the laptop because the relevant REST tables were not exposed/readable in that path.
- Lovable must provide SQL evidence after the fix.

## Safety

No live SMS, email, payment, webhook, calendar, WhatsApp, Messenger, Viber, Telegram, or voice action was intentionally triggered.

Only safe `example.com` QA email addresses were used.

## Follow-Up

Created Lovable fix handoff:

`docs/handoffs/Lovable-paste-message-025-phase-1b1a-patient-active-clinic-fix.md`

Next step: send handoff 025 to Lovable as a custom response / Plan or Build fix request for Phase 1B.1a only.
