# Lovable Paste Message 022 - Phase 1B Evidence And App Scope Plan

Status: superseded by `Lovable-paste-message-023-phase-1b1-app-scope-plan.md` after Ross provided the correct Phase 1B completion evidence.

Please read this Phase 1B post-migration QA result and respond in **Plan mode only**. Do not build yet.

Codex performed live QA after Ross reported the Phase 1B migration was run and published.

QA report:

https://github.com/aihustler2025/ClinicPilotX/blob/main/09-exports/request-021-phase-1b-migration-qa-2026-06-25.md

## Important

The DOCX Ross provided as the completion result appears to contain the prior exact SQL review document, not the actual migration completion/post-check output.

The app smoke QA looks good, but Codex still needs the actual Phase 1B migration evidence before the next build phase.

## What Codex verified

Live app smoke pass:

- Dashboard loads with real metrics.
- Leads loads with `17` active leads.
- Patients loads with populated records.
- Appointments loads with `29 total appointments`.
- Payments loads.
- Communication Hub loads.
- Automation Center loads with `Professional` and `7 / 13 Active`.
- Settings still renders.
- No `No Plan` state observed.
- No visible route-level permission/missing-table/settings errors observed.

Read-only API shape check:

- `clinic_id` is selectable on 20 of the 23 expected tables.
- The 3 internal chat tables could not be checked through anon REST because of the known pre-existing `internal_channel_members` RLS recursion.

## Please provide actual Phase 1B evidence

Please paste the real migration completion evidence:

1. Pre-check output:
   - exactly one pilot clinic,
   - baseline row counts for all 23 tables.

2. Post-check output:
   - total row count unchanged for each table,
   - `clinic_id IS NULL` count is 0 for all 23 tables,
   - `count(DISTINCT clinic_id)` is 1 for non-empty tables and 0 for empty tables,
   - 23 `idx_*_clinic_id` indexes exist,
   - 23 foreign keys to `public.clinics(id)` exist.

3. Linter comparison:
   - confirm no new linter findings versus pre-migration baseline.

4. Safety confirmation:
   - no NOT NULL,
   - no defaults,
   - no RLS rewrites,
   - no app code changes,
   - no useSubscription/ClinicContext changes,
   - no Settings changes,
   - no live sends/integrations/workflows/payment/calendar actions.

5. Internal chat note:
   - confirm whether `internal_channels`, `internal_messages`, and `internal_channel_members` received `clinic_id` despite the known RLS recursion.
   - confirm that the RLS recursion is pre-existing and not caused by Phase 1B.

## Next planning request

After providing the evidence above, please also propose **Phase 1B.1 planning only** for the next safe app-code step.

This should be a plan only for:

- reading active clinic from `profiles.active_clinic_id` / `current_clinic_id()`,
- introducing a safe active-clinic context/hook if needed,
- stamping `clinic_id` on new inserts,
- gradually adding `.eq('clinic_id', activeClinicId)` filters to reads,
- keeping the current single-pilot clinic behavior unchanged,
- avoiding NOT NULL/defaults/RLS rewrite until writes and reads are verified.

Do not build Phase 1B.1 yet.

## Safety boundaries

For the next response:

- Plan mode only.
- Do not run migrations.
- Do not change app code.
- Do not rewrite RLS.
- Do not add NOT NULL/defaults.
- Do not touch live integrations, workflows, email, SMS, payment, calendar, WhatsApp, Messenger, Viber, Telegram, or voice.

## Expected response

Please respond with:

1. Actual Phase 1B migration evidence.
2. Any discrepancies from the approved SQL.
3. Confirmation whether rollback is still clean.
4. Phase 1B.1 app-scope plan only.
5. Risks/open questions.
