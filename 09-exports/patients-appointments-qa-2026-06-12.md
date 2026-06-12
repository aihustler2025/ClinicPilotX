# Patients and Appointments QA - 2026-06-12

Live app:

`https://clinic-pilot-x.lovable.app/patients`

## Scope

Focused QA pass after Leads export QA, using the existing dummy converted patient:

- `CPX TEST Lead June 11`
- `cpx.test+lead-20260611@example.com`
- Patient ID shown in UI: `#PT00024`

No live Call, Message, Video, payment, reminder, SMS, email, or workflow action was triggered.

## Verified

- Patients page loaded behind login with `Professional` visible.
- Converted dummy patient is visible in the Patients list.
- Clicking `CPX TEST Lead June 11` opens the patient detail panel.
- Detail panel shows:
  - Patient name and ID
  - Call / Message / Video / Book Appointment actions
  - Total Visits
  - Total Spent
  - Status
  - Contact Information
  - Medical Information
  - Appointments tab
  - Transactions tab
  - Notes
- Dummy patient notes include converted-lead context and original service request.

## Issues Found

### 1. No Visible Edit Patient Action

The patient detail panel does not expose an obvious `Edit Patient`, `Update`, or `Save` path. For CRM readiness, staff need a safe way to update patient name, contact info, status, notes, and medical/profile fields without editing database records manually.

### 2. Patient Detail Book Appointment Button Did Not Open Booking UI

Codex clicked `Book Appointment` from the dummy patient's detail panel. No booking dialog or visible state change appeared in this pass.

### 3. Appointment Booking Persistence Already Suspect

Prior QA from 2026-06-11 attempted to book `CPX TEST Appointment Audit` from the Appointments module. The form accepted details and closed, but no success message appeared, total count did not change, and the new appointment was not visible in the list.

## Recommendation

Create a Lovable fix plan before marking Patients or Appointments ready:

- Add or expose a clear patient edit flow.
- Ensure patient edits persist and are visible after refresh.
- Make `Book Appointment` from patient detail open the same safe booking flow as the Appointments module, prefilled with the selected patient.
- Fix or confirm appointment creation persistence and success/error feedback.
- Add visible error handling if appointment save fails.
- Do not trigger SMS/email/reminder/payment side effects during booking unless explicitly enabled and approved.
