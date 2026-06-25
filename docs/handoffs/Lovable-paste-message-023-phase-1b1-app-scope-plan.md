# Lovable Paste Message 023 - Phase 1B.1 App Scope Plan

Please read this Phase 1B.1 planning request and respond in **Plan mode only**. Do not build yet.

Phase 1B migration evidence and Codex live QA are now accepted.

QA report:

https://github.com/aihustler2025/ClinicPilotX/blob/main/09-exports/request-021-phase-1b-migration-qa-2026-06-25.md

## Context

Phase 1B added nullable `clinic_id` to existing tenant/data tables and backfilled all current rows to the pilot clinic.

The next safe step is **not** RLS rewrite, NOT NULL, defaults, or per-clinic Settings.

The next safe step should be app-code planning for active clinic awareness:

- how the app reads the active clinic,
- how new inserts get `clinic_id`,
- how existing reads can gradually filter by active clinic,
- how we avoid breaking the current one-clinic pilot behavior.

## Request

Please propose **Phase 1B.1 app-code plan only**.

Include:

1. Active clinic source
   - Use `profiles.active_clinic_id` and/or `current_clinic_id()`.
   - Explain fallback behavior if active clinic is missing.
   - Explain what happens for platform admin users.

2. App architecture
   - Whether to introduce `ClinicContext`, `useActiveClinic`, or another existing pattern.
   - Exact files/components/hooks to inspect or edit.
   - How loading/error states should behave.

3. Insert stamping
   - Which create/insert paths should begin writing `clinic_id`.
   - Leads.
   - Patients.
   - Appointments.
   - Payments.
   - Conversations/messages.
   - Workflows/automation logs where applicable.
   - Services and quick responses if staff can create/edit them.

4. Read filtering
   - Which list/detail queries should filter by active clinic first.
   - Which pages should not be filtered yet.
   - How to avoid hiding existing data during rollout.

5. Sequencing
   - Break this into small build requests.
   - Recommend the first smallest build slice.
   - Avoid touching every module in one giant build.

6. QA
   - UI smoke checks.
   - Create a safe TEST lead and confirm it gets `clinic_id`.
   - Create a safe TEST appointment and confirm it gets `clinic_id`.
   - Confirm Dashboard, Leads, Patients, Appointments, Payments, Communication Hub, Automation Center, and Settings still render.
   - Confirm no live sends or workflow side effects.

7. Rollback
   - How to revert the app-code changes without rolling back the Phase 1B migration.

## Boundaries

For this response:

- Plan mode only.
- Do not build yet.
- Do not run migrations.
- Do not add NOT NULL.
- Do not add defaults.
- Do not rewrite RLS.
- Do not change per-clinic Settings yet.
- Do not change useSubscription unless you explain why it must be included and make it a separate optional slice.
- Do not trigger email, SMS, workflow, payment, webhook, calendar, WhatsApp, Messenger, Viber, Telegram, or voice actions.

## Expected Response

Please respond with:

1. Recommended Phase 1B.1 scope.
2. Exact files/components/hooks to inspect/edit.
3. First small build slice.
4. Later slices.
5. QA checklist.
6. Rollback plan.
7. Risks and open questions.
