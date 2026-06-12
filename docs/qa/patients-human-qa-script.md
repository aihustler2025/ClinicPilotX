# Patients Module Human QA Script

Status: draft for assistant/human tester confirmation.
Last updated: 2026-06-12.

## Purpose

This script lets a human tester repeat controlled Patients module checks in the live ClinicPilotX dashboard.

Use only dummy data. Do not use real patient/client data.

## Safety Rules

- Do not click Call, Message, Video, payment, SMS, email, reminder, or live workflow-send buttons.
- Do not delete existing real-looking records unless Ross explicitly approves cleanup.
- Use clearly marked dummy records.
- Screenshot every failed or confusing step.

## Test Data

Suggested new patient:

- Full name: `CPX TEST Human Patient 01`
- Email: `cpx.test+human-patient-01@example.com`
- Phone: `5558878888` if the form has a country picker, or `+15558878888` if it only accepts full international format
- Notes: `Controlled human QA dummy patient. Do not send live communications.`

Existing converted patient for cross-checks:

- `CPX TEST Lead June 11`
- `cpx.test+lead-20260611@example.com`
- UI patient ID: `#PT00024`

## Test Steps

### 1. Open Patients

1. Log in to ClinicPilotX.
2. Open `Patients`.
3. Confirm these are visible:
   - Export
   - Add Patient
   - Status filter
   - Sort control
   - Patient list/cards or table
   - Existing patient names and contact details

Pass if the module loads and expected controls are visible.

### 2. Search / Locate A Patient

1. Search for `CPX TEST Lead June 11`, if search is available.
2. Confirm the matching patient appears.
3. Clear the search and confirm the full list returns.

Pass if search narrows and clears predictably.

### 3. View Patient Details

1. Open `CPX TEST Lead June 11`.
2. Confirm the detail view shows:
   - Patient name
   - Patient ID
   - Email
   - Phone
   - Status
   - Notes
   - Appointments section or tab
   - Transactions section or tab
   - Edit button
   - Book Appointment button
3. Do not click Call, Message, or Video.

Pass if the detail view matches the selected patient.

### 4. Edit Existing Patient

1. In the patient detail view, click `Edit`.
2. Confirm the edit form pre-fills current patient details.
3. Add this text to notes: `Human QA edit check. Do not send live communications.`
4. Save.
5. Close and reopen the same patient.
6. Confirm the edited note is still visible.
7. Refresh the page and confirm the edited note remains visible.

Pass if the edit persists after close/reopen and refresh.

### 5. Add New Patient

1. Click `Add Patient`.
2. Enter the suggested dummy patient data.
3. For phone:
   - If a country picker exists, choose United States and type digits only: `5558878888`.
   - The field should auto-format for display, such as `+1 (555) 887-8888`.
   - The tester should not need to type brackets, spaces, or dashes.
4. Save.
5. Confirm a success message appears.
6. Confirm the new patient appears in the Patients list.
7. Open the patient and confirm the details match.

Pass if creation succeeds and the patient is searchable/viewable.

Flag if the phone input requires manual punctuation or stores/displays inconsistent phone formats.

### 6. Patient Export

1. Click `Export`.
2. Record what happens:
   - Immediate download
   - Export dialog
   - No visible response
3. If a file downloads, open it and confirm:
   - File type
   - Filename
   - Headers/columns
   - Whether it exported all patients or current filters only
   - Whether dummy test patient appears when expected
4. Compare against the Leads export dialog.

Expected improvement:

- Patients export should open a dialog similar to Leads export.
- Tester should be able to choose all patients, current filters, selected patients, columns, and clear filename/scope.

### 7. Row / Action Menu

For a dummy patient only, check available actions:

- View Details
- Edit Patient
- Delete Patient

For `Delete Patient`:

1. Do not confirm deletion unless Ross explicitly approves.
2. If a confirmation dialog appears, screenshot it and cancel.

Pass if dangerous actions require confirmation and can be safely cancelled.

### 8. Book Appointment From Patient

1. Open a dummy patient detail view.
2. Click `Book Appointment`.
3. Confirm the Appointments booking modal opens.
4. Confirm the selected patient is prefilled.
5. Confirm TEST mode is on by default if available.
6. Cancel without saving, unless Ross asks the tester to create a test appointment.

Pass if the selected patient carries into the appointment booking flow.

## Findings Format

For each issue, record:

- Module: Patients
- Step number
- Expected result
- Actual result
- Screenshot filename
- Severity: blocker, high, medium, low
- Notes
