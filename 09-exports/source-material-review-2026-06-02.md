# ClinicPilotX Source Material Review

Date: 2026-06-02
Reviewer: Codex

## Scope

Ross provided 30 old/source files from `D:\PROJECTS\CLINICPILOT X (Old)`. These are now treated as reference materials for the new official ClinicPilotX project.

Official active workspace:

`D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`

Important: these documents may describe earlier architecture assumptions. Use them to understand product intent, workflows, modules, language, pricing, and launch expectations. Do not blindly reuse old stack choices, old credentials, old generated Markdown, or old repo history.

## Files Reviewed

### Final

- `ClinicPilot GPT Agent – System Instructions.docx`
- `ClinicPilot Possible Video Titles.docx`
- `ClinicPilot PriorityBook Documentation.docx`
- `ClinicPilot Product Documentation (For Investors).docx`
- `ClinicPilot Suggested Pricing Packages.docx`
- `ClinicPilot Website Pages.docx`
- `ClinicPilot_Master_Checklist_Prefilled.xlsx`
- `ClinicPilot – System Documentation (Developer Handbook).docx`
- `ClinicPilot Feature Map.docx`

### Misc

- `ClinicPilot_Email_and_SMS_Templates.docx`
- `ClinicPilot_Feature_Map.docx`
- `ClinicPilot_Incoming_Workflow.docx`
- `ClinicPilot_Integrations_and_Credentials.docx`
- `ClinicPilot_Outgoing_Workflow.docx`
- `ClinicPilot (Website Copies).docx`
- `ClinicPilot Complete Documentation (Oct-17-2025).docx`
- `ClinicPilot_Automation_Center_Settings_Schema.docx`
- `ClinicPilot_Developer_Handoff_n8n.docx`

### Misc 2

- `Checklist_ClinicPilot X – AI-Powered Front Desk Assistant.docx`
- `ClinicPilot_Build_Checklist (1).xlsx`
- `ClinicPilot X – AI-Powered Front Desk Assistant.pdf`
- `ClinicPilot Ecosystem.pdf`
- `ClinicPilot_X_Handoff_Sheet.docx`
- `ClinicPilot_X_Voice_Assistant_Use_Cases.docx`
- `FULL DOCUMENTATION_ClinicPilot X – AI-Powered Front Desk Assistant.docx`
- `N8N Expert Response to Questions.docx`
- `SYSTEM DOCUMENTATION_ClinicPilot X – AI-Powered Front Desk Assistant.docx`
- `System instructions_ClinicPilot X – AI-Powered Front Desk Assistant.docx`
- `TABLE OF CONTENTS_ClinicPilot X – AI-Powered Front Desk Assistant.docx`
- `Title_ ClinicPilot X – n8n Automation Blueprint & Handoff Pack.docx`

## Duplicate / Variant Notes

- `ClinicPilot Website Pages.docx` and `ClinicPilot (Website Copies).docx` appear to be duplicate or near-duplicate website copy sources.
- `ClinicPilot Product Documentation (For Investors).docx` and `ClinicPilot Complete Documentation (Oct-17-2025).docx` appear to be very similar investor/product overview sources.
- `SYSTEM DOCUMENTATION_ClinicPilot X – AI-Powered Front Desk Assistant.docx` and `System instructions_ClinicPilot X – AI-Powered Front Desk Assistant.docx` appear to be duplicate or near-duplicate large system documents.
- `ClinicPilot Feature Map.docx` and `ClinicPilot_Feature_Map.docx` overlap as feature-map references.
- `ClinicPilot_Build_Checklist (1).xlsx` appears to contain blank/empty sheets when read through the workbook extractor.
- `ClinicPilot_Master_Checklist_Prefilled.xlsx` contains useful MVP checklist rows and should be treated as the better checklist source.

## Durable Product Intent

ClinicPilotX is an AI-powered front desk and growth assistant for clinics and appointment-based service businesses.

Target customers include:

- Plastic surgery practices
- Cosmetic clinics
- Dental clinics and dental surgery offices
- Dermatology practices
- Med spas
- Beauty/wellness businesses
- Salons and other appointment-based service businesses

Core value proposition:

- Capture more leads across channels.
- Respond faster to patients/prospects.
- Reduce front desk workload.
- Reduce no-shows.
- Improve follow-up consistency.
- Prioritize high-value opportunities.
- Turn the front desk into an automation-assisted growth system.

## Core Product Modules From Source Materials

### Unified Lead Capture

Source materials consistently describe intake from multiple channels into one lead system:

- Email/contact form
- Chatbot/website assistant
- Voice/phone intake
- Social lead ads
- Manual/staff entry
- Future messaging channels such as WhatsApp/Messenger

For current Lovable QA, verify whether Leads are real backend records, what fields exist, and which source channels are actually connected vs only planned.

### AI Intake / Classification

Sources describe classifying incoming messages into categories such as credible lead, spam, unclear case, existing patient, or vendor/general message.

For current Lovable QA, verify whether classification exists, whether it is rule-based or AI-based, and whether it writes a status/source/priority field to the database.

### Patient Acknowledgment

Source docs expect fast auto-acknowledgment to the patient/prospect by email and/or SMS, commonly within 5 minutes.

For current Lovable QA, verify whether any acknowledgment workflow exists, whether templates exist, and whether messages are actually sent or only represented in UI.

### Staff Alerts

Source docs expect staff alerts when a lead arrives, typically by email/SMS with extracted lead details.

For current Lovable QA, verify whether there is a notification log, staff alert configuration, and any real integration behind it.

### Smart Booking / Appointment Requests

Source docs describe appointment request handling, calendar checks, booking holds, appointment confirmations, and reminders.

The `N8N Expert Response to Questions` doc clarifies an important product decision: do not auto-book the first available slot. Instead, collect 2-3 preferred dates/times and let staff confirm the final slot. The system should support a single shared calendar first and later multiple providers/practitioners.

For current Lovable QA, verify whether appointments are confirmed bookings, appointment requests, or mock calendar items.

### Payment / Deposit Flow

Source docs mention Stripe/PayPal payment links and booking deposits.

The expert-response doc states an intended policy: fixed $100 deposit, mandatory before finalized booking, no pay-on-arrival, no installment payments.

For current Lovable QA, do not activate payment integrations. Verify whether payments are real, mocked, planned, or only UI placeholders.

### Reminders / No-Show Logic

Source docs mention reminder cadence such as 48h, 24h, and 2h before appointment, with quiet-hour rules and per-clinic customization.

The expert-response doc says no-show handling should not auto-reschedule. It should send a follow-up explaining that the deposit is forfeited and a new deposit is required.

For current Lovable QA, verify reminder settings, message templates, and whether reminders actually send.

### Outgoing Follow-Up

Sources describe identifying old/stale leads and sending follow-up email/SMS/AI call attempts. The master checklist mentions 3-day-old leads and 2-3 AI call attempts within 7 days.

For current Lovable QA, verify whether follow-up workflows are real or planned, and whether there is an automation log/status history.

### Review / Reputation Requests

Sources describe post-consult and post-procedure review request messages.

For current Lovable QA, verify whether review automation exists or is planned only.

### PriorityBook

PriorityBook is a smart prioritization/scoring concept for incoming appointment requests and services.

Source concepts:

- Score requests by service tier, revenue potential, urgency/intent, doctor involvement, schedule fit, and returning-patient bonus.
- Help staff prioritize high-value or time-sensitive services.
- Integrate with scheduling/calendar logic.
- Keep initial implementation rule-based before advanced AI scoring.

For current Lovable QA, verify whether PriorityBook exists, whether scoring is visible, whether service configuration exists, and whether any scores are stored in the backend.

### Automation Center

The Automation Center settings schema source is useful for product structure.

Settings categories include:

- Acknowledgment delay
- Channel toggles: email, SMS, calls
- Follow-up limits and quiet hours
- Booking search radius and hold duration
- Deposit amount
- Review timing
- PriorityBook weights
- Per-clinic overrides

For current Lovable QA, verify whether the current app has an Automation Center, what toggles/settings exist, and whether settings persist per clinic.

### Voice Assistant

Voice assistant sources mention VAPI, inbound/outbound calls, missed call recovery, lead qualification, appointment requests, and follow-up calls.

For current Lovable QA, verify whether voice assistant UI is real, configured, mock-only, or planned. Do not connect/activate VAPI without explicit approval.

## Integrations Mentioned In Source Materials

Potential integrations from source docs:

- Gmail / Google Workspace
- Google Sheets as earlier data store concept
- Google Calendar
- Calendly as possible early scheduling path
- Stripe
- PayPal
- Twilio
- VAPI
- Voiceflow or chatbot platform
- Facebook / Instagram Lead Ads
- n8n workflows
- Optional dashboard DB: Baserow, Airtable, or Supabase
- WhatsApp/Messenger as future or constrained channels

Important: many source docs assume n8n + Google Sheets. The current Lovable project may instead use Supabase, Lovable Cloud, or another backend. Verify current backend before approving any architecture work.

## Master Checklist Extract

Useful source checklist from `ClinicPilot_Master_Checklist_Prefilled.xlsx`:

| ID | Area | Feature | Task | Source Status | Priority |
| --- | --- | --- | --- | --- | --- |
| CL-001 | Incoming | Unified Intake | Merge Email, Chatbot, Voice into one Leads sheet | In Progress | P1 |
| CL-002 | Incoming | Acknowledgment | Send auto-email + SMS to patients within 5 minutes | Not Started | P1 |
| CL-003 | Incoming | Staff Alerts | Send auto-email + SMS to clinic staff for new lead | Not Started | P1 |
| CL-004 | Booking | Smart Booking | Google Calendar freeBusy check + propose slots | Not Started | P1 |
| CL-005 | Booking | Payments | Generate Stripe Checkout link + webhook for confirmation | Not Started | P1 |
| CL-006 | Booking | Status Tracking | Implement HOLD -> AWAITING_PAYMENT -> CONFIRMED flow | Not Started | P1 |
| CL-007 | Booking | Reminders | Email/SMS reminders 2d/1d/2h before appointment | Not Started | P1 |
| CL-008 | Outgoing | Follow-ups | Identify 3-day-old leads and send follow-up email + AI call | In Progress | P2 |
| CL-009 | Outgoing | Call Cadence | 2-3 AI call attempts within 7 days | Not Started | P2 |
| CL-010 | Outgoing | Outcome Logging | Mark Interested/Not Interested/No Response | Not Started | P2 |
| CL-011 | Premium | Reviews | Post-consult and post-procedure review request SMS/email | Not Started | P3 |
| CL-012 | Premium | Lead Scoring | Implement PriorityBook scoring formula | Not Started | P3 |
| CL-013 | Premium | Missed Call Recovery | Auto-SMS + optional AI callback for missed calls | Not Started | P3 |
| CL-014 | Premium | Two-way SMS | Parse reschedule replies and update Calendar | Not Started | P3 |
| CL-015 | Premium | Social Ad Leads | Connect Facebook/Instagram Lead Ads to Leads sheet | Not Started | P3 |
| CL-016 | Dashboard | Automation Center | UI toggles for cadences, channels, ACK delays | Not Started | P3 |
| CL-017 | Future | Doctor App | Voice dictation -> AI care notes -> patient aftercare emails | Not Started | P4 |

## Pricing / Packaging Direction

Source pricing documents mention tiering around starter/professional/premium-style packages. Feature differentiation appears to be based on lead capture, dashboard, automations, integrations, voice/SMS, PriorityBook, and premium channels.

Pricing should be revisited after the live Lovable audit shows what is actually built and what is still aspirational.

## Website / Marketing Direction

Website sources include pages for:

- Home
- About
- Features
- Integrations
- FAQ
- Pricing
- Contact/demo request

Marketing website should remain secondary until product/dashboard functionality is audited and stabilized.

## QA Implications For Current Lovable Project

Before approving any Lovable build, Codex should verify:

1. Current project identity, preview URL, and project ID.
2. Whether the app is dashboard/admin/staff portal/marketing site or all-in-one.
3. Backend provider and database schema.
4. Auth and roles.
5. Every left-navigation route/module.
6. Which modules persist real data.
7. Which modules are mock/demo/static.
8. Whether Leads exist as real records and what source/status/priority fields exist.
9. Whether Appointments are real bookings, requests, or mock data.
10. Whether Calendar connects to real availability or is UI-only.
11. Whether Automation Center settings exist and persist.
12. Whether payment, SMS, email, VAPI, chatbot, n8n, Meta, WhatsApp/Messenger, and calendar integrations are real, partial, or planned.
13. Whether any paid integrations are active.
14. Whether any sensitive credentials are stored in UI, code, or docs.
15. Console errors, broken buttons, broken forms, and route/auth issues.

## Recommended Use In New Project

Use these source materials as a product reference layer, not an implementation authority.

The immediate plan should be:

1. Audit the live Lovable project.
2. Compare its actual modules against this source-material feature map.
3. Mark each module as Verified, Claimed, Mock/Demo, Incomplete, Planned, or Not Present.
4. Build the official Product Spec from verified app behavior plus durable product intent from these docs.
5. Only then approve focused Lovable build prompts.
