# Dashboard / Analytics Human QA Script

Last updated: 2026-06-24

## Purpose

Use this script to manually verify that Dashboard and Analytics numbers match the real CRM modules after Lovable fixes Dashboard metrics.

Use only dummy/test data. Do not click live send, payment, reminder, calendar, webhook, workflow, or credential actions.

## Preparation

1. Log in to the ClinicPilotX dashboard.
2. Confirm the header plan chip eventually shows `Professional`.
3. If a page briefly shows `No Plan` or empty data, wait a few seconds and refresh once. Record whether the flicker happened.

## Dashboard Checks

1. Open `Dashboard`.
2. Record the visible values for:
   - Total Leads
   - Today's Appointments
   - Conversion Rate
   - Total Calls
   - Upcoming Appointments
   - Leads by Source
   - New Patients
   - Pending
   - Completed
   - Cancelled
   - Follow-ups
   - Revenue
   - Recent Leads
3. Note whether any card says `0` or `No data` while the related module has visible records.
4. Confirm each card label clearly explains the scope, such as today, this month, all time, or selected date range.

## Leads Cross-Check

1. Open `Leads`.
2. Record:
   - Total Leads
   - New Leads
   - Contacted
   - Qualified
   - Unassigned
3. Compare Dashboard `Total Leads`, `Recent Leads`, and `Leads by Source` against the Leads page.
4. Dashboard should not say there are no leads if the Leads page shows lead rows.

## Patients Cross-Check

1. Open `Patients`.
2. Confirm patient cards/rows are visible.
3. Record whether there are active, inactive, and archived patient examples.
4. Compare Dashboard patient/revenue widgets against the Patients page.
5. If Dashboard uses a date range, confirm the label clearly says so.

## Appointments Cross-Check

1. Open `Appointments`.
2. Record:
   - Total appointments
   - Today
   - Pending
   - Confirmed
   - Completed
   - Payment Pending
3. Compare Dashboard appointment widgets against Appointments.
4. If Dashboard shows today's appointments only, confirm the label says `Today` and does not imply all appointments.

## Analytics Checks

1. Open `Analytics & Reporting`.
2. Record the active date range.
3. Record:
   - Total Revenue
   - Appointments
   - Lead Conversion
   - Active Staff
   - Lead Sources
   - Appointment Status
4. Compare Analytics with CRM records in the same date range.
5. Confirm Dashboard and Analytics either agree or clearly explain why their scopes differ.

## Pass Criteria

Dashboard / Analytics can pass only when:

- Dashboard no longer shows misleading empty-state data while CRM modules have records.
- Each metric has a clear source and date scope.
- Analytics date range is visible and understandable.
- No live communications, payments, reminders, calendar writes, or workflows are triggered during QA.

## Fail Criteria

Fail the module if:

- Dashboard says `0` or `No data` while Leads/Patients/Appointments show records and no clear date-scope explains it.
- Dashboard labels imply all-time totals but only query today's data.
- Analytics and Dashboard show conflicting values without scope explanation.
- Any QA step triggers a live external action.
