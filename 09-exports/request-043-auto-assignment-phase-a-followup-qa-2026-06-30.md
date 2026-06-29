# Request 043 - Auto-Assignment Phase A Follow-Up QA

Date: 2026-06-30
App: https://clinic-pilot-x.lovable.app
Scope: Auto-Assignment Phase A follow-up after Lovable publish.

## Lovable Completion Message

Phase A follow-up shipped: migration applied for clinic_staff_settings, and AutoAssignment.tsx now refetches after every write, gates toasts on confirmed row writes, reads max-conversations from the new clinic-scoped table, adds a labelled delete confirm, and DialogDescriptions clear the Radix warning.

## Result

Auto-Assignment follow-up: PASS for the tested CRUD/readiness scope.

Separate subscription display regression: FAIL / follow-up required.

## QA Steps Run

1. Opened `/auto-assignment` in the authenticated live app.
2. Confirmed the page no longer hangs on loading.
3. Created disposable rule `QA TEST AUTO ASSIGN 20260630-A`.
4. Confirmed the rule appeared immediately and `Assignment Rules (1)` updated without reload.
5. Reloaded the page and confirmed the rule persisted.
6. Toggled the rule inactive; confirmed `aria-checked=false`, visible `Inactive`, and persistence after reload.
7. Toggled the rule active; confirmed `aria-checked=true`, visible `Active`, and persistence after reload.
8. Changed Kizha Kaye max conversations from 10 to 12; confirmed immediate UI update and persistence after reload.
9. Reverted Kizha Kaye max conversations from 12 back to 10; confirmed persistence after reload.
10. Opened delete action for the QA rule; confirmed the delete button is labelled `Delete rule QA TEST AUTO ASSIGN 20260630-A` and the AlertDialog names the rule.
11. Clicked Cancel; confirmed the rule remained.
12. Reopened delete, clicked Delete; confirmed the rule disappeared immediately and stayed gone after reload.
13. Checked browser console warnings/errors; none appeared during final Auto-Assignment checks.
14. Opened Automation Center > Activity Logs; newest visible rows were old, starting at 10 days ago. No fresh workflow rows appeared from this QA.

## Verified Fixes

- `/auto-assignment` loads.
- Rule create refetches and updates the row/count immediately.
- Rule create persists after reload.
- Active/inactive toggle updates immediately and persists after reload.
- Staff max-conversations writes to the new clinic-scoped settings table and persists after reload.
- Delete action is labelled.
- Delete confirmation uses an in-app AlertDialog and includes the rule name.
- Delete cancel preserves the row.
- Delete confirm removes the row immediately and after reload.
- DialogDescription warning is no longer visible in console.
- No workflow/send/payment/calendar side effects were visible in Automation Center Activity Logs.

## Regression Found

The subscription display appears broken again in the authenticated live app:

- `/auto-assignment` header shows `No active plan`.
- `/automation` shows `Current Plan: No active plan`.
- `/subscription` shows `Current Plan: No active plan`.
- `/subscription` still lists `Professional` under available plans, but it is not shown as the current plan.
- `/automation` shows `4 / 5 Active`, which appears to be based on the no-plan/starter entitlement path rather than the pilot clinic's Professional subscription.

This conflicts with Request 040, where the live app previously showed:

- Dashboard/header: `Professional`.
- Automation Center: `Professional`.
- Subscription page: `Current Plan: Professional` and `Status: Active`.

## Safety Notes

- No workflow toggles were clicked.
- No send reminder, test-send, SMS, email, payment, calendar, API key, webhook, or external integration action was clicked.
- The disposable QA assignment rule was deleted before ending QA.
- Kizha Kaye max conversations was restored to 10.

## Decision

Auto-Assignment Phase A can be treated as passed for the tested scope.

Do not proceed to broad visual refresh or Dr. Hong email AI sorting until the subscription display regression is corrected again, because plan-gated UI and demo messaging depend on accurate subscription state.
