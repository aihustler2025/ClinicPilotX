# Request 038 - Clinic Workspace Phase A Polish QA

Date: 2026-06-28

## Scope

Ross approved and published Lovable's Clinic Workspace Phase A QA polish plan.

Approved polish scope:

- Services & Pricing row action labels/tooltips and delete confirmation.
- Overview checklist loading behavior so it no longer flashes a false `0 of 6`.
- Integrations Status safer wording.
- Read-only SQL evidence for the pilot clinic rows and send-capable table counts.

Out of scope:

- email inbox connection,
- email AI sorting,
- chatbot/API intake,
- knowledge uploads/embeddings,
- Google Calendar connection,
- SMS/calls,
- payment links,
- live workflows,
- main left-nav changes,
- subscription/entitlement display fix.

## Result

UI polish passed.

Evidence follow-up still required because Lovable's completion message did not include the promised read-only SQL results.

## Live QA

Tested against:

`https://clinic-pilot-x.lovable.app`

### Services & Pricing

Passed.

Verified:

- Existing service delete buttons now have accessible label `Delete service`.
- Blank/new service plus button now has accessible label `Add service`.
- Clicking delete opens an in-app confirmation dialog:
  - title: `Delete this service?`
  - body includes the service name,
  - buttons: Cancel and Delete.
- Cancel keeps the service row.
- Confirm Delete removes a disposable QA service after reload.

Disposable service used:

- `QA TEST DELETE SERVICE 20260628`

Notes:

- Confirm Delete showed a `Deleted` toast.
- The disposable row still appeared immediately after the toast, but was gone after reload. This is acceptable for the current polish pass, but the UI would feel cleaner if the row disappeared immediately after deletion.
- Existing QA service `QA TEST Service 20260627` remained present.

### Overview Checklist

Passed.

Verified:

- Hard navigation did not show a false `0 of 6 steps complete`.
- During the earliest observed loading state, the page showed `Loading settings...`.
- After data resolved, Overview showed `4 of 6 steps complete`.

### Integrations Status

Passed.

Verified safer copy:

- Caption: `These reflect saved settings, not live delivery health.`
- Google Calendar: `Configured, not tested`
- Stripe: `Not connected`
- Email notifications: `Enabled (not verified)`
- SMS notifications: `Enabled (not verified)`
- Call notifications: `Coming later`

No item claimed `Connected and verified`.

### Automation / Side Effects

Passed for visible UI safety scope.

Verified:

- Automation Center still loads.
- No `just now`, `seconds ago`, or `minutes ago` workflow activity was visible during this pass.
- Browser console showed no errors/warnings during the Automation Center check.

No live send/payment/calendar/workflow action was clicked.

### Known Issue Still Present

Subscription/entitlement display remains inconsistent:

- Header / Automation Center showed `No Plan`.
- Automation Center showed `7 / 5 Active`.

This was explicitly out of scope for this polish pass and should be handled next as a dedicated follow-up before plan-gated features are trusted.

## Missing From Lovable Completion

Lovable's completion message did not include the read-only SQL evidence promised in the approved plan.

Still needed:

- pilot clinic workspace/profile snapshot,
- QA service row evidence,
- QA FAQ row evidence,
- AI guardrails row evidence,
- send-capable / workflow row counts during the QA window:
  - `workflow_executions`
  - `automation_logs`
  - `email_delivery_logs`
  - `scheduled_messages`
  - `reminders`
  - `messages`

## Recommended Next Step

Send Lovable handoff 038 in Plan mode only:

`docs/handoffs/Lovable-paste-message-038-clinic-workspace-polish-evidence-and-subscription-plan.md`

After Lovable provides the missing SQL evidence and plans the subscription display reconciliation, approve only the subscription/entitlement display fix.

Do not start the Dr. Hong test-inbox Email AI Sorting demo until:

1. Clinic Workspace Phase A evidence is accepted.
2. Subscription/plan display is no longer misleading.
3. Ross has confirmed or replaced the QA workspace values with real Dr. Hong pilot data.
