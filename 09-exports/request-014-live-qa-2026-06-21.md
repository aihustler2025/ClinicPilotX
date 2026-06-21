# Request 014 Live QA - 2026-06-21

Scope: live QA after Lovable's Request 014 publish for patient archive-vs-delete behavior and appointment phone/time display polish.

URL tested:

`https://clinic-pilot-x.lovable.app`

Browser path:

- In-app browser control restored using the current installed browser plugin path.
- QA was performed directly by Codex against the authenticated live app.

## Appointments Display Polish

Verified in Appointments List View:

- `CPX TEST Disposable Patient Delete QA 20260620` displays phone as `+1 (213) 555-0199`, not raw `+12135550199`.
- `CPX TEST Lead June 11` displays phone as `+1 (500) 555-0111`, not raw `+15005550111`.
- Appointment times display as `3:30 PM`, `2:45 PM`, and `3:45 PM`, not trailing-second values like `15:30:00`.

Verified in Calendar View / detail drawer:

- June 12 drawer for `CPX TEST Lead June 11` shows time `2:45 PM` and phone `+1 (500) 555-0111`.
- June 21 drawer for `CPX TEST Archive Related QA 20260621` shows time `3:45 PM` and phone `+1 (213) 555-0102`.

Safety:

- Did not click appointment `Confirm`, `Cancel`, `Send Reminder`, or `Add to Google Calendar`.
- No SMS, email, workflow, payment, reminder, or calendar action was triggered.

## Zero-Related Patient Delete QA

Created disposable patient:

- `CPX TEST Zero Related Delete QA 20260621`
- `cpx.test+zero-delete-20260621@example.com`
- Phone displayed as `+1 (213) 555-0101`
- Profile showed `No appointments found`.

Verified delete dialog:

- Title: `Delete patient?`
- Copy: `This action is permanent and cannot be undone.`
- Shows patient name, email, and ID.
- Buttons: `Cancel`, `Delete patient`.

Verified:

- Cancel closes dialog and leaves patient visible.
- Confirm `Delete patient` removes the patient.
- Searching the exact patient name afterward shows `No patients found`.

Result: pass.

## Related-Record Archive QA

Created disposable patient:

- `CPX TEST Archive Related QA 20260621`
- `cpx.test+archive-related-20260621@example.com`
- Phone displayed as `+1 (213) 555-0102`

Created related TEST appointment:

- Service: `CPX TEST Archive Appointment 20260621`
- Date: June 21, 2026
- Time: `15:45`
- TEST checkbox was checked.
- Booking succeeded.
- Appointments total increased from 28 to 29.
- Row shows TEST badge.

Observed booking-modal polish issue:

- The disabled phone field in the booking modal still showed raw `+12135550102` instead of friendly `+1 (213) 555-0102`.

Verified archive dialog:

- Title: `Archive patient?`
- Copy states the patient has `1 appointment` and `0 payments`.
- Copy explains the patient will be archived instead of deleted to preserve clinic history.
- Shows patient name, email, and ID.
- Buttons: `Cancel`, `Archive patient`.
- No `Delete anyway` option is present.

Verified:

- Cancel closes dialog and leaves patient active.
- Confirm `Archive patient` closes dialog and changes patient status to `archived`.
- Active filter plus exact search hides the archived patient and shows `No patients found`.
- Archived filter plus exact search shows the patient with `archived` status.
- Related TEST appointment remains visible in Appointments, which is expected for history preservation.

Result: pass for archive branching.

## Stale Panel Follow-Up

Created and cleaned up:

- `CPX TEST Stale Panel Delete QA 20260621`

Finding:

- When a patient profile side panel is open, the row action menu is covered/blocked by the panel in the current viewport and does not open through the normal visible row action path.
- Because the delete/archive action is not reachable while the profile panel is open in this UI state, the original stale-panel bug path could not be reproduced directly.
- After closing the panel, zero-related delete still works and the cleanup patient was removed.

Result: stale-panel closure not directly reproducible in current UI path; no stale panel was observed during successful delete/archive flows performed from the patient list.

## New Follow-Up Issues

1. Booking modal disabled phone field still displays raw E.164 for the selected patient:
   - Observed: `+12135550102`
   - Expected: `+1 (213) 555-0102`

2. Appointment calendar/detail drawer labeled the new patient-created archived appointment as `Lead` instead of `Patient`.

3. Appointment calendar/detail drawer showed stray `0` text nodes near action buttons around `Send Reminder` / `Add to Google Calendar`.

4. Patients page can still intermittently load as `No Plan` / `No patients found`; routing through Dashboard restored `Professional` and real patient data during this pass. This is pre-existing but still important.

## Current QA Status

Request 014 core behavior: pass.

Remaining polish should be handled in a follow-up request, not treated as a blocker to the archive-vs-delete safety fix.
