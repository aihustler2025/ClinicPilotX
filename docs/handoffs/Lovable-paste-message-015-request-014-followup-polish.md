# Lovable Paste Message 015 - Request 014 Follow-Up Polish

Please read this QA follow-up and respond in Plan mode only. Do not build yet.

Codex completed live QA after Request 014. The core archive-vs-delete safety behavior passes, and Appointments list/calendar phone/time formatting is mostly fixed. A few polish issues remain.

## Verified Passes

- Zero-related patient delete path works:
  - `Delete patient?`
  - permanent warning
  - Cancel works
  - `Delete patient` removes the disposable patient

- Related-record patient path archives instead of deleting:
  - `Archive patient?`
  - shows `1 appointment` and `0 payments`
  - explains history preservation
  - Cancel works
  - `Archive patient` changes status to `archived`
  - no `Delete anyway` option exists
  - Active filter hides archived patient
  - Archived filter shows archived patient

- Appointment display polish works in key surfaces:
  - Appointments list shows friendly phone values such as `+1 (213) 555-0199` and `+1 (500) 555-0111`.
  - Appointments list and calendar drawer show friendly times such as `3:30 PM`, `2:45 PM`, `3:45 PM`.
  - Calendar drawer shows friendly phone values.

## Follow-Up Bugs / Polish

1. Booking modal selected-patient phone display

Repro:

- Patients > open patient profile > Book Appointment.
- Selected patient is prefilled.
- The disabled Phone field in the booking modal still displays raw E.164.

Observed:

`+12135550102`

Expected:

`+1 (213) 555-0102`

Please apply the shared display-phone formatter to disabled/pre-filled booking modal patient phone fields too. Keep storage/API payload E.164.

2. Appointment detail drawer patient type label

Repro:

- Create a TEST appointment from a Patient profile.
- Open it from Appointments Calendar View.

Observed:

The drawer labels the record as `Lead`.

Expected:

If the appointment is tied to a patient record, show `Patient`.

Please verify the appointment detail drawer determines lead vs patient from the correct relationship field.

3. Appointment detail drawer stray `0` text

Repro:

- Open appointment from Calendar View.
- Inspect the action area around `Confirm`, `Cancel`, `Send Reminder`, and `Add to Google Calendar`.

Observed:

Stray `0` text appears near the action buttons.

Expected:

No standalone numeric artifacts should render in the drawer.

Please remove/guard whatever falsey/count value is leaking into the JSX.

4. Existing entitlement/data-load flicker

The Patients page can still intermittently load as `No Plan` / `No patients found`. Routing through Dashboard restored `Professional` and real patient data during QA.

This may be a separate issue, but please include a read-only diagnosis in the plan:

- Is this subscription/entitlement state loading before auth/profile/org context is ready?
- Should CRM data loading wait until the correct org/subscription context is resolved?
- Do not hide real data behind transient `No Plan` if the session is valid.

## Safety

Do not touch:

- SMS/email/reminder sends
- Google Calendar writes
- payment links
- workflow activation
- secrets/integrations

Keep TEST behavior intact.

Please respond in Plan mode only with exact files/functions you would inspect or edit.
