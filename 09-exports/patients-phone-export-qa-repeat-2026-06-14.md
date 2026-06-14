# Patients Phone / Export Repeat QA - 2026-06-14

## Context

Ross reported that Lovable said a build was done and Ross published it.

Lovable's message referenced:

- Financial Transparency wording.
- Volunteer waiver language.
- `docs/QA_TESTING.md`, `docs/CONTENT_EDITING.md`, `docs/RUNBOOK.md`.
- An internal `/handoff` page.

Those claims do not match the active ClinicPilotX Patients module workstream.

## QA Target

Live app:

`https://clinic-pilot-x.lovable.app`

Routes tested:

- `/handoff`
- `/patients`

## Result

Fail / likely project or build mismatch.

The published ClinicPilotX app still does not show the requested Patients phone/export implementation.

## `/handoff` Check

Observed:

- `https://clinic-pilot-x.lovable.app/handoff` returns the app's 404 page.
- Visible text: `404` and `Oops! Page not found`.

Expected if Lovable's message applied to this live ClinicPilotX project:

- A noindexed internal handoff page should exist.

## Source Docs Check

The local official ClinicPilotX GitHub clone at:

`C:\Users\user\Documents\ClinicPilotX`

does not contain:

- `docs/QA_TESTING.md`
- `docs/CONTENT_EDITING.md`
- `docs/RUNBOOK.md`

This suggests Lovable's response may belong to another Lovable project or another branch/source context.

## Patients Add Form Check

Observed after opening `Patients > Add Patient`:

- `Phone` is still a plain text input.
- `Phone` placeholder is `+1 (555) 123-4567`.
- `Emergency Contact Phone` is still a plain text input.
- `Emergency Contact Phone` placeholder is `+1 (555) 987-6543`.
- No country picker, flag, or `+1` selector was visible.
- Staff still appear expected to type punctuation manually or paste a full number.

Expected:

- Shared phone input matching Leads.
- Country selector / country-aware behavior.
- Digits-only typing.
- Friendly U.S./Canada formatting such as `+1 (555) 887-8888`.
- E.164 output/storage underneath.

## Patients Export Check

Observed:

- Patients page shows `Export`.
- No `Export Patients` dialog appeared during this QA pass.
- No scope selector was visible.
- No column picker was visible.
- No row-count preview was visible.

Expected:

- Export dialog modeled after Leads export.
- Scope selector: all/current filters/selected.
- Column picker.
- Row-count preview.
- Phone columns should include friendly display and E.164 export values.

## Patient List Phone Display Check

Observed mixed phone display values:

- Friendly: `+1 (416) 555-0701`
- Legacy hyphenated: `+1-416-555-0198`
- Raw E.164-like value: `+15005550111`

Expected:

- Staff-facing list/detail display should use friendly formatting whenever parseable.
- Canonical E.164 should remain available for integrations/export.

## Safety

No live SMS, email, call, video, payment, reminder, or workflow action was triggered.

No new patient was created because the requested Add Patient form behavior was visibly missing.

## Conclusion

Do not mark Patients phone/export polish complete.

Ask Lovable to confirm whether it built/published to the correct project:

`https://clinic-pilot-x.lovable.app`

Lovable should respond in Plan mode only before Ross approves another build.
