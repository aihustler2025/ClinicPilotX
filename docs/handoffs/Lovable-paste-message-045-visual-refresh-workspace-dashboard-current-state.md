# Lovable Paste Message 045 - Visual Refresh / Workspace UX Plan, Current State

Please read this design/product brief and respond in Plan mode only. Do not build yet.

This refresh replaces the older visual refresh request where Auto-Assignment was still listed as broken. Auto-Assignment and subscription display are now stable enough to resume UX planning.

## Current Verified State

Codex QA now confirms:

- Dashboard/header shows `Professional`.
- Auto-Assignment/header shows `Professional`.
- Auto-Assignment loads and shows `Assignment Rules (0)` plus `Staff Configuration (2)`.
- Auto-Assignment rule create/toggle/delete and staff max-conversation persistence passed QA in Request 043.
- Automation Center shows `Professional` and `7 / 13 Active`.
- Subscription page shows `Current Plan: Professional` and `Status: Active`.
- Recent read-only QA did not create workflow executions or live-send side effects.

Reference QA reports:

- Auto-Assignment follow-up QA: https://github.com/aihustler2025/ClinicPilotX/blob/main/09-exports/request-043-auto-assignment-phase-a-followup-qa-2026-06-30.md
- Subscription safe-view QA: https://github.com/aihustler2025/ClinicPilotX/blob/main/09-exports/request-044-subscription-safe-view-qa-2026-06-30.md

## Reference Images

These are inspiration references only. Do not copy them exactly, clone another product, or import unrelated ecommerce/finance concepts. Translate the strongest ideas into ClinicPilotX's healthcare CRM/subscriber-workspace context.

Metronic-style references:

- Teams / members cards: https://github.com/aihustler2025/ClinicPilotX/blob/main/docs/design-references/clinic-workspace-dashboard-refresh-2026-06-29/metronic-teams.png
- Company profile / account profile: https://github.com/aihustler2025/ClinicPilotX/blob/main/docs/design-references/clinic-workspace-dashboard-refresh-2026-06-29/metronic-company-profile.png
- API keys / webhooks: https://github.com/aihustler2025/ClinicPilotX/blob/main/docs/design-references/clinic-workspace-dashboard-refresh-2026-06-29/metronic-api-keys.png
- Integrations cards: https://github.com/aihustler2025/ClinicPilotX/blob/main/docs/design-references/clinic-workspace-dashboard-refresh-2026-06-29/metronic-integrations.png
- Notifications settings: https://github.com/aihustler2025/ClinicPilotX/blob/main/docs/design-references/clinic-workspace-dashboard-refresh-2026-06-29/metronic-notifications.png
- Light sidebar / dashboard widgets: https://github.com/aihustler2025/ClinicPilotX/blob/main/docs/design-references/clinic-workspace-dashboard-refresh-2026-06-29/metronic-light-sidebar-dashboard.png

Vykins-style dashboard references:

- Home dashboard: https://github.com/aihustler2025/ClinicPilotX/blob/main/docs/design-references/clinic-workspace-dashboard-refresh-2026-06-29/vykins-home-dashboard.png
- Products dashboard: https://github.com/aihustler2025/ClinicPilotX/blob/main/docs/design-references/clinic-workspace-dashboard-refresh-2026-06-29/vykins-products-dashboard.png
- Wallet dashboard: https://github.com/aihustler2025/ClinicPilotX/blob/main/docs/design-references/clinic-workspace-dashboard-refresh-2026-06-29/vykins-wallet-dashboard.png

Clerivo-style integrations reference:

- Integrations grid/status cards: https://github.com/aihustler2025/ClinicPilotX/blob/main/docs/design-references/clinic-workspace-dashboard-refresh-2026-06-29/clerivo-integrations.png

## Product Context

ClinicPilotX is a subscription-based clinic CRM and automation platform.

Each clinic/subscriber needs a friendly workspace setup experience where the owner/admin can configure:

- clinic/business profile,
- logo and brand color,
- website and public links,
- business hours,
- services and pricing,
- team/users/roles,
- knowledge FAQs,
- future knowledge sources such as files, URLs, text notes, and website pages,
- AI guardrails and escalation rules,
- integrations readiness/status,
- API/webhook readiness for chatbot/contact-form intake,
- subscription/plan status.

Ross's concern: the current Clinic Workspace inside Settings feels buried, developer-like, and not friendly enough for a subscriber onboarding/setup experience. He wants Lovable to use its UX/UI strength rather than Codex over-prescribing layout.

## UX Direction Requested

Please propose a better ClinicPilotX UX direction.

Do not assume the current Settings > Clinic Workspace layout is the final answer.

Do not simply polish the existing subtabs.

Use Lovable's product/design judgment and propose the best subscriber-facing experience for clinic owners/admins.

The answer could involve:

- a dedicated workspace setup route,
- an onboarding/setup wizard,
- a workspace/account area under System,
- dashboard setup prompts/cards,
- a top-bar clinic/workspace selector,
- better owner/admin settings IA,
- or a combination.

Codex is intentionally not prescribing exact layout. Please propose the experience.

## Visual Style Preferences To Consider

Ross likes these qualities from the references:

- cleaner light-gray page background with white panels/cards,
- modern panels with subtle shadows,
- clearer spacing and segmentation,
- stronger visual hierarchy with larger, confident summary numbers,
- a fresher accent color than the current dull blue,
- top search field and cleaner top bar patterns,
- collapsible or cleaner left sidebar patterns,
- dashboard cards that feel more modern and less flat,
- integrations shown as compact cards with status chips/toggles,
- dashboard widgets for recent activity, lead sources, upcoming consultations/appointments, and setup progress,
- left/right carousel controls where useful instead of awkward horizontal scrolling.

Do not copy exact brand assets, logos, illustrations, or proprietary layouts.

## Areas To Include In The Plan

### 1. Clinic Workspace / Subscriber Setup

Propose how a new clinic owner/admin should configure their account after subscribing.

The flow should feel chronological and nontechnical.

Example setup areas:

- Profile basics,
- Branding,
- Hours,
- Services/pricing,
- Team,
- Knowledge base starter content,
- AI guardrails,
- Integrations readiness,
- API/webhook readiness for website forms and chatbot intake.

### 2. Dashboard/Homepage Refresh

The current dashboard feels too plain and dull.

Please propose a dashboard refresh that can support near-term Dr. Hong demo needs without creating fake data.

Potential widgets:

- lead source summary: chatbot, email/contact form, manual, missed calls, Facebook/Instagram later, WhatsApp/SMS later,
- recent lead activity,
- upcoming appointments / video consultations,
- setup completion / workspace health,
- knowledge base health,
- automation readiness/status,
- recent internal activity.

Important: use truthful data only. If a feature is not connected yet, label it as not connected, coming soon, or setup needed. Do not invent fake production metrics.

### 3. Integrations and API/Webhook Area

Ross likes the integrations card/grid references.

Please propose where integrations should live and how they should be represented for:

- email inbox connection,
- Google Calendar,
- Twilio/SMS,
- Vapi/voice,
- Stripe/payment links,
- Facebook/Instagram/Messenger,
- WhatsApp/Telegram/Viber later,
- chatbot/contact-form API/webhooks,
- future ClinicPilotX chatbot.

Important: do not connect live credentials or create real sends in this phase.

### 4. Automation Center Visual Direction

The current Automation Center workflows are acceptable functionally but not visually strong enough.

Please propose how workflow cards/statuses could be improved using the reference direction:

- clearer status chips,
- plan gates,
- connected/not connected status,
- test/safe mode visibility,
- setup-required states,
- cleaner cards.

Do not implement workflow execution changes in this phase.

## Safety / Scope Rules

Plan mode only. Do not build yet.

Do not trigger or connect:

- live email inboxes,
- SMS/calls,
- payment links,
- Google Calendar writes,
- real webhooks,
- chatbot/API intake,
- workflow test sends,
- live credentials.

Do not use fake metrics as if they are real.

Do not remove existing CRM functionality.

Do not make this depend on n8n.

Keep Lovable Cloud/Supabase as the preferred backend path.

## Response Requested

Please respond with:

1. Recommended UX/IA direction in plain English.
2. Which areas/routes should change.
3. What should happen to the current Clinic Workspace tab.
4. Suggested dashboard/homepage refresh plan.
5. Suggested integrations/API/webhook visual plan.
6. Suggested Automation Center visual plan.
7. Phased implementation plan.
8. Exact files/tables likely involved.
9. What remains out of scope.
10. QA checklist after build.
11. Any questions for Ross before build approval.
