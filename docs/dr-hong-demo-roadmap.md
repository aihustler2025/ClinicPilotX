# ClinicPilotX Pilot Demo Roadmap

Last updated: 2026-06-26

## Purpose

This is the near-term ClinicPilotX roadmap for preparing a practical pilot demo using Dr. Colin Hong as the first real clinic workspace.

ClinicPilotX remains the product. Dr. Hong is not a custom one-off build. He is the first pilot clinic we can use to prove the product with real-world clinic data, website/chatbot context, and email-intake workflows.

The goal is not to finish every module. The goal is to show the highest-value pieces first:

- A clinic/client account can exist inside ClinicPilotX.
- Each clinic can personalize ClinicPilotX with its own setup, team, business facts, services, branding, and integrations.
- Email inquiries can be filtered into useful categories.
- Real leads can land in the Leads module.
- Appointment requests can be recognized and routed safely.
- Chatbot or website form submissions can send lead data into ClinicPilotX.

Payments, video consultation, WhatsApp, Messenger, Viber, Telegram, and advanced social messaging are later phases.

## Plain-English Build Order

### 1. Finish Internal Appointments Safety

Status: mostly done for the current QA scope.

What this means:

- The built-in ClinicPilotX calendar/list should work before outside automations connect to it.
- Staff can safely mark a TEST appointment as Confirmed or Cancelled.
- Confirm/Cancel should update the appointment inside ClinicPilotX only.
- These buttons should not accidentally send email, SMS, calendar invites, refunds, or workflows unless explicitly designed and approved.

Why it matters:

Email and chatbot automations may later create appointment requests. Those requests need a safe internal status path before they trigger client-facing communications.

### 2. Audit Communication Hub

Status: next major QA/audit target.

What Codex should check first:

- What tabs and message views already exist.
- Whether existing message data is real, mock, or empty.
- Whether any send buttons exist.
- Whether message sending is safely disabled or could trigger real email/SMS.
- Whether internal staff chat is usable or blocked by backend/RLS issues.

Near-term build focus:

- Client email inbox/intake review.
- Basic internal communication record/timeline.
- Possibly SMS later, but not before safety and consent handling are reviewed.

Later:

- WhatsApp.
- Facebook Messenger.
- Viber.
- Telegram.
- Other social channels.

### 3. Create Client / Clinic Account Setup

Status: required before a real pilot demo.

What this means:

Each clinic/client needs its own setup area so ClinicPilotX can know:

- Clinic name.
- Logo/branding.
- Contact email.
- Phone number.
- Website.
- Address/location.
- Staff/users.
- Services.
- Pricing or consultation fee guidance.
- Business hours.
- Appointment preferences.
- Templates.
- Knowledge base / clinic facts.
- Connected inboxes and chatbot sources.
- Google Calendar connection status.
- Automation settings.
- Subscription plan / feature access.

Why it matters:

Each clinic should be able to make ClinicPilotX feel like its own operating system. Dr. Hong should be the first pilot workspace, but the same setup should work later for any subscribing clinic.

### 3A. Client Knowledge Base

Status: required for AI features.

Each clinic needs a knowledge base/business profile that AI workflows can reference.

It should include:

- Services and descriptions.
- Pricing ranges.
- FAQs.
- Hours of operation.
- Booking rules.
- Cancellation/no-show policies.
- Provider bios.
- Location/parking notes.
- Business tone/brand voice.
- Common patient instructions.
- Things AI should never say.

This knowledge base should be separated per clinic so one client's information never leaks into another client's automation.

### 4. Build Lead Intake API / Webhook Path

Status: high priority before chatbot integration.

What this means:

ClinicPilotX needs a controlled way for outside systems to submit leads.

Examples:

- ConvoCore chatbot submits a lead.
- A future ClinicPilotX chatbot submits a lead.
- A website contact form submits a lead.
- A simple test form submits a lead for demo purposes.

Expected lead data:

- Name.
- Email.
- Phone.
- Requested service.
- Preferred contact time.
- Original message or conversation summary.
- Source, such as `chatbot`, `website`, or `email`.
- Consent/contact permission fields.
- Client/clinic identifier.

Important:

This should go through a safe ClinicPilotX-controlled API, webhook, or backend function. Outside chatbots should not write directly into tables without validation.

### 5. Email AI Sorting Demo

Status: highest-value demo feature for Dr. Hong.

What this means:

ClinicPilotX watches a test inbox or connected clinic inbox and classifies incoming email.

Example categories:

- Spam / ignore.
- General inquiry.
- Real lead.
- Appointment request.
- Existing patient message.
- Billing/payment question.
- Urgent or high-priority message.

Near-term safe demo:

- Use a test inbox first.
- Send sample emails into that inbox.
- ClinicPilotX classifies them.
- Real leads become Leads records.
- Appointment requests become lead records or pending appointment requests.
- The original email content is saved to the lead timeline or communication record.

Do not connect Dr. Hong's real inbox until the test inbox flow works and Ross approves.

### 6. Automation Center Alignment

Status: audit before major build.

What this means:

The email sorting feature belongs inside or alongside Automation Center, but the current Automation Center must be audited before we trust it.

Codex needs to review:

- Which workflows already exist.
- Which are real vs demo.
- Which are enabled.
- Which reference old n8n logic.
- Which call Supabase/Lovable functions.
- Which might send SMS/email/payment/calendar actions.

Near-term Automation Center priorities:

- Email lead filtering.
- Chatbot/website lead intake.
- Staff notification settings.
- Appointment request handling.
- Missed appointment/no-show follow-up, later.

## Deferred Work

Not part of the immediate Dr. Hong demo unless Ross explicitly changes priority:

- Payments and Billing.
- Stripe/payment links.
- Video Consultation.
- WhatsApp.
- Messenger.
- Viber.
- Telegram.
- Live SMS campaigns.
- Live phone/AI calling.
- Google Calendar writes.

## Recommended Next Steps

1. Finish the current foundation follow-ups:
   - get Lovable SQL evidence for Internal Chat clinic_id rows,
   - fix/plan the `No Plan` subscription display issue,
   - fix/plan external conversation selection so notes can be tested.
2. Create a Lovable Plan-mode request for the clinic workspace/setup concept:
   - workspace switcher,
   - Dr. Colin Hong pilot workspace,
   - clinic profile,
   - team/users,
   - website,
   - services/pricing,
   - hours,
   - integration status,
   - Knowledge Base entry point.
3. Create a Lovable Plan-mode request for the per-clinic Knowledge Base.
4. Create a Lovable Plan-mode request for safe lead intake API/webhook.
5. Create a Lovable Plan-mode request for email AI sorting using a test inbox first.
6. Build the Dr. Hong demo path around test data before connecting live credentials.

## Demo Safety Rules

- Use test inbox first.
- Use test chatbot/form submissions first.
- Do not connect live SMS, WhatsApp, Messenger, payment, or calendar integrations yet.
- Do not connect Dr. Hong's real email until test classification works.
- Do not send external messages from ClinicPilotX until the outgoing-send rules are reviewed and approved.
