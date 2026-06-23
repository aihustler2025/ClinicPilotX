# Dashboard / Analytics QA - 2026-06-24

## Scope

Codex performed a read-only authenticated QA pass against the published Lovable app:

`https://clinic-pilot-x.lovable.app`

Routes checked:

- `/dashboard`
- `/leads`
- `/patients`
- `/appointments`
- `/analytics`

No create, edit, delete, send, reminder, payment, calendar, workflow, webhook, or credential action was triggered.

## Result

Partial pass / Dashboard follow-up required.

The Analytics page appears to be using a June date range and its appointment count is plausibly aligned with the visible June TEST appointments. The Dashboard, however, is showing all-zero lead/patient/activity widgets while the supporting CRM modules contain real/test data.

## Dashboard Findings

Dashboard visible values during this pass:

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

This does not match the current CRM data exposed elsewhere in the app.

## Supporting CRM Evidence

### Leads

`/leads` showed:

- `Total Leads`: `17`
- `New Leads`: `9`
- `Contacted`: `5`
- `Qualified`: `3`
- `Unassigned`: `17`
- Visible source/service/status rows exist, including Manual, Website, Facebook, Instagram, and Referral examples.

Therefore Dashboard `Total Leads 0`, `Leads by Source No leads data available`, and `Recent Leads No leads yet` are not reliable.

### Patients

`/patients` showed populated patient cards, including:

- Amanda Lee
- Andrew Wilson
- Brandon Scott
- CPX TEST records
- many active patient records with formatted phone numbers, visits, and spend values.

Therefore Dashboard patient widgets should either display a clearly scoped value, such as "New patients today/month", or pull real counts consistently.

### Appointments

`/appointments` showed:

- `29 total appointments`
- `Today`: `0`
- `Pending`: `6`
- `Confirmed`: `13`
- `Completed`: `4`
- `Payment Pending`: `0`

Visible June 2026 TEST appointments exist on June 12, June 20, and June 21.

Dashboard `Today's Appointments 0` may be accurate for June 24 if there are no appointments today, but the Dashboard should make that scope clear. The all-zero Dashboard appointment/status summary is suspicious if the section is intended to summarize all appointments or current range.

## Analytics Findings

`/analytics` showed date range:

`Jun 01 - Jun 30`

Visible values:

- `Total Revenue`: `$0.00`
- `Appointments`: `3`
- `Lead Conversion`: `14.3%`
- `Active Staff`: `2`
- Lead Sources: `manual: 100%`
- Appointment Status: `pending: 100%`

Assessment:

- `Appointments 3` appears plausible because June contains the visible TEST appointments on June 12, June 20, and June 21.
- `pending: 100%` also appears plausible for those June TEST appointments.
- `Total Revenue $0.00` may be plausible if the June TEST appointments have no fees/revenue.
- Analytics still needs deeper validation later after the data-source logic is confirmed, but it is not the primary blocker found in this pass.

## Console Notes

The recurring console error remains:

`Error fetching settings: Object`

This did not block navigation, but it continues to point to a shared settings/context issue that should be diagnosed.

## Required Follow-Up

Create a Lovable plan-mode fix request for Dashboard data sources and metric scope.

Dashboard should not show empty-state copy when the underlying CRM modules have data. Each Dashboard card/section should either:

- pull real data from the same source as the relevant module, or
- clearly label itself as a scoped metric such as today, this week, this month, current org, current branch, or current filter.

## Safety

No live actions were triggered.

Do not connect or test real communication, reminder, payment, calendar, workflow, or webhook behavior as part of this Dashboard metrics fix.
