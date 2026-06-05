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
## 2026-06-03 Authenticated Browser QA Access Restored

Codex fixed the authenticated UI QA blocker by bypassing the crashing in-app browser connector and attaching Playwright to a dedicated Chrome QA browser through local Chrome remote debugging on port `9222`.

Ross logged into the Chrome QA browser, and Codex successfully performed authenticated read-only navigation across every left-navigation module.

New reports saved:

- `09-exports/playwright-chrome-qa-tutorial.md`
- `09-exports/authenticated-platform-audit-2026-06-03.md`

Key authenticated findings:

- Dashboard, Leads, Patients, Appointments, Communication Hub, Payments, Analytics, Staff, Automation Center, Subscription, and Settings load behind admin login.
- Automation Activity Logs are present and show prior workflow executions.
- Auto-Assignment Rules is currently broken because `assignment_rules` is referenced by the frontend but missing/unavailable in Supabase schema cache.
- Video Consultation and main Profile route are currently "Coming Soon".
- Subscription state appears inconsistent, sometimes showing `Professional` and sometimes `No Plan` for the same logged-in session.
- Communication Hub external inbox and internal chat tabs open; internal chat currently shows an empty select-channel state.
- Settings tabs open, including Integrations, Email Logs, and Audit Log.

Current next step: continue authenticated QA module by module, starting with Automation Center safe-testing protocol and Supabase/backend verification before triggering any send/test/payment actions.
## 2026-06-03 n8n / Hostinger Recovery Investigation

Ross asked for the cheapest/free path to recover or replace the old n8n setup.

Hostinger hPanel was visible in the Chrome QA browser. The old VPS `srv841701.hstgr.cloud` is shown as offline on KVM 4, with a renewal prompt showing 12 days remaining and a visible discounted renewal price of `$28.99/mo`. No paid action was clicked.

Codex found local old/reference n8n workflow exports at `D:\BUZZOOKA WORKSPACE\Products\ClinicPilot X\04-automations\old-n8n-workflows`. The credentials file was not opened. Safe metadata confirms reusable workflow exports for Gmail/email agent, SMS/Twilio, VAPI inbound calling, outbound reachout, notifications, and daily clinic-member reporting.

Report saved at `09-exports/n8n-hostinger-recovery-options-2026-06-03.md`.

Current recommendation: do not renew Hostinger yet. First map the local n8n workflow exports against the current ClinicPilotX Automation Center and decide which automations can run through existing Supabase/Lovable infrastructure. n8n hosting should be added only if there is a confirmed need.
## 2026-06-04 GitHub / Laptop Transfer Status

Ross confirmed no hosted n8n account will be purchased. Hostinger renewal, n8n Cloud, Oracle Cloud, and new paid VPS options are rejected for this stage.

Official GitHub repo created and verified:

`https://github.com/aihustler2025/ClinicPilotX`

The old repo `aihustler2025/clinicpilot-x` exists but remains old/wrong-project history and must not be used as the official source of truth.

Transfer plan saved at `09-exports/github-laptop-n8n-local-transfer-plan-2026-06-04.md`.

Next step: push local `main` from `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX` to GitHub, then clone the repo onto the laptop for local n8n review/testing.
## 2026-06-05 Laptop n8n Transfer Plan

Ross confirmed ClinicPilotX will need n8n for automation review/testing, but no paid hosted n8n path will be used right now.

Current direction:

- GitHub source of truth: `https://github.com/aihustler2025/ClinicPilotX`
- PC working mirror: `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`
- Laptop target folder: `%USERPROFILE%\Documents\ClinicPilotX`
- Laptop n8n role: local review/testing/import only
- Production rule: do not make commercial ClinicPilotX depend on laptop-hosted n8n for client-facing workflows.

New handoff saved at:

`docs/handoffs/Codex-to-Laptop-Codex-001-clinicpilotx-local-n8n-transfer.md`

Recommendation: use a hybrid automation strategy. Supabase/Lovable should carry core product automations that must be reliable for clients. Local n8n should be used to import, inspect, and map old workflows. Later, if n8n is clearly required for production, move it to proper hosted infrastructure after cost/security/backups are solved.
