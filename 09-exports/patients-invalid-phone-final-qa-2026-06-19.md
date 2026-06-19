# Patients Invalid Phone Final QA - 2026-06-19

Live app: `https://clinic-pilot-x.lovable.app`

Tester: Codex, using authenticated in-app browser after Ross approved, published, and shared Lovable's Request 012 completion message.

## Scope

Retest the final invalid-phone UX fix and regressions:

- Add Patient with invalid short phone.
- Add Patient with valid U.S. phone and blank emergency phone.
- Leads invalid-phone regression.

## Verdict

Pass.

The remaining invalid-phone UX issue from Request 012 is resolved in the live published app.

## Patients Invalid Phone

Test:

- Open Patients.
- Click `Add Patient`.
- Full name: `CPX TEST Invalid Phone Final 20260619`.
- Main phone: `123`.
- Emergency phone: blank.
- Click `Add Patient`.

Verified:

- Modal stays open.
- Invalid phone input remains visible as partial formatted value `1 23`.
- Inline helper appears:
  `Enter a valid phone number for the selected country (e.g. +1 (213) 555-0199).`
- No patient row is created for the invalid test record.

## Patients Valid Phone Regression

Test patient created:

- `CPX TEST Patient Valid Phone Final 20260619`
- `cpx.test+patient-valid-final-20260619@example.com`
- Main phone: `2135550199`
- Emergency phone: blank

Verified:

- Add Patient saves successfully.
- Modal closes after successful save.
- Patient row appears in Patients list.
- Patient list displays `+1 (213) 555-0199`.
- Emergency phone blank path remains non-blocking.

## Leads Invalid Phone Regression

Test:

- Open Leads.
- Click `Add Lead`.
- Full name: `CPX TEST Lead Invalid Phone Final 20260619`.
- Main phone: `123`.
- Click `Create Lead`.

Verified:

- Modal stays open.
- Inline helper appears:
  `Enter a valid phone number for the selected country (e.g. +1 (213) 555-0199).`
- No lead row is created for the invalid test record.

## Safety

No live SMS, calls, emails, payment requests, workflow activations, credential changes, storage bucket changes, or paid integrations were triggered.

## Status

Patients phone/export polish is complete for the tested Add/Edit/Export/phone-validation paths.

Separate future Patients QA still needed:

- Delete confirmation with dummy record only.
- Filters and sorting.
- Full patient detail tab walkthrough.
- Patient-to-appointment downstream regression.
