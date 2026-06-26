# Request 033 - Phase 1B.1c Internal Chat Fix QA

Date: 2026-06-26

Published build reported by Lovable:

- SQL migration applied.
- `InternalChat.tsx` updated to use the new `create_dm_channel` RPC.
- Internal chat initialization is now scoped to the active clinic.

## Result

Pass for the tested Internal Chat fix scope.

Follow-up issues remain outside this exact build scope:

- Subscription/plan display still showed `No Plan` and `7 / 5 Active` during this pass.
- External conversation selection still did not open the conversation detail pane.
- DB-level row checks still require Lovable/Supabase SQL evidence because Codex does not currently have authenticated SQL access.

## Baseline

Opened:

`https://clinic-pilot-x.lovable.app/automation`

Observed:

- Automation Center rendered.
- Header/current plan showed `No Plan`.
- Active workflow count showed `7 / 5 Active`.
- Activity Logs newest visible workflow rows were `7 days ago`.

This means there were no fresh visible workflow rows before the Internal Chat test.

## Internal Chat QA

Opened:

`https://clinic-pilot-x.lovable.app/communication-hub`

Steps:

1. Opened Communication Hub.
2. Opened Internal Chat tab.
3. Confirmed group channels rendered:
   - `All Staff`
   - `Doctors`
   - `Front Desk`
4. Clicked staff member `Kizha Kaye`.
5. Confirmed `DM: Kizha Kaye` appeared under Direct Messages.
6. Confirmed the `DM: Kizha Kaye` chat pane opened.
7. Typed safe internal-only message:
   - `QA TEST INTERNAL CHAT 20260626-A`
8. Pressed Enter.
9. Confirmed the message appeared in the DM thread with timestamp `10:41:49 AM`.

Console:

- No errors or warnings observed after the internal chat send.

## Automation Safety Check

Returned to Automation Center > Activity Logs after sending the internal chat message.

Observed:

- Newest visible workflow rows were still `7 days ago`.
- No fresh `Lead Acknowledgment`, `Smart Follow-up Sequence`, `Appointment Confirmation`, or other workflow execution appeared.

Result:

- No visible send-capable automation side effects were triggered by the internal staff chat message.

## Not Triggered

The following were not clicked or activated:

- SMS
- email
- WhatsApp
- Messenger
- Viber
- Telegram
- voice
- payment links
- Stripe
- Google Calendar
- scheduled messages
- Automation Center test-send buttons
- live credentials

## Remaining Follow-Up

1. Ask Lovable to provide SQL evidence:
   - `internal_channels` direct channel row has the active pilot `clinic_id`.
   - `internal_channel_members` has exactly two rows for the DM channel: QA user and Kizha.
   - `internal_messages` row has the same `clinic_id` as the channel.
   - zero new rows in `messages`, `scheduled_messages`, `workflow_executions`, `automation_logs`, `email_delivery_logs`, and `reminders`.
2. Fix or plan the `No Plan` / `7 / 5 Active` subscription display issue.
3. Fix or plan external conversation selection so `ConversationNotesPanel` can be reached and QA-tested.
4. Keep `scheduled_messages` deferred until a separate safety plan exists.

