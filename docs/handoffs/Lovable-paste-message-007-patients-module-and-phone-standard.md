# Lovable Plan Request 007 - Patients Module Polish and Shared Phone Standard

Please respond in Plan mode only. Do not build yet.

Codex and Ross reviewed the live Patients module after the Patients/Appointments fix. The cross-module booking fix passed, but the Patients module itself still needs a dedicated polish pass and consistency improvements.

## Safety Rules

- Do not activate live SMS, email, calling, video, payment, reminder, or automation sends.
- Do not connect or require live credentials.
- Do not create paid integrations.
- Preserve existing patient/lead/appointment data.
- Keep the existing TEST-row safety behavior.

## Required Context

Please read:

- `docs/phone-number-standard.md`
- `docs/qa/patients-human-qa-script.md`
- `docs/qa/appointments-human-qa-script.md`
- `09-exports/patients-appointments-fix-qa-2026-06-12.md`

## Issues / Improvements To Plan

### 1. Shared Phone Input Standard

Leads has a country-aware phone field, but the visible format still does not fully match the requested UX.

Expected:

- User chooses country from a picker.
- User types digits only.
- U.S./Canada display should auto-format as `+1 (555) 887-8888`.
- Staff should not type brackets, spaces, or dashes.
- Store canonical phone values in E.164 for Twilio/VAPI readiness, for example `+15558878888`.
- Use libphonenumber-style parsing/validation, not a simple regex.
- Reuse one shared phone input component across Leads and Patients where possible.

Please explain whether the current Lead phone component can be adjusted and reused for Patients.

### 2. Patients Add/Edit Form Needs Phone Upgrade

Patients `Add Patient` currently appears less polished than Leads.

Expected:

- Add Patient and Edit Patient should use the same country-aware, auto-formatting, validated phone input behavior.
- If possible, preserve normalized E.164 storage while displaying friendly formatted values.

### 3. Patients Export Should Match Leads Export Pattern

Leads export now opens a useful dialog with scope and columns. Patients export currently appears to export immediately.

Expected Patients export:

- Open an `Export Patients` dialog.
- Let user choose:
  - All patients
  - Current filters
  - Selected patients, disabled if none selected
  - Columns
  - Optional status/date filters if already supported by data model
- Show estimated row count.
- Generate a clear CSV filename.

### 4. Patients Module QA Coverage

Codex needs to test:

- Add Patient
- View Details
- Edit Patient
- Export
- Search/filter/sort
- Delete confirmation for dummy records only
- Book Appointment from patient detail

Please include a manual QA checklist that aligns with `docs/qa/patients-human-qa-script.md`.

## Requested Lovable Response

Please provide a plan that explains:

1. Exact files/components/functions/tables you will touch.
2. How you will reuse or refactor the Leads phone input for Patients.
3. How E.164 storage and friendly display will work.
4. How existing patient phone values will be handled safely.
5. How Patients export will work.
6. Manual QA checklist after build.

Do not build until Ross sends approval.
