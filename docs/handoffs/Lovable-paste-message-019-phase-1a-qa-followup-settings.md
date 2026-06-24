# Lovable Paste Message 019 - Phase 1A QA Follow-Up And Settings Fix

Please read this Phase 1A QA follow-up and respond in **Plan mode only**. Do not build yet.

Codex QA found that Phase 1A mostly looks safe:

- The live app still loads Dashboard, Leads, Patients, Appointments, Communication Hub, and Automation Center.
- The new tenant root tables exist on Supabase project `imuyfbvsombbpgdgkhrb`.
- Anonymous reads return no rows from the new tenant/admin tables, which is good.
- New helper functions return safe anonymous values.
- No live sends/workflows/calendar/payment actions were triggered during QA.

QA report:

https://github.com/aihustler2025/ClinicPilotX/blob/main/09-exports/request-018-phase-1a-tenant-root-qa-2026-06-24.md

Before Phase 1B, please plan a small verification/fix pass only.

## Request

### 1. Confirm Phase 1A seed data with SQL

Please provide the exact read-only SQL checks you will run and the expected result shape for:

- `clinics` has exactly one pilot clinic with slug `dr-colin-hong`.
- `teambuzzooka@gmail.com` is a member with role `owner`.
- `teambuzzooka@gmail.com` is in `platform_admins`.
- `kizha.buzzooka@gmail.com` is a member with role `admin`.
- both users have `profiles.active_clinic_id` set to the pilot clinic id.
- `current_clinic_id()` returns the pilot clinic id for each seeded user when called as that user.

Do not expose secrets or access tokens.

### 2. Diagnose and fix Settings fetch error

Codex QA still sees:

`Settings -> Loading settings...`

Console:

`Error fetching settings: Object`

This may be pre-existing, but it needs to be fixed before onboarding/setup work because clinic setup will likely depend on Settings.

Please inspect:

- Settings page/component data fetches,
- `settings` table shape and RLS,
- whether `settings` is still a single global row,
- whether any recent Phase 1A profile columns affected Settings indirectly,
- whether this is tied to auth/session readiness or old `No Plan` context behavior.

### 3. Safety boundaries

For this request:

- Do not add `clinic_id` to existing CRM tables yet.
- Do not rewrite existing RLS yet.
- Do not change `useSubscription` yet.
- Do not build onboarding UI yet.
- Do not connect or trigger email, SMS, workflow, payment, webhook, or calendar actions.
- Do not change Automation Center send behavior.

## Expected Plan Response

Please respond with:

1. SQL verification plan for Phase 1A seed data.
2. Files/components/functions you will inspect for the Settings error.
3. Exact minimal code/database change you propose for Settings, if any.
4. QA checklist.
5. Confirmation that no live sends/integrations/workflows will be triggered.
