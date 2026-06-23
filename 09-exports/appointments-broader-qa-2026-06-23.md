# Appointments Broader QA - 2026-06-23

## Scope

Codex performed a broader safe QA pass on the live authenticated Appointments module after Request 015 passed.

Live app:

`https://clinic-pilot-x.lovable.app/appointments`

This pass focused on baseline loading, list search, filters, Date Range, export, sort, calendar/list consistency, and read-only calendar drawer behavior.

## Result

Partial pass / follow-up required.

The core Appointments list and Calendar View are usable, and the Request 015 drawer polish still passes. Several Appointments-specific UX and data-quality issues remain before this module should be considered ready.

## Verified Passes

- Appointments recovered to `Professional` and `29 total appointments` after routing through Dashboard.
- List View loaded rows with patient, service, date/time, type, status, and actions columns.
- Search for `Archive Related` narrowed the list to one expected appointment: `CPX TEST Archive Related QA 20260621`.
- Keyboard clearing the search field restored `All Appointments (29)`.
- Filter dialog opens and includes Status, Consultation Type, Payment Status, Reset Filters, and Close.
- Consultation Type options are `All Types`, `In-Person`, and `Video`.
- Payment Status options are `All Statuses`, `Paid`, `Pending`, `Unpaid`, and `Not Required`.
- Sort options are `Recently Added`, `Date Ascending`, `Date Descending`, `Last 7 Days`, and `Last Month`.
- `Date Ascending` changed list ordering to earliest visible appointments first.
- Calendar View opens and shows June 2026 test appointments on June 12, June 20, and June 21.
- Calendar drawer for `CPX TEST Archive Related QA 20260621` still shows `Patient`, `3:45 PM`, `Pending`, `In-Person`, `+1 (213) 555-0102`, and the expected email/notes.

## Issues Found

### 1. `No Plan` / zero-data flicker still appears

Initial navigation to Appointments loaded `No Plan`, `0 total appointments`, disabled Refresh, and an empty table. Routing through Dashboard and back restored `Professional`, `29 total appointments`, and real appointment rows.

### 2. Appointment Status filter is missing `Pending`

The Status filter options were `All Statuses`, `Scheduled`, `Confirmed`, `Checked In`, `Checked Out`, `Cancelled`, and `No Show`.

But the Appointments summary and multiple visible rows use `Pending`.

Expected: staff should be able to filter `Pending` appointments, and status labels/options should match actual stored/displayed statuses.

### 3. Status vocabulary is inconsistent

Observed visible statuses include `Pending`, `Confirmed`, `Completed`, `Scheduled`, `Checked in`, and `Payment_pending`.

Concerns:

- `Payment_pending` is shown raw with underscore.
- `Checked in` casing does not match filter option `Checked In`.
- `Pending` appears in data but not in appointment-status filter.
- `Completed` appears in summary/list but not in appointment-status filter.

### 4. Date Range control appears broken or incomplete

Clicking `Date Range` changed the button to expanded state, but no visible date picker, dialog, or date-range controls appeared in the DOM.

### 5. Export lacks Appointments export dialog

Clicking `Export` showed a toast: `Appointments exported to CSV`.

No export dialog appeared, and the controlled browser did not capture a download event.

Expected: Appointments export should match Leads/Patients export UX with scope, date range, filters, column picker, row count preview, clear filename, and phone display/E.164 columns where relevant.

### 6. Some legacy phone values still cannot be normalized for display

Visible row example: `Test Patient` showed phone `+1 234567890`.

This may be invalid legacy data, but the UI should handle it deliberately with a consistent fallback and optional data-quality indicator.

## Gated / Not Tested

The following controls were intentionally not clicked because they may trigger live side effects or status workflow side effects:

- Appointment drawer `Confirm`
- Appointment drawer `Cancel`
- `Send Reminder`
- `Add to Google Calendar`
- Any payment, message, email, SMS, workflow, webhook, or calendar write action

Before testing these, Lovable should confirm which actions only mutate local DB state, which trigger edge functions or workflows, whether TEST appointments suppress sends/writes, and whether staff gets confirmation before any external side effect.

## Console Notes

The browser console showed the recurring known error:

`Error fetching settings: Object`

This did not block the read-only Appointments QA path, but it may be related to the broader settings/subscription/context loading issue.

## Recommended Next Step

Send Lovable Request 016 in Plan mode only for Appointments module polish:

- Fix entitlement/data-load flicker.
- Align status vocabulary and status filters.
- Repair Date Range.
- Upgrade Appointments export UX.
- Add explicit test-safe handling/confirmation around status actions and external side-effect buttons.
