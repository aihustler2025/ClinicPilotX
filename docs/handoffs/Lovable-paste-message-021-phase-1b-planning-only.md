# Lovable Paste Message 021 - Phase 1B Planning Only

Please read this Phase 1B planning request and respond in **Plan mode only**. Do not build yet.

Request 020 Settings grant QA passed.

QA report:

https://github.com/aihustler2025/ClinicPilotX/blob/main/09-exports/request-020-settings-grant-qa-2026-06-24.md

## Context

Phase 1A tenant root foundation is live and verified enough to move forward:

- pilot clinic exists,
- seeded users are linked to the pilot clinic,
- helper/RLS checks were confirmed by Lovable,
- Settings now renders and saves after the narrowed grant fix.

Now we need a careful **Phase 1B plan only** for tenant-scoping existing ClinicPilotX data.

This is riskier than Phase 1A because it may touch existing CRM tables such as leads, patients, appointments, messages, payments, workflows, settings, services, logs, and automation data. Do not build until Codex and Ross review the plan.

## What Phase 1B Should Plan

Please propose a safe migration plan for adding clinic/workspace scoping to existing data.

Include:

1. Exact table inventory
   - Which existing tables need `clinic_id`.
   - Which tables should not get `clinic_id` yet.
   - Which tables are global/platform tables.
   - Which tables are lookup/catalog tables.

2. Migration phasing
   - Add nullable `clinic_id` columns first.
   - Backfill current records to the pilot clinic.
   - Verify counts.
   - Only later consider NOT NULL/defaults.
   - Only later rewrite existing RLS.

3. Backfill strategy
   - How every existing lead, patient, appointment, message, payment, workflow, and log row will be assigned to the pilot clinic.
   - How orphaned/legacy rows will be handled.
   - How TEST rows will be handled.

4. App code impact
   - Which pages/hooks/queries will eventually need active clinic filtering.
   - Whether the app should introduce a `ClinicContext` or similar.
   - How to avoid breaking current Dashboard, Leads, Patients, Appointments, Communication Hub, Automation Center, Payments, and Settings while migration is in progress.

5. RLS plan
   - Do not rewrite existing table RLS in the first migration.
   - Explain the later RLS rewrite phase separately.
   - Include helper functions used for member/admin access.
   - Include platform admin behavior.

6. Subscription/settings plan
   - How `clinic_subscriptions`, `clinic_addons`, and Settings should eventually connect to the active clinic.
   - Whether Settings should remain global until later or become per-clinic in a dedicated later phase.

7. QA and rollback
   - Pre-migration count checks.
   - Post-migration count checks.
   - UI smoke checks.
   - SQL verification checks.
   - Rollback plan.

## Safety Boundaries

For this response:

- Plan mode only.
- Do not build.
- Do not run migrations.
- Do not change RLS.
- Do not change app code.
- Do not trigger email, SMS, workflows, payment, webhook, calendar, WhatsApp, Messenger, Viber, Telegram, or voice actions.

## Expected Response

Please respond with:

1. Recommended Phase 1B scope.
2. Tables to include/exclude.
3. Exact migration sequence.
4. App-code change sequence.
5. RLS rewrite strategy, clearly marked as later/not part of first migration.
6. QA checklist.
7. Rollback plan.
8. Risks and open questions.
