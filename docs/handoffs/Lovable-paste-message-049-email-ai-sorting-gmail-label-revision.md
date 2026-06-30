# Lovable Paste Message 049 - Email AI Sorting Gmail Label Revision

Please revise the Email AI Sorting plan in Plan mode only. Do not build yet.

Codex reviewed your Phase A plan. It is safe and thoughtful, but Ross clarified the actual pilot direction. We need the plan to explicitly support a future Gmail-label / connected-inbox workflow for the Dr. Colin Hong pilot, while still keeping the first build safe.

## Clarified Pilot Context

ClinicPilotX is the product. Dr. Colin Hong is the first pilot clinic workspace, not a custom one-off.

Known email flow from Ross:

- Public clinic email: `info@drcolinhong.com`.
- Messages are forwarded into a customer-care inbox that Ross can access through Gmail / Google Workspace.
- Ross wants ClinicPilotX to eventually connect to that accessible inbox and sort real incoming messages.
- The first safe demo can still be simulated or test-only, but the plan must show how it grows into Gmail label sorting without a redesign.

## Required Product Behavior

Ross wants Email AI Sorting to do three practical things:

1. Read incoming clinic email messages.
2. Classify them into useful buckets.
3. Route the useful ones into ClinicPilotX Leads, while leaving uncertain items for human review.

Target classifications:

- real lead / consultation inquiry,
- appointment request,
- existing patient or admin message,
- general question,
- spam / sales solicitation,
- questionable / needs human review.

For Gmail specifically, plan around labels rather than destructive folders:

- `ClinicPilotX/Lead`
- `ClinicPilotX/Appointment Request`
- `ClinicPilotX/Spam or Solicitation`
- `ClinicPilotX/Questionable`
- `ClinicPilotX/Processed`

Do not delete, archive, send replies, mark as read, or move mail out of the inbox in the first connected-inbox phase unless Ross explicitly approves.

## Revise The Phase Plan

Please revise your plan into these phases:

### Phase A - Safe ClinicPilotX Test Intake

Keep your no-live-inbox approach:

- paste/import test emails inside ClinicPilotX,
- classify with AI,
- show a review queue,
- approve/reject,
- create test Leads only after human approval,
- stamp correct `clinic_id`,
- set `is_test = true`,
- suppress all send-capable workflows.

This lets Codex and Ross QA the classifier, extraction, review queue, and lead creation before touching any real inbox.

### Phase B - Gmail Label Pilot, Still Safe

Plan the future connected Gmail pilot for the customer-care inbox:

- Use OAuth / least-privilege Gmail API access if possible.
- Prefer read + label-management scopes only.
- Read from one approved label or query window first, not the whole mailbox.
- Apply ClinicPilotX labels based on classification.
- Create Leads only after human review, or only in test mode until Ross approves production conversion.
- Never send replies in this phase.
- Never delete/archive messages in this phase.
- Never store Google passwords.
- Store tokens securely according to Lovable/Supabase best practice, and explain where this would live.

If OAuth is not practical in Lovable for the first demo, propose a fallback:

- manual Gmail export/import,
- forwarding to a ClinicPilotX-controlled intake address,
- or a test-only mailbox,

but explain the tradeoffs.

### Phase C - Future Client Onboarding

Plan how a subscriber clinic would connect email later:

- Gmail / Google Workspace connection,
- Microsoft 365 / Outlook connection,
- forwarding address option,
- manual setup checklist for domain/hosting providers if needed,
- no domain/DNS changes required for inbound sorting if mail already reaches the connected inbox,
- outbound sending requires a separate approval path.

Keep inbound sorting separate from outbound sending.

## Explain Resend / Outbound Email Separately

Please explicitly explain in the plan:

- Resend or similar email providers are for sending outbound email, not for reading/sorting an inbox.
- For a production clinic to send from its own domain, the clinic may need domain verification such as SPF/DKIM/DMARC.
- A simpler demo option is a ClinicPilotX-managed sender with `Reply-To` set to the clinic address, but this is only for later outbound workflows and should not be part of this Phase A build.

## Feedback Loop Requirement

Ross wants the classifier to improve over time.

Please plan a simple product-safe feedback loop:

- human marks classification as correct or wrong,
- human can move a message from Questionable to Lead or Spam,
- store those reviewed examples as clinic-scoped classifier feedback/rules,
- do not claim the model "learns automatically" unless there is an explicit implementation for that,
- keep all feedback separated by `clinic_id`.

## Safety Boundaries

Do not build yet.

Do not connect Dr. Hong's real inbox yet.

Do not connect OAuth, Gmail, Microsoft, Resend, Twilio, VAPI, ElevenLabs, Stripe, calendar, n8n, or live credentials in this phase.

Do not send email, SMS, calls, calendar writes, payment requests, webhook pushes, or workflow executions.

Do not activate live automations.

Do not change existing CRM pages outside the smallest required discoverability link unless you explain why.

## What To Return

Please return a revised Plan-mode response with:

1. Updated phased plan.
2. Exact proposed UI surfaces.
3. Exact proposed schema/RLS, if any.
4. How Gmail labels would work in the future.
5. How test intake converts to Leads safely.
6. How `is_test` and workflow suppression are guaranteed.
7. What credentials/scopes would eventually be needed, but not connected now.
8. QA checklist for Codex.
9. Clear build boundary for Phase A only.

Wait for Codex/Ross approval before any build.
