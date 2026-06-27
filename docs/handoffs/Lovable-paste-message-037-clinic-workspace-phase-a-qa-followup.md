# Lovable Paste Message 037 - Clinic Workspace Phase A QA Follow-Up

Please read this QA follow-up and respond in Plan mode only. Do not build yet.

Codex tested the published Clinic Workspace Phase A build. Overall result: pass with small follow-up polish required before we use this setup for the Dr. Hong email AI demo.

## What Passed

- Clinic Workspace is correctly under Settings, not the main left nav.
- Sub-nav renders: Overview, Business Profile, Branding, Business Hours, Services & Pricing, Team & Roles, Knowledge FAQs, Knowledge Sources, AI Guardrails, Integrations Status.
- URL deep links work via `?tab=clinic-workspace&section=...`.
- Business Profile save persisted after reload.
- Services & Pricing add path persisted after reload.
- Knowledge FAQ add path persisted after reload.
- Knowledge Sources correctly shows a Phase B placeholder.
- AI Guardrails save persisted after reload.
- Team & Roles renders read-only.
- No live send/payment/calendar/workflow action was clicked.
- No visible fresh Automation Center workflow activity appeared during QA.

## Issues To Plan

### 1. Services row actions need labels and safer delete

Existing service rows have an icon-only trash button with no visible label/tooltip/aria label.

Codex clicked one during QA and got `Deleted`; after reload, the row was gone.

Please plan:

- Add accessible labels/tooltips:
  - `Delete service`
  - `Add service`
- Add an in-app confirmation dialog before deleting an existing service.
- Prefer inactive/archive behavior if that already exists or is safer than hard delete.

### 2. Overview checklist briefly flashes false `0 of 6`

On one navigation, Overview showed `0 of 6 steps complete` before correcting to `4 of 6`.

Please plan:

- Show a loading skeleton or `Checking setup...` until the underlying clinic workspace data has loaded.
- Do not show a false zero progress state while data is still loading.

### 3. Integrations Status wording should be safer

The page shows:

- Google Calendar - Configured
- Email notifications - Configured
- SMS notifications - Configured
- Call notifications - Configured

For a client demo, this can be misleading if those are not live/verified connections.

Please plan safer status labels:

- `Connected and verified`
- `Configured, not tested`
- `Not connected`
- `Coming later`

Do not imply Google Calendar, SMS, call, or email is live unless it has actually been verified.

### 4. Subscription display still inconsistent

Header / Automation Center still showed:

- `No Plan`
- `7 / 5 Active`

This is not necessarily part of Clinic Workspace, but it is important before plan-gated features are trusted. Please include whether this should be fixed now or tracked as a separate request.

### 5. Provide SQL evidence for QA rows

Codex verified UI persistence, but cannot independently run authenticated SQL.

Please provide SQL evidence for:

- pilot clinic row workspace/profile values,
- QA service row `QA TEST Service 20260627` with `clinic_id`, price, currency,
- QA FAQ row `QA TEST FAQ 20260627` with `clinic_id`,
- AI guardrails row with `clinic_id`,
- send-capable/workflow row counts unchanged during the QA window, especially:
  - `workflow_executions`
  - `automation_logs`
  - `email_delivery_logs`
  - `scheduled_messages`
  - `reminders`
  - `messages`

## Out Of Scope

Do not build:

- email inbox connection,
- email AI sorting,
- chatbot intake/API intake,
- knowledge file upload/indexing,
- embeddings/vector search,
- Google Calendar connection,
- SMS/call sends,
- payment links,
- live workflows,
- new left-nav Knowledge Base item.

Plan only. Do not build yet.
