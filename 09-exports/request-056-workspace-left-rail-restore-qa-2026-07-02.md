# Request 056 - Workspace Left Rail Restore QA

Date: 2026-07-02

App: https://clinic-pilot-x.lovable.app

Lovable project: 8b4d9031-af8d-4faf-81d3-135c41ad73b7

## Reason

Ross reviewed the Request 055 Workspace IA/UX D1 result and disliked the new top/horizontal Workspace menu. He preferred the prior Workspace layout with:

- main app sidebar on the far left,
- dedicated Workspace section sidebar beside it,
- selected Workspace section highlighted in that second sidebar,
- content panel on the right.

Reference screenshots were provided in `Screenshot 2026-07-02 090038.zip`.

## Fix Requested

Codex asked Lovable for a targeted frontend-only correction, not a full Lovable version revert:

- Restore the dedicated Workspace left sidebar.
- Remove the top/horizontal `Jump to a section` chip menu.
- Keep `Auto-Fill From Website` prominent on Workspace Home.
- Preserve Workspace deep links and existing forms/data.
- Do not touch backend, migrations, RLS, edge functions, inbox, crawler/AI, sends, workflows, payments, calendar, or live integrations.

## Lovable Result

Lovable reported:

- Files changed: `src/pages/Workspace.tsx` only.
- Restored two-column `md:grid-cols-[220px_1fr]` layout.
- Restored `<WorkspaceNav>` as the dedicated left rail.
- Removed breadcrumb, horizontal step chips, and prev/next buttons.
- `WorkspaceHome.tsx` still leads with `WorkspaceAutoFillHero`.
- Typecheck: `bunx tsgo --noEmit` exit `0`.
- No backend/integration files touched.

Codex published using `Publish` -> `Update`.

## Live QA Result

Result: pass for tested correction scope.

Verified on the live app:

- `/workspace` loads with the dedicated Workspace left navigation restored.
- Main app sidebar remains visible on the far left.
- Workspace left panel includes:
  - Home
  - Business profile
  - Branding & logo
  - Hours of operation
  - Services & pricing
  - Team & roles
  - Knowledge FAQs
  - Knowledge sources
  - AI guardrails
  - Integrations status
  - Email inbox
- The top/horizontal `Jump to a section` chip menu is gone.
- `Auto-Fill From Website` remains the first content block on Workspace Home.
- Guardrails remain visible: draft only, human review required, no sends, no automation.
- `/workspace?section=business-profile` loads the Business Profile editor.
- `/workspace?section=knowledge-sources` loads Knowledge Sources and the Site Import Assistant.
- Existing draft run/fact review data remained visible.

## Safety

No new site import run or fact was created during this QA pass.

No sends, workflows, inbox connections, crawler/AI extraction, payments, calendar writes, or integrations were triggered.

## Remaining

- Complete mobile-width Workspace QA in a session with working viewport control.
- Continue Dr. Hong workspace/knowledge-base population only after Ross approves real/sanitized source facts.
