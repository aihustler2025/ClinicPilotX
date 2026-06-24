# Communication Hub Read-Only Audit - 2026-06-24

## Scope

Codex performed a read-only audit of the published Communication Hub:

`https://clinic-pilot-x.lovable.app/communication-hub`

No messages were sent. No integrations, workflows, credentials, reminders, SMS, email, WhatsApp, Messenger, or internal chat messages were activated.

## Result

Partial / not ready for Dr. Hong demo yet.

The Communication Hub route exists and shows a useful shell, but the current implementation appears mostly seeded/demo and has key interaction gaps.

## External Messages

Visible state:

- Page title: `Communication Hub`
- Tabs:
  - `External Messages`
  - `Internal Chat`
- External list title: `Conversations`
- Search box: `Search by name, phone, or message...`
- Filter button.
- `Select All (11)` checkbox.
- 11 visible conversation records.

Visible channel labels:

- SMS
- WhatsApp
- Messenger

Visible contact labels:

- Patient
- Lead

Sample visible messages include:

- Appointment confirmation-style SMS.
- Payment request-style appointment message.
- WhatsApp product conversation.
- Messenger reschedule request.
- Lead follow-up messages.

## External Messages Findings

### Working / present

- External Messages tab loads behind authenticated session.
- Conversation list appears with 11 records.
- Search can narrow results, verified with `Brandon`.
- Filters panel opens.
- Filter controls are present for:
  - Channel
  - Date Range
  - Contact Type

### Issues / gaps

1. Conversation detail did not open during the audit.

   Codex clicked a visible conversation message. The right/detail pane still showed:

   `Select a conversation`

   `Select a conversation to view messages`

   This means either the wrong visible element is clickable, the row click target is not accessible, or the detail pane is not wired.

2. Search clear behavior is unreliable in controlled QA.

   Searching `Brandon` narrowed results to `Select All (1)`. Reload restored all 11 conversations.

   A later keyboard-clear attempt left the list in `No conversations found` state with the search input still containing partial text (`SM`). This may be browser-control specific, but the search field should include a clear button or reliably restore all conversations when emptied.

3. No visible email inbox / email filtering surface.

   The Communication Hub currently shows SMS/WhatsApp/Messenger examples, but no obvious Email inbox tab or email classification queue.

   Since Dr. Hong's near-term demo depends on email filtering, this likely belongs in either:

   - Communication Hub as an Email Inbox / Intake Queue tab, and/or
   - Automation Center as an Email AI Sorting workflow configuration and review queue.

4. Sample messages include send/payment-style content.

   Some seeded rows include appointment confirmations and payment request wording. Treat these as demo data until Lovable confirms the source and whether they are connected to real sends/logs.

## Internal Chat

Visible state:

- Internal Chat tab opens.
- Left panel title: `Channels & Staff`
- Sections:
  - `GROUP CHANNELS`
  - `DIRECT MESSAGES`
  - `STAFF MEMBERS`
- One visible staff member:
  - `Kizha Kaye`
  - `kizha.buzzooka@gmail.com`

## Internal Chat Findings

### Working / present

- Internal Chat tab renders.
- Staff member list appears.

### Issue

Clicking `Kizha Kaye` failed with toast:

`Error`

`Failed to create direct message channel`

The main panel remained:

`Select a channel`

`Select a channel or staff member to start messaging`

This suggests the internal chat channel creation path is broken or blocked by backend/RLS/schema assumptions.

## Console Notes

The recurring console error remains:

`Error fetching settings: Object`

No new communication-specific console error was exposed in the controlled log, but the UI toast clearly reported direct message channel creation failure.

## Dr. Hong Demo Impact

Communication Hub is not yet the best next build target for the Dr. Hong demo.

The demo priority should be:

1. Audit Automation Center email-related workflows/settings.
2. Design client/clinic account setup.
3. Design email AI sorting with a test inbox.
4. Design lead intake API/webhook for ConvoCore, external chatbots, website forms, and future ClinicPilotX chatbot.
5. Decide whether classified email/message records should appear in:
   - Leads timeline,
   - Communication Hub inbox,
   - Automation Center review queue,
   - or all of the above.

## Recommended Follow-Up

Before asking Lovable to build Communication Hub features, complete a read-only Automation Center audit focused on:

- Email filtering.
- Lead intake.
- Appointment request detection.
- Existing workflow rows.
- Whether current workflows are demo, Supabase/Lovable, or old n8n-inspired.
- Whether anything can send real SMS/email/payment/calendar actions.

After that audit, create one Lovable plan-mode request for the Dr. Hong demo foundation:

- client/clinic account setup,
- test inbox email classification,
- lead creation from classified emails,
- external chatbot/API lead intake path,
- no live outgoing sends.

## Safety

No outbound messages or internal chat messages were sent.

No live SMS, email, WhatsApp, Messenger, payment, calendar, workflow, webhook, or credential action was triggered.
