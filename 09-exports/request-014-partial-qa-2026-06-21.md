# Request 014 Partial QA - 2026-06-21

Scope: Lovable's patient delete related-record behavior and appointment display polish after Ross approved and published Request 014.

Lovable reported:

- Archive-vs-delete branching is in place.
- Stale patient panel closes on success.
- Time and phone display polish applied across PatientDetailPanel, Appointments, and AppointmentDetailsPanel.

## Verified In Live Chrome

URL tested:

`https://clinic-pilot-x.lovable.app/appointments`

Verified:

- Appointments list loads with 28 total appointments.
- The previously created test appointment `CPX TEST Disposable Patient Delete QA 20260620` now displays phone as `+1 (213) 555-0199`, not raw `+12135550199`.
- The older test appointment `CPX TEST Lead June 11`, previously shown in Ross's screenshot with raw `+15005550111`, now displays as `+1 (500) 555-0111`.
- Appointment times in the list display as friendly times such as `3:30 PM` and `2:45 PM`, not `15:30:00`.
- Other visible appointment rows also display U.S./Canada phones in friendly format when the number is parseable.

Safety:

- No `Confirm`, `Cancel`, `Send Reminder`, `Add to Google Calendar`, SMS, email, payment, or workflow action was triggered.
- No schema, secret, integration, or workflow setting was changed.

## Not Yet Verified

The following Request 014 items still need live click QA before the task can be closed:

- Delete/archive dialog title and copy for patients with zero related records.
- Hard delete path for patients with zero related appointments/payments.
- Archive-only path for patients with related appointments/payments.
- Absence of any `Delete anyway` escape hatch when related records exist.
- Stale patient profile panel closes after archive/delete success.
- Archived patient appears under Archived status filter and no longer appears as active.
- Appointment calendar/detail drawer phone/time display polish.

## Tooling Limitation During This Pass

The normal in-app browser control runtime failed before attaching to the logged-in tabs. A Windows/Chrome screenshot fallback was used to verify non-destructive visible UI state.

That fallback was reliable for navigation and visual inspection, but not reliable enough for destructive delete/archive confirmation clicks. Because patient delete/archive changes production-like CRM records, Codex stopped before performing destructive QA through unreliable coordinate clicks.

## Current QA Status

Result: partial pass.

Request 014 display polish passes for the Appointments list view. Request 014 archive/delete branching remains pending until Codex has reliable browser control for click-through destructive QA.

## Next Step

Re-run live browser QA with reliable browser control:

1. Create or identify a disposable CPX test patient with zero related records.
2. Verify hard delete dialog/cancel/confirm behavior.
3. Create or identify a disposable CPX test patient with one TEST appointment.
4. Verify archive-only dialog/cancel/confirm behavior.
5. Verify stale panel closes and Archived filter behavior.
6. Verify Appointments calendar/detail drawer phone and time formatting.
