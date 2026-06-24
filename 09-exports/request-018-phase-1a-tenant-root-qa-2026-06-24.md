# Request 018 Phase 1A Tenant Root QA - 2026-06-24

## Scope

Lovable reported that Phase 1A is live:

- pilot clinic `Dr. Colin Hong (Pilot)` created,
- `teambuzzooka@gmail.com` seeded as owner and platform admin,
- `kizha.buzzooka@gmail.com` seeded as admin,
- `profiles.active_clinic_id` set for both users,
- no existing table, policy, or app code touched.

This QA pass checked the live deployed app and public/read-only Supabase API behavior after publish.

## Result

Status: **partial pass / one follow-up required before Phase 1B**.

The existing CRM app still loads normally and the new Phase 1A database objects are present on the same Supabase project as the live app. The seeded user/member claims still need Lovable/Supabase confirmation because the current UI does not expose those rows and RLS correctly hides them from anonymous reads.

## Live App Smoke QA

Verified after publish:

- Dashboard loads behind authentication.
- Header still shows `Professional`.
- Dashboard still shows real/scoped metrics, including `Total Leads 20`, `Conversion Rate 15%`, `Follow-ups Coming soon`, and `Revenue (MTD) $0`.
- Leads loads and shows `17` active pipeline leads.
- Patients loads and shows populated patient records with friendly phone formatting.
- Appointments loads and shows `29 total appointments`, including friendly status/phone/time display.
- Communication Hub loads and still shows External Messages and Internal Chat.
- Automation Center loads and still shows `Professional` plus `7 / 13 Active`.
- No `No Plan` or zero-data regression was observed on Dashboard, Leads, Patients, Appointments, Communication Hub, or Automation Center during this pass.

## Supabase API Checks

Live deployed app still uses Supabase project:

`imuyfbvsombbpgdgkhrb`

Read-only anon API checks:

- `public.clinics` exists and returns `[]` to anonymous access.
- `public.clinic_members` exists and returns `[]` to anonymous access.
- `public.platform_admins` exists and returns `[]` to anonymous access.
- `public.clinic_invitations` exists and returns `[]` to anonymous access.
- `public.platform_admin_audit` exists and returns `[]` to anonymous access.
- `public.profiles` accepts selecting `active_clinic_id` and `onboarding_completed_at`, confirming the new columns exist.
- `public.is_platform_admin()` returns `false` for anonymous access.
- `public.current_clinic_id()` returns `null` for anonymous access.
- `public.is_clinic_member(random uuid)` returns `false` for anonymous access.
- `public.has_clinic_role(random uuid, owner)` returns `false` for anonymous access.

Interpretation:

- Phase 1A objects appear to exist on the correct Supabase project.
- Anonymous users cannot read the new tenant/admin rows.
- Helper functions exist and return safe anonymous values.

## Safety Check

During this QA pass, Codex did not:

- create leads,
- edit patients,
- change appointments,
- click send/test buttons,
- trigger SMS,
- trigger email,
- trigger workflows,
- trigger payment actions,
- trigger Google Calendar actions.

Observed network/resource activity did not include send/workflow/calendar/payment-write calls. The only payment-related observed request was a read-only dashboard revenue query against `payments`.

## Remaining Follow-Up

### 1. Settings still has a fetch error

The Settings page stayed on:

`Loading settings...`

Console showed:

`Error fetching settings: Object`

This error existed before Phase 1A, but it should be fixed before clinic onboarding/setup work because Settings will likely become the place where clinic profile, services, hours, templates, and integrations are managed.

### 2. Seeded member/profile claims need SQL confirmation

Codex cannot independently confirm the exact seeded rows from the current UI because Phase 1A intentionally has no UI and RLS hides the new records from anonymous reads.

Lovable/Supabase should provide read-only SQL results confirming:

- one pilot clinic exists with slug `dr-colin-hong`,
- `teambuzzooka@gmail.com` is owner and platform admin,
- `kizha.buzzooka@gmail.com` is admin,
- both profiles have the same `active_clinic_id`.

## Recommendation

Do not begin Phase 1B yet.

Next Lovable request should be a small QA follow-up:

1. confirm Phase 1A seeded rows with SQL,
2. diagnose/fix the existing Settings fetch error,
3. keep all work additive and avoid adding `clinic_id` to existing CRM tables until this foundation is verified.
