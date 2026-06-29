# Lovable Paste Message 040 - Workspace UX Reset and Auto-Assignment Note

Please read this QA and product-direction note, then respond in Plan mode only. Do not build yet.

Codex verified the subscription/RLS fix: Dashboard header, Automation Center, and Subscription page now show `Professional`, and the old `No active plan` / `No Plan` display is gone for the pilot owner account.

QA report:

https://github.com/aihustler2025/ClinicPilotX/blob/main/09-exports/request-040-subscription-pass-workspace-ux-reset-2026-06-29.md

## What We Need From Lovable Now

Ross is unhappy with the current Clinic Workspace experience. The concern is not only visual polish; it is product flow.

ClinicPilotX is a subscription product. A new clinic subscriber needs a clear, friendly setup path where they can configure their clinic before using automations.

Please propose a better UX/product plan for subscriber workspace setup.

## Important Direction

Do not treat the current Settings > Clinic Workspace layout as sacred.

Do not simply polish the existing subtabs.

Use Lovable's design/product judgment to propose the best user experience.

Codex is intentionally not prescribing exact layout, card structure, tab order, or visual treatment. Lovable should propose the UX.

## Required Product Outcomes

The setup experience must help a clinic owner/admin configure, at minimum:

- clinic/business profile,
- logo/branding,
- website and public links,
- business hours,
- services and pricing,
- team/users/roles,
- knowledge FAQs,
- future knowledge sources such as files, URLs, website pages, and text notes,
- AI guardrails and escalation rules,
- integration readiness/status,
- subscription/plan status.

The experience should feel chronological and friendly for a nontechnical clinic owner, not like a developer/admin database settings screen.

Please consider whether the right answer is:

- an onboarding/setup wizard,
- a dedicated workspace setup area,
- a better owner/admin settings IA,
- dashboard setup prompts/cards,
- a top-bar clinic/workspace selector,
- or a combination.

Again: propose the best UX. Do not assume Codex's earlier placement decision was correct.

## Constraints / Safety

Keep this as Plan mode only.

Do not connect live integrations.

Do not send email, SMS, calls, payment links, calendar writes, webhooks, chatbot/API requests, or workflow test sends.

Do not build knowledge uploads/embeddings yet unless your plan separates them into a later phase.

Do not break existing CRM routes.

## Existing Issue To Acknowledge

Auto-Assignment remains broken/stuck at `Loading assignment rules...` with console error `Error fetching rules: Object` on:

`/auto-assignment`

Please include whether you recommend fixing Auto-Assignment before, after, or separately from the workspace UX reset.

## Response Requested

Please respond with:

1. Recommended UX direction in plain English.
2. Proposed route/location/navigation approach.
3. Proposed phased implementation.
4. Exact files/tables likely involved.
5. What will remain out of scope.
6. QA checklist after build.
7. Any questions for Ross before build.
