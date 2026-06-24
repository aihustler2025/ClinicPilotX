# Request 019 Settings Fix QA - 2026-06-24

## Scope

Lovable shipped a frontend-only Settings fix after Phase 1A tenant root QA.

Reported changes:

- `Settings.tsx` uses `.maybeSingle()` for the `settings` row.
- Audit logs use a two-step `audit_logs` plus `profiles` fetch instead of the broken PostgREST embed.
- Empty-state guard added for a missing settings row.
- Phase 1A seed/helper/RLS evidence was confirmed by Lovable.

## Result

Status: **failed / follow-up required before Phase 1B**.

The original indefinite spinner is improved, but Settings still does not render the real settings form. It now falls into the missing-row fallback:

`Settings row missing - contact support.`

Because Settings is unusable, do not approve Phase 1B yet.

## QA Performed

Codex reloaded the live published app at:

`https://clinic-pilot-x.lovable.app/settings`

Observed after hard reload and wait:

- App shell loads.
- Header/left nav load.
- Plan badge shows `Professional`.
- Settings page initially shows `Loading settings...`.
- After additional wait, Settings changes to `Settings row missing — contact support.`
- No Settings form controls are visible.
- No Settings tabs are visible.
- No notification toggle/save QA could be performed because the Settings form never rendered.

Observed Settings-related network/resource calls:

- `https://imuyfbvsombbpgdgkhrb.supabase.co/rest/v1/settings?select=*`
- `https://imuyfbvsombbpgdgkhrb.supabase.co/rest/v1/audit_logs?select=*&table_name=eq.settings&order=created_at.desc&limit=50`
- `https://imuyfbvsombbpgdgkhrb.supabase.co/rest/v1/email_delivery_logs?select=*&order=created_at.desc&limit=50`
- `https://imuyfbvsombbpgdgkhrb.supabase.co/rest/v1/profiles?select=*&id=eq.03ebaa68-d9aa-41c7-a4b3-042d1e6acaf4`
- `https://imuyfbvsombbpgdgkhrb.supabase.co/rest/v1/profiles?select=id%2Cfull_name%2Cemail&id=in.%2803ebaa68-d9aa-41c7-a4b3-042d1e6acaf4%29`

## Regression Spot Checks

Core pages still load:

- Dashboard route loads, but a quick sample did not show all dashboard metric text before route change; retest after Settings is fixed.
- Leads loads and shows `17` active pipeline leads.
- Patients loads and shows populated patient records.
- Appointments loads and shows `29 total appointments`.
- Automation Center loads and shows `Professional` and `7 / 13 Active`.

Console/log observation:

- `Error fetching settings: Object` still appeared after visiting Appointments and Automation Center.

## Interpretation

The broken audit-log embed appears to have been removed correctly, but Settings still cannot read/render the expected settings row for the authenticated user.

Likely areas to inspect:

- Whether the `settings` query now returns zero rows because of RLS or query shape.
- Whether the `settings` table has exactly one row on the live project.
- Whether authenticated `teambuzzooka@gmail.com` can select that row through current RLS.
- Whether `.maybeSingle()` is masking a real read-permission failure or unexpected empty result.
- Whether the new empty-state guard should include better diagnostic logging and not replace a valid settings row.

## Safety

Codex did not:

- edit Settings,
- toggle notification switches,
- save Settings,
- trigger emails/SMS/workflows/payments/calendar actions,
- modify leads/patients/appointments.

## Recommendation

Send Lovable a focused follow-up. Do not approve Phase 1B until:

1. `/settings` renders the real settings form,
2. the notification toggle save/revert QA can be completed,
3. the `Error fetching settings: Object` console error is gone,
4. Dashboard/Leads/Patients/Appointments/Automation spot checks still pass afterward.
