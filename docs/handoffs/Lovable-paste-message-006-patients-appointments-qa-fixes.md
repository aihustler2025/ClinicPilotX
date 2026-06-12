# Lovable Plan Request 006 - Patients and Appointments QA Fixes

Please respond in Plan mode only. Do not build yet.

Codex continued controlled QA on the live published ClinicPilotX app after the Leads v2 fixes. This pass focused on Patients and Appointments using dummy data only.

## Safety Rules

- Do not activate live SMS, email, calling, video, payment, reminder, or automation sends.
- Do not connect or require live credentials.
- Do not create paid integrations.
- Keep all changes compatible with the existing Lovable/Supabase setup.
- Preserve existing patient/lead data.

## QA Evidence

Test patient:

- Name: `CPX TEST Lead June 11`
- Email: `cpx.test+lead-20260611@example.com`
- UI patient ID: `#PT00024`
- This patient was created through a controlled dummy lead-to-patient conversion.

Codex verified:

- Patients page loads behind login with `Professional` visible.
- The dummy converted patient appears in the Patients list.
- Clicking the dummy patient opens a detail panel.
- Detail panel shows patient ID, contact info, medical information, appointments, transactions, and notes.
- No live Call, Message, Video, payment, reminder, or send action was triggered.

## Issues To Address

### 1. Missing or Hidden Patient Edit Flow

The patient detail panel does not expose an obvious `Edit Patient`, `Update`, or `Save` action.

Expected:

- Staff can edit patient details from the patient detail panel or a clearly accessible edit dialog.
- Editable fields should include at minimum:
  - Full name
  - Email
  - Phone
  - Status
  - Notes
  - Basic profile/medical fields already represented in the current data model
- Save should persist to Supabase.
- UI should show success or clear error feedback.
- Updated values should remain after closing/reopening the patient and after refresh.

### 2. Patient Detail `Book Appointment` Did Not Open Booking UI

Codex clicked `Book Appointment` from the dummy patient's detail panel. No booking modal, route change, or visible state change appeared.

Expected:

- `Book Appointment` from a patient detail panel should open the appointment booking flow.
- Selected patient should be prefilled.
- Staff should not need to re-search for the same patient.
- If booking cannot open, show a clear error message.

### 3. Appointment Creation Persistence / Feedback Issue

Prior controlled QA attempted to book:

- Service: `CPX TEST Appointment Audit`
- Patient: `CPX TEST Lead June 11`
- Fee: `0`
- Dummy notes only

The booking form accepted the values and closed, but:

- No success message appeared.
- Appointment total did not change.
- New appointment row was not visible.

Expected:

- Appointment creation should either persist and show a clear success state, or fail visibly with a useful error.
- New appointment should appear in the list/calendar without requiring unclear manual recovery.
- Booking must not send SMS/email/reminders/payment requests unless those side effects are explicitly enabled and Ross approves.

## Requested Lovable Response

Please provide a plan that explains:

1. Current root cause or likely root cause for the missing patient edit path.
2. Current root cause or likely root cause for patient-detail `Book Appointment` not opening.
3. Current root cause or likely root cause for appointment creation closing without visible persistence.
4. Exact files/components/functions/tables you will touch.
5. How you will preserve no-live-send safety.
6. Manual QA checklist after build.

Do not build until Ross sends approval.
