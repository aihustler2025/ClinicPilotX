# Lovable Paste Message 016 - Appointments Broader QA Fixes

Please read this Appointments QA follow-up and respond in Plan mode only. Do not build yet.

Codex completed a broader safe QA pass on the live Appointments module after Request 015 passed. Core list/calendar browsing works, but several Appointments-specific issues remain.

Detailed QA report:

`09-exports/appointments-broader-qa-2026-06-23.md`

## Verified Working

- Appointments list can load with `29 total appointments` after valid `Professional` state is restored.
- Search works: searching `Archive Related` narrowed the table to the expected single TEST appointment.
- Keyboard clearing search restored `All Appointments (29)`.
- Filter dialog opens.
- Consultation Type options exist: `All Types`, `In-Person`, `Video`.
- Payment Status options exist: `All Statuses`, `Paid`, `Pending`, `Unpaid`, `Not Required`.
- Sort options exist and `Date Ascending` changes list order.
- Calendar View opens and shows June 2026 TEST appointments.
- Calendar drawer still shows friendly phone/time, `Patient` label, and no stray `0`.

## Bugs / Polish To Diagnose

### 1. Entitlement / data-load flicker

Initial Appointments navigation loaded `No Plan`, `0 total appointments`, disabled Refresh, and an empty table.

Routing through Dashboard and back restored `Professional`, `29 total appointments`, and real appointment data.

Please diagnose the shared route/context loading issue. CRM pages should not show `No Plan` / empty protected data while auth/org/subscription context is still resolving.

### 2. Appointment Status filter is missing real statuses

Status filter options currently include:

- `All Statuses`
- `Scheduled`
- `Confirmed`
- `Checked In`
- `Checked Out`
- `Cancelled`
- `No Show`

But visible rows and summary cards include:

- `Pending`
- `Confirmed`
- `Completed`
- `Scheduled`
- `Checked in`
- `Payment_pending`

Please align status values, labels, summary counts, filters, and displayed badges.

Expected:

- Include `Pending` in appointment status filter.
- Include `Completed` if completed appointments are displayed and counted.
- Avoid raw labels such as `Payment_pending`; display as `Payment Pending`.
- Normalize casing such as `Checked in` vs `Checked In`.
- Ensure filter values match stored enum/database values.

### 3. Date Range control appears broken

Clicking `Date Range` changed the button to expanded state, but no visible date picker, dialog, or date-range controls appeared.

Expected:

- A clear date-range picker/dialog.
- Start/end date selection or presets.
- Apply/Clear controls.
- Visible active date range.
- Works in both List View and Calendar View where appropriate.

### 4. Appointments Export should match Leads/Patients export quality

Clicking `Export` showed `Appointments exported to CSV`.

But no scoped export dialog appeared, and Codex's controlled browser did not capture a download event.

Please upgrade Appointments export to a dialog similar to Leads/Patients:

- Scope: all appointments, current filters, selected only if row selection exists.
- Date range.
- Status/type/payment filters.
- Column picker.
- Row count preview.
- Clear filename.
- Include friendly display phone and canonical E.164 phone columns where applicable.
- Confirm download works after export.

### 5. Legacy/invalid phone fallback

Visible row example:

- Patient: `Test Patient`
- Phone: `+1 234567890`

If this value is invalid legacy data, please handle it deliberately:

- Valid numbers: friendly display format.
- Invalid/unparseable values: consistent fallback plus optional data-quality indicator.
- Do not break Twilio/VAPI-ready E.164 handling for valid numbers.

### 6. Status actions / external side-effect safety

The drawer shows `Confirm`, `Cancel`, `Send Reminder`, and `Add to Google Calendar`.

Codex did not click these because they may trigger workflow, reminder, calendar, email, SMS, or status side effects.

Please include a Plan-mode safety diagnosis:

- Which actions only update local appointment status?
- Which actions call edge functions, Automation Center workflows, reminders, SMS/email, or Google Calendar?
- Do TEST appointments suppress every external send/write path?
- Should `Confirm` / `Cancel` show in-app confirmation dialogs?
- Should `Send Reminder` and `Add to Google Calendar` require explicit confirmation before external writes?

## Safety Rules

Do not activate live sends, reminders, payments, calendar writes, webhooks, or workflows.

Do not change secrets or credentials.

Do not remove TEST-mode protections.

Please respond in Plan mode only with exact files/functions/components/migrations you would inspect or edit.
