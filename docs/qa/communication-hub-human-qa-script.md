# Communication Hub Human QA Script

Last updated: 2026-06-24

## Purpose

Use this script to manually check the Communication Hub without sending messages or activating integrations.

This is read-only QA.

## Safety Rules

Do not send SMS, email, WhatsApp, Messenger, Viber, Telegram, internal chat messages, or test messages.

Do not connect credentials.

Do not click any button that says Send, Reply, Test, Connect, Sync, Invite, or Start unless Ross explicitly approves.

## External Messages

1. Open `Communication Hub`.
2. Confirm the `External Messages` tab loads.
3. Record the visible conversation count, such as `Select All (11)`.
4. Record the visible channel labels, such as SMS, WhatsApp, Messenger, or Email.
5. Click one conversation row.
6. Confirm whether the right-side/detail pane opens.
7. If the pane still says `Select a conversation`, mark this as failed.
8. Search for a visible name or word, such as `Brandon`.
9. Confirm results narrow correctly.
10. Clear the search field.
11. Confirm all conversations return.
12. Open Filters.
13. Record filter options for Channel, Date Range, and Contact Type.
14. Do not send or reply to anything.

## Internal Chat

1. Click `Internal Chat`.
2. Record visible group channels, direct messages, and staff members.
3. Click one staff member.
4. Confirm whether a direct message thread opens.
5. If an error appears, record the exact text.
6. Do not type or send any internal message.

## Pass Criteria

Communication Hub can pass read-only QA when:

- External conversation rows open a readable detail view.
- Search narrows and clears reliably.
- Filters are visible and understandable.
- Internal Chat can open a staff/channel thread without errors.
- No outbound message is sent during QA.

## Current Known Issues

As of 2026-06-24:

- External conversation click did not open the detail pane during Codex QA.
- Internal Chat direct message creation failed for `Kizha Kaye`.
- No email inbox or email AI sorting surface is visible yet.
