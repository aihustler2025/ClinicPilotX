# Lovable Paste Message 046 - Phase 1 Visual QA Fix

Please fix one Phase 1 QA issue only. Build mode is okay for this small polish fix.

Codex QA passed the desktop visual/chrome refresh, but found a mobile overflow issue on the Dashboard.

Observed on `https://clinic-pilot-x.lovable.app/dashboard` at a phone-sized viewport:

- Viewport set to `390x844`.
- Document client width was `375`.
- Document scroll width was `401`.
- A horizontal scrollbar appears at the bottom of the mobile dashboard.
- The dashboard cards load correctly after data readiness, so this is not a data-loading blocker.
- It looks like a shell/header/page-width issue from the Phase 1 visual refresh.

Fix request:

- Remove mobile horizontal overflow from the app shell/dashboard.
- Keep the Phase 1 visual direction: slate background, Plus Jakarta Sans, indigo accent, sticky header, refreshed sidebar, refreshed dashboard cards.
- Do not change routes or IA.
- Do not touch CRM logic, migrations, RLS, edge functions, workflows, integrations, credentials, sends, payments, calendar actions, webhooks, or Settings > Clinic Workspace.
- Do not start Phase 2 yet.

After the fix, report the exact files changed and confirm typecheck/build status.
