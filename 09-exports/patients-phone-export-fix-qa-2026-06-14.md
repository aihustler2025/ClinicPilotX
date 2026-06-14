# Patients Phone / Export Fix QA

Date: 2026-06-14

Live app tested:

`https://clinic-pilot-x.lovable.app/patients`

## Result

Partial pass.

Lovable's corrected Patients phone/export implementation is now visible on the active ClinicPilotX dashboard, and the previous publish/workstream mismatch is resolved for this module. The main shared-phone-input and export-dialog work landed, but there are still polish/QA issues before Patients phone/export can be marked complete.

## Dummy Record Used

Created during QA:

- Patient: `CPX TEST Patient Phone QA 20260614`
- Main phone typed as digits: `2135550199`
- Emergency phone typed as digits: `2135550101`

No live calls, messages, payments, reminders, workflow activations, or credential actions were triggered.

## Verified

- Patients list loads behind login and shows `Professional`.
- Existing patient list phone values now render in friendly U.S./Canada display format, for example:
  - `+1 (416) 555-0198`
  - `+1 (500) 555-0111`
  - `+1 (500) 555-0006`
- Add Patient now uses shared country-aware phone fields for both:
  - `Phone`
  - `Emergency Contact Phone`
- Edit Patient now uses shared country-aware phone fields.
- The shared phone component includes an international country selector and defaults to United States.
- Invalid short phone input blocks saving and shows visible validation text.
- Valid U.S. digits save successfully when both phone fields are valid.
- The created dummy patient persisted in the Patients list.
- The created dummy patient displays as `+1 (213) 555-0199` in the list.
- Patient detail opens and shows formatted contact phone and formatted emergency phone.
- Patient edit opens with the shared phone inputs prefilled:
  - Main phone: `+1 213 555 0199`
  - Emergency phone: `+1 213 555 0101`
- Patients Export now opens an `Export Patients to CSV` dialog.
- Export dialog includes scope choices:
  - `All patients (25)`
  - `Current filters (25)`
  - `Selected only (0)` disabled when no rows are selected
- Export dialog includes column toggles, including separate display and E.164 phone fields:
  - `Phone (Display)`
  - `Phone (E.164)`
  - `Emergency Phone (Display)`
  - `Emergency Phone (E.164)`
- Export dialog shows the row count: `25 rows will be exported`.
- Leads Add Lead modal still opens after the shared phone import change and shows the shared country-aware phone component.

## Issues / Polish

1. Optional phone fields should not default to a validation-blocking `+1`.

   In Add Patient, `Emergency Contact Phone` starts as `+1`. If staff leaves that optional field unused, the form can be blocked because `+1` is treated as an invalid entered phone number. Optional phone fields should submit as blank/null unless the user types real digits beyond the country code.

2. The while-typing value is spaced, not the requested U.S./Canada mask.

   Typing `2135550199` shows `+1 213 555 0199` inside the input. Saved/list/detail display correctly shows `+1 (213) 555-0199`, but Ross requested the friendlier parenthesized style while staff are entering/viewing U.S./Canada numbers.

3. `555` demo numbers are rejected by libphonenumber validation.

   This is technically correct for strict validation, but UI examples and QA docs should use valid test ranges such as `+1 (213) 555-0199`, not `5558878888`, unless the product intentionally allows demo/fake numbers in test mode.

4. Downloaded CSV file contents are not verified.

   The Codex in-app browser reports that downloads are not supported, so the export modal UI was verified but the actual downloaded CSV filename, headers, row count, selected columns, and phone formats still need a normal-browser download check.

5. Leads may inherit the same optional `+1` behavior.

   The Leads Add Lead phone field also defaults to `+1`. Since phone is optional for leads, Lovable should confirm that a lead can be created with no phone and that the empty default is stored as blank/null, not as invalid `+1`.

## Decision

Do not mark Patients phone/export complete yet.

The core implementation is now in the right project and mostly working, but Lovable should do one focused polish pass for optional phone handling and input display consistency. After that, Codex should retest:

- Add Patient with no emergency phone.
- Add Patient with valid main phone and blank optional phone fields.
- Edit Patient without touching optional phone fields.
- Add Lead with blank optional phone.
- Export CSV download contents in a normal browser.

