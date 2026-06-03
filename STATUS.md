# ClinicPilotX Status

Last updated: 2026-05-27

## Current State

ClinicPilotX has been established as the official Buzzooka product workspace for this project. The project is already far along in Lovable, but its current structure, backend, data model, integrations, and readiness have not yet been independently audited.

Official local workspace:

`D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`

Filesystem findings:

- External drive detected: `D:\`
- Buzzooka Workspace detected: `D:\BUZZOOKA WORKSPACE`
- Standard product folder detected: `D:\BUZZOOKA WORKSPACE\02-PRODUCTS`
- Official ClinicPilotX folder detected and expanded: `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`
- A separate spaced folder also exists at `D:\BUZZOOKA WORKSPACE\Products\ClinicPilot X`; do not use or compare it unless Ross explicitly asks.

## Git State

- Local Git repo initialized in the official workspace.
- Branch: `main`
- Initial baseline commit: `71d4010 Initialize official ClinicPilotX project memory`
- Local Git identity for this repo: `Codex <codex@buzzooka.local>`
- Remote: none connected yet.

## GitHub State

- GitHub CLI status: `gh` is not installed in the local shell.
- GitHub connector currently available to Codex can read/write files in an existing repository, but no repo creation tool is available in this session.
- GitHub repository still needs to be created manually or identified by repo URL/full name before the local folder can be connected and pushed.

## Current Rule

Do not build or approve new Lovable build work until the current Lovable project has been audited and its claims have been verified.

## Immediate Next Step

Send the first Lovable audit/intake message from:

`docs/handoffs/Codex-to-Dashboard-Lovable-001-project-audit-intake.md`

After Lovable replies, save the response as the next matching `Dashboard-Lovable-to-Codex-001-...md` file, then review the claims and create a verification plan.

## 2026-06-02 Clarification

Ross confirmed the official new ClinicPilotX workspace is `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`.

The old folder `D:\BUZZOOKA WORKSPACE\Products\ClinicPilot X` is not the active project. It contains 118 files and is connected to the old GitHub repo `aihustler2025/clinicpilot-x`, with May 2026 project-management history from the wrong Lovable project. Do not use that repo or its Markdown files as the new source of truth.

A scan of the old/reference folder found no Word or PDF source documents. The only non-Markdown files found were old n8n JSON workflow exports and one CSV inventory. Inventory saved at `09-exports/old-reference-non-md-inventory-2026-06-02.md`.

Next step: wait for Ross to provide/login to the new Lovable preview so Codex can perform live QA across every left-navigation module, inspect behavior, collect bugs, and prepare the next Lovable inventory/audit message.

## 2026-06-02 Source Document Review

Ross provided 30 Word/PDF/XLSX source materials from `D:\PROJECTS\CLINICPILOT X (Old)`. Codex extracted and reviewed them as product reference inputs. Summary saved at `09-exports/source-material-review-2026-06-02.md`.

High-level finding: the durable product intent is an AI-powered clinic front desk system with unified lead capture, acknowledgments, staff alerts, appointment request handling, reminders, deposits/payments, outgoing follow-up, review requests, PriorityBook scoring, Automation Center settings, and optional voice/chat/social integrations.

Caveat: many docs assume an older n8n/Google Sheets architecture. Current Lovable backend and database must be audited before any build decisions.

## 2026-06-02 Live App Pre-Login Inventory

Codex audited https://clinic-pilot-x.lovable.app without login. Lovable project ID resolved as `8b4d9031-af8d-4faf-81d3-135c41ad73b7`; Lovable connector reports status `ready`.

The deployed app is protected and redirects protected routes to `/auth`, so Codex does not yet have full access. Valid admin login is needed for click-by-click QA.

Backend evidence from deployed bundle shows standalone Supabase project `imuyfbvsombbpgdgkhrb` at `https://imuyfbvsombbpgdgkhrb.supabase.co`. UI copy also mentions Lovable Cloud secrets for integration credentials, so the current assumption is standalone Supabase for DB/auth plus Lovable-managed secrets for integrations until Lovable confirms.

Pre-login report saved at `09-exports/live-app-inventory-prelogin-2026-06-02.md`. Next Lovable handoff saved at `docs/handoffs/Codex-to-Dashboard-Lovable-002-live-app-inventory-and-security-questions.md`.

High-priority findings: public anon read access appears too broad on some operational tables, and internal chat tables return an RLS infinite recursion error.

## 2026-06-03 Platform Investigation Update

Ross logged into Supabase, GitHub, and Lovable in the in-app browser, but Codex's browser-control connector still crashes in this Windows sandbox and cannot use the authenticated tab. Codex therefore performed a deeper deployed-code/backend investigation instead.

Report saved at `09-exports/platform-investigation-2026-06-03.md`.

Key additions:

- Current app uses standalone Supabase project `imuyfbvsombbpgdgkhrb` for DB/auth/realtime/storage.
- Edge/server functions referenced by frontend: `ai-assistant`, `ai-suggestions`, `auto-assign-leads`, `calculate-lead-score`, `create-payment-link`, `send-email`, `send-sms`, `test-workflow-message`, and `workflow-appointment-confirmation`.
- No literal n8n references were found in the deployed frontend bundle.
- Automation Center has 19 workflow rows, with 7 enabled and several config UIs present.
- Do not test Automation Center sends/payments until sandbox/live credential status is confirmed.
- GitHub repo `aihustler2025/ClinicPilotX` still does not exist; old `aihustler2025/clinicpilot-x` remains old/reference-only.
