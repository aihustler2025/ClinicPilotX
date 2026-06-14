# Patients Phone and Export QA - 2026-06-14

Live app:

`https://clinic-pilot-x.lovable.app/patients`

## Scope

Focused QA after Ross approved and published Lovable's Patients module polish / shared phone standard build.

Goal:

- Verify Patients Add/Edit uses the shared country-aware phone input.
- Verify Patients export opens the scoped export dialog.
- Verify patient phone display is consistently friendly while retaining E.164 readiness.

No live Call, Message, Video, payment, reminder, SMS, email, or workflow action was triggered.

## Result

Fail. The published app does not appear to include the planned Patients phone/export changes.

## Verified / Evidence

### Patients Page Loads

- Patients page loaded behind login.
- `Professional` plan label was visible.
- Patients list rendered with existing patient cards.

### Issue 1: Add Patient Still Uses Plain Phone Inputs

Opened `Add Patient`.

Observed:

- `Phone` field is still a plain text input.
- Placeholder is `+1 (555) 123-4567`.
- No country picker is visible.
- No flag or `+1` selector is visible.
- `Emergency Contact > Phone` is also a plain text input with placeholder `+1 (555) 987-6543`.

Expected from approved plan:

- Country picker on the left with flag and country code.
- Staff types digits only.
- U.S./Canada display auto-formats as `+1 (555) 887-8888`.
- Underlying value emits/stores E.164.

### Issue 2: Edit Patient Still Uses Plain Phone Inputs

Opened `CPX TEST Lead June 11`, then clicked `Edit`.

Observed:

- `Phone` field is still a plain text input.
- Current value showed raw E.164: `+15005550111`.
- No country picker is visible.
- No flag or `+1` selector is visible.
- Emergency phone field is also still plain.

Expected from approved plan:

- Edit Patient uses the same shared phone component as Leads.
- Existing E.164 values derive the selected country and display friendly formatting.
- `+15005550111` should display as `+1 (500) 555-0111` or equivalent valid localized formatting if parseable.

### Issue 3: Patients Export Did Not Open Export Dialog

Clicked `Export` on Patients.

Observed:

- No `Export Patients` dialog opened.
- No visible scope selector appeared.
- No column picker appeared.
- No visible row count appeared.

Expected from approved plan:

- Export dialog opens.
- Scope options include All patients, Current filters, and Selected only.
- Column picker includes `Phone (Display)` and `Phone (E.164)` as independent toggles.
- Dialog shows estimated row count before download.

### Issue 4: Patient List Phone Display Still Mixed

Observed in list:

- Some phones are friendly formatted, such as `+1 (416) 555-0701`.
- Some phones still show raw E.164, such as `+15005550111`.
- Some legacy formats remain, such as `+1-416-555-0198`.

Expected:

- Display should normalize parseable values through `formatDisplay(...)` consistently.
- Raw E.164 values should not be shown to staff when they can be formatted.

## Not Tested

Because the main published changes were missing, Codex did not create a new dummy patient in this pass.

Reason:

- The Add Patient form clearly still had plain phone fields, so creating a record would not verify the intended feature.
- Avoided adding unnecessary dummy data while the feature is visibly not present.

## Decision

Do not treat the Patients phone/export polish as complete.

Send a Lovable fix request with this QA evidence and ask Lovable to confirm whether the build was actually deployed/published, whether the implementation was skipped, or whether the wrong branch/project/build was published.
