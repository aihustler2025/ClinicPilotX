# Automation Center Human QA Script

Last updated: 2026-06-24

## Purpose

Use this script to inspect Automation Center without triggering live automations.

This is read-only QA.

## Safety Rules

Do not click:

- Send Test SMS.
- Send Test Email.
- Save Configuration.
- Workflow switches.
- Upgrade.
- Connect.
- Activate.
- Payment actions.
- Calendar actions.

Do not connect credentials or enter real phone/email test destinations.

## Workflow Inventory

1. Open `Automation Center`.
2. Record the current plan.
3. Record active workflow count, such as `7 / 13 Active`.
4. List each workflow by section:
   - Lead Intake.
   - Nurture.
   - Patient Engagement.
   - Payments.
   - Reminders.
   - Reporting.
5. Record which workflows show `Configure`.
6. Record which workflows show `Upgrade`.
7. Record which switches appear on/off.
8. Do not toggle switches.

## Configure Panels

For each workflow, open `Configure` only to read.

Record:

- Template fields.
- Timing controls.
- Variables.
- Test buttons.
- Save button.
- Any warning copy.

Then close the panel without saving.

## Activity Logs

1. Open `Activity Logs`.
2. Record visible workflow names.
3. Record statuses: Completed, Failed, etc.
4. Record rough timing such as 5 days ago, 12 days ago.
5. Do not rerun anything.

## Pass Criteria

Automation Center read-only QA passes when:

- Every visible workflow is inventoried.
- Send-capable workflows are identified.
- Activity Logs are reviewed.
- No workflow, test send, save, switch, credential, or paid action is triggered.

## Current Known Notes

As of 2026-06-24:

- Several active workflows are send-capable.
- Lead Acknowledgment has `Send Test SMS`.
- Appointment Confirmation has `Send Test SMS` and `Send Test Email`.
- No visible email AI sorting workflow exists yet.
- Lead Scoring configure panel says configuration is not available yet.
