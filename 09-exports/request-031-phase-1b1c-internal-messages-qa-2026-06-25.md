# Request 031 - Phase 1B.1c Internal Messages QA

Date: 2026-06-25

Published build reported by Lovable:

- `ConversationNotesPanel` stamps `clinic_id` with active-clinic readiness guard.
- `InternalChat` stamps `clinic_id` on `internal_messages` and `internal_channels` inserts.
- Scope intentionally excluded `scheduled_messages`, live sends, payment links, edge functions, RLS, migrations, and external channels.

## Result

Partial fail / follow-up required.

The safety side passed: no fresh Automation Center workflow activity appeared during this QA pass.

The internal chat functional path failed: direct-message channel creation still errors before a staff chat can be opened or an internal message can be sent.

## Baseline

Automation Center > Activity Logs before testing:

- newest visible rows were about 6 hours old,
- no fresh `Lead Acknowledgment`, `Smart Follow-up Sequence`, `Appointment Confirmation`, or other workflow rows were visible at baseline.

## Communication Hub Checks

Opened:

`https://clinic-pilot-x.lovable.app/communication-hub`

Verified:

- Communication Hub renders behind login.
- External Messages tab renders.
- Internal Chat tab renders.
- Staff member `Kizha Kaye` is visible under Staff Members.

## Conversation Notes Check

Attempted to open a visible external conversation (`Cold Lead Test`) to reach the detail/notes panel.

Observed:

- Clicking the visible conversation did not open the detail pane.
- The right-side pane stayed on `Select a conversation`.

Result:

- `ConversationNotesPanel` could not be reached through the current UI.
- This appears related to the pre-existing Communication Hub conversation-selection issue and blocks UI QA for conversation notes.

## Internal Chat Check

Opened Internal Chat and clicked `Kizha Kaye`.

Observed:

- Toast/error appeared: `Failed to create direct message channel`.
- The chat pane stayed on `Select a channel or staff member to start messaging`.
- No internal channel opened.
- No internal message composer became available.

Console:

- `Error fetching channels: Object`

Result:

- Internal chat still fails at channel fetch/create.
- Phase 1B.1c cannot be treated as passed because the changed `internal_channels` / `internal_messages` path is not usable from the UI.

## Safety Check After Failed Internal Chat

Returned to Automation Center > Activity Logs after the failed internal chat attempt.

Observed:

- newest visible workflow rows were still about 6 hours old.
- no fresh workflow rows appeared.

Result:

- No visible send-capable workflow side effects were triggered by this QA pass.

## Not Tested

The following were not clicked or triggered:

- Send SMS
- Send email
- WhatsApp / Messenger / Viber / Telegram sends
- Payment links
- Stripe
- Google Calendar
- Automation Center test-send buttons
- `scheduled_messages`
- edge functions

## Follow-Up Needed

Lovable should diagnose and fix the Communication Hub internal chat data path before Phase 1B.1c can pass:

- why channel fetching logs `Error fetching channels: Object`,
- why clicking `Kizha Kaye` still shows `Failed to create direct message channel`,
- whether `internal_channels`, `internal_channel_members`, and `internal_messages` RLS/helper logic allows the active clinic owner/admin to read/create the required rows,
- whether the direct-channel creation code now adds `clinic_id` to `internal_channels` but then fails at `internal_channel_members` or a read-back query,
- how to verify the created internal channel/message rows carry the active pilot `clinic_id`,
- keep `scheduled_messages` and all live-send paths out of scope.

