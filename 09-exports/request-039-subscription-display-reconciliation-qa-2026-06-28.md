# Request 039 - Subscription Display Reconciliation QA

Date: 2026-06-28

## Scope

Ross approved and published Lovable's Phase 1B.x subscription / entitlement display reconciliation build.

Lovable reported:

- Phase A SQL evidence is posted.
- Pilot clinic now has an active Professional subscription.
- `useSubscription` is scoped by `clinicId` with tri-state status.
- Automation Center's counter only counts plan-allowed enabled workflows.
- `7 / 5` should be gone.

## Result

Fail / follow-up required.

The `7 / 5` counter is gone, but the live UI still does not show the pilot clinic as Professional.

## Live QA

Tested against:

`https://clinic-pilot-x.lovable.app`

### Dashboard / Header

Failed.

Observed after hard reload and wait:

- Header shows `No active plan`.
- Header does not show `Professional`.
- Old copy `No Plan` is gone, but the new state is still incorrect if the pilot clinic has an active Professional row.

### Automation Center

Partial pass / failed main subscription claim.

Observed:

- Current Plan: `No active plan`
- Counter: `4 / 5 Active`
- Old counter `7 / 5 Active` is gone.
- Header still shows `No active plan`.
- Console errors/warnings: none observed in final Automation Center check.

This proves the counter logic changed, but subscription resolution still does not find the Professional pilot subscription.

### Subscription Page

Failed.

Observed:

- Header shows `No active plan`.
- Page heading says `Current Plan: No active plan`.
- Available Plans still include Starter / Professional / Enterprise.
- The Professional plan is visible in available plans, but it is not shown as the current active plan.

### Settings / Clinic Workspace

Still loads.

Checked:

- `Settings -> Clinic Workspace -> Business Profile`
- `Settings -> Clinic Workspace -> Team & Roles`

Team & Roles still shows:

- `teambuzzooka@gmail.com` as owner
- `kizha.buzzooka@gmail.com` as admin

This confirms the active Clinic Workspace context still looks like the Dr. Colin Hong pilot workspace from the UI.

## What Improved

- The old `No Plan` wording is gone.
- The old `7 / 5 Active` counter is gone.
- Automation Center now shows `4 / 5 Active`.

## What Is Still Wrong

- The UI still cannot display the active Professional subscription for the pilot clinic.
- Dashboard/header, Automation Center, and Subscription page all agree on the wrong state: `No active plan`.
- If the seeded `clinic_subscriptions` row exists, then either:
  - the frontend query is not matching it,
  - RLS is hiding it,
  - the inserted row does not match the expected active/status/date filters,
  - the plan join/shape is not matching the code,
  - or the active clinic id used by the hook is not the same clinic id used for the subscription row.

## Safety

No live email, SMS, call, payment, calendar, workflow send, chatbot/API, or integration action was clicked.

No visible fresh workflow activity was triggered during this QA pass.

## Recommended Next Step

Send Lovable handoff 039 as a custom fix request.

`docs/handoffs/Lovable-paste-message-039-subscription-display-followup.md`

Do not proceed to the Dr. Hong email AI sorting demo until:

- the header shows Professional for the pilot clinic,
- Automation Center shows the same plan,
- Subscription page says Current Plan: Professional,
- and the counter is truthful.
