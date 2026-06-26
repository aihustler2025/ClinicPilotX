# Communication Hub Internal Chat Human QA Script

Last updated: 2026-06-26

## Purpose

This script lets a human tester verify the internal staff chat path without triggering SMS, email, payments, calendar writes, or external workflows.

## Safety Rules

Do not click:

- Send SMS
- Send Email
- WhatsApp
- Messenger
- Viber
- Telegram
- payment link buttons
- Google Calendar buttons
- Automation Center test-send buttons

Only test the **Internal Chat** tab.

## Test Data

Use this message:

`QA TEST INTERNAL CHAT HUMAN CHECK`

## Steps

1. Log in to ClinicPilotX.
2. Open `Communication Hub`.
3. Click the `Internal Chat` tab.
4. Confirm group channels are visible:
   - `All Staff`
   - `Doctors`
   - `Front Desk`
5. Find staff member `Kizha Kaye`.
6. Click `Kizha Kaye`.
7. Confirm a direct message thread opens:
   - expected heading: `DM: Kizha Kaye`
8. Type:
   - `QA TEST INTERNAL CHAT HUMAN CHECK`
9. Press Enter.
10. Confirm the message appears in the thread with a timestamp.
11. Open Automation Center > Activity Logs.
12. Confirm no brand-new workflow execution appeared immediately after the internal chat message.

## Pass Criteria

Pass if:

- Internal Chat opens.
- Kizha DM opens without an error toast.
- The test message appears.
- No SMS/email/payment/calendar action happens.
- Automation Center Activity Logs do not show a fresh workflow row caused by the internal message.

## Fail Criteria

Fail if:

- `Failed to create direct message channel` appears.
- `Error fetching channels` appears.
- The message does not appear after pressing Enter.
- A new Automation Center workflow row appears immediately after the internal message.
- Any external-send prompt or payment/calendar prompt appears.

