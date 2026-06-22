# Request 015 Live QA - 2026-06-22

## Scope

Lovable reported three Request 015 polish fixes after Ross approved and published:

- Booking modal phone now formats when prefilled.
- Appointment drawer badge derives `Patient` / `Lead` from `apt.patient_id`.
- Stray `0` guards use `(apt.consultation_fee ?? 0) > 0`.

QA was performed against the live authenticated app:

`https://clinic-pilot-x.lovable.app`

## Result

Pass for the tested Request 015 scope.

## Verified

- Opened Patients and confirmed existing test patient phone display still uses friendly formatting.
- Opened active patient `CPX TEST Patient Valid Phone Final 20260619`.
- Clicked `Book Appointment` from the patient profile.
- Verified the booking modal prefilled the patient name, email, and disabled phone field.
- Verified the disabled booking phone field displays `+1 (213) 555-0199`, not raw E.164.
- Opened Appointments list.
- Verified `CPX TEST Archive Related QA 20260621` list row still displays `+1 (213) 555-0102` and `3:45 PM`.
- Switched to Calendar View and opened the June 21, 2026 appointment drawer.
- Verified the drawer badge now shows `Patient`, not `Lead`.
- Verified the drawer still shows friendly phone `+1 (213) 555-0102`.
- Verified the drawer still shows friendly time `3:45 PM`.
- Verified the stray standalone `0` no longer appears before the action buttons.

## Safety

No live side-effect actions were triggered.

Codex did not click:

- `Confirm`
- `Cancel`
- `Send Reminder`
- `Add to Google Calendar`
- Any call, message, email, SMS, payment, workflow, or webhook action.

## Console Notes

Browser console still showed repeated `Error fetching settings: Object` messages from the deployed bundle. This was already known from earlier QA and did not block the Request 015 flows tested here.

## Remaining Appointments Work

Request 015 closes the immediate polish issues from Request 014. The next recommended task is broader Appointments module QA:

- Status action behavior for TEST appointments only.
- Safe rules for `Confirm` and `Cancel`.
- Explicit no-send behavior around reminders and calendar actions.
- Appointment filters, export, date range, search, and calendar/list consistency.
- Dashboard and Analytics impact from appointment changes.
