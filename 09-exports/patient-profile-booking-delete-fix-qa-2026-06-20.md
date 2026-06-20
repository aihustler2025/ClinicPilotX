# Patient Profile Booking / Delete Fix QA - 2026-06-20

## Scope

Codex retested the live published app after Lovable completed Request 013.

Focus:

- Patient profile `Book Appointment` route-state and time validation fix.
- TEST appointment no-send path.
- Patient profile Appointments tab.
- In-app patient delete confirmation cancel/confirm behavior.
- Side effects after deleting a patient with a related TEST appointment.

Safety boundary:

- Dummy data only.
- TEST appointment only.
- No live calls.
- No live messages.
- No payments.
- No workflow activation.

## Disposable Patient Used

- Patient: `CPX TEST Disposable Patient Delete QA 20260620`
- Email: `cpx.test+delete-qa-20260620@example.com`
- Patient ID: `#PT00028`

## Patient Profile Booking Fix

Result: pass for the previous blocker.

Verified:

- Patients page loaded with `Professional` state.
- Disposable patient was found.
- Patient profile side panel opened.
- Clicking `Book Appointment` navigated to `/appointments`.
- Booking modal opened automatically.
- Patient was prefilled as `CPX TEST Disposable Patient Delete QA 20260620 (#PT00028)`.
- TEST checkbox was checked before submit.
- TEST warning text was visible.
- Time input accepted and retained `15:30`.
- Submit succeeded.
- Appointment total increased from `27` to `28`.
- New appointment row appeared with `TEST` badge.

Created TEST appointment:

- Service: `CPX TEST Profile Booking Regression 20260620`
- Date/time: `Jun 20, 2026`, `3:30 PM`
- Type: `In-Person`
- Status: `Pending`
- TEST badge: visible

## Patient Profile Appointment Tab

Result: pass with display polish note.

Verified:

- Returning to Patients and opening the patient profile showed the new appointment in the Appointments tab.
- Appointment displayed service name, provider placeholder, consultation type, date/time, and status.

Polish note:

- Patient profile displayed time as `Jun 20, 2026 at 15:30:00`.
- Preferred display is staff-friendly, such as `Jun 20, 2026 at 3:30 PM` or `15:30`, not `15:30:00`.

## Delete Confirmation

Result: pass for cancel and confirm.

Verified:

- Row menu still exposes `View Details`, `Edit Patient`, and `Delete Patient`.
- Clicking `Delete Patient` opens an in-app dialog instead of native `window.confirm`.
- Dialog includes:
  - Title: `Delete patient?`
  - Patient name
  - Patient email
  - Patient ID `#PT00028`
  - `Cancel`
  - destructive `Delete patient`
- Cancel closes dialog and patient remains.
- Confirm shows success toast: `Patient deleted` / `CPX TEST Disposable Patient Delete QA 20260620 was removed.`
- Reloading Patients and searching the deleted patient showed `No patients found`.

## Issues Found After Delete

### Issue 1: Stale Patient Profile Panel Remains Open After Delete

Observed:

- After confirming delete, the filtered patient list changed to `No patients found`.
- However, the patient profile side panel stayed open and still showed the deleted patient's details and appointment.
- Reload cleared the stale panel.

Expected:

- After successful delete, close the patient detail/profile panel if it is showing the deleted patient.
- Clear selected patient state.

### Issue 2: Related Appointment Remains After Patient Delete

Observed:

- After patient delete, Appointments still showed:
  - Patient: `CPX TEST Disposable Patient Delete QA 20260620`
  - Phone: `+12135550199`
  - Service: `CPX TEST Profile Booking Regression 20260620`
  - TEST badge
- Appointment total remained `28`.

Open product/data question:

- Should deleting a patient be allowed when related appointments exist?
- If allowed, should related appointments be deleted, preserved as historical records, anonymized, or marked as patient-deleted?
- For safety, Codex recommends not silently orphaning related records.

### Issue 3: Appointments Row Phone Display Still Raw E.164

Observed:

- Appointment row for the test patient showed `+12135550199`.

Expected:

- Staff-facing appointment rows should use the same friendly display standard as Leads/Patients where possible: `+1 (213) 555-0199`.

## Current Assessment

Request 013 fixed the two original blockers:

- Patient-profile booking with `15:30` now saves.
- Native delete confirmation has been replaced with in-app dialog.

New follow-up is needed before treating patient delete behavior as complete:

- Decide and implement related-record behavior for patient deletion.
- Close stale profile panel after delete.
- Polish appointment display values for profile and list.

