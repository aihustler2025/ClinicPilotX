# Lovable Paste Message 010 - Patients Phone Polish Follow-Up

Use this in Lovable Plan mode only. Do not build until Ross/Codex reviews the plan.

## Context

Codex QA-tested the published ClinicPilotX Patients phone/export implementation after Ross clicked Approve and Publish.

The good news: the corrected Patients work is now visible on the active ClinicPilotX dashboard. The previous publish/workstream mismatch appears resolved.

QA report:

`09-exports/patients-phone-export-fix-qa-2026-06-14.md`

## Verdict

Partial pass. Please plan a small polish/fix pass before Patients phone/export is considered complete.

## Verified

- Patients Add/Edit now uses the shared country-aware phone input.
- Patient list/detail display formats U.S./Canada phones like `+1 (213) 555-0199`.
- Valid U.S. digits can be typed and saved.
- Invalid short phone values show visible validation.
- Patients Export now opens a CSV dialog with scope, row count, and column picker.
- Export columns include separate display and E.164 fields for patient and emergency phones.
- Leads Add Lead still opens with the shared phone component after the import refactor.

## Required Fixes

1. Optional phone fields must not default to a validation-blocking `+1`.

   In Add Patient, Emergency Contact Phone starts as `+1`. If staff leaves it unused, the form can be blocked because `+1` is treated as an invalid entered value.

   Expected behavior:

   - Optional phone fields should be blank/null unless staff types real digits beyond the country code.
   - `+1` alone must not be submitted or validated as user-entered phone data.
   - Add Patient should save when main phone is valid and emergency phone is untouched/blank.
   - Edit Patient should save existing records without forcing optional emergency phone completion.
   - Leads should also allow phone to remain blank/null when staff does not enter a phone.

2. U.S./Canada input display should match the product standard as closely as possible.

   Current typed value displays as:

   `+1 213 555 0199`

   Desired staff-facing display for U.S./Canada:

   `+1 (213) 555-0199`

   Keep canonical storage in E.164, for example:

   `+12135550199`

3. Replace invalid examples/test hints if needed.

   Strict libphonenumber validation rejects many fake `555` numbers. Use valid reserved/test-style examples such as:

   `+1 (213) 555-0199`

   Do not loosen production validation just to accept bad demo numbers unless you explicitly propose a test-mode-only exception.

4. Confirm CSV export implementation details.

   Codex could verify the export dialog UI, but the in-app browser cannot save downloads. Please confirm the CSV generator includes:

   - Correct selected scope.
   - Correct row count.
   - Correct selected columns only.
   - `Phone (Display)` and `Emergency Phone (Display)` in friendly format.
   - `Phone (E.164)` and `Emergency Phone (E.164)` in canonical format.
   - Clear filename.

## Safety

Do not add live SMS, calls, emails, payment requests, reminders, workflow triggers, storage buckets, credentials, secrets, or paid integrations.

## Please Respond With

A concise Plan-mode response only:

- Files/components you will edit.
- Exact behavior changes.
- QA checklist you will use after build.
- Confirmation that no live integrations or secrets are touched.

