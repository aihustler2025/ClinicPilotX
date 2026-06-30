# Lovable Paste Message 048 - Test-Inbox Email AI Sorting Plan

Please respond in Plan mode only. Do not build yet.

Phase 2 Workspace Home passed Codex QA. We are ready to plan the next functional demo priority: safe test-inbox Email AI Sorting for the Dr. Colin Hong pilot workspace.

Important context:

- ClinicPilotX is a multi-client subscription product.
- Dr. Colin Hong is the first pilot clinic workspace, not a one-off custom build.
- Do not connect Dr. Hong's real inbox yet.
- Do not send emails, SMS, calls, payments, calendar writes, or workflow/test-send actions.
- Use a safe test inbox / simulated inbox approach first.
- No live credentials should be requested, entered, stored, or activated in this phase.

Product goal:

ClinicPilotX should be able to review incoming clinic email inquiries, classify them safely, and convert credible lead/appointment-request emails into Leads for the correct clinic workspace.

Near-term demo goal:

Build or plan a safe demo path where Codex/Ross can feed test emails into ClinicPilotX and see:

1. Email captured into an intake queue.
2. AI classification result, such as:
   - likely lead,
   - appointment request,
   - general question,
   - spam/noise,
   - existing patient/admin message,
   - needs human review.
3. Extracted contact details when present:
   - name,
   - email,
   - phone,
   - requested service,
   - preferred time/date,
   - message summary,
   - urgency.
4. Safe conversion of approved lead/appointment-request emails into Leads with correct `clinic_id` and `is_test` handling.
5. No outbound send or workflow side effects during QA.

Plan request:

Please propose the safest Phase A architecture for this demo.

Address these questions:

1. What is the safest input method for Phase A?
   - Manual paste/import test email form?
   - Test inbox polling later?
   - Webhook/API intake later?
   - Gmail/Microsoft OAuth later?

2. What new UI should exist, and where?
   - Automation Center workflow detail?
   - Communication Hub email intake queue?
   - Workspace integrations status?
   - Separate Email Intake / AI Sorting page?

3. What database tables or columns already exist that can support this?
   - If schema changes are needed, do not build yet. Provide exact proposed tables/columns and RLS plan for Codex review.

4. How should AI classification be safely stored and reviewed before lead creation?

5. How should test records be protected?
   - `is_test = true` where applicable.
   - `QA TEST` / `cpx.test+...@example.com` safety heuristic where applicable.
   - No workflow executions for QA rows.

6. How should this connect to existing Leads module fields?
   - source = email / website contact form / test inbox,
   - service requested,
   - preferred contact,
   - consent status,
   - notes/timeline,
   - lead activity.

7. How does this later expand to:
   - real client inbox connection,
   - website contact forms,
   - ConvoCore chatbot/webhook intake,
   - future ClinicPilotX chatbot,
   - Communication Hub conversation history?

Hard boundaries for this planning pass:

- No build yet.
- No real inbox connection.
- No live OAuth.
- No live credentials.
- No outbound sends.
- No SMS/calls/payments/calendar writes.
- No active workflow triggers from QA records.
- No n8n production dependency.
- Prefer Lovable/Supabase/Lovable Cloud/app-native implementation first.

Deliverables requested from Lovable:

- Recommended Phase A plan in plain language.
- Exact file/component/page list if build is later approved.
- Exact schema/RLS/function changes if any are needed, but do not run them yet.
- Safety plan for QA/test records.
- QA checklist for Codex.
- Rollback plan.
