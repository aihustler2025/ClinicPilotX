# Automation Center Read-Only Audit - 2026-06-24

## Scope

Codex performed a read-only audit of the published Automation Center:

`https://clinic-pilot-x.lovable.app/automation`

No switches were toggled. No configuration was saved. No test SMS, test email, payment, reminder, calendar, webhook, workflow activation, credential connection, or outbound message was triggered.

## Result

Partial / high-risk area.

Automation Center is not just a static mock. It has active workflow switches and Activity Logs showing prior workflow executions. It must be treated as a live-capable automation surface until Lovable/Supabase confirms exact sandbox/test suppression behavior.

## Summary

Visible plan:

- `Professional`

Visible active count:

- `7 / 13 Active`

Top-level tabs:

- `Workflows`
- `Activity Logs`

## Visible Workflow Inventory

### Lead Intake

- `Multi-Channel Sync` - enterprise / Upgrade
- `AI Voice Agent - Inbound` - enterprise / Upgrade
- `Lead Scoring & Assignment` - professional / Configure / switch off
- `Facebook Messenger Bot` - professional / Configure / switch off
- `WhatsApp Business Integration` - professional / Configure / switch off
- `Lead Acknowledgment` - starter / Configure / switch on

### Nurture

- `Advanced Lead Nurture AI` - enterprise / Upgrade
- `AI Voice Agent - Outbound` - enterprise / Upgrade
- `Smart Follow-up Sequence` - professional / Configure / switch on
- `Follow-up After Visit` - starter / Configure / switch on

### Patient Engagement

- `Follow-Up Sequences` - professional / Configure / switch on

### Patient-Engagement

- `No-Show Recovery` - professional / Configure / switch on

### Payments

- `Payment Reminder Sequence` - professional / Configure / switch off
- `Payment Receipt` - starter / Configure / switch off

### Reminders

- `Predictive Booking Suggestions` - enterprise / Upgrade
- `Appointment Confirmation` - starter / Configure / switch on / `Executions 21`
- `Appointment Reminders` - starter / Configure / switch on

### Reporting

- `Daily AI Briefing` - enterprise / Upgrade
- `Weekly Performance Report` - professional / Configure / switch off

## Activity Logs

Activity Logs show recent workflow executions, including:

- `Smart Follow-up Sequence` completed 5 days ago.
- `Lead Acknowledgment` failed 5 days ago.
- `Smart Follow-up Sequence` completed many times 12-13 days ago.
- `Lead Acknowledgment` completed and failed 12-13 days ago.
- `Appointment Confirmation` completed 28 days ago and 7 months ago.

Important implication:

The Automation Center is connected to real workflow execution records. It should not be treated as a harmless mock UI.

## Configuration Panels Inspected

### Lead Acknowledgment

Purpose:

- Automatically send acknowledgment when a new lead is captured.

Findings:

- Has AI-generated message toggle.
- Has SMS template with variables:
  - `{{name}}`
  - `{{service}}`
  - `{{clinic_name}}`
- Has Email template.
- Has previews for SMS and Email.
- Has `Send Test SMS`.
- Has `Send Test Email`.
- SMS testing copy says to use Twilio test number `+15005550006` or a real number.
- Email testing copy says emails are currently only logged, not sent.

Risk:

- `Send Test SMS` appears live-capable or Twilio-capable. Do not click without explicit approval and verified sandbox/test number behavior.

Demo relevance:

- This is related to lead intake, but it is an outbound acknowledgment workflow, not the email AI sorting feature Ross wants to demo first.

### Lead Scoring & Assignment

Purpose:

- Automatically score leads and assign to staff.

Findings:

- Configure panel only says:

`Configuration not available for this workflow yet.`

Demo relevance:

- Useful conceptually, but not demo-ready from the current UI.

### Appointment Confirmation

Purpose:

- Send confirmation when appointment is booked.

Findings:

- Active.
- Shows `Executions 21`.
- Has SMS and Email templates.
- Has timing options:
  - Immediate.
  - Delayed.
  - After Payment.
  - On Status Change.
- Current selection says:

`Confirmations will be sent 5 minutes after appointments are booked.`

- Has `Send Test SMS`.
- Has `Send Test Email`.

Risk:

- This is clearly a send-capable workflow. It should remain gated for real client data until TEST suppression and live credential status are verified.

### Smart Follow-up Sequence

Purpose:

- Automatically nurture cold leads with a series of re-engagement messages.

Findings:

- Active.
- Trigger: `Cold (no activity 30+ days)`.
- Inactivity threshold shown as `7 days`.
- Has Day 1, Day 3, and Day 7 follow-up message areas.
- SMS preview shown.

Risk:

- Follow-up messaging should not be used with real leads until consent, opt-out, source-of-truth, and live-send safety are defined.

### No-Show Recovery

Purpose:

- Automatically reach out to patients who missed appointments to reschedule.

Findings:

- Active.
- Has delay setting.
- Copy says delay can be set to `0` to send immediately.
- Has SMS template.

Risk:

- High. It can imply immediate outbound SMS after no-show detection. Keep gated until safety/consent and test suppression are verified.

## Dr. Hong Demo Impact

No visible workflow currently represents:

- incoming email inbox monitoring,
- AI email spam/lead classification,
- email-to-lead conversion,
- chatbot/API lead intake,
- contact-form-to-lead intake,
- clinic/client-specific knowledge base setup.

Therefore, the Dr. Hong demo foundation needs a new planned build or a major extension of existing Automation Center behavior.

## Recommended Next Lovable Request

Ask Lovable in Plan mode only to design the Dr. Hong demo foundation:

- Client/clinic account setup.
- Test inbox email AI sorting.
- Classified email-to-lead creation.
- Appointment request detection from emails.
- Lead intake API/webhook for ConvoCore, other chatbots, website forms, and future ClinicPilotX chatbot.
- Clear no-live-send protections.
- Review queue / audit trail for classified messages.
- How this ties into Automation Center and Communication Hub.

## Deferred

Do not build or activate yet:

- WhatsApp.
- Messenger.
- Viber.
- Telegram.
- Live SMS campaigns.
- Live email sends.
- Payments.
- Video consultation.
- Google Calendar writes.
- Voice calling.

## Safety

Codex did not click:

- Send Test SMS.
- Send Test Email.
- Save Configuration.
- Workflow switches.
- Upgrade.
- Payment actions.
- Calendar actions.
- Any credential connection.
