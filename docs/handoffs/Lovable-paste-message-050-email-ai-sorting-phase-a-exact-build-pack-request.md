# Lovable Paste Message 050 - Email AI Sorting Phase A Exact Build Pack Request

Codex reviewed your revised Email AI Sorting plan. The product direction is approved, but do not build yet.

Please stay in Plan mode and return an exact Phase A build pack before Ross/Codex clicks Approve.

## What Looks Good

The revised plan now correctly includes:

- `Workspace > Integrations > Email Inbox`,
- clinic-owner-friendly setup guidance,
- Gmail / Microsoft / forwarding choices,
- clear safety language,
- paste/import test email intake,
- sample fixtures,
- review queue,
- classification feedback,
- Gmail label future path,
- forwarding future path,
- no live OAuth or inbox connection in Phase A,
- no outbound sends, calls, texts, calendar writes, payments, n8n, or live credentials.

## Blocker To Clarify

Your plan says:

> Proposed schema + RLS (NOT executed in Phase A)

But Phase A appears to require persistence for:

- test email intake rows,
- classifications,
- review actions,
- feedback rows,
- created lead linkage,
- QA evidence,
- RLS checks.

Please clarify one of the following:

1. **Schema is included in Phase A.**  
   If yes, provide exact forward SQL, rollback SQL, RLS policies, grants, indexes, triggers if any, and rerun-safety checks.

2. **Schema is not included in Phase A.**  
   If no, explain exactly where intake rows, classifications, review state, and feedback are stored, and how Codex can QA persistence/reload/RLS.

Codex will not approve Build mode until this is resolved.

## Required Exact Phase A Build Pack

Please return an exact build pack with these sections:

### 1. Phase A Scope

List exactly what will be built in Phase A and what will remain disabled/planned.

Confirm again:

- no Gmail OAuth,
- no Microsoft OAuth,
- no forwarding webhook,
- no real inbox,
- no live credentials,
- no Resend/outbound sender,
- no Twilio/VAPI/ElevenLabs,
- no Stripe/payment,
- no calendar write,
- no n8n production dependency.

### 2. Exact SQL / RLS

If database changes are included, provide exact SQL for:

- new tables,
- new columns,
- indexes,
- grants,
- RLS policies,
- helper functions if any,
- rollback SQL,
- pre-checks and post-checks.

No blind migration approval without exact SQL.

### 3. Exact Edge Function Changes

Provide exact functions/files touched.

Avoid broad wording like "all send-capable workflow functions" unless you list each one.

For each function, state:

- why it needs an `is_test` guard,
- what row/table it checks,
- what it returns when skipped,
- whether it writes a log row,
- proof it cannot send when `is_test = true`.

### 4. AI Classifier Details

Provide:

- function name,
- model,
- JSON response schema,
- categories,
- extraction fields,
- confidence threshold,
- fallback behavior when AI fails,
- whether full email body is stored,
- confirmation that full email body is not written to edge logs.

### 5. UI Files

List exact files/components to be added or edited.

Confirm this is still under:

`Workspace > Integrations > Email Inbox`

Confirm Gmail/Microsoft/forwarding cards are visible but disabled/planned in Phase A, while paste/import test email is active.

### 6. Lead Creation Safety

Confirm:

- Phase A creates Leads only after human approval.
- All Phase A created Leads have `is_test = true`.
- Correct `clinic_id` is stamped.
- `source = email_intake`.
- Test leads are hidden by default unless `Show test records` is enabled.
- No existing real leads/patients/appointments are modified.

### 7. QA Evidence Expected After Build

After Phase A build, Lovable should be ready to provide:

- migration SQL applied,
- changed files list,
- test intake row SQL evidence,
- classification row SQL evidence,
- feedback row SQL evidence,
- lead row SQL evidence with `clinic_id` and `is_test`,
- workflow/activity/log evidence showing zero send-capable side effects.

## Build Approval Rule

Please return this as a Plan-mode response only.

Do not build until Codex reviews the exact build pack and Ross/Codex explicitly approve Phase A Build mode.
