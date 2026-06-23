# Request 016 Appointments QA - 2026-06-23

## Scope

Ross approved and published Lovable's Request 016 Appointments polish build.

Lovable reported:

- `useSubscription` auth gate with `isReady`.
- Appointments fetch gated on session.
- Header/total skeleton loading behavior.
- Centralized appointment status map.
- Date Range popover with presets, Clear, and Apply.
- New `ExportAppointmentsDialog`.
- Display/E.164 phone export columns.
- Legacy phone fallback.
- Drawer Confirm/Cancel confirmation dialogs.
- Disabled Send Reminder and Add to Google Calendar buttons.

QA was performed against:

`https://clinic-pilot-x.lovable.app/appointments`

## Result

Pass for the tested Request 016 UI and safety scope, with one download-verification caveat.

## Verified

### Loading gate

- Direct navigation to `/appointments` first showed a neutral loading state.
- It did not show the previous `No Plan` / `0 total appointments` state.
- After load, the page showed real data:
  - `Professional`
  - `29 total appointments`
  - appointment rows

### Status filters and labels

- Appointment Status filter now includes:
  - Scheduled
  - Pending
  - Confirmed
  - Checked In
  - Checked Out
  - Completed
  - Cancelled
  - No Show
  - Payment Pending
  - Rescheduled
- `Payment Pending` filter returned the expected Amanda Lee row.
- `Payment Pending` displays as friendly text, not `Payment_pending`.
- Tested rows still display friendly phone/time formatting.

### Date Range

- Date Range popover exposes:
  - Today
  - This week
  - This month
  - Next 30 days
  - Clear
  - Apply
- The old "expanded but invisible" Date Range issue is resolved for the tested DOM state.

### Export dialog

- Clicking Export now opens `Export Appointments to CSV`.
- Dialog includes:
  - Scope radio buttons.
  - Current filters selected by default.
  - Column picker.
  - Phone Display and Phone E.164 columns.
  - Row count preview.
  - Download CSV button.

Caveat:

- The controlled browser did not capture a download event after clicking `Download CSV`.
- The dialog closed after the click. This may be a controlled-browser limitation, but CSV download should still be verified once in a normal Chrome download path.

### Legacy phone fallback

- `Test Patient` now displays `+1234567890 (unverified)`.
- Valid numbers still show friendly formatting, for example `+1 (213) 555-0102`.

### Calendar drawer and action safety

- Calendar drawer still shows:
  - `Patient`
  - `3:45 PM`
  - `Pending`
  - `+1 (213) 555-0102`
  - no stray `0`
- `Send Reminder` is disabled.
- `Add to Google Calendar` is disabled.
- Confirm opens a confirmation dialog that states the action only updates status and sends no SMS, email, or calendar invite.
- Cancel opens a confirmation dialog that states the action only updates status and sends no cancellation SMS, email, or refund.
- Codex dismissed both dialogs without accepting the status changes.

## Not Tested

- Accepted Confirm status update.
- Accepted Cancel status update.
- Real CSV file contents after download.
- Request Payment, because it may invoke send/payment behavior and was out of scope.

## Console Notes

The known recurring console error still appears:

`Error fetching settings: Object`

It did not block Request 016 Appointments QA, but it should remain on the backlog for the broader settings/context investigation.

## Next Recommendation

Treat Request 016 as passed for the tested Appointments polish scope.

Recommended next development step:

- Continue Appointments module completion with a controlled TEST-only status action QA plan, or
- Move to Dashboard / Analytics verification to confirm visible metrics reflect Leads, Patients, and Appointments test data correctly.

Do not test reminder, payment, calendar, SMS, email, or workflow sends without explicit safety approval.
