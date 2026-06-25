# Lovable Paste Message 032 - Phase 1B.1c Internal Chat Follow-Up

Date: 2026-06-25

Use this in Lovable Plan mode only. Do not build yet.

```text
Codex QA did not pass Phase 1B.1c yet.

Published scope tested:
- ConversationNotesPanel clinic_id stamping
- InternalChat clinic_id stamping for internal_channels and internal_messages
- scheduled_messages remained out of scope

QA result:
- Safety passed: Automation Center Activity Logs did not show any fresh workflow rows after testing.
- Internal chat failed: Communication Hub > Internal Chat > clicking Kizha Kaye still shows "Failed to create direct message channel".
- Console shows: "Error fetching channels: Object".
- The chat pane stays on "Select a channel or staff member to start messaging".
- No internal channel opens, so Codex could not send a safe internal-only test message.
- External conversation selection also still does not open the detail pane, so ConversationNotesPanel could not be reached from the UI.

Please respond with a Plan-mode fix proposal only.

Diagnose before proposing edits:
1. Why channel fetching logs "Error fetching channels: Object".
2. Why direct-message channel creation fails when clicking Kizha Kaye.
3. Whether internal_channels, internal_channel_members, and internal_messages RLS/helper logic allows the current active clinic owner/admin to read/create the required rows.
4. Whether direct-channel creation now inserts internal_channels.clinic_id but then fails on internal_channel_members insert, member lookup, or read-back.
5. Whether any existing internal channel/member rows are missing clinic_id or clinic membership after Phase 1B.

Fix scope allowed:
- Communication Hub internal chat fetch/create logic.
- Internal chat RLS/helper fix only if required, but show the exact SQL first if any SQL is needed.
- Internal channel/message clinic_id stamping needed to make staff-only chat usable.
- Conversation selection/detail-pane bug may be included only if it is a small Communication Hub UI fix needed to reach ConversationNotesPanel for QA.

Keep out of scope:
- scheduled_messages
- live sends
- SMS/email/WhatsApp/Messenger/Viber/Telegram/voice
- payment links
- Stripe
- Google Calendar
- Automation Center workflow changes
- edge functions
- Settings
- Subscription
- Phase 1B.2 read filtering
- clinic switcher/onboarding

Required QA plan after build:
1. Open Communication Hub > Internal Chat.
2. Click Kizha Kaye.
3. Confirm a direct channel opens without error.
4. Send one clearly marked safe internal message, such as "QA TEST INTERNAL CHAT 20260625-A".
5. Verify the message appears in the thread.
6. Verify the new internal_channels/internal_messages rows carry the active pilot clinic_id.
7. Verify no rows appear in messages, scheduled_messages, workflow_executions, automation_logs, email_delivery_logs, reminders, or any send-capable table.
8. If conversation selection is included, open a conversation and add a safe internal note, then verify conversation_notes.clinic_id.

Do not build until Codex reviews this plan.
```

