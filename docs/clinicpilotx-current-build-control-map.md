# ClinicPilotX Current Build Control Map

Last updated: 2026-06-28

## Purpose

This document gives Ross a plain-English control map for the current ClinicPilotX build.

The goal is to make sure Ross can always see:

- what phase we are in,
- what Codex is testing,
- what Lovable is building,
- what is done,
- what is blocked,
- what comes next,
- what a future assistant/human tester should verify.

## Current Stage

We are in the **multi-client foundation and safe internal workflow stage**.

This is not the final Automation Center build yet.

In plain English, we are making sure ClinicPilotX can safely support multiple clinic clients before we connect real automation sources such as email inboxes, chatbots, SMS, calendars, payments, or client credentials.

## Why This Stage Matters

ClinicPilotX is intended to be a subscription product.

That means each subscribing clinic needs its own workspace/account, with its own:

- clinic profile,
- users/team,
- leads,
- patients,
- appointments,
- payments,
- messages,
- knowledge base,
- connected inboxes,
- automation settings,
- subscription plan,
- future chatbot/API sources.

The current work is about preventing one clinic's data or automation from mixing with another clinic's data.

## Current Tenant / Clinic Foundation Status

Completed or mostly completed:

- Pilot clinic workspace exists for `Dr. Colin Hong (Pilot)`.
- Ross/teambuzzooka is seeded as owner/platform admin.
- Kizha is seeded as clinic admin.
- Main CRM tables have `clinic_id`.
- Existing rows were backfilled with pilot clinic id.
- Lead creation stamps active `clinic_id`.
- Patient creation stamps active `clinic_id`.
- Test/QA lead and patient rows are flagged so lead automation does not send.
- Appointment creation stamps active `clinic_id`.
- Payment/invoice creation stamps active `clinic_id`.
- Internal staff chat channels/messages now open and send safely for tested DM path.

Completed or partially completed in the latest pass:

- Settings now has a `Clinic Workspace` tab.
- Clinic Workspace is not added to the main left nav.
- Business Profile saves clinic facts.
- Services & Pricing can add clinic services/prices.
- Knowledge FAQs can add structured Q&A.
- Knowledge Sources shows a Phase B placeholder.
- AI Guardrails can save safety/tone/escalation rules.
- Team & Roles shows owner/admin members read-only.
- Integrations Status renders.

Still pending:

- Phase 1B.2 read filtering across existing modules.
- Workspace/clinic switcher UI.
- Full clinic onboarding/setup wizard.
- Per-clinic Knowledge Base file/URL/text source uploads and indexing.
- External conversation detail pane fix.
- Subscription/plan display consistency.

## Current Module Status

### Dashboard

Status: usable after earlier fixes, but should be retested after each foundation change.

Known issue:

- Subscription/plan display can still show `No Plan` unexpectedly.

### Leads

Status: improved and usable for manual QA/test leads.

Completed:

- Add Lead improved.
- Shared phone input.
- Service selector.
- Export dialog.
- Lead details/timeline improvements.
- QA/test lead safety guard.

Not done:

- Email-to-lead intake.
- Chatbot/API lead intake.
- Website contact form intake.
- Duplicate/spam handling.
- Full Automation Center alignment.

### Patients

Status: improved and usable for manual QA/test patients.

Completed:

- Add/Edit patient phone behavior.
- Export dialog.
- Patient detail panel basics.
- Patient archive/delete safety behavior.

Not done:

- Full patient profile build-out.
- Files/photos/attachments.
- Complete communications timeline.
- Patient knowledge/history summary.

### Appointments

Status: usable for TEST appointment QA.

Completed:

- Booking from patient detail.
- TEST toggle/default safety.
- Confirm/Cancel status tests.
- Export dialog.
- Calendar/list display improvements.
- Active clinic stamping.

Deferred:

- Live reminders.
- Google Calendar writes.
- Real appointment confirmation sends.
- Complex appointment request automation.

### Payments

Status: basic invoice/payment rows tested safely.

Completed:

- QA invoice create path stamps clinic id.
- No payment link was clicked in QA.

Deferred:

- Stripe/PayPal connection.
- Real payment link sends.
- Payment reminder automations.

### Communication Hub

Status: partially working.

Completed in latest pass:

- Internal Chat loads.
- Group channels render.
- Direct message with Kizha opens.
- Safe internal-only test message posts.
- No visible workflow side effects.

Still broken or not finished:

- External conversation selection still does not open the detail pane.
- Conversation notes cannot yet be QA-tested through the UI.
- Email inbox is not built yet.
- SMS/WhatsApp/Messenger/Viber/Telegram live sends are deferred.

### Automation Center

Status: high-risk area, not ready for live automations.

Known:

- Several workflows exist and some are active.
- Lead test-row safety was added to prevent QA leads from firing send workflows.
- Activity Logs are being used as a safety monitor.

Not done:

- Email AI sorting.
- Chatbot/contact-form intake controls.
- Safe workflow configuration redesign.
- Client-specific automation setup.
- Production n8n decision.

### Settings / Subscription

Status: Settings renders and now includes Clinic Workspace Phase A.

Completed:

- Business Profile.
- Branding.
- Business Hours.
- Services & Pricing.
- Team & Roles read-only view.
- Knowledge FAQs.
- Knowledge Sources placeholder.
- AI Guardrails.
- Integrations Status mirror.

Known issue:

- Plan/subscription state still appears inconsistent: `Professional` in some passes, `No Plan` in others.
- Automation Center can show `No Plan` and `7 / 5 Active`.
- Clinic Workspace Overview can briefly show a false setup score before data finishes loading.
- Services & Pricing delete action needs labels/tooltips and confirmation.

This should be fixed before plan-gated features are trusted.

## Near-Term Build Priorities

### Priority 1 - Finish Foundation Safety

Finish the remaining small blockers that affect trust:

- get Lovable SQL evidence for Internal Chat rows,
- fix or plan `No Plan` subscription display,
- fix external conversation detail selection,
- keep live sends disabled.

### Priority 2 - Clinic Workspace / Client Setup

Current status: Phase A is built and QA-passed with small follow-up fixes required.

Latest small fixes now QA-passed:

- plus/delete service icons have accessible labels,
- service delete has confirmation,
- false `0 of 6` checklist flash was not seen in the retest,
- integration status labels now avoid implying live verification.

Still needed:

- get Lovable SQL evidence for Phase A QA rows,
- fix subscription/entitlement display. Latest state: old `7 / 5 Active` changed to `4 / 5 Active`, but header, Automation Center, and Subscription page still show `No active plan` instead of `Professional`.

Broader client workspace concept Ross described:

- top-bar workspace/clinic switcher similar in spirit to the provided BuzzForge screenshot,
- create/select clinic workspace,
- clinic profile,
- logo,
- website,
- business hours,
- services/pricing,
- team/users/roles,
- integrations status,
- knowledge base status.

UX decision for the next plan:

- Do not add Knowledge Base as a new main left-nav item yet.
- Keep the left nav focused on daily CRM work.
- Put clinic setup under Settings as an owner/admin area.
- Add a top-bar clinic/workspace selector for switching clients.
- Add dashboard setup/knowledge-health cards later for quick visibility.

Likely Settings structure:

- Settings > General
- Settings > Notifications
- Settings > Integrations
- Settings > Profile
- Settings > Clinic Workspace
  - Overview / Setup Checklist
  - Business Profile
  - Branding
  - Business Hours
  - Services & Pricing
  - Team / Roles
  - Knowledge Base
  - AI Guardrails
  - Integrations Status

This is the product foundation for multiple subscribers.

### Priority 3 - Per-Clinic Knowledge Base

Create a per-clinic Knowledge Base that becomes the clinic's single source of truth for AI and automations.

This should power:

- chatbot answers,
- email sorting,
- appointment request understanding,
- service/pricing questions,
- staff summaries,
- future voice agents,
- future mobile app,
- future Automation Center actions.

### Priority 4 - Lead Intake API / Webhook

Build a safe intake path so external systems can create leads:

- ConvoCore chatbot,
- future ClinicPilotX chatbot,
- website contact forms,
- test demo form,
- later social/messaging sources.

### Priority 5 - Email AI Sorting Demo

Build the first demo automation using a test inbox:

- detect spam,
- detect real leads,
- detect appointment requests,
- create lead records,
- save original email context,
- route uncertain/medical-risk items to staff.

Do not connect Dr. Hong's real inbox until the test inbox flow works and Ross approves.

Clinic Workspace Phase A is the foundation for this. The demo should use the active clinic's business profile, services, FAQs, and AI guardrails so the email AI can classify messages using the right clinic context.

## What Ross Should See After Each Lovable Build

For every Lovable build, Codex should give Ross:

1. Plain-English purpose of the build.
2. What changed.
3. What Codex tested live.
4. What passed.
5. What failed or is still unknown.
6. What Ross or a human tester can check later.
7. What Lovable should do next.
8. GitHub docs updated and pushed.

## Human QA Packet Rule

Every module should eventually have a human QA checklist that a non-developer assistant can follow.

The checklist should include:

- setup/preconditions,
- exact clicks,
- safe dummy data to use,
- expected result,
- what not to click,
- screenshots or notes to capture,
- pass/fail fields.
