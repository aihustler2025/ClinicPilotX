# Lovable Paste Message 017 - Dashboard / Analytics QA Fixes

Please read this Dashboard / Analytics QA follow-up and respond in Plan mode only. Do not build yet.

Codex completed a read-only QA pass after Request 016. Appointments polish passed, so the next module check was Dashboard / Analytics.

Detailed QA report:

`09-exports/dashboard-analytics-qa-2026-06-24.md`

## Main Finding

Dashboard is showing all-zero/empty-state metrics even though the related CRM modules contain data.

Dashboard currently shows:

- `Total Leads`: `0`
- `Today's Appointments`: `0`
- `Conversion Rate`: `0%`
- `Total Calls`: `0`
- `Upcoming Appointments`: `No upcoming appointments`
- `Leads by Source`: `No leads data available`
- `New Patients`: `0`
- `Pending`: `0`
- `Completed`: `0`
- `Cancelled`: `0`
- `Follow-ups`: `0`
- `Revenue`: `$0`
- `Recent Leads`: `No leads yet. Start capturing leads from your integrations!`

But the source modules show:

- Leads: `17` total, `9` new, `5` contacted, `3` qualified, `17` unassigned.
- Patients: many populated patient records.
- Appointments: `29 total appointments`, including `6` pending, `13` confirmed, `4` completed, and visible June TEST appointments.

## Expected Behavior

Dashboard should not display empty-state copy when the underlying CRM pages have data.

Please diagnose whether Dashboard is:

- reading the wrong tables,
- blocked by organization/profile/subscription context,
- using stale/mock placeholders,
- querying only today's data while labels imply all-time totals,
- using filters/date ranges that are not shown to the user,
- failing silently because of RLS, RPC, or settings/profile errors.

## Required Fix Direction

Please propose a plan to make Dashboard metrics trustworthy.

For each Dashboard card/section, define the source table/query and the intended scope:

- Total Leads
- Today's Appointments
- Conversion Rate
- Total Calls
- Upcoming Appointments
- Leads by Source
- New Patients
- Appointment status summary: Pending / Completed / Cancelled / Follow-ups
- Revenue
- Recent Leads

If a card is truly scoped to today, this week, this month, or another date range, label it clearly.

If a metric is not implemented yet, replace misleading zeroes with a deliberate placeholder such as `Coming soon`, `Not connected`, or `No data for selected range`, depending on the real state.

## Analytics Notes

Analytics currently shows range `Jun 01 - Jun 30`.

Observed Analytics values:

- Appointments: `3`
- Appointment Status: `pending: 100%`
- Lead Sources: `manual: 100%`
- Total Revenue: `$0.00`
- Active Staff: `2`

This may be plausible because June contains visible TEST appointments on June 12, June 20, and June 21. Do not treat Analytics as failed yet, but please include in your plan how Analytics and Dashboard share or intentionally differ in data-source/date-range logic.

## Known Console Error

The recurring console error still appears:

`Error fetching settings: Object`

Please include in the plan whether this settings fetch error is related to Dashboard empty metrics or the earlier CRM context/entitlement flicker.

## Safety Rules

Do not trigger live sends, reminders, payments, calendar writes, webhooks, workflows, or integrations.

Do not change secrets or credentials.

Do not remove TEST-mode protections.

Please respond in Plan mode only with exact files/components/functions/queries you would inspect or edit.
