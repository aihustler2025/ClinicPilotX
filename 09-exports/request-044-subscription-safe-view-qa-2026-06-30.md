# Request 044 - Subscription Safe View QA

Date: 2026-06-30
App: https://clinic-pilot-x.lovable.app
Scope: QA after Lovable changed the subscription hook to read from `clinic_subscriptions_safe`.

## Lovable Completion Message

Done. The subscription hook now reads from the new clinic_subscriptions_safe view, which is visible to every clinic member while Stripe IDs on the base table remain restricted to owners/admins — pilot owner should see Professional again across header, Auto-Assignment, Automation Center, and Subscription pages.

## Result

PASS for the tested subscription display regression fix.

## QA Steps Run

1. Opened `/dashboard`.
2. Confirmed header/chrome shows `Professional`.
3. Confirmed no visible `No active plan` or `No Plan` text.
4. Opened `/auto-assignment`.
5. Confirmed header/chrome shows `Professional`.
6. Confirmed no visible `No active plan` or `No Plan` text.
7. Confirmed Auto-Assignment still loads and shows `Assignment Rules (0)` and `Staff Configuration (2)`.
8. Opened `/automation`.
9. Confirmed header/chrome shows `Professional`.
10. Confirmed Automation Center current plan shows `Professional`.
11. Confirmed Automation Center counter shows `7 / 13 Active`, not the broken `4 / 5 Active` fallback observed in Request 043.
12. Opened `/subscription`.
13. Confirmed `Current Plan: Professional` and `Status: Active`.
14. Opened Automation Center > Activity Logs.
15. Confirmed there were no fresh workflow rows from this read-only QA; newest visible rows started at 10 days ago.
16. Checked browser console warnings/errors; none were present in the final check.

## Verified Behavior

- Dashboard/header subscription display is restored to `Professional`.
- Auto-Assignment/header subscription display is restored to `Professional`.
- Automation Center current plan is restored to `Professional`.
- Automation Center entitlement counter is restored to `7 / 13 Active`.
- Subscription page current plan is restored to `Professional` with `Status: Active`.
- The previous `No active plan` regression is no longer visible in the tested pages.
- Auto-Assignment remains functional from the prior Request 043 pass.

## Safety Notes

- This was read-only QA.
- No workflow toggles were clicked.
- No send reminder, test-send, SMS, email, payment, calendar, API key, webhook, or external integration action was clicked.
- No new workflow activity appeared during QA.

## Decision

The Request 043 subscription display regression can be treated as resolved.

Next recommended step: return to the visual refresh / workspace UX planning path. Send or revisit the Lovable Plan-mode visual refresh request, with Lovable owning UX/UI direction and Codex constraining only product outcomes, safety, data integrity, and QA. After the UX direction is approved, resume Dr. Hong demo preparation and safe test-inbox Email AI Sorting.
