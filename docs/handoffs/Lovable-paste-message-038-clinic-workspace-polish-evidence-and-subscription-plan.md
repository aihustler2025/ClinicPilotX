# Lovable Paste Message 038 - Clinic Workspace Polish Evidence + Subscription Plan

Please read this follow-up and respond in Plan mode only. Do not build yet.

Codex QA-tested the published Clinic Workspace Phase A polish pass.

## UI QA Result

The UI polish passed:

- Services & Pricing buttons now have accessible labels.
- Delete opens an in-app confirmation dialog.
- Cancel keeps the row.
- Delete removes the disposable QA service after reload.
- Overview no longer showed a false `0 of 6` during the observed load.
- Integrations Status now uses safer wording:
  - `Configured, not tested`
  - `Enabled (not verified)`
  - `Not connected`
  - `Coming later`
- No live send/payment/calendar/workflow action was clicked.
- No fresh visible Automation Center workflow activity appeared during Codex QA.

## Evidence Still Missing

Your completion message did not include the read-only SQL evidence from the approved plan.

Please provide the SQL result tables for:

- pilot clinic workspace/profile snapshot,
- QA service row `QA TEST Service 20260627`,
- QA FAQ row `QA TEST FAQ 20260627`,
- AI guardrails row,
- send-capable / workflow row counts for the approved UTC QA window:
  - `workflow_executions`
  - `automation_logs`
  - `email_delivery_logs`
  - `scheduled_messages`
  - `reminders`
  - `messages`

Use the same lookup already approved:

```sql
where name = 'Dr. Colin Hong (Pilot)'
   or slug = 'dr-colin-hong'
```

Use the same QA window already approved:

```text
2026-06-27 14:30:00+00 to 2026-06-27 15:15:00+00
```

## Next Plan Request

Please also propose a separate Plan-mode-only fix for:

`Phase 1B.x - Subscription / Entitlement Display Reconciliation`

Problem still observed:

- header shows `No Plan`,
- Automation Center shows `No Plan`,
- Automation Center shows `7 / 5 Active`.

Why it matters:

- plan-gated features cannot be trusted if the displayed subscription state is wrong,
- this should be fixed before we demo Automation Center or start email AI sorting for Dr. Hong.

Please include:

1. Root-cause investigation plan.
2. Exact files likely touched.
3. Tables/functions/settings involved.
4. Whether the source of truth should be subscription table, profile role, platform admin status, or plan mapping.
5. How Automation Center should compute active workflow allowance.
6. QA checklist.
7. Rollback.

## Out Of Scope

Do not build:

- email inbox connection,
- email AI sorting,
- chatbot/API intake,
- knowledge uploads/embeddings,
- Google Calendar connection,
- SMS/calls,
- payment links,
- live workflows,
- main left-nav changes.

Plan only. Do not build yet.
