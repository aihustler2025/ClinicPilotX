# Lovable Paste Message 027 - Phase 1B.1a Safety Exact SQL Review

Date: 2026-06-25

Codex reviewed Lovable's Phase 1B.1a workflow safety plan.

Do not click the generic approve button yet. Send this as a custom response.

```text
Codex reviewed the Phase 1B.1a workflow safety plan.

Direction is approved, but do not build yet. Please provide the exact SQL/function/body patch for final Codex review before execution.

The proposed safety direction is correct:
- add `is_test` to leads and patients,
- backfill existing QA/test rows,
- short-circuit lead acknowledgment and smart follow-up triggers for test leads,
- add edge-function defense-in-depth for direct/manual invocation,
- auto-mark QA/test lead and patient inserts from the frontend when name/email matches our QA pattern.

Before build approval, please provide:
1. Full migration SQL exactly as it will be run, including full `CREATE OR REPLACE FUNCTION` bodies for:
   - `public.trigger_lead_acknowledgment()`
   - `public.trigger_smart_follow_up()`
2. Exact edge-function files and patch summary for:
   - `workflow-lead-acknowledgment`
   - `workflow-smart-follow-up`
3. Exact frontend files and fields changed for:
   - `LeadFormDialog.tsx`
   - `Patients.tsx`
4. Confirmation the trigger guard returns before any workflow_executions, automation_logs, email_delivery_logs, reminders, scheduled_messages, messages, email, SMS, webhook, or external send attempt is created.
5. Confirmation existing QA rows will be backfilled to `is_test = true` using the `QA TEST%` / `cpx.test+%@example.com` pattern.

Do not run a negative-control live workflow test in the production/pilot database. Skip that unless there is a true isolated throwaway environment with no real credentials or send capability.

Out of scope remains:
- Phase 1B.1b,
- Appointments,
- Payments,
- Messages,
- Communication Hub,
- Settings,
- Subscription/useSubscription,
- RLS/GRANT changes,
- Automation Center UI,
- integrations or credentials.

Please respond in Plan mode only with the exact SQL and patch details. Do not build yet.
```
