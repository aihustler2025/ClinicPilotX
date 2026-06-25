# Lovable Paste Message 025 - Phase 1B.1a Patient Active Clinic Fix

Date: 2026-06-25

Codex ran QA after Phase 1B.1a was published. Do not proceed to Phase 1B.1b yet.

## Result

Phase 1B.1a is not fully passing.

Leads path appears to work from the UI.

Patients path is blocked by the new active-clinic guard.

## Browser QA Evidence

Environment:

- Published app: `https://clinic-pilot-x.lovable.app`
- Logged-in user visible in header: `TE`
- Dashboard loaded after hard reload.

Dashboard smoke:

- Dashboard rendered.
- Metrics rendered.
- Sidebar navigation rendered.
- No visible `No Plan`, Settings, auth, or missing-table error.

Leads smoke:

- Opened `/leads`.
- Page rendered with 17 active leads before the test.
- Opened Add Lead.
- Tried Lovable's suggested blank email + blank phone test first.
- Current validation rejected it with: `Either email or phone must be provided`.
- This means the QA plan should not say blank email/phone works unless form validation is intentionally changed.
- Retried with safe test email only:
  - Name: `QA TEST 1B1A LEAD 20260625-1255`
  - Email: `cpx.test+1b1a-lead-20260625-1255@example.com`
  - Phone: blank
  - Source: Manual
- Result: UI toast `Lead created`.
- Leads total increased from 17 to 18.
- New row appeared at top of Leads list.

Patients smoke:

- Opened `/patients`.
- Page rendered with existing patient cards.
- Opened Add Patient.
- Tried Lovable's suggested blank email + blank phone test first.
- Current validation rejected it with: `Either email or phone must be provided`.
- Retried with safe test email only:
  - Name: `QA TEST 1B1A PATIENT 20260625-1258`
  - Email: `cpx.test+1b1a-patient-20260625-1258@example.com`
  - Phone: blank
- Result: patient was not created.
- Toasts shown:
  - `No active clinic`
  - `No active clinic selected. Contact an admin.`
- Reloaded `/patients`, waited, reopened Add Patient, and retried:
  - Name: `QA TEST 1B1A PATIENT RETRY 20260625-1303`
  - Email: `cpx.test+1b1a-patient-retry-20260625-1303@example.com`
  - Phone: blank
- Result repeated:
  - `No active clinic`
  - `No active clinic selected. Contact an admin.`

Console:

- Only visible warning captured:
  - `Warning: Missing Description or aria-describedby={undefined} for {DialogContent}.`
- No visible fatal console error during the patient failure.

Backend verification:

- Codex could not verify the new Lead row's `clinic_id` through anon REST from the laptop because the relevant REST tables were not exposed/readable in that path.
- Lovable must provide SQL evidence after the fix.

## Required Fix

Please fix Phase 1B.1a only.

Do not build Phase 1B.1b or Phase 1B.1c.

Do not touch:

- Appointments
- Payments
- Messages
- Communication Hub
- Automation Center
- Settings
- useSubscription
- subscription logic
- RLS
- defaults
- NOT NULL constraints
- migrations
- edge functions
- workflows
- integrations

Investigate why `src/pages/Patients.tsx` sees `clinicId` as missing while the app session is valid and the Leads path can create a row.

Likely areas to inspect:

- `src/hooks/useActiveClinic.tsx`
- `src/components/layout/AppLayout.tsx`
- `src/pages/Patients.tsx`
- whether Patients is reading from the same provider/hook path as Leads
- whether Patients is guarding before active-clinic loading finishes
- whether `clinicId` is destructured from the hook/context incorrectly
- whether the provider is mounted around the Patients route in all app states

Expected behavior:

- If active clinic is still loading, Add Patient should not submit yet. Prefer disabling the submit button or showing a loading state instead of firing the `No active clinic` toast prematurely.
- Once active clinic resolves, Add Patient should create the row and stamp `clinic_id`.
- If active clinic truly cannot resolve, the guard toast is correct.

## QA After Fix

Use safe QA-only data. Do not use real contact details.

Because current form validation requires either email or phone, use safe `example.com` emails unless you intentionally change validation.

Run:

1. Hard reload `/dashboard`.
2. Verify Dashboard renders.
3. Open `/leads`.
4. Create:
   - Name: `QA TEST 1B1A LEAD FIX`
   - Email: `cpx.test+1b1a-lead-fix@example.com`
   - Phone: blank
5. Verify with SQL that the inserted lead has non-null `clinic_id` equal to the pilot clinic id.
6. Open `/patients`.
7. Create:
   - Name: `QA TEST 1B1A PATIENT FIX`
   - Email: `cpx.test+1b1a-patient-fix@example.com`
   - Phone: blank
8. Verify with SQL that the inserted patient has non-null `clinic_id` equal to the pilot clinic id.
9. Confirm no SMS, email, payment, webhook, calendar, WhatsApp, Messenger, Viber, Telegram, or voice actions fired.
10. Confirm no new rows were created in the QA window for:
    - `email_delivery_logs`
    - `workflow_executions`
    - `reminders`
    - `automation_logs`
    unless the row is clearly an internal non-send audit and explained.

## Deliverables Required From Lovable

After build, provide:

- exact files changed,
- root cause of Patients `No active clinic`,
- SQL evidence for the test Lead `clinic_id`,
- SQL evidence for the test Patient `clinic_id`,
- side-effect log counts for the QA window,
- confirmation no out-of-scope files or systems were touched.
