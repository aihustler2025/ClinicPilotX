# Lovable Request 013: Patient Profile Booking + Delete Confirmation Fixes

Mode requested from Lovable: Plan mode only. Do not build yet.

## Context

Codex performed live QA on the published ClinicPilotX app after Patients phone/export fixes.

QA report:

`09-exports/patient-profile-booking-delete-qa-2026-06-20.md`

Disposable patient created during QA:

- `CPX TEST Disposable Patient Delete QA 20260620`
- `cpx.test+delete-qa-20260620@example.com`
- `#PT00028`

Safety boundary:

- Dummy data only.
- TEST appointments only.
- No live SMS.
- No live email.
- No live calls.
- No payment links.
- No workflow activation.
- No secrets or integrations.

## Issue 1: Patient Profile Book Appointment Fails Time Validation

### Repro

1. Open Patients.
2. Create or open `CPX TEST Disposable Patient Delete QA 20260620`.
3. Open the patient profile panel.
4. Click `Book Appointment`.
5. Confirm `/appointments` opens with `Book New Appointment` modal.
6. Confirm selected patient is prefilled as `CPX TEST Disposable Patient Delete QA 20260620 (#PT00028)`.
7. Confirm TEST checkbox is on and no-send warning is visible.
8. Enter:
   - Service: `CPX TEST Profile Booking Regression 20260620`
   - Date: default `June 20th, 2026`
   - Time: `15:30`
   - Consultation type: `In-Person`
   - Fee: `0`
   - Notes: `Controlled QA booking from patient profile. TEST mode on. No live sends.`
9. Submit.

### Observed

- First submit showed `Invalid time format (HH:MM)`.
- On inspection, native `input[type="time"]` value was blank after the failed submit.
- Codex re-entered `15:30` and verified the native time input value was `15:30`.
- Second submit still showed `Invalid time format (HH:MM)`.
- Modal stayed open.
- Appointment count stayed `27`.
- Test appointment was not created.

### Expected

- A native time input value of `15:30` should pass `HH:MM` validation.
- Valid TEST appointment should save.
- Success toast should clearly say TEST / no sends.
- Appointment count should increase.
- Appointment list should show the new appointment with a TEST badge.
- Patient profile should show the new appointment in the Appointments tab.

### Files to inspect

Likely:

- `src/pages/Appointments.tsx`
- Appointment form validation schema / Zod schema
- Appointment time normalization/parsing helper if one exists
- Any route state handling for `prefillPatientId` and `isTest`

### Fix expectations

- Use one canonical internal time format, preferably `HH:mm`.
- Make `input[type="time"]` controlled value match validation expectations.
- Normalize before validation if needed.
- Preserve TEST mode from patient profile path.
- Do not invoke any live workflow/client-side function for TEST rows.

## Issue 2: Patient Delete Uses Native Browser Confirm, Blocking Reliable QA

### Repro

1. Open Patients.
2. Filter to disposable patient.
3. Open row action menu.
4. Click `Delete Patient`.

### Observed

- Row menu shows `View Details`, `Edit Patient`, and `Delete Patient`.
- Clicking `Delete Patient` triggers a native browser confirmation.
- The native confirmation freezes Codex browser automation before cancel/confirm can be safely verified.

### Expected

Replace native confirm with an in-app confirmation modal/dialog:

- Shows selected patient name/email/ID.
- Has clear `Cancel` and `Delete Patient` actions.
- Cancel closes modal and leaves the row intact.
- Confirm deletes only that selected patient.
- Shows success/failure toast.
- Does not affect unrelated records.

Use a normal app modal/component so QA can verify cancel and confirm paths safely.

### Files to inspect

Likely:

- `src/pages/Patients.tsx`
- Patient row/card action menu component if separate
- Patient delete handler / mutation
- Toast handling

## Issue 3: Reconfirmed Subscription/Data Flicker

During this pass, returning to Patients briefly showed:

- `No Plan`
- `No patients found`

Reload restored:

- `Professional`
- Full patient list

This is not the main fix request unless related to route reload/state handling, but please keep it on the known-issue list.

## Required Lovable Response

Please respond in Plan mode only with:

1. Your diagnosis for the time validation bug.
2. Exact files you will change.
3. Confirmation that TEST appointments remain no-send/no-workflow.
4. Your proposed in-app delete confirmation UX.
5. Manual QA checklist after build.

Do not build until Ross sends your plan back to Codex and Codex approves it.

