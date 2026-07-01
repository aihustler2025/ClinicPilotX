# Lovable Paste Message 052 - Email AI Sorting Final Schema Safety Fixes

Codex reviewed the revised Phase A exact build pack. It is very close and most Request 051 blockers are resolved.

Do not build yet. Please make the final schema safety revisions below and respond in Plan mode only.

## What Is Now Accepted

Codex accepts these revisions:

- `leads.is_test` is now treated as pre-existing and is not dropped in rollback.
- `public.is_platform_admin()` is used instead of the incorrect `public.has_role(auth.uid(), 'admin')`.
- policies are rerun-safe with `DROP POLICY IF EXISTS`.
- edge-function blast radius is narrowed.
- appointment/payment/calendar functions are no longer touched.
- Phase A has one new edge function only: `classify-email-intake`.
- `trigger_calculate_lead_score` is the only existing function body proposed for replacement, and only to skip `is_test` rows before score calculation.

## Final Blocker 1 - Enforce Same-Clinic Relationship Between Intake and Classifications

Current SQL:

```sql
email_intake_classifications.intake_id references public.email_intake(id)
email_intake_classifications.clinic_id references public.clinics(id)
```

This does not prove that the classification row belongs to the same clinic as the intake row.

Required fix:

Enforce at the database level that:

```text
email_intake_classifications.intake_id + clinic_id
must match
email_intake.id + clinic_id
```

Acceptable implementation:

```sql
CREATE UNIQUE INDEX IF NOT EXISTS email_intake_id_clinic_id_uidx
ON public.email_intake (id, clinic_id);

ALTER TABLE public.email_intake_classifications
ADD CONSTRAINT email_intake_classifications_intake_clinic_fk
FOREIGN KEY (intake_id, clinic_id)
REFERENCES public.email_intake(id, clinic_id)
ON DELETE CASCADE;
```

If the exact syntax needs adjusting for Postgres constraints/indexes, please provide the corrected exact SQL.

Also include rollback for this constraint/index.

## Final Blocker 2 - Enforce Same-Clinic Relationship Between Leads and Email Intake

Phase A adds:

```sql
public.leads.intake_id references public.email_intake(id)
```

But the test Lead should never be linkable to an intake row from another clinic.

Required fix:

If feasible, enforce at DB level that:

```text
leads.intake_id + leads.clinic_id
must match
email_intake.id + email_intake.clinic_id
```

Preferred implementation:

```sql
ALTER TABLE public.leads
ADD CONSTRAINT leads_intake_clinic_fk
FOREIGN KEY (intake_id, clinic_id)
REFERENCES public.email_intake(id, clinic_id)
ON DELETE SET NULL;
```

If Postgres cannot use `ON DELETE SET NULL` cleanly with this composite relationship, propose the safest alternative:

- a trigger check before insert/update, or
- keep the simple FK but add a server-side invariant check in the approve-to-lead function and explain why DB-level enforcement is not practical.

Do not leave this as "UI will handle it."

## Final Blocker 3 - Confirm `has_clinic_role` Helper Evidence

The revised SQL uses:

```sql
public.has_clinic_role(clinic_id, 'owner'::public.clinic_role)
public.has_clinic_role(clinic_id, 'admin'::public.clinic_role)
```

Please include pre-check evidence that this exact helper exists.

Example:

```sql
select to_regprocedure('public.has_clinic_role(uuid, public.clinic_role)');
```

If the actual signature is different, revise the policies to match the existing helper.

## Final Blocker 4 - Lead Activity Timeline

Earlier plans said approved Email Intake leads should create a timeline/activity entry.

Please confirm whether Phase A writes a `lead_activity` row when an intake email becomes a Lead.

Preferred:

- write a `lead_activity` row such as `created_from_email_intake`,
- include `intake_id`, classification, confidence, and source,
- keep it internal only,
- no sends or workflows.

If not included in Phase A, say so explicitly and explain whether the Lead detail timeline will still show the source.

## Return Format

Please return:

1. Revised exact SQL snippets for the same-clinic constraints/checks.
2. Rollback SQL for those constraints/checks.
3. `has_clinic_role` helper evidence.
4. Confirmation of lead activity behavior.
5. Confirmation that no new edge functions or workflows were added beyond the already revised Phase A boundary.

After this, Codex expects to be able to approve Phase A Build mode if the revised response is clean.
