# Lovable Paste Message 036 - Clinic Workspace SQL Review Fixes

Date: 2026-06-27

Use this in Lovable Plan mode only. Do not build yet.

```text
Codex reviewed the exact SQL for Clinic Workspace Setup + Per-Clinic Knowledge Base Phase A.

Direction is still approved, but do not build or run SQL yet. Please revise the plan/SQL to address these blockers and respond in Plan mode only.

1. clinics UPDATE policy issue

The current SQL says it will "tighten" clinics UPDATE access by adding a new policy alongside existing ones.

That does not actually tighten RLS if any existing permissive UPDATE policy already allows broader writes. Supabase/Postgres permissive policies are OR'd together.

Please provide the current existing policies on public.clinics, especially UPDATE policies, and revise the SQL so the final effective UPDATE rules are actually:

- platform admin can update,
- clinic owner/admin can update their own clinic,
- staff/doctor/front_desk/viewer cannot update clinic profile/workspace fields.

If an existing broader UPDATE policy exists, propose the exact DROP/replace SQL for that policy. Do not just add another permissive policy and call it tightened.

2. services policy / constraint safety

Please provide current public.services policies before migration.

Confirm whether the existing app_role admin policies should remain, and whether adding clinic owner/admin policies creates any unwanted broader write access.

Also make the services constraint additions rerun-safe:

- services_price_cents_nonneg
- services_duration_nonneg

If PostgreSQL/Supabase cannot use ADD CONSTRAINT IF NOT EXISTS directly, wrap each ADD CONSTRAINT in a DO block that checks pg_constraint first.

3. trigger creation should be rerun-safe

The migration uses CREATE TABLE IF NOT EXISTS but then creates triggers unconditionally.

Please make trigger creation rerun-safe for:

- clinic_business_hours_set_updated_at
- clinic_faqs_set_updated_at
- clinic_ai_guardrails_set_updated_at

Use DROP TRIGGER IF EXISTS before CREATE TRIGGER or a pg_trigger guard.

4. CREATE POLICY should be rerun-safe

For new tables, CREATE POLICY statements should either:

- be wrapped with pg_policies existence checks, or
- use DROP POLICY IF EXISTS before CREATE POLICY.

This prevents a partial migration retry from failing.

5. Rollback note

Rollback currently restores global services_name_key only if no duplicate service names exist. That is acceptable, but please explicitly call out that rollback may not fully restore the old uniqueness constraint after real multi-clinic services are added.

6. Keep scope unchanged

Keep these out of scope:

- live email inbox connection,
- email AI sorting,
- chatbot/API intake,
- SMS/email/WhatsApp/Messenger/Viber/Telegram/voice sends,
- Stripe/payment links,
- Google Calendar writes,
- scheduled_messages,
- Automation Center workflow behavior,
- edge functions,
- file uploads,
- URL crawling,
- embeddings/vector store,
- ClinicSwitcher, which is deferred to Phase A1.

Please respond with:

1. revised exact forward SQL,
2. revised exact rollback SQL,
3. current clinics and services policy evidence,
4. confirmation that the final effective RLS is not accidentally broader,
5. frontend file list,
6. QA plan.

Do not build until Codex reviews the revised SQL.
```

