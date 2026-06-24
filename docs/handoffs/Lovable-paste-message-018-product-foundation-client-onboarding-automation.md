# Lovable Paste Message 018 - Product Foundation, Client Onboarding, and Automation

Please read this request and respond in Plan mode only. Do not build yet.

Important framing:

ClinicPilotX is a multi-client subscription product, not a custom one-off build for one clinic. Dr. Colin Hong is the first real pilot/test clinic workspace we want to use for a demo. The implementation must support many clinics/customers over time, each with its own setup, team, data, automations, integrations, and subscription plan access.

Codex completed read-only audits of Communication Hub and Automation Center.

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
- No visible workflow currently handles incoming email AI sorting, spam filtering, email-to-lead conversion, external chatbot lead intake, website contact-form intake, or client-specific knowledge base setup.

## Product Goal

Create the foundation for ClinicPilotX as a subscription product where each clinic can onboard and personalize the platform.

Dr. Colin Hong should be treated as the first pilot workspace only.

The product must eventually support:

- Multiple clinics/clients.
- Separate clinic data/workspaces.
- Plan-based feature access.
- Clinic-specific knowledge base and business settings.
- Clinic-specific team/staff permissions.
- Clinic-specific integrations such as email inbox, Google Calendar, chatbot/contact form, SMS later, etc.
- App-native automations where practical, preferably using Lovable/Supabase/Lovable Cloud rather than relying on old or expired n8n infrastructure.

## Requested Plan

Please propose a Plan-mode implementation for the ClinicPilotX product foundation.

Do not build yet.

Include exact files/components/functions/tables/migrations you would inspect or edit.

## Required Areas

### 1. Multi-Client / Workspace Structure

Please inspect the current app and explain whether it already has a true multi-client model.

We need to know:

- Does the app currently support multiple clinic accounts/workspaces?
- How is data separated by clinic/client?
- Are users tied to one clinic or multiple clinics?
- Is there an organization/workspace/clinic table already?
- Are leads, patients, appointments, messages, automations, and settings scoped by clinic?
- What RLS/policy assumptions exist?
- What would be needed before real paying clients can use separate accounts safely?

### 2. Clinic Onboarding / Setup Wizard

Design a first-run setup experience for a clinic.

It should collect and store:

- Clinic/business name.
- Logo/brand assets.
- Website URL.
- Public contact email.
- Phone number.
- Address/location.
- Time zone.
- Business hours.
- Services offered.
- Pricing / consultation fee guidance.
- Appointment types.
- Staff/team members.
- Staff roles/permissions.
- Notification preferences.
- Default templates.
- Clinic policies or FAQs.
- Knowledge base/business facts.
- Connected chatbot/contact-form/API sources.
- Connected inbox/test inbox.
- Google Calendar connection status.
- Automation preferences.

The setup should be simple enough for nontechnical clinic owners/staff to complete.

Please explain whether this belongs in Settings, a new Onboarding route, an Admin/Clinic Profile area, or another structure.

### 3. Client Knowledge Base

Each clinic needs a knowledge base or business profile that ClinicPilotX can use for AI features.

Examples:

- Services and descriptions.
- Pricing ranges.
- Frequently asked questions.
- Business hours.
- Booking rules.
- Cancellation/no-show policies.
- Insurance/payment/deposit notes.
- Doctor/provider bios.
- Location and parking notes.
- Tone/brand voice.
- Common patient instructions.
- What the AI should never say.

Please propose:

- Where this data should live.
- How staff can edit it.
- How it would be used by email AI sorting, chatbot intake, lead classification, and future automation.
- How to avoid mixing one clinic's knowledge with another clinic's knowledge.

### 4. Subscription Plans and Feature Gates

ClinicPilotX is intended to be sold as a subscription product with plan tiers.

Automation Center already shows plan labels like starter/professional/enterprise and Upgrade buttons.

Please inspect and explain:

- Where current plan information comes from.
- How plan gates are currently implemented.
- Which workflows/features are locked or unlocked by plan.
- Whether pricing/package definitions are hardcoded, in Supabase, or elsewhere.
- How this should connect to the marketing website pricing later.
- How clinic admins should see what is included vs requiring upgrade.

Do not build payment/subscription billing yet unless explicitly approved. This request is planning only.

### 5. Google Calendar Integration Planning

Clinics should eventually be able to connect Google Calendar so appointments can sync safely.

Please plan only. Do not enable live Google Calendar writes yet.

Plan should address:

- Per-clinic Google Calendar connection.
- Which staff calendar(s) can be selected.
- How ClinicPilotX internal appointments map to calendar events.
- How appointment requests differ from confirmed appointments.
- Whether Google Calendar sync is one-way or two-way.
- How disconnect/reconnect works.
- How TEST appointments are blocked from real calendar writes.
- How permission/scopes/secrets should be handled safely.

### 6. Email AI Sorting

Design an inbound email AI sorting feature.

Near-term safe demo:

- Use a test inbox first.
- Do not connect Dr. Hong's live email yet.
- Do not send outbound replies.

Expected categories:

- Spam / ignore.
- General inquiry.
- Real lead.
- Appointment request.
- Existing patient message.
- Billing/payment question.
- Urgent/high-priority message.

Required behavior:

- Incoming email is logged.
- AI classification is reviewable.
- Valid leads create Leads records or draft Leads records.
- Appointment requests link to Leads or a pending appointment-request queue.
- Original email content is saved to timeline/history.
- Staff can review and correct classification.
- Nothing sends automatically in this phase.

### 7. Lead Intake API / Webhook

Design a controlled API/webhook path for outside lead sources.

Expected sources:

- Dr. Hong's existing chatbot.
- ConvoCore chatbot.
- Future ClinicPilotX chatbot.
- Website contact form.
- Other third-party chatbots.

Expected payload fields:

- Clinic/workspace identifier.
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
- Authenticate/authorize incoming requests safely.

### 8. Automation Center Relationship

Explain how these product foundations should appear in Automation Center.

Possible new/updated workflow cards:

- Email AI Sorting.
- Email to Lead Intake.
- Chatbot Lead Intake.
- Website Contact Form Intake.
- Appointment Request Detection.
- Google Calendar Sync.
- Knowledge Base Assisted Responses.

For this phase, these should be inbound/review workflows only. No automatic outbound SMS/email should be activated.

Also explain how existing send-capable workflows should be protected while building this:

- Lead Acknowledgment.
- Smart Follow-up Sequence.
- Follow-up After Visit.
- Follow-Up Sequences.
- No-Show Recovery.
- Appointment Confirmation.
- Appointment Reminders.

### 9. Communication Hub Relationship

Explain whether classified email/chatbot/contact-form messages should appear in:

- Communication Hub inbox.
- Lead timeline.
- Automation Center review queue.
- Patient profile timeline.
- All of the above.

Please account for the current Communication Hub issues:

- external conversation detail did not open,
- internal direct message creation failed,
- no Email Inbox tab exists.

### 10. n8n / Automation Architecture

Ross no longer has access to the old n8n account, and local n8n is only for review/testing.

Please plan under this assumption:

- Do not rely on old/expired n8n infrastructure.
- Do not make production ClinicPilotX depend on laptop-hosted n8n.
- Old n8n workflows may be useful as reference/blueprints only.
- Prefer app-native Lovable/Supabase/Lovable Cloud automations where practical.
- If any workflow truly requires n8n later, explain why and what production-grade hosting/security/backup/cost plan would be required before activation.

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
- Do not hard-code Dr. Hong as the only clinic; he is the first pilot workspace.

## Deliverable

Please respond in Plan mode only with:

- Proposed architecture.
- Existing files/components/functions/tables/migrations to inspect.
- Any new database tables or columns needed.
- Any edge functions needed.
- How clinic/workspace separation will work.
- How onboarding/setup will work.
- How the knowledge base will work.
- How subscription plan gates will work.
- How the test inbox would work without live client credentials.
- How chatbot/contact-form submissions would authenticate safely.
- How Google Calendar should be planned but kept inactive.
- QA checklist.
- Risks and assumptions.
