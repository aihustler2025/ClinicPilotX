# Lovable Paste Message 039 - Subscription Display Follow-Up

Please read this QA failure report and respond with a fix plan. Do not expand scope.

Codex tested the published Phase 1B.x subscription / entitlement display reconciliation build.

## Result

Fail / follow-up required.

The old `7 / 5 Active` counter is gone, but the live UI still does not show the pilot clinic as Professional.

## Observed In Live QA

### Dashboard / Header

- Header shows `No active plan`.
- Header does not show `Professional`.
- Old copy `No Plan` is gone, but the subscription still does not resolve.

### Automation Center

- Current Plan: `No active plan`
- Counter: `4 / 5 Active`
- Old `7 / 5 Active` is gone.
- Header still says `No active plan`.

### Subscription Page

- Header shows `No active plan`.
- Page says `Current Plan: No active plan`.
- Professional appears only under available plans, not as the active current plan.

### Settings / Clinic Workspace

Still loads and Team & Roles still shows:

- `teambuzzooka@gmail.com` owner
- `kizha.buzzooka@gmail.com` admin

This suggests the active workspace still appears to be the pilot clinic from the UI.

## Required Diagnosis

Please verify with exact read-only evidence:

1. The active clinic id returned/used by `useActiveClinic()` for the logged-in Ross/teambuzzooka session.
2. The exact `clinic_subscriptions` row for `8ed615bf-afd3-4986-86a8-fecec8887db3`.
3. Its `status`, `current_period_start`, `current_period_end`, `plan_id`, and any date/status filters used by the frontend.
4. The joined `subscription_plans` row for the seeded Professional plan.
5. Whether RLS permits the logged-in user to select that subscription row through the same query used by `useSubscription`.
6. The exact query now used by `useSubscription`.
7. Whether the hook waits for `clinicId` before querying, or accidentally runs once with null/undefined and sticks on `none`.
8. Whether `maybeSingle()` is returning null because of row mismatch, RLS, date filtering, or join shape.

## Fix Requirements

Keep scope to:

- `src/hooks/useSubscription.tsx`
- `src/components/layout/AppHeader.tsx`
- `src/pages/AutomationCenter.tsx`
- `src/pages/Subscription.tsx` only if required for the page's current-plan display.

Do not touch:

- email inbox,
- email AI sorting,
- chatbot/API intake,
- knowledge uploads/embeddings,
- Google Calendar,
- SMS/calls,
- payment links,
- live workflow execution,
- main left nav,
- unrelated CRM modules.

## Expected QA After Fix

- Dashboard header shows `Professional`.
- Automation Center Current Plan shows `Professional`.
- Subscription page shows `Current Plan: Professional`.
- No page flashes or sticks on `No active plan` after loading.
- Counter no longer shows impossible states.
- No live send/payment/calendar/workflow action is triggered.

Please respond with a focused plan or, if the bug is obvious, the smallest fix path and exact files.
