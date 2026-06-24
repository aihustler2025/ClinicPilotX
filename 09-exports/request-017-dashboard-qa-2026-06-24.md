# Request 017 Dashboard QA - 2026-06-24

## Scope

Ross approved and published Lovable's Request 017 Dashboard metrics build.

Lovable reported:

- Dashboard queries now gate on the authenticated session.
- Dashboard cards now use real queries with truthful scope/labels.
- Fake sparklines and fabricated values were removed.
- Follow-ups now shows `Coming soon`.
- Revenue now shows MTD sum or `Not connected`.
- TEST rows are excluded where supported.
- Appointment badges use the shared Request 016 status helper.

QA was performed against:

`https://clinic-pilot-x.lovable.app/dashboard`

Cross-check routes:

- `/leads`
- `/appointments`
- `/patients`
- `/analytics`

## Result

Pass for the tested Request 017 Dashboard scope.

The old permanent all-zero Dashboard state is resolved.

## Verified Dashboard Values

After auth/session resolution, Dashboard displayed:

- `Total Leads`: `20`
- `Today's Appointments`: `0`
- `Conversion Rate`: `15%`
- `Total Calls`: `0`
- `Leads by Source`:
  - Facebook: `2`
  - Referral: `2`
  - Website: `3`
  - Instagram: `2`
  - Manual: `11`
- `New Patients (this week)`: `1`
- `Pending`: `3`
- `Completed Today`: `0`
- `Cancelled Today`: `0`
- `Follow-ups`: `Coming soon`
- `Revenue (MTD)`: `$0`
- `Recent Leads`: shows the latest real lead rows instead of empty-state copy.

## Cross-Checks

### Leads

`/leads` showed:

- Active pipeline leads: `17`
- New: `9`
- Contacted: `5`
- Qualified: `3`
- Unassigned: `17`

Dashboard `Total Leads 20` appears to be an all-time count that includes converted leads, while the Leads module headline is active pipeline count. This aligns with Dashboard's `15%` conversion rate if 3 of 20 leads are converted.

Dashboard source breakdown sums to 20:

`2 + 2 + 3 + 2 + 11 = 20`

### Appointments

`/appointments` showed:

- `29 total appointments`
- Today: `0`
- Pending: `6`
- Confirmed: `13`
- Completed: `4`
- Payment Pending: `0`

Dashboard showed `Pending 3`, which is plausible because Lovable intentionally excluded TEST rows from headline metrics. The Appointments page includes 3 visible TEST pending appointments, so `6 total pending - 3 TEST pending = 3 non-test pending`.

Dashboard `Today's Appointments 0` matches Appointments `Today 0`.

### Patients

`/patients` showed populated patient records.

Dashboard no longer shows fake patient-derived zeroes; it shows `New Patients (this week) 1`, which is clearly scoped.

### Analytics

`/analytics` still shows:

- Date range: `Jun 01 - Jun 30`
- Appointments: `3`
- Appointment Status: `pending: 100%`
- Lead Sources: `manual: 100%`
- Revenue: `$0.00`

This remains plausible for the visible June TEST appointment data and was not changed by Request 017.

## Loading Behavior

On hard navigation to `/dashboard`, the page first showed the Dashboard shell and section headings without values. After auth/data resolution, the real values appeared.

The old bad behavior did not recur:

- No permanent `Total Leads 0` state.
- No permanent `No leads data available` state.
- No permanent `No leads yet` state.

## Console Notes

The known console error still appears after visiting Appointments:

`Error fetching settings: Object`

Lovable correctly identified this as a separate follow-up ticket in the Request 017 plan. It did not block Dashboard QA.

## Not Tested

- Sign-out behavior.
- Internal query code or Supabase logs.
- Real revenue/payment aggregation with live payment records.
- Follow-up tracking, because the card is intentionally `Coming soon`.

## Safety

No live sends, calls, reminders, payments, calendar writes, workflows, webhooks, edits, deletes, or credential actions were triggered.

## Recommendation

Treat Request 017 as passed for the tested Dashboard QA scope.

Recommended next step:

- Continue Appointments completion with controlled TEST-only status-action QA for Confirm and Cancel.
- Keep Send Reminder, Google Calendar, Request Payment, SMS, email, workflows, and webhooks gated.
