# Lovable Fix Request 008 - Patients Phone / Export QA Failed After Publish

Please respond in Plan mode only. Do not build yet.

Ross approved the revised Patients module polish / shared phone standard plan and published the app. Codex then QA-tested the live published app at:

`https://clinic-pilot-x.lovable.app/patients`

## Safety Rules

- Do not activate live SMS, email, calling, video, payment, reminder, or automation sends.
- Do not connect or require live credentials.
- Do not create paid integrations.
- Preserve existing patient/lead/appointment data.
- Keep existing TEST-row safeguards untouched.

## QA Result

Fail. The published app does not appear to include the planned Patients phone/export changes.

Detailed QA evidence:

`09-exports/patients-phone-export-qa-2026-06-14.md`

## Blocking Findings

### 1. Add Patient Still Has Plain Phone Inputs

Observed in live app:

- `Add Patient > Phone` is a plain text input.
- Placeholder is `+1 (555) 123-4567`.
- No country picker is visible.
- No flag / `+1` selector is visible.
- Emergency contact phone is also plain.

Expected:

- Shared country-aware phone component.
- Staff types digits only.
- U.S./Canada display auto-formats as `+1 (555) 887-8888`.
- Underlying value emits/stores E.164.

### 2. Edit Patient Still Has Plain Phone Inputs

Observed in live app:

- `Edit Patient > Phone` is a plain text input.
- Existing dummy patient value shows raw E.164: `+15005550111`.
- No country picker is visible.
- No flag / `+1` selector is visible.

Expected:

- Edit Patient uses the same shared phone component.
- Existing E.164 values derive selected country and show friendly formatting.

### 3. Patients Export Did Not Open Dialog

Observed:

- Clicking `Export` did not open an `Export Patients` dialog.
- No scope selector appeared.
- No column picker appeared.
- No row count appeared.

Expected:

- Export dialog with All / Current filters / Selected scope.
- Column toggles including `Phone (Display)` and `Phone (E.164)`.
- Estimated row count before download.

### 4. Patient List Phone Display Is Still Mixed

Observed examples:

- Friendly: `+1 (416) 555-0701`
- Raw E.164: `+15005550111`
- Legacy hyphen format: `+1-416-555-0198`

Expected:

- Parseable values display in friendly localized format.
- E.164 remains available for integrations/export, but staff-facing list/detail should not show raw E.164 when it can be formatted.

## Requested Lovable Response

Please explain:

1. Was the Patients phone/export implementation actually built?
2. Was it published to the same live project at `https://clinic-pilot-x.lovable.app`?
3. If yes, why is the live Patients UI still showing the old plain inputs and old export behavior?
4. Exact files/components/functions you will touch to complete the missing implementation.
5. Manual QA checklist after build.

Please do not build until Ross approves your revised plan.
