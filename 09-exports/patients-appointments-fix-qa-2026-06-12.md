# Patients and Appointments Fix QA - 2026-06-12

Live app:

`https://clinic-pilot-x.lovable.app`

## Scope

Focused QA after Ross approved, Lovable built, and Ross published the Patients/Appointments fix.

Dummy patient:

- `CPX TEST Lead June 11`
- `cpx.test+lead-20260611@example.com`
- UI patient ID: `#PT00024`

Safety boundary:

- No live Call, Message, Video, payment, reminder, SMS, email, or workflow action was triggered.
- Appointment was created with the new TEST toggle on.
- The test booking was treated as dummy QA data only.

## Lovable Build Summary Under Test

Lovable reported:

- Added `is_test` to appointments, payments, and scheduled confirmations.
- Guarded appointment/payment/follow-up/no-show/receipt triggers to early-return on test rows.
- Updated scheduled confirmation processing to filter out test rows.
- Added patient detail `Edit` and wired `Book Appointment`.
- Appointments now consumes patient prefill state, persists `patient_id` and `is_test`, removes the client-side `workflow-appointment-confirmation` invoke, and shows a TEST toggle and TEST badge.

## Verified

- Patients page loaded with `Professional` visible.
- `CPX TEST Lead June 11` opened from the Patients list.
- Patient detail panel now shows an `Edit` button.
- Editing patient notes saved successfully.
- Reopening the patient detail panel showed the edited note:
  - `QA edit retest 2026-06-12: patient edit persistence check. Do not send real communications.`
- Patient detail panel now shows a working `Book Appointment` button.
- Clicking `Book Appointment` navigated to `/appointments` and opened `Book New Appointment`.
- Booking modal prefilled the selected patient:
  - `CPX TEST Lead June 11 (#PT00024)`
- TEST checkbox was checked by default.
- TEST warning text was visible and explicitly stated no SMS, email, payment, or workflow sends should fire.
- Submitting the booking with blank required fields kept the modal open and showed validation messages for service and time.
- Valid test appointment submission succeeded.
- Success toast appeared:
  - `Appointment created for CPX TEST Lead June 11 on Jun 12, 2026 at 14:45 (TEST - no sends)`
- Appointments total increased to 27.
- New appointment row appeared in the appointment list:
  - Patient: `CPX TEST Lead June 11`
  - Service: `CPX TEST Appointment Audit 2026-06-12`
  - Date/time: `Jun 12, 2026`, `2:45 PM`
  - Type: `In-Person`
  - Status: `Pending`
  - Badge: `TEST`
- Returning to Patients and opening the dummy patient showed the appointment details from the patient side.

## Notes

The native time field did not accept a direct automation `fill()` call in the first attempt, but it accepted normal human-style typing of `14:45`. This appears to be an automation/tooling quirk rather than a user-facing blocker.

Browser console/log verification of Supabase triggers and edge-function non-execution was not available from the UI. The UI evidence is strong because:

- TEST toggle was checked.
- Warning copy explicitly promised no sends.
- Success toast included `TEST - no sends`.
- Appointment row included the TEST badge.

Final confirmation of trigger behavior should still be done by Lovable/Supabase code review or database/edge logs before any real client pilot with active automations.

## Result

Pass for the tested Patients/Appointments fix path.

Patients and Appointments remain `Partially verified` overall until the broader module QA is completed, including status changes, calendar behavior, reminders, payments, exports, dashboard/analytics updates, and non-test production booking behavior under approved sandbox conditions.
