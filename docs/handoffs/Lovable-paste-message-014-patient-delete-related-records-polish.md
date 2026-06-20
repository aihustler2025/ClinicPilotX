# Lovable Request 014: Patient Delete Related Records + Appointment Display Polish

Mode requested from Lovable: Plan mode only. Do not build yet.

## Context

Request 013 was approved, built, published, and QA-tested by Codex.

QA report:

`09-exports/patient-profile-booking-delete-fix-qa-2026-06-20.md`

Good news:

- Patient profile `Book Appointment` now opens the Appointments modal with patient prefilled.
- TEST mode is on.
- `15:30` now saves successfully.
- Appointment count increased from `27` to `28`.
- New appointment showed `TEST` badge.
- Native `window.confirm` was replaced with an in-app delete dialog.
- Delete dialog cancel works.
- Delete dialog confirm works for the disposable test patient.

## New Issues Found

### Issue 1: Stale Patient Profile Panel Remains Open After Delete

Repro:

1. Open Patients.
2. Filter to `CPX TEST Disposable Patient Delete QA 20260620`.
3. Open the patient profile side panel.
4. Open row action menu.
5. Delete patient through the in-app dialog.

Observed:

- Success toast appears.
- Patient list/filter changes to `No patients found`.
- But the side panel remains open and still shows the deleted patient details.
- Reload clears it.

Expected:

- On successful delete, if the deleted patient is currently selected/open in the detail panel, close the panel and clear selected patient state.

Likely file:

- `src/pages/Patients.tsx`

### Issue 2: Related Appointment Remains After Patient Delete

After deleting the disposable patient, Appointments still shows the related TEST appointment:

- Patient: `CPX TEST Disposable Patient Delete QA 20260620`
- Phone: `+12135550199`
- Service: `CPX TEST Profile Booking Regression 20260620`
- TEST badge visible
- Appointment total remains `28`

This creates a product/data question.

Please propose the safest behavior:

Option A: Block patient deletion if related appointments/transactions exist, and tell staff to archive instead.

Option B: Allow delete only after showing a stronger warning listing related records, then delete/anonymize related records according to a clear rule.

Option C: Convert hard delete into archive/deactivate for patients with related records.

Codex preference: avoid silent orphaning. For a clinic CRM, archiving/deactivating is probably safer than hard-deleting patients with historical appointments, unless Ross explicitly chooses hard-delete behavior.

Please inspect the current data relationships and recommend the least risky implementation.

Likely files:

- `src/pages/Patients.tsx`
- Appointment query/delete logic if related records are checked
- Supabase relationship or table constraints if relevant

### Issue 3: Appointment Display Polish

Observed:

- Patient profile Appointments tab shows `Jun 20, 2026 at 15:30:00`.
- Appointment row shows phone as raw E.164: `+12135550199`.

Expected:

- Staff-facing time should display as `3:30 PM` or `15:30`, not `15:30:00`.
- Staff-facing phone should display as `+1 (213) 555-0199` where possible, while storage remains E.164.

Likely files:

- `src/pages/Appointments.tsx`
- `src/components/patients/PatientDetailPanel.tsx`
- Shared phone/date/time formatting helper if available

## Safety

No live SMS.
No live email.
No live calls.
No payment links.
No workflow activation.
No secrets.
No migrations unless absolutely necessary and explained first.

## Required Lovable Response

Please respond in Plan mode only with:

1. Your recommendation for patient deletion when related appointments exist.
2. Exact files you would change.
3. Whether any database/schema/RLS change is required.
4. How you will close/clear stale selected patient state after delete.
5. How you will format appointment time and phone display.
6. Manual QA checklist after build.

Do not build until Ross sends your plan back to Codex and Codex approves it.

