# Patient Profile and Leads Intake Roadmap

Last updated: 2026-06-19

## Purpose

This document captures Ross's intended direction for two connected ClinicPilotX areas:

- Patient profiles inside the Patients module.
- Leads intake across email, contact forms, chatbot, social channels, SMS, and phone.

This is a planning and QA roadmap. It is not a Lovable build request yet.

## Patient Profile Direction

In the Patients module, clicking a patient card or patient name opens a patient side panel. This side panel should become the practical patient profile surface for staff.

Current verified / partially verified profile surface includes:

- Patient identity and patient ID.
- Contact information.
- Formatted phone display.
- Summary metrics such as visits and total spent.
- Medical information area.
- Appointments tab.
- Transactions tab.
- Action buttons: `Call`, `Message`, `Video`, `Edit`, and `Book Appointment`.

## Patient Profile QA / Build Classification

### Ready For Near-Term QA

These are safe to test with dummy data:

- Open patient profile from patient card/list.
- Edit patient demographics and notes.
- Validate phone inputs.
- Verify appointments tab shows related appointments.
- Verify transactions tab shows related transactions or empty state.
- Test `Book Appointment` from patient profile with TEST mode on.
- Confirm profile updates persist after closing and reopening.

### Near-Term Build / Polish Candidates

These can be improved before live integrations are connected:

- Make the profile feel like a complete patient record, not only a demo side panel.
- Add clearer sections for:
  - Contact details.
  - Treatment interests.
  - Medical notes.
  - Consultation notes.
  - Uploaded files/photos placeholder.
  - Communication timeline placeholder.
  - Appointment history.
  - Payment/transaction history.
- Replace native browser delete confirmation with an in-app confirmation modal later if needed.
- Add stronger empty states that explain what staff should expect once real data exists.

### Later / Depends On Other Modules

These should not be fully activated until their owning modules are audited and safe:

- `Call`: depends on Communication Hub, phone provider, Twilio/VAPI strategy, permissions, consent, logging, and no-live-call safeguards.
- `Message`: depends on Communication Hub, SMS/email/channel consent, templates, opt-out/suppression handling, and delivery logs.
- `Video`: depends on Video Consultation module, meeting/session provider choice, consent, and patient link workflow.
- Files/photos: depends on storage bucket design, permissions, security rules, file-size/type policy, and patient privacy handling.

## Patient Profile Product Intent

The patient profile should eventually answer these staff questions:

- Who is this person?
- How did they come in?
- What did they ask for?
- What services or treatments are they interested in?
- What conversations have happened?
- What files/photos have they submitted?
- What appointments have they booked or missed?
- What payments, deposits, or invoices exist?
- What follow-up is due?
- What should staff do next?

## Leads Intake Direction

Ross clarified that the Leads module is nowhere near complete. Current work has improved the manual-entry foundation, but the final system must capture leads from multiple real-world channels.

Expected lead sources:

- Manual entry by staff.
- Website contact page submissions.
- Direct email inquiries sent to the clinic email address.
- AI-filtered email intake, separating spam/non-leads from legitimate lead inquiries.
- Chatbot submissions from the future ClinicPilotX chatbot project.
- SMS messages.
- Phone calls and AI voice intake.
- Facebook.
- WhatsApp.
- Viber.
- Other social/messaging channels as the product grows.

## Leads Intake Product Intent

A lead record should capture:

- Name.
- Email.
- Phone.
- Preferred contact method.
- Preferred contact time.
- Requested service or concern.
- Source channel.
- Original message or conversation summary.
- Consent/contact permission state.
- Attachments or photos when available.
- AI classification or qualification notes.
- Spam/invalid-lead filtering result.
- Timeline of all interactions.
- Follow-up status and next action.

## Email / Contact Form Intake Concept

Expected future flow:

1. A prospect submits a website contact form or emails the clinic.
2. Intake automation checks the message.
3. AI or rule-based filtering separates spam, irrelevant messages, and actual leads.
4. Valid lead inquiries are converted into Leads records.
5. The original message is saved into the lead timeline.
6. Staff can review, edit, contact, convert, or schedule the lead.
7. No outbound email/SMS/call should send unless the workflow is explicitly approved and safely configured.

## Chatbot Intake Concept

The future chatbot project should be able to create leads in ClinicPilotX through a controlled integration path.

Expected chatbot lead payload:

- Name.
- Email.
- Phone.
- Requested service.
- Preferred appointment/contact time.
- Conversation transcript or summary.
- Source: chatbot.
- Bot/project identifier if there are multiple chatbot deployments.
- Consent/contact permission fields.

The chatbot should not directly bypass ClinicPilotX validation rules. It should submit through an API, webhook, Supabase function, or approved backend route that normalizes phone numbers, validates required fields, and logs source/timeline data.

## Social / Messaging Intake Concept

Future channels may include Facebook, WhatsApp, Viber, SMS, and other messaging platforms.

Before production activation, each channel needs:

- Account/project ownership confirmed.
- Cost reviewed and approved.
- Consent and opt-out handling.
- Message logging policy.
- Spam and duplicate handling.
- Rate limits and failure handling.
- Staff notification rules.
- Automation Center settings.

## Phone / AI Voice Intake Concept

Future phone intake may use VAPI, Twilio, or another provider.

Before production activation:

- Phone numbers must be stored in E.164 for reliable dialing.
- Staff-facing display should remain friendly, such as `+1 (213) 555-0199`.
- Consent, call recording, disclosures, and jurisdiction-specific requirements must be reviewed.
- Test calls must use approved test numbers only.
- No live calling campaign should run without explicit Ross approval.

## Automation Center Relationship

The Automation Center should eventually control or reflect the intake automations behind these lead sources.

Possible Automation Center settings:

- Enable/disable channel intake.
- Configure business hours and quiet hours.
- Configure AI spam filtering strictness.
- Configure staff notifications.
- Configure auto-assignment rules.
- Configure follow-up timing.
- Configure source-specific templates.
- Configure whether a channel can create leads automatically or requires staff review first.

## Current Status

Manual Leads foundation has been improved:

- Country-aware phone entry.
- E.164 storage.
- Friendly U.S./Canada display in detail paths.
- Service selection.
- Timeline and activity views.
- Export dialog UI.
- Edit safety for tested status/temperature behavior.

Still pending:

- Full intake architecture.
- Contact form/email intake.
- Chatbot integration.
- SMS/social/phone intake.
- AI filtering and classification.
- Communication timeline connected to real messages.
- Attachment/photo intake.
- Lead-to-patient-to-appointment downstream flow hardening.

## Recommended Order

1. Finish safe Patients profile QA and patient-to-appointment regression.
2. Finish Appointments module QA with TEST mode.
3. Audit Communication Hub before activating message/call actions.
4. Audit Automation Center settings and workflow safety.
5. Design the lead intake API/webhook contract.
6. Build one safe intake source first, likely website/contact email or chatbot test payload.
7. Add additional channels only after the first intake path is stable.

## Not Yet Approved

Do not build or activate:

- Live email sends.
- Live SMS sends.
- Live phone calls.
- Paid messaging integrations.
- Production chatbot API writes.
- Social messaging integrations.
- Automatic lead follow-up sequences.

These require explicit approval after architecture, safety, cost, and QA review.
