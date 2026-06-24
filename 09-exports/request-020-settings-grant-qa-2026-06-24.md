# Request 020 Settings Grant QA - 2026-06-24

## Scope

Lovable applied the narrowed Settings grant fix after Request 020.

Reported change:

- `authenticated` now has `SELECT` on `public.settings`.
- No new schema/table/RLS/app-code changes were reported.
- Supabase linter warnings were reported as pre-existing permissive-RLS findings on other tables.

## Result

Status: **pass for the tested Settings grant scope**.

Settings now renders the real Settings UI after hard reload. The missing-row fallback is gone, and the reversible notification save/revert QA passed.

## QA Performed

### Settings hard reload

Tested:

`https://clinic-pilot-x.lovable.app/settings`

Verified:

- App shell loads.
- Header plan state shows `Professional`.
- Settings page renders real tabs:
  - General
  - Notifications
  - Integrations
  - Profile
  - Email Logs
  - Audit Log
- General tab renders Clinic Configuration, Email Signature, and Business Model Configuration sections.
- No `Loading settings...` hang.
- No `Settings row missing - contact support` fallback.
- No console errors observed on Settings.

### Reversible notification save test

Performed only the approved harmless QA rider:

1. Opened Notifications tab.
2. Confirmed Email, SMS, and Call notification switches were ON.
3. Turned Call Notifications OFF.
4. Clicked Save Changes.
5. Verified toast: `Settings updated successfully`.
6. Turned Call Notifications back ON.
7. Clicked Save Changes again.
8. Verified toast: `Settings updated successfully`.
9. Hard reloaded Settings.
10. Confirmed Email, SMS, and Call notification switches were all ON again.

No business-facing clinic name, logo, email, phone, address, template, integration, payment, calendar, or automation setting was changed.

### Audit Log

Verified:

- Audit Log tab opens.
- New settings update entries are visible for both QA saves.
- Actor shows `teambuzzooka@gmail.com`.
- The final entry records `call notifications enabled: enabled`, confirming the reversible QA change was restored.

### Core route smoke checks

Verified after the Settings fix:

- Dashboard renders real metrics after data load:
  - `Total Leads 20`
  - `Conversion Rate 15%`
  - `Revenue (MTD) $0`
  - `Recent Leads`
- Leads loads and shows `17` active leads.
- Patients loads with populated patient records.
- Appointments loads and shows `29 total appointments`.
- Payments loads.
- Communication Hub loads.
- Automation Center loads and shows `Professional` plus `7 / 13 Active`.

No `No Plan` state was observed during this pass.
No `Error fetching settings: Object` console error was observed during this pass.

## Safety

Codex did not:

- trigger email sends,
- trigger SMS sends,
- trigger workflows,
- trigger payment actions,
- trigger calendar actions,
- click Automation Center test-send buttons,
- modify leads, patients, appointments, payments, or workflows.

## Recommendation

Request 020 passes.

ClinicPilotX can now move to **Phase 1B planning only** for tenant-scoping existing CRM data. Do not approve Phase 1B build until Lovable provides a careful migration plan with table list, data backfill strategy, RLS plan, rollback, and QA.
