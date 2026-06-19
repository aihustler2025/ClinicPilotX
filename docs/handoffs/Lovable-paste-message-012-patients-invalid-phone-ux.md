# Lovable Paste Message 012 - Patients Invalid Phone UX

Use this in Lovable Plan mode only. Do not build until Ross/Codex reviews the plan.

## Context

Ross approved and published the Patient ID / phone polish fix. Codex retested the live ClinicPilotX dashboard.

QA report:

`09-exports/patients-phone-id-fix-qa-2026-06-19.md`

## Verdict

The prior blocker is fixed. Add Patient now succeeds for authenticated staff users, including the path with valid main phone and blank emergency phone.

Patients export CSV contents were also verified in Chrome.

## Verified

- `generate_patient_id` permission blocker is resolved for the Add Patient trigger path.
- Add Patient created `CPX TEST Patient ID Fix 20260619`.
- New patient list display: `+1 (213) 555-0199`.
- Edit Patient pre-fills main phone as `(213) 555-0199` with separate `+1` chip.
- Blank optional emergency phone remains blank.
- Edit Patient save succeeds without touching emergency phone.
- Leads blank-phone regression passes.
- Patients CSV export includes correct row count, display phone, E.164 phone, and blank emergency phone columns.

## Remaining Fix Needed

Invalid Add Patient phone UX is still wrong.

Codex tested:

- Full name: `CPX TEST Invalid Phone 20260619`
- Main phone: `123`
- Emergency phone: blank

Observed:

- Phone input showed `1 23`.
- Submit closed the modal.
- No visible inline validation/helper appeared.
- No patient row was created.

Expected:

- Modal stays open.
- Invalid phone field shows inline validation.
- Helper uses the approved parenthesized example:

`Enter a valid phone number for the selected country (e.g. +1 (213) 555-0199).`

- No patient is created until staff either enters a valid phone or clears the optional phone field.

Please check whether the invalid phone path is being converted to `null`, failing silently, or letting an error close the modal without surfacing feedback.

## Safety

Do not add live SMS, calls, emails, payment requests, reminders, workflow triggers, storage buckets, credentials, secrets, paid integrations, or production n8n dependencies.

## Please Respond With

A concise Plan-mode response only:

- Files/components/validation paths you will inspect.
- Exact behavior change for invalid phone submit.
- QA checklist you will run after build.
- Confirmation that no live integrations, sends, secrets, or paid services are touched.
