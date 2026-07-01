# Lovable Paste Message 051 - Email AI Sorting Build Pack Safety Revisions

Codex reviewed the Phase A exact build pack. Do not build yet.

The plan is much closer, but there are blocking safety revisions before Ross/Codex can approve Build mode.

## Product Direction

Approved directionally:

- `Workspace > Integrations > Email Inbox`
- Phase A simulated/paste intake only
- review queue
- test Lead creation after human approval only
- no real Gmail/Microsoft/forwarding/OAuth/live inbox
- no sends, calls, payments, calendar writes, n8n, live credentials
- Gmail/Microsoft/forwarding cards visible as disabled/planned

## Blocking Issue 1 - Do Not Drop Existing `leads.is_test`

Your rollback SQL includes:

```sql
ALTER TABLE public.leads
DROP COLUMN IF EXISTS intake_classification,
DROP COLUMN IF EXISTS intake_id,
DROP COLUMN IF EXISTS is_test;
```

This is not acceptable.

`leads.is_test` already exists from prior workflow-safety work. It is not new to this Email Intake phase. Dropping it would remove an existing safety guard used outside Email Intake.

Required revision:

- Do not drop `leads.is_test` in rollback.
- Treat `leads.is_test` as pre-existing if present.
- Only add/rollback columns introduced by this phase:
  - `intake_id`
  - `intake_classification`
- If you believe `leads.is_test` does not exist in the current project, provide a pre-check result proving that. Otherwise leave it untouched.

## Blocking Issue 2 - Reduce Edge Function Blast Radius

Your plan modifies 13 edge functions, including appointment, payment, scheduled confirmation, and payment-link functions.

That is too broad for Phase A.

Phase A only creates `is_test=true` Leads from simulated email intake. It should not create appointments, payments, scheduled confirmations, messages, calls, or calendar records.

Required revision:

1. Identify which send-capable functions are actually triggered by inserting an Email Intake test Lead.
2. Touch only the smallest required set for Phase A.
3. If you still believe a function must be touched, explain the exact trigger path from:

`email_intake approval -> test lead insert -> function invoked`

Do not modify appointment/payment/calendar functions unless there is a concrete Phase A trigger path.

Preferred Phase A approach:

- Keep existing prior `is_test` workflow-safety guards in place.
- Add/verify guards only for lead-created workflows that can actually run from a new Lead insert, such as:
  - lead acknowledgment,
  - smart follow-up / follow-up sequence,
  - auto-assignment / scoring only if currently triggered by lead insert and not already guarded.

Avoid broad edits to:

- appointment confirmation,
- appointment reminders,
- no-show recovery,
- payment receipt,
- payment reminder,
- create-payment-link,
- process-scheduled-confirmations,
- transport primitive functions.

## Blocking Issue 3 - RLS Helper Evidence

Your RLS policies use:

```sql
public.has_role(auth.uid(), 'admin')
```

Before approval, provide evidence that this helper exists and means platform/admin access as intended in this app.

Required pre-check:

```sql
select to_regprocedure('public.has_role(uuid,text)');
```

Also confirm whether this app's current platform-admin pattern is:

- `public.has_role(auth.uid(), 'admin')`, or
- `platform_admins`, or
- `is_platform_admin()`, or
- another helper.

Use the existing app pattern. Do not introduce a new privilege path.

## Blocking Issue 4 - Rerun-Safe Policies

The SQL uses `CREATE POLICY`, but policies do not use `IF NOT EXISTS`.

Required revision:

- Add `DROP POLICY IF EXISTS ...` before each `CREATE POLICY`, or use a safe DO block.
- The migration should be safe after a partial failed attempt.

## Blocking Issue 5 - Automation Log Expectations

The plan says skipped `is_test` workflows may write `automation_logs` rows with `event_type='skipped_is_test'`.

For Phase A, the cleaner target is:

- approving an Email Intake test Lead should not invoke send-capable workflows at all where avoidable,
- if a guard is invoked, it may write `skipped_is_test`,
- but the QA evidence must clearly distinguish:
  - zero external sends,
  - zero delivery rows,
  - zero messages/calls/payments,
  - skipped guard logs if any.

Please update the QA evidence language so it does not imply workflow invocation is required or desirable.

## Required Revised Response

Please stay in Plan mode and return a revised exact Phase A pack with:

1. Corrected SQL and rollback.
2. Pre-check proving whether `leads.is_test` already exists.
3. RLS helper evidence and alignment with existing app admin/platform-admin pattern.
4. Rerun-safe policies.
5. Narrowed edge function list with exact trigger paths.
6. Confirmation that Phase A does not touch appointment/payment/calendar functions unless a concrete trigger path exists.
7. Updated QA evidence for zero external side effects.

Do not build until Codex reviews the revised exact pack and Ross/Codex explicitly approve Build mode.
