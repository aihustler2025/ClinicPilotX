# Patients Phone / ID Fix QA - 2026-06-19

Live app: `https://clinic-pilot-x.lovable.app`

Tester: Codex, using authenticated Chrome browser control after Ross approved, published, and shared Lovable's completion message.

## Scope

Retest Lovable's fix for:

- `permission denied for function generate_patient_id`
- Patients phone display/input polish
- Optional emergency phone blank save path
- Patients export CSV contents
- Leads blank-phone regression

## Verdict

Pass for the prior blocker and the main Patients phone/export requirements.

One remaining UX issue should be fixed: invalid short patient phone entry closes the Add Patient modal without visible validation and without creating a patient.

## Test Records Created

Patient:

- `CPX TEST Patient ID Fix 20260619`
- `cpx.test+patient-id-fix-20260619@example.com`
- Main phone: `2135550199`
- Emergency phone: untouched/blank

Lead:

- `CPX TEST Lead Blank Phone PostID 20260619`
- `cpx.test+lead-blank-postid-20260619@example.com`
- Phone: untouched/blank

## Verified Passes

- Add Patient now succeeds for a normal authenticated staff user.
- The previous `permission denied for function generate_patient_id` blocker did not recur.
- Add Patient with valid main phone and untouched blank emergency phone saves successfully.
- New patient row appears in Patients list.
- Patient list displays `+1 (213) 555-0199`.
- Edit Patient opens for the new patient.
- Edit Patient pre-fills main phone as `(213) 555-0199` with separate `+1` country chip.
- Emergency Contact Phone remains blank in Edit Patient.
- Updating the patient without touching emergency phone succeeds.
- Leads Add Lead with blank phone saves successfully and does not store/display bare `+1`.
- Patients Export dialog shows 26 rows.
- Downloaded CSV file was verified in Chrome:
  - File: `patients-filtered-2026-06-19.csv`
  - Row count: 26
  - Headers include `Phone (Display)`, `Phone (E.164)`, `Emergency Phone (Display)`, and `Emergency Phone (E.164)`.
  - New dummy patient row exported with `Phone (Display)=+1 (213) 555-0199`.
  - New dummy patient row exported with `Phone (E.164)=+12135550199`.
  - Emergency phone export fields were blank for the untouched optional emergency phone.

## Remaining Issue

Invalid Add Patient phone UX still needs a small fix.

Test:

- Open Add Patient.
- Enter full name `CPX TEST Invalid Phone 20260619`.
- Enter main phone `123`.
- Leave other fields blank.
- Submit.

Observed:

- Phone input displayed `1 23` before submit.
- Modal closed after submit.
- No visible validation helper/error appeared.
- No visible patient row was created.

Expected:

- Modal should stay open.
- Invalid phone field should show the inline validation helper.
- Helper should use the approved example: `+1 (213) 555-0199`.
- No patient should be created until staff enters a valid phone or clears the optional phone field.

## Safety

No live SMS, calls, emails, payment requests, workflow activations, credential changes, storage bucket changes, or paid integrations were triggered.

## Next Step

Send Lovable the small follow-up fix request:

`docs/handoffs/Lovable-paste-message-012-patients-invalid-phone-ux.md`
