# Lovable Paste Message 042 - Auto-Assignment Phase A QA Follow-Up

Please read this Auto-Assignment Phase A QA report and respond with a focused fix plan. Do not build yet.

QA report:

https://github.com/aihustler2025/ClinicPilotX/blob/main/09-exports/request-042-auto-assignment-phase-a-qa-2026-06-29.md

## Summary

Phase A is a partial pass, not complete.

The page no longer spins forever, which is good. But several core interactions still fail or mislead the user.

## Passes

- `/auto-assignment` loads.
- `Loading assignment rules...` is gone.
- `Assignment Rules (0)` renders.
- `Staff Configuration (2)` renders.
- Creating a QA rule persists after reload.
- Deleting the QA rule persists after reload.
- No fresh Automation Center workflow activity appeared during QA.

## Issues To Fix

### 1. Create Rule UI Does Not Refresh

Creating `QA TEST AUTO ASSIGN 20260629-A` showed `Rule created successfully`, but the page still displayed `Assignment Rules (0)` until browser reload.

Expected: new rule appears immediately and count updates without reload.

### 2. Delete Rule UI Does Not Refresh

Deleting the QA rule showed `Rule deleted successfully`, but the page still displayed the deleted rule and `Assignment Rules (1)` until browser reload.

Expected: deleted rule disappears immediately and count updates without reload.

### 3. Active/Inactive Toggle Does Not Work

Clicking the rule switch did not change it:

- `aria-checked` stayed `true`.
- badge/text stayed `Active`.
- coordinate click on the visible switch also did not change state.

Expected: switch toggles active/inactive and persists after reload.

### 4. Staff Max Conversations Save Does Not Persist

Changing Kizha Kaye from 10 to 12 showed `Staff settings updated successfully`, but the row stayed `Max conversations: 10`; after reload it was still 10.

Expected: value persists and updates visibly, or the setting should be disabled/removed until it is correctly wired.

### 5. Accessibility / Feedback Polish

- Rule delete action is icon-only and unlabeled.
- Dialog console warning appears: `Missing Description or aria-describedby={undefined} for {DialogContent}`.
- Success toast should not show if the visible UI did not actually update or the save did not persist.

## Scope For Fix

Keep this limited to Auto-Assignment only.

Allowed files likely include:

- `src/pages/AutoAssignment.tsx`
- supporting Auto-Assignment components if any
- small RLS/SQL fix only if required for toggle/staff persistence

Do not touch:

- dashboard visual refresh,
- workspace IA,
- sidebar/header tokens,
- integrations/API pages,
- Automation Center redesign,
- live integration credentials,
- email/SMS/calls/payments/calendar/webhooks,
- workflow execution logic.

## Required QA After Fix

1. Load `/auto-assignment`: no spinner, no console error.
2. Create QA rule: appears immediately, count updates immediately, persists after reload.
3. Toggle rule inactive: UI updates immediately, persists after reload.
4. Toggle rule active: UI updates immediately, persists after reload.
5. Change staff max conversations from 10 to 12: row updates immediately, persists after reload.
6. Revert staff max conversations back to 10.
7. Delete QA rule: disappears immediately, count updates immediately, persists after reload.
8. Confirm no fresh workflow rows in Automation Center Activity Logs.
9. Confirm delete button/dialogs have accessible label/description and no Radix dialog description warning.

Please respond with a focused fix plan only.
