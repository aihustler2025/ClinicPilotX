# Appointments Module Human QA Script

Status: draft for assistant/human tester confirmation.
Last updated: 2026-06-12.

## Purpose

This script lets a human tester repeat controlled Appointments module checks in the live ClinicPilotX dashboard.

Use only dummy data. Do not trigger live client communications.

## Safety Rules

- Keep TEST mode on for appointment creation if the toggle is available.
- Do not trigger SMS, email, reminder, payment request, phone call, or workflow-send actions.
- Use only dummy patients and dummy services.
- Screenshot every failed or confusing step.

## Test Data

Suggested appointment:

- Patient: `CPX TEST Lead June 11 (#PT00024)`
- Service: `CPX TEST Human Appointment QA`
- Date: a near-future date
- Time: `14:45`
- Type: `In-Person`
- Fee: `0`
- Notes: `Controlled human QA test appointment. TEST mode only. Do not send live communications.`

## Test Steps

### 1. Open Appointments

1. Log in to ClinicPilotX.
2. Open `Appointments`.
3. Confirm these are visible:
   - Refresh
   - Book Appointment
   - Date Range
   - Filters
   - Recently Added
   - Export
   - Summary cards
   - List View
   - Calendar View
   - Appointment list/table

Pass if the module loads with expected controls.

### 2. List View Check

1. Stay in `List View`.
2. Confirm rows show:
   - Patient
   - Service
   - Date and time
   - Type
   - Status
   - Actions
3. Find any `TEST` appointment row if available.

Pass if appointment rows are readable and status badges make sense.

### 3. Calendar View Check

1. Click `Calendar View`.
2. Confirm the calendar opens.
3. Look for the dummy TEST appointment date if it exists.
4. Return to `List View`.

Pass if switching views does not break or lose the appointment list.

### 4. Create Appointment From Appointments Module

1. Click `Book Appointment`.
2. Select `CPX TEST Lead June 11 (#PT00024)`.
3. Confirm patient contact fields prefill.
4. Enter the test appointment details.
5. Confirm TEST mode is on.
6. Click `Book Appointment`.
7. Confirm a success message appears.
8. Confirm the new appointment appears in the list with a `TEST` badge.

Pass if the booking saves, confirms success, and appears in the list.

Fail if the modal closes without success or the new appointment is missing.

### 5. Required Field Validation

1. Open `Book Appointment`.
2. Leave service and time blank.
3. Click `Book Appointment`.
4. Confirm the modal stays open.
5. Confirm visible validation errors appear.
6. Cancel.

Pass if invalid submission is blocked with clear messages.

### 6. Book Appointment From Patient Detail

1. Open `Patients`.
2. Open `CPX TEST Lead June 11`.
3. Click `Book Appointment`.
4. Confirm the Appointments booking modal opens.
5. Confirm the patient is prefilled.
6. Confirm TEST mode is on by default.
7. Cancel or create a dummy TEST booking if Ross asks for it.

Pass if the patient-detail flow opens the same booking experience.

### 7. Status Change Checks

Only use a dummy TEST appointment.

1. Open the row action menu if available.
2. Record available status actions.
3. Do not trigger sends, reminders, payments, or client communication.
4. If a safe status change is available, change status only after Ross approves.

Expected future QA:

- Pending to confirmed
- Confirmed to completed
- No-show handling
- Cancellation

These require workflow-safety confirmation before full testing.

### 8. Export

1. Click `Export`.
2. Record whether the app downloads immediately or opens a dialog.
3. If a file downloads, verify:
   - File type
   - Filename
   - Headers/columns
   - Whether TEST appointments are included
   - Whether current filters are respected

Expected improvement:

- Appointments export should eventually offer scope, filters, date range, columns, and filename preview, similar to Leads export.

## Findings Format

For each issue, record:

- Module: Appointments
- Step number
- Expected result
- Actual result
- Screenshot filename
- Severity: blocker, high, medium, low
- Notes
