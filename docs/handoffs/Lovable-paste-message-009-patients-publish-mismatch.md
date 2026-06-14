# Lovable Fix Request 009 - Patients Publish Mismatch / Wrong Workstream Suspected

Please respond in Plan mode only. Do not build yet.

Ross published after Lovable reported the following changes:

- Financial Transparency wording changed.
- Volunteer waiver language changed.
- `docs/QA_TESTING.md`, `docs/CONTENT_EDITING.md`, and `docs/RUNBOOK.md` exist.
- Internal `/handoff` page added.

Codex QA-tested the live ClinicPilotX app after publish and these claims do not match what is visible in the active ClinicPilotX dashboard project.

Live app tested:

`https://clinic-pilot-x.lovable.app`

## Safety Rules

- Do not activate live SMS, email, calling, video, payment, reminder, automation, or workflow sends.
- Do not connect live credentials.
- Do not create paid integrations.
- Preserve existing patient/lead/appointment data.
- Keep TEST safeguards untouched.

## QA Evidence

Detailed QA evidence:

`09-exports/patients-phone-export-qa-repeat-2026-06-14.md`

## Blocking Findings

### 1. `/handoff` Is Not Present On ClinicPilotX

Observed:

- `https://clinic-pilot-x.lovable.app/handoff` returns the app 404 page.
- Visible text includes `404` and `Oops! Page not found`.

Expected from Lovable's message:

- Internal noindexed `/handoff` page should exist.

### 2. Claimed Source Docs Are Not In Official ClinicPilotX GitHub Clone

Codex checked the official local GitHub clone and did not find:

- `docs/QA_TESTING.md`
- `docs/CONTENT_EDITING.md`
- `docs/RUNBOOK.md`

Please confirm whether Lovable built against the correct GitHub repo/project.

Official GitHub repo:

`https://github.com/aihustler2025/ClinicPilotX`

Known dashboard project:

`https://clinic-pilot-x.lovable.app`

Known Lovable project ID:

`8b4d9031-af8d-4faf-81d3-135c41ad73b7`

### 3. Patients Phone Input Still Not Updated

Observed in `Patients > Add Patient`:

- `Phone` is still a plain text input.
- `Emergency Contact Phone` is still a plain text input.
- No country picker, flag, or `+1` selector is visible.

Expected:

- Shared Leads-style country-aware phone input.
- Digits-only typing.
- U.S./Canada display like `+1 (555) 887-8888`.
- E.164 canonical storage/export underneath.

### 4. Patients Export Still Not Updated

Observed:

- `Export` does not show the expected advanced `Export Patients` dialog.
- No all/current filters/selected scope selector.
- No column picker.
- No row-count preview.

Expected:

- Patients export dialog should match the Leads export pattern.
- Include phone display and phone E.164 column options.

### 5. Patient Phone Display Still Mixed

Observed examples:

- `+1 (416) 555-0701`
- `+1-416-555-0198`
- `+15005550111`

Expected:

- Parseable staff-facing phone values display in friendly format.
- E.164 remains available for integrations/export.

## Requested Lovable Response

Please answer:

1. Did the last build run on the correct ClinicPilotX dashboard project?
2. Did the last publish target `https://clinic-pilot-x.lovable.app`?
3. Why did Lovable's summary mention financial transparency, volunteer waiver, and docs/handoff work instead of the Patients phone/export fix?
4. Are there multiple Lovable projects or branches involved here?
5. What exact files/components/functions will you touch to complete the Patients shared phone input and export dialog work?
6. What manual QA checklist should Codex run after Ross approves and publishes the next build?

Please do not build until Ross approves your revised plan.
