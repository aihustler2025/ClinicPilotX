# Lovable Paste Message 018 - Dr. Hong Demo Foundation

Please read this request and respond in Plan mode only. Do not build yet.

Codex completed read-only audits of Communication Hub and Automation Center. The near-term product priority is a demo for Dr. Colin Hong focused on email AI sorting, lead intake, and client/clinic setup, not payments, video, WhatsApp, Messenger, or live SMS.

Reference reports:

- `09-exports/communication-hub-readonly-audit-2026-06-24.md`
- `09-exports/automation-center-readonly-audit-2026-06-24.md`
- `docs/dr-hong-demo-roadmap.md`

## Current Findings

### Communication Hub

- External Messages exists with SMS, WhatsApp, and Messenger demo rows.
- Conversation rows did not open the detail pane during QA.
- Internal Chat direct message creation failed with `Failed to create direct message channel`.
- No visible Email Inbox or Email AI Sorting area exists.

### Automation Center

- Automation Center has active workflow switches and Activity Logs.
- Current plan shows `Professional`.
- Active count shows `7 / 13 Active`.
- Activity Logs show completed/failed executions for Smart Follow-up, Lead Acknowledgment, and Appointment Confirmation.
- Several workflows are send-capable.
- Lead Acknowledgment has SMS/email templates and a `Send Test SMS` button.
- Appointment Confirmation has SMS/email templates and `Send Test SMS` / `Send Test Email`.
- No visible workflow currently handles incoming email AI sorting, spam filtering, email-to-lead conversion, external chatbot lead intake, or client-specific knowledge base setup.

## Business Goal

Prepare a safe Dr. Colin Hong demo path.

Ross wants to show:

1. A clinic/client can have its own setup in ClinicPilotX.
2. Incoming email can be classified by AI.
3. Spam/non-leads can be separated from real leads.
4. Real lead emails can create Leads records.
5. Appointment request emails can be detected and routed safely.
6. External chatbot or website form submissions can create Leads through a controlled API/webhook.
7. No live outgoing messages should be sent during the demo unless explicitly approved later.

## Requested Plan

Please propose a Plan-mode implementation for the Dr. Hong demo foundation.

Do not build yet.

Include exact files/components/functions/tables/migrations you would inspect or edit.

## Required Areas

### 1. Client / Clinic Account Setup

Design a safe client/clinic setup model for Dr. Hong.

It should support:

- Clinic/client name.
- Website.
- Contact email.
- Phone.
- Location/time zone.
- Business hours.
- Services.
- Pricing/consultation fee guidance.
- Staff users.
- Templates.
- Knowledge base / clinic facts.
- Connected inbox sources.
- Chatbot/contact-form/API sources.
- Automation settings.

Please explain whether existing tables already support this or whether new tables are needed.

### 2. Email AI Sorting Demo

Design a test-inbox-first email intake flow.

Expected categories:

- Spam / ignore.
- General inquiry.
- Real lead.
- Appointment request.
- Existing patient message.
- Billing/payment question.
- Urgent/high-priority message.

Required behavior:

- Use a test inbox first.
- Do not connect Dr. Hong's live email yet.
- Incoming email should be logged.
- AI classification should be reviewable.
- Valid leads should create Leads records or draft Leads records.
- Appointment requests should be linked to Leads or a pending appointment-request queue.
- Original email content should be saved to timeline/history.
- No outbound replies should send automatically in this phase.

### 3. Lead Intake API / Webhook

Design a controlled API/webhook path for outside lead sources.

Expected sources:

- ConvoCore chatbot.
- Future ClinicPilotX chatbot.
- Website contact form.
- Other third-party chatbots.

Expected payload fields:

- Client/clinic identifier.
- Name.
- Email.
- Phone.
- Requested service.
- Preferred appointment/contact time.
- Original message.
- Conversation transcript or summary.
- Source channel.
- Bot/project identifier.
- Consent/contact permission.

Required behavior:

- Validate and normalize phone numbers.
- Label source as chatbot/contact-form/email/etc.
- Create or draft a Lead record.
- Save source message/transcript to lead timeline or communication history.
- Avoid duplicates where possible.
- Never bypass ClinicPilotX validation.

### 4. Automation Center Relationship

Explain how this should appear in Automation Center.

Possible new/updated workflow cards:

- Email AI Sorting.
- Email to Lead Intake.
- Chatbot Lead Intake.
- Website Contact Form Intake.
- Appointment Request Detection.

For this phase, these should be inbound/review workflows only. No automatic outbound SMS/email should be activated.

### 5. Communication Hub Relationship

Explain whether classified email/chatbot messages should appear in:

- Communication Hub inbox.
- Lead timeline.
- Automation Center review queue.
- All of the above.

Please account for the current Communication Hub issues:

- external conversation detail did not open,
- internal direct message creation failed,
- no Email Inbox tab exists.

## Safety Rules

- Do not send SMS.
- Do not send email.
- Do not connect real client inbox credentials.
- Do not connect Dr. Hong's live email yet.
- Do not activate WhatsApp, Messenger, Viber, Telegram, payment, video, calendar, or voice integrations.
- Do not change Stripe/payment behavior.
- Do not change Google Calendar behavior.
- Do not trigger existing send-capable Automation Center workflows.
- Keep TEST/demo mode protections.

## Deliverable

Please respond in Plan mode only with:

- Proposed architecture.
- Exact source files/components/functions/tables/migrations to inspect or edit.
- Any new database tables or columns needed.
- Any edge functions needed.
- How the test inbox would work without live client credentials.
- How chatbot/contact-form submissions would authenticate safely.
- QA checklist.
- Risks and assumptions.
