# Request 040 - Subscription Fix QA and Workspace UX Reset Notes

Date: 2026-06-29

## Scope

Ross approved and published Lovable's `clinic_subscriptions` RLS fix after Request 039.

Lovable reported:

- migration applied,
- pre-existing linter warnings unrelated,
- pilot owner can now read the clinic subscription row,
- header, Automation Center, and Subscription page should resolve to Professional without frontend changes.

Codex also inspected the current Clinic Workspace placement and Auto-Assignment route after Ross raised UX concerns.

## Subscription QA Result

Pass for the required subscription display surfaces.

### Dashboard / Header

Observed on `https://clinic-pilot-x.lovable.app/dashboard`:

- Header shows `Professional`.
- `No active plan` is not present.
- `No Plan` is not present.
- No console errors were observed in this pass.

### Automation Center

Observed on `https://clinic-pilot-x.lovable.app/automation`:

- Header shows `Professional`.
- Current Plan shows Professional-related content.
- `No active plan` is not present.
- `No Plan` is not present.
- Counter now shows `7 / 13 Active`, not the old broken `7 / 5 Active` state.
- No console errors/warnings were observed in this pass.

### Subscription Page

Observed on `https://clinic-pilot-x.lovable.app/subscription`:

- Header shows `Professional`.
- Page shows `Current Plan: Professional`.
- Page shows `Status: Active`.
- `No active plan` is not present.
- `No Plan` is not present.
- No console errors/warnings were observed in this pass.

## Auto-Assignment Route Check

Observed on `https://clinic-pilot-x.lovable.app/auto-assignment`:

- Header shows `Professional`.
- Page remains stuck at `Loading assignment rules...`.
- Console error observed: `Error fetching rules: Object`.

This is an existing module blocker and should not be treated as resolved by the subscription fix.

## Workspace UX Concern

Ross raised a valid product concern: ClinicPilotX is a subscription product, and each subscriber needs an easy, chronological setup experience for their clinic workspace.

Current issue:

- Clinic Workspace is hidden inside Settings between other technical/admin tabs.
- The workspace setup is split into many subtabs immediately.
- The flow feels more like an internal admin configuration screen than a subscriber onboarding experience.
- Codex's previous Lovable prompts were too prescriptive about UI structure, which may have constrained Lovable's design strengths.

Corrected product direction:

- Codex should define outcomes, safety rules, data requirements, QA checks, and backend constraints.
- Lovable should propose the UX/UI approach.
- Future Lovable prompts should avoid overly specific layout/design instructions unless required for safety, compliance, or data integrity.

## Safety

During this QA pass, Codex did not click or trigger:

- email sends,
- SMS/calls,
- payment links,
- Google Calendar writes,
- chatbot/API intake,
- webhook tests,
- Automation Center test sends,
- live credential connections.

## Recommended Next Step

Send Lovable a Plan-mode UX/product reset request.

Goal: ask Lovable to propose the best subscriber-facing workspace setup/onboarding experience for ClinicPilotX without prescribing the exact layout.

The plan should also acknowledge that Auto-Assignment remains stuck/loading, but that can be handled as a separate repair unless Lovable sees a shared root cause.
