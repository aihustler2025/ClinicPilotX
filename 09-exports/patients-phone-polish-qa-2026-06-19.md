# Patients Phone Polish QA - 2026-06-19

Live app: `https://clinic-pilot-x.lovable.app`

Tester: Codex, using the authenticated in-app browser after Ross logged in.

## Scope

Retest Lovable's Patients phone polish follow-up after Ross clicked Approve and Publish.

Focus:

- Patients Add Patient phone behavior.
- Optional emergency phone behavior.
- U.S./Canada phone display and helper examples.
- Patients Export dialog.
- Leads blank-phone regression.

## Verdict

Fail / partial pass.

The shared phone component is present, and Leads blank-phone handling works, but Patients cannot pass Add Patient QA because normal patient creation fails with a database permission error.

## Verified Passes

- Patients page loads behind authenticated login.
- Patients list/detail display already-saved U.S./Canada numbers in friendly format, for example `+1 (213) 555-0199`.
- Patients Export opens `Export Patients to CSV`.
- Export dialog includes scope choices, row count, column picker, and both display/E.164 phone columns.
- Invalid Patients phone input blocks submit and shows visible inline validation.
- Leads Add Lead with untouched phone field starting at `+1` saves successfully as blank phone, not bare `+1`.

Lead created during regression QA:

- `CPX TEST Lead Blank Phone 20260619`
- `cpx.test+lead-blank-phone-20260619@example.com`

## Blocking Issue

Add Patient failed after entering a valid main phone and leaving optional Emergency Contact Phone untouched.

Attempted patient:

- `CPX TEST Patient Phone Polish 20260619`
- `cpx.test+patient-phone-polish-20260619@example.com`
- Main phone entered as digits only: `2135550199`
- Emergency Contact Phone left untouched at its default country-code-only state.

Observed error:

`permission denied for function generate_patient_id`

Impact:

- A normal authenticated user cannot create a patient through the Patients module.
- This blocks final QA of Add Patient, optional emergency phone persistence, and saved display for newly created patients.

## Formatting Issues Still Present

The phone component still shows spaced input values inside Add/Edit forms, for example:

- `+1 213 555 0199`
- `+1 213 555 0101`

The product standard remains:

- Staff-facing U.S./Canada display: `+1 (213) 555-0199`
- Canonical storage/API value: `+12135550199`

Invalid phone helper copy also still uses the spaced example:

`Enter a valid phone number for the selected country (e.g. +1 213 555 0199).`

Expected helper example:

`Enter a valid phone number for the selected country (e.g. +1 (213) 555-0199).`

## Export Limitation

The Patients export dialog UI is verified, but the in-app browser cannot save downloads. Actual CSV filename, row count, headers, selected-column behavior, and phone value formatting still need normal-browser download verification or Lovable/code confirmation.

## Safety

No live SMS, calls, emails, payment requests, workflow activations, credential changes, storage bucket changes, or paid integrations were triggered.

## Next Step

Send Lovable the follow-up fix handoff:

`docs/handoffs/Lovable-paste-message-011-patients-phone-polish-qa-fixes.md`
