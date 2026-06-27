# ClinicPilotX Status

Last updated: 2026-06-24

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
## 2026-06-05 Handoff Revision: Lovable Cloud, Marketing Site, and Laptop File Access

Ross clarified that ClinicPilotX is primarily a Lovable-based project and that his Lovable package includes Lovable Cloud/back-end/hosting benefits. Future planning should prefer Lovable Cloud/Lovable hosting/Supabase before recommending unrelated paid hosting or backend platforms.

Ross also clarified that there is a separate, partially built ClinicPilotX marketing website in Lovable that may need to merge or coordinate with the main CRM/dashboard Lovable project. Product/dashboard functionality remains the priority, but the marketing website must be tracked as part of the broader architecture.

The laptop handoff now explicitly states that repo-relative paths like `docs/handoffs/...`, `AGENTS.md`, `STATUS.md`, and `09-exports/...` are available only after cloning GitHub onto the laptop. The laptop does not need access to this PC's D-drive to read project memory.

Updated handoff:

`docs/handoffs/Codex-to-Laptop-Codex-001-clinicpilotx-local-n8n-transfer.md`

## 2026-06-05 Laptop Clone and Docker Check

Laptop Codex cloned the official GitHub repo to:

`C:\Users\user\Documents\ClinicPilotX`

Verified Git is installed at:

`C:\Program Files\Git\cmd\git.exe`

Verified the required repo-relative files are available after clone, including `AGENTS.md`, `STATUS.md`, `TASKS.md`, `PRODUCT_SPEC.md`, `docs/handoffs/`, and `09-exports/`.

Docker Desktop is not currently available on this laptop:

- `docker` command not found on PATH.
- `C:\Program Files\Docker\Docker\Docker Desktop.exe` not found.
- `com.docker.service` not found.

Local n8n setup is therefore blocked until Ross installs and starts Docker Desktop for Windows. Status report saved at:

`09-exports/laptop-local-n8n-setup-status-2026-06-05.md`

Lovable clarification handoff created at:

`docs/handoffs/Codex-to-Dashboard-Lovable-003-project-backend-marketing-cloud-clarification.md`

Current next step: Ross installs Docker Desktop with WSL 2 backend, starts Docker, then Codex can create the persistent n8n volume and run `clinicpilotx-n8n` on port `5678`.

## 2026-06-10 Docker Desktop Install Progress

Ross asked Codex to handle Docker Desktop/n8n setup directly because he is not a developer.

Codex downloaded Docker Desktop for Windows from Docker's official desktop installer URL and ran the installer in per-user mode.

Current installed paths:

- Docker Desktop app: `C:\Users\user\AppData\Local\Programs\DockerDesktop\Docker Desktop.exe`
- Docker CLI: `C:\Users\user\AppData\Local\Programs\DockerDesktop\resources\bin\docker.exe`

Codex also ran elevated WSL setup commands:

- `wsl --install`
- `wsl --install --no-distribution`

Current blocker:

- `wsl --status` reports WSL default version 2.
- WSL 2 still cannot start because virtualization is not enabled on this machine.
- Docker Desktop is installed, but the Docker engine cannot run until virtualization is enabled and Docker Desktop starts successfully.

Next step: restart the laptop, then open Docker Desktop. If Docker/WSL still reports virtualization disabled, enable CPU virtualization in BIOS/UEFI before continuing n8n setup.

## 2026-06-11 Local n8n Running

Ross created/sign-in to Docker Personal and restarted the laptop.

Docker Desktop is now running successfully:

- Docker Desktop version: `4.77.0`
- Docker engine version: `29.5.3`
- Docker context: `desktop-linux`
- WSL default distribution: `docker-desktop`
- WSL default version: `2`

Codex created the persistent n8n Docker volume:

`clinicpilotx_n8n_data`

Codex started the local n8n container:

`clinicpilotx-n8n`

Container status:

- Running.
- Image: `docker.n8n.io/n8nio/n8n`
- Port mapping: `0.0.0.0:5678->5678/tcp`
- n8n version from logs: `2.25.7`
- Local URL verified with HTTP `200 OK`: `http://localhost:5678`

Current next step: Ross creates the first local-only n8n owner account in the browser. Do not connect live credentials and do not activate workflows.

## 2026-06-11 First Local n8n Workflow Imported

Ross completed local n8n owner setup.

Codex created and imported the first safe local n8n workflow:

`ClinicPilotX - Test Lead Intake Webhook`

Workflow file:

`09-exports/n8n-workflows/clinicpilotx-test-lead-intake-webhook.json`

Verified by n8n export:

- Workflow exists in local n8n.
- `active: false`
- No credentials.
- Nodes: webhook intake, field normalization, JSON confirmation response.

Codex also searched common laptop folders for old non-credential `.json` exports and did not find obvious ClinicPilotX workflow exports. A workflow inventory was created at:

`09-exports/n8n-local-workflow-inventory-2026-06-11.md`

Current direction: Codex can build workflows directly from Ross's plain-English automation descriptions. Old n8n JSON recovery remains useful if Ross can provide/copy the files, but it is not required to begin safe local prototyping.

## 2026-06-11 Project Manager Reorientation

Ross clarified that Codex's core role is to manage the whole existing ClinicPilotX project, not start from n8n or rebuild from scratch.

Operating model confirmed:

- GitHub is the cross-device project brain.
- PC and laptop are workstations/mirrors.
- Lovable is the main app build partner.
- Codex is project manager, auditor, QA lead, documentation keeper, and automation architect.
- Google Drive/cloud storage is for large client assets and deliverables.
- n8n is local review/testing/import support, not the center of the product.

Ross logged into the live dashboard in the in-app browser at:

`https://clinic-pilot-x.lovable.app/dashboard`

Current limitation: this Codex session can see the current in-app browser URL from context, but no direct browser-control tool is currently exposed. If direct click-by-click inspection remains unavailable, Codex must use Lovable/GitHub/deployed-bundle evidence and ask Ross for screenshots or a controllable browser session for module QA.

New operating model document:

`docs/clinicpilotx-project-takeover-operating-model.md`

Current next step: complete authenticated dashboard audit, send/collect Lovable project clarification, and create module/workflow readiness matrices before approving build work.

## 2026-06-11 In-App Browser Control Restored and Dashboard Audit Started

Codex connected browser control to the authenticated in-app browser on the laptop. No separate Playwright install is currently needed for the in-app audit path.

Read-only authenticated audit completed across the live left-navigation modules at:

`https://clinic-pilot-x.lovable.app`

New report saved:

`09-exports/authenticated-dashboard-module-audit-2026-06-11.md`

Key verified points:

- Dashboard, Leads, Patients, Appointments, Communication Hub, Payments, Analytics, Staff, Automation Center, Subscription, and Settings load behind login.
- Video Consultation and main Profile route still show `Coming Soon`.
- Auto-Assignment Rules still appears broken/stuck at `Loading assignment rules...`.
- Automation Center Workflows and Activity Logs tabs open.
- Automation Center shows current plan `Professional` and `7 / 13 Active` during this pass.
- Activity Logs show completed `Appointment Confirmation` workflow executions from about 15 days earlier.
- Settings tabs verified: General, Notifications, Integrations, Profile, Email Logs.
- Settings > Integrations includes Twilio, Facebook Messenger, Viber, Google Calendar, Stripe, and email test fields, and states API credentials are managed via Lovable Cloud secrets.

Current rules remain unchanged: do not trigger send/call/payment/workflow actions and do not approve new Lovable build work until backend, secrets, Supabase, and project structure are confirmed.

Current next step: perform a second safe Automation Center configuration audit, then create the first controlled test-data plan for Leads, Patients, Appointments, Communication, and Payments.

## 2026-06-11 Controlled CRM QA Started

Ross approved safe dummy-data testing and emphasized that QA notes must become future product documentation/tutorial material.

Codex created:

- `docs/user-guide/README.md`
- `docs/user-guide/leads.md`
- `docs/qa/controlled-test-data-plan.md`
- `09-exports/controlled-crm-test-log-2026-06-11.md`

First dummy record:

- Lead: `CPX TEST Lead June 11`
- Email: `cpx.test+lead-20260611@example.com`

Verified:

- Add Lead form works.
- Created lead persisted in the lead table.
- Lead count increased from 11 to 12 after creation.
- Search found the dummy lead and filtered unrelated leads out.
- Edit Lead dialog prefilled existing values.
- Edited service/notes saved successfully.

New concern:

- Editing the dummy lead changed status/temperature from `NEW LEAD`/cold to `CONTACTED`/hot without an explicit status/temperature edit. This may be intentional scoring/status logic or an unintended side effect and needs investigation before final documentation.

## 2026-06-11 Controlled CRM QA Continued

Additional verified flow:

- Lead Details opened successfully for the dummy lead.
- The details view showed contact info, service, notes, timeline, Details/Communication/Activity sections, and action buttons.
- No live Call, Email, Message, Calculate Score, or Mark as Lost action was triggered.
- Converted `CPX TEST Lead June 11` to a patient.
- Verified the converted patient appears in Patients with the same email and phone, active status, 0 visits, and $0.00 value.
- Verified Appointments booking form lists the converted patient and auto-fills name/email/phone.

New concerns:

- Subscription/entitlement display still flickers between `Professional` and `No Plan` on CRM pages.
- Appointment booking attempt for `CPX TEST Appointment Audit` closed the modal but showed no clear success message; the total stayed at 26 and the new appointment was not visible. Treat as a likely booking persistence/confirmation issue until Lovable/backend logs confirm the cause.

Current next step: document these findings, commit/push the QA docs, then continue with patient edit testing, Dashboard/Analytics validation, and a Lovable fix prompt for the appointment booking and plan-state inconsistencies.

## 2026-06-11 Leads Human QA Script Added

Ross clarified that each module audit should produce a repeatable human tester script after Codex performs its own testing.

Created:

- `docs/qa/leads-human-qa-script.md`

Additional Leads findings:

- Status pills are clickable and change table/filter state.
- Summary cards appear to remain overall totals instead of reflecting the active status filter.
- `Show Converted 0` produced confusing count/table behavior during QA and needs Lovable review.
- Export is currently too opaque from a UX standpoint. It should become an export dialog with scope, status/date/source filters, file type, column selection, estimated row count, and clear filename.

Current browser limitation: Codex cannot inspect downloaded export files inside the in-app browser, so human QA must verify downloaded CSV/XLSX contents.

## 2026-06-11 Leads Improvement Direction

Ross reviewed the Create New Lead modal and confirmed Leads is not done yet.

New requirements captured:

- Phone should use a country code picker and auto-format from digits-only typing.
- For U.S./Canada-style numbers, display should be like `+1 (555) 123-4567`.
- Service Requested should become a searchable dropdown/combobox with custom service support.
- Leads should eventually receive records from chatbot, website contact forms, email inquiry automation, phone/voice assistant, manual entry, and social channels.
- Lead Details should eventually show the full relationship timeline: conversations, files/photos, follow-ups, assignment, status changes, appointment booking, and conversion.

Created Lovable handoff:

- `docs/handoffs/Codex-to-Dashboard-Lovable-004-leads-module-improvements.md`

Do not build chatbot/email/social automations yet. For now, make Leads data/UI ready for those future intake sources.

Additional dummy data added:

- `CPX TEST Chatbot Lead 01` / `cpx.test+chatbot-lead-01@example.com`
- `CPX TEST Email Lead 01` / `cpx.test+email-lead-01@example.com`

New confirmed concern:

- After creating `CPX TEST Email Lead 01`, the previously created `CPX TEST Chatbot Lead 01` changed from `NEW LEAD`/Cold to `CONTACTED`/Hot without explicit editing. The status/temperature mutation bug is broader than the earlier edit-flow concern.

## 2026-06-11 Published Leads v2 QA After Lovable Build

Ross approved and published Lovable's Leads module improvement build. Codex tested the live published app at:

`https://clinic-pilot-x.lovable.app/leads`

New dummy lead created:

- `CPX TEST Leads V2 20260611-19504`
- `cpx.test+leads-v2-20260611-19504@example.com`

Verified:

- Add Lead dialog now includes contact, phone country selector, service selector, source, preferred contact, urgency, consent, and notes fields.
- Phone accepts digits-only input and stores normalized E.164 value, verified as `+12135550199`.
- Service selector saved `Botox`.
- New dummy lead initially saved as `NEW LEAD` and `Cold`.
- Lead Details tabs now include Overview, Timeline, Comms, Files, and Activity.
- Timeline logs `Lead created` and `Lead edited`.
- Files tab correctly shows a disabled future storage/upload placeholder and no live upload path.

Blocking issue still present:

- Editing only the notes on the new dummy lead changed temperature from `Cold` to `Hot` while status stayed `NEW LEAD`. Lovable's response claimed edit safety and scoped temperature triggers, but live QA shows temperature is still being recalculated/mutated by a safe edit.

Additional polish issues:

- Invalid phone entry such as `5551234567` kept the create dialog open without an obvious visible validation message during QA.
- U.S. phone display currently appears like `+1 213 555 0199`; Ross requested the cleaner display style `+1 (213) 555-0199` for U.S./Canada-style numbers.
- Export dialog could not be fully verified from the active detail-panel state in this pass and still needs retest after Lovable fixes the blocking temperature issue.

New Lovable fix request saved at:

`docs/handoffs/Lovable-paste-message-005-leads-v2-qa-fixes.md`

Current next step: send the above GitHub handoff link to Lovable in Plan mode and do not treat Leads as complete until the notes-only edit preserves both status and temperature.

## 2026-06-12 Leads v2 Fix QA After Lovable Publish

Ross approved and published Lovable's Leads v2 QA fix build.

Codex retested the live published app at:

`https://clinic-pilot-x.lovable.app/leads`

New dummy lead created:

- `CPX TEST Leads V2 fixB-678321`
- `cpx.test+leads-v2-fixb-678321@example.com`

Verified:

- Invalid phone input now shows a visible inline validation message and blocks creation.
- Replacing invalid phone input with valid U.S. digits clears the validation message.
- Lead creation with valid phone succeeds after consent is checked.
- New lead starts as `NEW LEAD` and `Cold`.
- Notes-only edit preserves `NEW LEAD` and `Cold`; the previous temperature mutation blocker is resolved for this QA path.
- Timeline shows both `Lead created` and `Lead edited`.
- Lead detail panel includes the formatted U.S. phone display `+1 (213) 555-0199`.

Remaining non-blocking polish:

- The main Leads table still displays the normalized E.164 phone value `+12135550199`; consider formatting the table display too.
- The invalid-phone helper example still uses spaced format rather than the preferred U.S./Canada display style.
- Export dialog still needs a focused retest.

## 2026-06-12 Leads Export QA

Codex performed a focused Leads export retest on the live published app.

Verified:

- Leads page returned to `Professional` state and 15 leads after using the page Refresh control.
- Export now opens an `Export Leads to CSV` dialog.
- Dialog includes scope choices for all leads, current filters, and selected-only leads.
- `Current filters (15)` is selected by default.
- `Selected only (0)` is disabled when no rows are selected.
- Dialog includes a column picker for lead fields.
- Column toggles are interactive; Codex unchecked `Phone` and verified the unchecked state.
- Dialog shows an estimated export count: `15 rows will be exported`.

Not verified:

- Actual CSV file contents, filename, row count, headers, and column inclusion/exclusion, because the Codex in-app browser reports downloads are not supported and Chrome extension control was unavailable in this session.

Additional issue reconfirmed:

- The `No Plan` / 0-lead subscription/data-load flicker still appears before page Refresh restores `Professional` / 15 leads.

Detailed QA note saved at:

`09-exports/leads-export-qa-2026-06-12.md`

Current next step: continue the controlled CRM audit with Patients edit and Appointments booking persistence. Leads export file-content QA remains pending for a normal browser download.

## 2026-06-12 Patients / Appointments QA

Codex continued controlled QA using the converted dummy patient:

- `CPX TEST Lead June 11`
- `cpx.test+lead-20260611@example.com`
- UI patient ID: `#PT00024`

Verified:

- Patients page loads with `Professional` visible.
- Converted dummy patient appears in the Patients list.
- Clicking the dummy patient opens a patient detail panel.
- Detail panel shows contact information, medical information, appointments, transactions, notes, and action buttons.

Issues found:

- No obvious `Edit Patient` / update action is exposed from the patient detail panel.
- Clicking `Book Appointment` from the patient detail panel did not open a booking dialog or visible booking state.
- This compounds the prior appointment issue where booking from the Appointments module closed without visible success or a new appointment row.

New detailed QA note:

`09-exports/patients-appointments-qa-2026-06-12.md`

New Lovable plan-mode handoff:

`docs/handoffs/Lovable-paste-message-006-patients-appointments-qa-fixes.md`

Current next step: send the Lovable handoff in Plan mode only, then review Lovable's plan before approving any build.

## 2026-06-12 Patients / Appointments Fix QA After Lovable Publish

Ross approved and published Lovable's Patients/Appointments fix build.

Codex retested the live published app with the converted dummy patient:

- `CPX TEST Lead June 11`
- `cpx.test+lead-20260611@example.com`
- UI patient ID: `#PT00024`

Verified:

- Patient detail now exposes an `Edit` button.
- Patient notes edit saved and persisted after reopening the patient detail panel.
- Patient detail `Book Appointment` now opens a prefilled booking modal on `/appointments`.
- TEST toggle is on by default for this patient-detail booking path.
- Required-field validation keeps the booking modal open and shows visible errors.
- A valid TEST appointment saved successfully.
- Success toast explicitly included `TEST - no sends`.
- Appointments count increased to 27.
- The new appointment row appeared with service `CPX TEST Appointment Audit 2026-06-12`, date `Jun 12, 2026`, time `2:45 PM`, status `Pending`, and a `TEST` badge.
- Returning to Patients showed the appointment details from the patient side.

Detailed note saved at:

`09-exports/patients-appointments-fix-qa-2026-06-12.md`

Current next step: continue broader Appointments QA, including calendar behavior, status changes, dashboard/analytics updates, and Lovable/Supabase confirmation that TEST rows cannot trigger live sends even when workflows are active.

## 2026-06-12 QA Process Clarification and Patients Polish Direction

Ross clarified that every module needs both:

- Codex-run QA, where Codex directly tests the module.
- Human-assistant QA scripts, so Ross or a future assistant can repeat the same checks step by step.

Codex added:

- `docs/qa/patients-human-qa-script.md`
- `docs/qa/appointments-human-qa-script.md`
- `docs/phone-number-standard.md`
- `docs/handoffs/Lovable-paste-message-007-patients-module-and-phone-standard.md`

Product decision:

- Store canonical phone numbers in E.164 for Twilio/VAPI readiness, for example `+15558878888`.
- Display phone numbers in friendly localized format, for example `+1 (555) 887-8888` for U.S./Canada.
- Staff should type digits only after choosing a country; they should not type parentheses, spaces, or dashes.
- Leads and Patients should use the same shared phone input behavior.

Current next step: send Lovable handoff 007 in Plan mode only for Patients export and shared phone input polish.

## 2026-06-14 Patients Phone / Export QA Failed After Publish

Ross approved and published Lovable's revised Patients module polish / shared phone standard build.

Codex QA-tested the live published Patients module at:

`https://clinic-pilot-x.lovable.app/patients`

Result: fail. The live app does not appear to include the planned Patients phone/export changes.

Findings:

- `Add Patient > Phone` is still a plain text input with placeholder `+1 (555) 123-4567`.
- `Add Patient > Emergency Contact Phone` is still plain.
- `Edit Patient > Phone` is still plain and showed raw E.164 for the dummy patient: `+15005550111`.
- No country picker, flag, or `+1` selector was visible in Add/Edit Patient.
- Clicking Patients `Export` did not open an export dialog with scope/columns/row count.
- Patient list phone display remains mixed: friendly formatted values, raw E.164 values, and legacy hyphenated values.

New QA report:

`09-exports/patients-phone-export-qa-2026-06-14.md`

New Lovable plan-mode fix request:

`docs/handoffs/Lovable-paste-message-008-patients-phone-export-qa-failed.md`

Current next step: send Lovable handoff 008 in Plan mode only. Do not treat Patients phone/export polish as complete.

## 2026-06-14 Repeat Publish QA / Lovable Workstream Mismatch

Ross published after Lovable reported changes involving Financial Transparency wording, volunteer waiver language, `docs/QA_TESTING.md`, `docs/CONTENT_EDITING.md`, `docs/RUNBOOK.md`, and an internal `/handoff` page.

Codex QA-tested the active ClinicPilotX dashboard again at:

`https://clinic-pilot-x.lovable.app`

Result: fail / likely project or build mismatch.

Findings:

- `/handoff` returns a 404 page on the active ClinicPilotX app.
- The official local ClinicPilotX GitHub clone does not contain `docs/QA_TESTING.md`, `docs/CONTENT_EDITING.md`, or `docs/RUNBOOK.md`.
- Patients `Add Patient > Phone` and `Emergency Contact Phone` are still plain text inputs.
- Patients Export still does not show the expected scope/columns/row-count dialog.
- Patient phone display remains mixed, including raw E.164-like values such as `+15005550111`.

New QA report:

`09-exports/patients-phone-export-qa-repeat-2026-06-14.md`

New Lovable plan-mode fix request:

`docs/handoffs/Lovable-paste-message-009-patients-publish-mismatch.md`

Current next step: send Lovable handoff 009 in Plan mode only. Ask Lovable to confirm correct project, publish target, GitHub connection, and exact files before any further build approval.

## 2026-06-14 Patients Phone / Export Fix QA Partial Pass

Ross approved and published Lovable's corrected Patients phone/export implementation for the active ClinicPilotX dashboard.

Codex QA-tested the live Patients module and confirmed the previous publish/workstream mismatch is resolved for this feature pass.

Verified:

- Patients Add/Edit now uses the shared country-aware phone input.
- Existing and newly created patient phones display in friendly U.S./Canada format such as `+1 (213) 555-0199`.
- Valid U.S. digits save successfully and persist.
- Invalid short phone numbers show visible validation.
- Patient detail shows formatted main and emergency phone values.
- Patients Export now opens an `Export Patients to CSV` dialog with scope, row count, column picker, and separate display/E.164 phone columns.

Remaining issues:

- Optional phone fields can default to validation-blocking `+1`, especially Emergency Contact Phone in Add Patient.
- U.S./Canada typing currently shows `+1 213 555 0199` inside the input rather than Ross's preferred `+1 (213) 555-0199`.
- Export downloaded CSV contents still require a normal-browser download check because the Codex in-app browser cannot save downloads.
- Leads may inherit the same optional `+1` behavior and should be checked/fixed at the shared component level.

New QA report:

`09-exports/patients-phone-export-fix-qa-2026-06-14.md`

New Lovable plan-mode follow-up:

`docs/handoffs/Lovable-paste-message-010-patients-phone-polish-followup.md`

Current next step: send Lovable handoff 010 in Plan mode only. Do not mark Patients phone/export as complete until optional phone handling and export CSV content verification are resolved.

## 2026-06-19 Patients Phone Polish QA After Lovable Publish

Ross approved and published Lovable's Patients phone polish follow-up. Codex retested the authenticated live app.

Result: partial pass / fail due to one blocker.

Verified:

- Patients still loads behind login.
- Existing patient list/detail phone display can show friendly U.S./Canada values such as `+1 (213) 555-0199`.
- Patients Export opens a scoped `Export Patients to CSV` dialog with row count, column picker, and display/E.164 phone columns.
- Invalid Patients phone entry is blocked with visible inline validation.
- Leads blank-phone regression passes: `CPX TEST Lead Blank Phone 20260619` was created with phone left untouched at default `+1`, and the saved lead shows blank phone instead of bare `+1`.

Blocking issue:

- Add Patient failed for a normal authenticated user with `permission denied for function generate_patient_id`.
- This blocks final Add Patient QA and must be fixed before Patients phone/export polish can be considered complete.

Remaining polish:

- Add/Edit Patient phone inputs still show spaced values such as `+1 213 555 0199` inside the form instead of the preferred `+1 (213) 555-0199`.
- Invalid phone helper copy still uses spaced example text.
- CSV file contents remain unverified because the Codex in-app browser does not support downloads.

New QA report:

`09-exports/patients-phone-polish-qa-2026-06-19.md`

New Lovable plan-mode fix request:

`docs/handoffs/Lovable-paste-message-011-patients-phone-polish-qa-fixes.md`

Current next step: send handoff 011 to Lovable in Plan mode only. Do not treat Patients as complete until Add Patient works, form phone formatting is polished, and CSV export contents are confirmed.

## 2026-06-19 Patients Phone / ID Fix QA After Lovable Publish

Ross approved and published Lovable's Patient ID / phone polish fix. Codex retested the authenticated live app through Chrome.

Result: pass for the prior blocker and main Patients phone/export requirements.

Verified:

- Add Patient now succeeds for a normal authenticated staff user.
- The previous `permission denied for function generate_patient_id` blocker did not recur.
- Created patient `CPX TEST Patient ID Fix 20260619` with valid main phone and untouched blank emergency phone.
- Patient list displays `+1 (213) 555-0199`.
- Edit Patient pre-fills main phone as `(213) 555-0199` with a separate `+1` country chip.
- Blank emergency phone remains blank in Edit Patient.
- Updating the patient without touching emergency phone succeeds.
- Leads blank-phone regression passes with `CPX TEST Lead Blank Phone PostID 20260619`.
- Patients CSV export downloaded in Chrome and was verified:
  - 26 rows.
  - Display and E.164 phone columns present.
  - New dummy patient exported with `Phone (Display)=+1 (213) 555-0199` and `Phone (E.164)=+12135550199`.
  - Emergency phone export fields were blank.

Remaining issue:

- Invalid Add Patient phone UX is still wrong. A short phone value `123` closed the modal without visible validation and did not create a visible patient row. The modal should stay open and show inline validation.

New QA report:

`09-exports/patients-phone-id-fix-qa-2026-06-19.md`

New Lovable plan-mode follow-up:

`docs/handoffs/Lovable-paste-message-012-patients-invalid-phone-ux.md`

Current next step: send handoff 012 to Lovable in Plan mode only for the small invalid-phone UX fix. Patients phone/export is otherwise close to complete for the tested Add/Edit/Export paths.

## 2026-06-19 Patients Invalid Phone Final QA

Ross approved and published Lovable's Request 012 invalid-phone UX fix. Codex retested the live app.

Result: pass.

Verified:

- Add Patient with invalid short phone `123` keeps the modal open.
- Inline helper appears with the approved example: `+1 (213) 555-0199`.
- No invalid patient row is created.
- Valid Add Patient regression still passes with `CPX TEST Patient Valid Phone Final 20260619`.
- Valid patient row displays `+1 (213) 555-0199`.
- Blank emergency phone remains non-blocking.
- Leads invalid-phone regression also passes: invalid lead phone keeps the modal open, shows helper text, and does not create a lead row.

New QA report:

`09-exports/patients-invalid-phone-final-qa-2026-06-19.md`

Current status: Patients phone/export polish is complete for the tested Add/Edit/Export/phone-validation paths. Broader Patients module QA still remains for delete confirmation, filters/sort, full detail tabs, and downstream appointment regressions.

## 2026-06-19 Patients Broader Module QA

Codex continued broader Patients module QA on the live authenticated app after the phone/export validation passed.

Verified:

- Patients search can isolate `CPX TEST Patient Valid Phone Final 20260619` and hide unrelated patients.
- Status filter options are present: `All Statuses`, `Active`, `Inactive`, `Archived`.
- Selecting `Inactive` filtered the list to inactive patient results during this pass.
- Sort options are present: `Name (A-Z)`, `Recently Added`, `Most Visits`, `Highest Spent`.
- `Most Visits` and `Highest Spent` produced plausible ranked ordering.
- Patient detail for `CPX TEST Patient Valid Phone Final 20260619` opens and shows contact details, formatted phone, summary metrics, action buttons, Appointments tab, and Transactions tab.

Delete QA status:

- The row action menu exposes `View Details`, `Edit Patient`, and `Delete Patient`.
- `Delete Patient` triggers a native browser confirmation dialog.
- Codex did not intentionally accept deletion.
- The native confirmation caused the browser automation connector to hang before a controlled cancel/confirm verification could be completed.

New QA report:

`09-exports/patients-broader-module-qa-2026-06-19.md`

Current next step: start a fresh browser QA pass for patient-detail `Book Appointment` regression and delete cancel/confirm behavior using a disposable dummy patient only.

## 2026-06-19 Patient Profile / Leads Intake Direction Captured

Ross clarified that the Patients side panel should be treated as the patient profile surface, not a throwaway demo panel.

Near-term patient profile work:

- Continue QA on open/view/edit behavior.
- Retest `Book Appointment` from the patient profile with TEST mode on.
- Treat `Call`, `Message`, and `Video` as dependent on Communication Hub and Video Consultation audits before activation.
- Later expand profile content into a fuller patient record with communication history, files/photos, appointments, transactions, notes, and follow-up context.

Ross also clarified again that Leads is not close to done. Manual lead creation is only the foundation. Future lead sources include contact form/email, AI-filtered inbox intake, chatbot, SMS, phone/AI voice, Facebook, WhatsApp, Viber, and other social/messaging sources.

New roadmap document:

`docs/patient-profile-and-leads-intake-roadmap.md`

Current next step remains: fresh browser QA pass for patient-profile `Book Appointment`, then continue Appointments and Communication Hub audit before connecting live actions.

## 2026-06-20 Patient Profile Booking / Delete QA

Codex created a disposable dummy patient:

- `CPX TEST Disposable Patient Delete QA 20260620`
- `cpx.test+delete-qa-20260620@example.com`
- UI patient ID `#PT00028`

Verified:

- Add Patient still works.
- Saved phone displays as `+1 (213) 555-0199`.
- Patient profile side panel opens.
- Profile shows email, formatted phone, notes, Appointments tab, Transactions tab, and actions.
- `Book Appointment` from the patient profile navigates to `/appointments`.
- Booking modal opens with the disposable patient prefilled.
- TEST checkbox is on before submit and the no-send warning is visible.

Blocking issue:

- Saving the TEST appointment fails with `Invalid time format (HH:MM)` even after Codex enters and verifies native time input value `15:30`.
- Appointment count stayed `27`; the test appointment was not created.

Delete QA:

- Row action menu shows `View Details`, `Edit Patient`, and `Delete Patient`.
- `Delete Patient` triggers a native browser confirmation.
- The native confirmation froze the browser automation connector again before cancel/confirm could be safely verified.
- Codex did not intentionally accept deletion.

Reconfirmed:

- Patients can briefly show `No Plan` / `No patients found`; reload restored `Professional` and the real patient list.

New QA report:

`09-exports/patient-profile-booking-delete-qa-2026-06-20.md`

New Lovable plan-mode handoff:

`docs/handoffs/Lovable-paste-message-013-patient-profile-booking-delete-fixes.md`

Current next step: send Request 013 to Lovable in Plan mode only. Do not continue Appointments module completion until the patient-profile booking time validation bug is fixed.

## 2026-06-20 Request 013 Fix QA

Ross approved and published Lovable's Request 013 fix. Codex retested the live app.

Passed:

- Patient-profile `Book Appointment` now opens `/appointments` with booking modal open.
- Disposable patient `CPX TEST Disposable Patient Delete QA 20260620 (#PT00028)` was prefilled.
- TEST checkbox was on and no-send warning was visible.
- Time input retained `15:30`.
- Submit succeeded.
- Appointment count increased from `27` to `28`.
- New appointment appeared with TEST badge.
- Patient profile Appointments tab showed the new appointment.
- Patient delete now uses an in-app AlertDialog instead of native browser confirm.
- Delete cancel leaves patient intact.
- Delete confirm removed the disposable patient; reload/search showed `No patients found`.

New issues:

- After delete, stale patient profile panel remained open until reload.
- Deleting the patient did not remove or otherwise resolve the related TEST appointment; Appointments still shows the deleted patient name/phone.
- Appointment row phone display still shows raw E.164 `+12135550199`.
- Patient profile appointment time displays as `15:30:00`.
- Ross provided Appointments calendar/detail drawer screenshots showing the same raw-phone issue on an older appointment: `+150055501111`.
- Appointment detail drawer includes action buttons such as `Confirm`, `Cancel`, `Send Reminder`, and `Add to Google Calendar`; these remain untested because live reminder/calendar side effects require explicit safety review.

New QA report:

`09-exports/patient-profile-booking-delete-fix-qa-2026-06-20.md`

New Lovable plan-mode handoff:

`docs/handoffs/Lovable-paste-message-014-patient-delete-related-records-polish.md`

Current next step: send Request 014 to Lovable in Plan mode only. Need a product-safe decision on whether deleting patients with related appointments should be blocked, archived, or cascade/anonymize related records.

## 2026-06-21 Request 014 Partial QA

Ross approved and published Lovable's Request 014 archive-vs-delete and appointment display polish build.

Codex verified the live Appointments list through Chrome after the in-app browser control runtime failed to attach to the logged-in tabs.

Verified:

- Appointments list loads with 28 total appointments.
- The `CPX TEST Disposable Patient Delete QA 20260620` appointment now displays phone as `+1 (213) 555-0199`, not raw E.164.
- The older `CPX TEST Lead June 11` appointment from Ross's screenshot now displays phone as `+1 (500) 555-0111`, not raw E.164.
- Appointment list times display as friendly times such as `3:30 PM` and `2:45 PM`, not `15:30:00`.

Not yet verified:

- Patient hard-delete path for zero related records.
- Patient archive-only path for related appointments/payments.
- Stale patient profile panel closure after archive/delete.
- Archived patient filter behavior.
- Appointments calendar/detail drawer display polish.

QA note saved at:

`09-exports/request-014-partial-qa-2026-06-21.md`

Current next step: re-run Request 014 destructive archive/delete QA only when reliable browser control is available. Do not ask Ross to do this manually; Codex should perform the QA directly.

## 2026-06-21 Request 014 Live QA Complete

Codex restored in-app browser control using the current installed browser plugin path and completed the live Request 014 QA directly.

Core Request 014 result: pass.

Verified:

- Appointments list and calendar/detail drawer now show friendly phone and time formatting for the tested rows.
- Zero-related patient hard-delete path works with the correct `Delete patient?` dialog, cancel behavior, and confirm behavior.
- Related-record patient path archives instead of deleting with the correct `Archive patient?` dialog, related record counts, cancel behavior, and confirm behavior.
- No `Delete anyway` option appears when related records exist.
- Archived patient is hidden under Active filter and visible under Archived filter.
- Related TEST appointment remains visible after archive, preserving history.

New follow-up polish found:

- Booking modal disabled patient phone field still shows raw E.164.
- Appointment calendar/detail drawer labeled a patient-created appointment as `Lead`.
- Appointment drawer shows stray `0` text near action buttons.
- Patients page can still intermittently load as `No Plan` / `No patients found` before routing through Dashboard restores `Professional`.

New files:

- `09-exports/request-014-live-qa-2026-06-21.md`
- `docs/handoffs/Lovable-paste-message-015-request-014-followup-polish.md`

Current next step: send Lovable Request 015 in Plan mode only for the remaining polish issues.

## 2026-06-22 Request 015 Live QA Complete

Ross approved and published Lovable's Request 015 follow-up polish build.

Codex retested the live authenticated app directly.

Result: pass for the tested Request 015 scope.

Verified:

- Booking modal disabled phone field now displays active patient phone in friendly format, for example `+1 (213) 555-0199`, not raw E.164.
- Appointments list still displays the archived QA appointment phone/time as `+1 (213) 555-0102` and `3:45 PM`.
- Appointments Calendar View drawer now labels the patient-linked appointment as `Patient`, not `Lead`.
- Appointment drawer no longer shows the stray standalone `0` near action buttons.
- Appointment drawer still shows friendly phone/time formatting.

No live communication, payment, reminder, calendar, workflow, or webhook action was triggered.

New QA report:

`09-exports/request-015-live-qa-2026-06-22.md`

Current next step: begin broader Appointments module QA using TEST appointments only, starting with safe status-action rules for `Confirm` and `Cancel`, then filters/search/export/calendar consistency. Do not test reminders or Google Calendar writes without explicit safety approval.

## 2026-06-23 Appointments Broader QA

Codex completed a safe broader QA pass on the live authenticated Appointments module.

Result: partial pass / follow-up required.

Verified:

- Appointments list loads real data after the known `No Plan` flicker is cleared by routing through Dashboard.
- Search works for known QA text such as `Archive Related`.
- Keyboard clearing search restores the full list.
- Filter dialog opens with Status, Consultation Type, and Payment Status controls.
- Consultation Type and Payment Status dropdown options are present.
- Sort options are present, and `Date Ascending` changes list order.
- Calendar View shows the June 2026 TEST appointments.
- Calendar drawer still shows friendly phone/time, `Patient` label, and no stray `0`.

Issues found:

- Initial Appointments load can still show `No Plan` and `0 total appointments`.
- Appointment Status filter is missing `Pending` even though visible rows and summary cards use `Pending`.
- Status labels are inconsistent, including raw `Payment_pending` and casing mismatch like `Checked in` vs `Checked In`.
- `Date Range` expands but no visible date picker/dialog appears.
- `Export` shows a success toast but no Appointments export dialog, and no download event was captured in the controlled browser.
- Some legacy phone values still display as unformatted invalid fallback, for example `+1 234567890`.

No live communication, payment, reminder, calendar, workflow, webhook, Confirm, or Cancel action was triggered.

New files:

- `09-exports/appointments-broader-qa-2026-06-23.md`
- `docs/handoffs/Lovable-paste-message-016-appointments-broader-qa-fixes.md`

Current next step: send Lovable Request 016 in Plan mode only. Do not approve build mode until Lovable explains the files/components/functions it will inspect or edit and confirms no live-send/calendar/payment/workflow paths will be activated.

## 2026-06-23 Request 016 Appointments QA

Ross approved and published Lovable's Request 016 Appointments polish build.

Codex retested the live authenticated Appointments module.

Result: pass for the tested Request 016 UI and safety scope, with one CSV download caveat.

Verified:

- Direct `/appointments` navigation no longer showed the previous `No Plan` / `0 total appointments` state.
- The page loaded real data after a neutral loading state.
- Appointment Status filter now includes `Pending`, `Completed`, `Payment Pending`, and other aligned status labels.
- `Payment Pending` filter returned the expected row and displays friendly text.
- Date Range now exposes presets, Clear, and Apply.
- Appointments Export now opens a scoped dialog with column picker, row count preview, Display Phone, and E.164 Phone columns.
- Legacy invalid phone fallback now shows `+1234567890 (unverified)`.
- Calendar drawer still shows friendly phone/time, `Patient` label, and no stray `0`.
- `Send Reminder` and `Add to Google Calendar` are disabled.
- `Confirm` and `Cancel` each open explicit confirmation dialogs stating no SMS/email/calendar/refund side effects.

Not accepted:

- Codex did not accept Confirm or Cancel status changes.
- Codex did not trigger reminders, Google Calendar, Request Payment, SMS, email, workflows, or webhooks.

Caveat:

- The controlled browser did not capture a CSV download event after `Download CSV`; verify actual file contents later through a normal Chrome download path.
- The known `Error fetching settings: Object` console error still appears.

New QA report:

`09-exports/request-016-appointments-qa-2026-06-23.md`

Current next step: continue Appointments completion with a controlled TEST-only status-action QA plan, or move to Dashboard / Analytics verification to confirm metrics reflect CRM data correctly. Keep reminders, payment, calendar, SMS, email, and workflow sends gated.

## 2026-06-24 Dashboard / Analytics QA

Codex performed a read-only authenticated Dashboard / Analytics pass after Request 016 Appointments QA.

Result: partial pass / Dashboard follow-up required.

Verified source module data:

- Leads page shows `17` total leads, including `9` new, `5` contacted, and `3` qualified.
- Patients page shows populated patient records.
- Appointments page shows `29 total appointments`, including `6` pending, `13` confirmed, and `4` completed.
- Analytics page is scoped to `Jun 01 - Jun 30` and shows `3` appointments, which appears plausible from visible June TEST appointments.

Issue:

- Dashboard still shows all-zero/empty-state values such as `Total Leads 0`, `Leads by Source No leads data available`, and `Recent Leads No leads yet`, despite the source modules containing data.

New files:

- `09-exports/dashboard-analytics-qa-2026-06-24.md`
- `docs/handoffs/Lovable-paste-message-017-dashboard-analytics-qa-fixes.md`
- `docs/qa/dashboard-analytics-human-qa-script.md`

Current next step: send Lovable Request 017 in Plan mode only. Do not approve build until Lovable explains Dashboard data sources, metric scopes, and whether the recurring `Error fetching settings: Object` console error is related to empty Dashboard data or prior context flicker.

## 2026-06-24 Request 017 Dashboard QA

Ross approved and published Lovable's Request 017 Dashboard metrics build. Codex retested the live app.

Result: pass for the tested Dashboard scope.

Verified:

- Dashboard no longer shows the old permanent all-zero/empty-state metrics.
- Dashboard resolves to real/scoped values after auth/session/data readiness.
- `Total Leads` shows `20`; this appears to be all-time leads, including converted leads.
- Leads page still shows `17` active pipeline leads, so the difference is explainable by scope.
- Leads by Source sums to `20`.
- `Conversion Rate 15%` is consistent with 3 converted leads out of 20 total leads.
- Dashboard `Pending 3` is plausible because Request 017 excludes TEST rows, while Appointments shows `6` pending including 3 TEST pending appointments.
- `Follow-ups` now shows `Coming soon` instead of a fabricated number.
- `Revenue (MTD)` shows `$0`.
- `Recent Leads` now displays real lead rows.

Known remaining note:

- The recurring `Error fetching settings: Object` console error still appears after visiting Appointments and remains a separate follow-up ticket.

New QA report:

`09-exports/request-017-dashboard-qa-2026-06-24.md`

Current next step: continue Appointments completion with controlled TEST-only status-action QA for Confirm and Cancel. Keep Send Reminder, Google Calendar, Request Payment, SMS, email, workflows, and webhooks gated.

## 2026-06-24 Appointments Status Actions QA

Ross approved continuing Appointments internal status testing after clarifying the near-term demo goal.

Codex tested status changes on a TEST appointment only:

- `CPX TEST Archive Related QA 20260621`
- `CPX TEST Archive Appointment 20260621`

Result: pass for the tested internal status-action scope.

Verified:

- `Confirm` opens a safety dialog saying the action only updates status and sends no SMS, email, or calendar invite.
- Accepting Confirm changed the TEST appointment from `Pending` to `Confirmed`.
- `Cancel` opens a safety dialog saying the action only updates status and sends no cancellation SMS, email, or refund.
- Accepting Cancel changed the same TEST appointment from `Confirmed` to `Cancelled`.
- The appointment remained visible with the TEST badge.
- Appointments list showed the row as `Cancelled`.
- Pending summary dropped from `6` to `5`.

Not clicked:

- Send Reminder.
- Add to Google Calendar.
- Payments.
- SMS/email/workflows/webhooks.

New files:

- `09-exports/appointments-status-actions-qa-2026-06-24.md`
- `docs/dr-hong-demo-roadmap.md`

Current next step: begin read-only Communication Hub audit, then Automation Center audit focused on email intake/lead workflows. The near-term demo priority is Dr. Colin Hong client setup, email AI filtering, and chatbot/API lead intake. Payments, video, WhatsApp, Messenger, Viber, Telegram, Google Calendar writes, and live SMS remain deferred.

## 2026-06-24 Communication Hub Read-Only Audit

Codex completed a read-only audit of the live Communication Hub.

Result: partial / not ready for the Dr. Hong demo yet.

Verified:

- Communication Hub loads behind authentication.
- External Messages tab is present.
- Internal Chat tab is present.
- External Messages shows 11 conversation records.
- Visible channel labels include SMS, WhatsApp, and Messenger.
- Visible contact labels include Patient and Lead.
- Filters panel opens with Channel, Date Range, and Contact Type controls.
- Search narrowed results for `Brandon`.

Issues:

- Clicking a visible external conversation did not open the detail pane; the pane stayed on `Select a conversation`.
- Internal Chat shows `Kizha Kaye`, but clicking her produced `Failed to create direct message channel`.
- No visible email inbox or email AI filtering surface exists in Communication Hub yet.
- Some seeded/demo messages include appointment confirmation and payment request wording; treat as demo data until source and send-log behavior are confirmed.

New files:

- `09-exports/communication-hub-readonly-audit-2026-06-24.md`
- `docs/qa/communication-hub-human-qa-script.md`

Current next step: audit Automation Center read-only, with focus on email filtering, lead intake, appointment request detection, and workflow safety. After Automation Center audit, create a Lovable plan-mode request for the Dr. Hong demo foundation.

## 2026-06-24 Automation Center Read-Only Audit

Codex completed a read-only Automation Center audit.

Result: partial / high-risk area.

Verified:

- Automation Center loads behind authentication.
- Current plan shows `Professional`.
- Active workflow count shows `7 / 13 Active`.
- Workflows and Activity Logs tabs are present.
- Activity Logs show real workflow execution history, including Smart Follow-up, Lead Acknowledgment, and Appointment Confirmation.
- Several active workflows are send-capable.

Important findings:

- `Lead Acknowledgment` is active and has SMS/email templates plus `Send Test SMS` and `Send Test Email`.
- `Appointment Confirmation` is active, shows `Executions 21`, has send templates, and says confirmations are currently sent 5 minutes after appointments are booked.
- `Smart Follow-up Sequence` is active and SMS-style lead nurture oriented.
- `No-Show Recovery` is active and SMS-oriented, with copy indicating it can send immediately if delay is 0.
- `Lead Scoring & Assignment` configure panel is only a placeholder: `Configuration not available for this workflow yet.`
- No visible workflow currently handles incoming email AI sorting, spam filtering, email-to-lead conversion, external chatbot intake, website contact form intake, or client knowledge base setup.

Not clicked:

- Send Test SMS.
- Send Test Email.
- Save Configuration.
- Workflow switches.
- Upgrade.
- Credentials.

New files:

- `09-exports/automation-center-readonly-audit-2026-06-24.md`
- `docs/qa/automation-center-human-qa-script.md`
- `docs/handoffs/Lovable-paste-message-018-dr-hong-demo-foundation.md`

Current next step: send Lovable Request 018 in Plan mode only. Do not approve build until Lovable explains the client/clinic setup, test inbox email AI sorting, lead intake API/webhook, Automation Center relationship, Communication Hub relationship, and no-live-send safeguards.

## 2026-06-24 Request 018 Reframed As Product Foundation

Ross clarified that ClinicPilotX is a multi-client subscription product and that Dr. Colin Hong is the first pilot/test clinic workspace, not a custom-only build.

Request 018 was rewritten to focus on product foundation:

- multi-client clinic/workspace structure,
- onboarding/setup wizard,
- client knowledge base,
- clinic branding/logo/business profile,
- services/pricing/business hours,
- staff/team roles and permissions,
- subscription plan gates,
- Google Calendar planning without live writes,
- email AI sorting,
- chatbot/contact-form/API lead intake,
- Automation Center relationship,
- Communication Hub relationship,
- app-native Lovable/Supabase automation strategy instead of relying on expired n8n.

New handoff:

`docs/handoffs/Lovable-paste-message-018-product-foundation-client-onboarding-automation.md`

Current next step: send the revised Request 018 in Plan mode only.

## 2026-06-24 Request 018 Phase 1A Tenant Root QA

Ross approved and published Lovable's Phase 1A tenant root foundation.

Lovable reported:

- pilot clinic `Dr. Colin Hong (Pilot)` created,
- `teambuzzooka@gmail.com` seeded as owner and platform admin,
- `kizha.buzzooka@gmail.com` seeded as admin,
- `profiles.active_clinic_id` set for both users,
- no existing app table, policy, or app code touched.

Codex retested the live app and performed read-only Supabase API checks.

Result: partial pass / follow-up required before Phase 1B.

Verified:

- Dashboard, Leads, Patients, Appointments, Communication Hub, and Automation Center still load behind authentication.
- Professional plan state remained visible during the pass.
- No Dashboard zero-data regression was observed.
- New tables `clinics`, `clinic_members`, `clinic_invitations`, `platform_admins`, and `platform_admin_audit` exist on live Supabase project `imuyfbvsombbpgdgkhrb`.
- Anonymous reads to those new tables return zero rows.
- New profile columns `active_clinic_id` and `onboarding_completed_at` exist.
- Helper functions exist and return safe anonymous values (`false`/`null`).
- No live sends, workflow actions, calendar writes, payment writes, or webhook calls were triggered during QA.

Issue:

- Settings remains stuck at `Loading settings...` with console error `Error fetching settings: Object`. This appears pre-existing, but it should be fixed before clinic onboarding/setup work.

Limitation:

- Codex cannot independently verify exact seeded member/profile rows from the current UI because Phase 1A has no UI and RLS correctly hides tenant/admin rows from anonymous reads. Lovable/Supabase should confirm with read-only SQL before Phase 1B.

New files:

- `09-exports/request-018-phase-1a-tenant-root-qa-2026-06-24.md`
- `docs/handoffs/Lovable-paste-message-019-phase-1a-qa-followup-settings.md`

Current next step: send Request 019 to Lovable in Plan mode only. Do not begin Phase 1B until the Phase 1A seed rows are confirmed and the Settings fetch error is diagnosed/fixed.

## 2026-06-24 Request 019 Settings Fix QA

Ross approved and published Lovable's frontend-only Settings fix.

Lovable also reported live Phase 1A evidence passed:

- pilot clinic `Dr. Colin Hong (Pilot)` / `dr-colin-hong`,
- `teambuzzooka@gmail.com` owner and platform admin,
- `kizha.buzzooka@gmail.com` admin,
- both profiles have the pilot `active_clinic_id`,
- helper/RLS checks passed.

Codex retested `/settings`.

Result: failed / follow-up required before Phase 1B.

Observed:

- `/settings` still does not render the Settings form.
- The page first shows `Loading settings...`.
- After waiting, it shows `Settings row missing - contact support.`
- No Settings tabs or form controls are visible.
- The requested notification toggle save/revert QA could not be performed.
- `Error fetching settings: Object` still appeared after visiting Appointments and Automation Center.

Core page spot checks:

- Leads, Patients, Appointments, and Automation Center still load.
- Appointments still shows `29 total appointments`.
- Automation Center still shows `Professional` and `7 / 13 Active`.

New files:

- `09-exports/request-019-settings-fix-qa-2026-06-24.md`
- `docs/handoffs/Lovable-paste-message-020-settings-row-missing-followup.md`

Current next step: send Request 020 to Lovable in Plan mode only. Do not approve Phase 1B until Settings renders and the save/revert QA passes.

## 2026-06-24 Request 020 Settings Grant QA

Ross approved and published Lovable's narrowed Settings grant fix.

Lovable reported:

- `authenticated` now has `SELECT` on `public.settings`,
- no new schema/table/RLS/app-code changes,
- linter warnings are pre-existing permissive-RLS findings on other tables.

Codex retested the live app.

Result: pass for the tested Settings grant scope.

Verified:

- `/settings` hard reload renders the real Settings UI.
- No `Loading settings...` hang.
- No `Settings row missing - contact support` fallback.
- No Settings console errors observed.
- General, Notifications, Integrations, Profile, Email Logs, and Audit Log tabs render.
- Approved reversible QA rider passed:
  - Call Notifications toggled off,
  - save succeeded with `Settings updated successfully`,
  - Call Notifications toggled back on,
  - save succeeded again,
  - reload confirmed notification switches restored on.
- Audit Log shows both QA updates with actor `teambuzzooka@gmail.com`.
- Dashboard, Leads, Patients, Appointments, Payments, Communication Hub, and Automation Center still load.
- No live sends, workflows, payment actions, or calendar actions were triggered.

New files:

- `09-exports/request-020-settings-grant-qa-2026-06-24.md`
- `docs/handoffs/Lovable-paste-message-021-phase-1b-planning-only.md`

Current next step: send Request 021 to Lovable in Plan mode only. Phase 1B should be planned carefully before any build because it will likely touch existing CRM data tables and tenant scoping.

## 2026-06-25 Request 021 Phase 1B Migration QA

Ross reported Lovable ran the approved Phase 1B migration and published.

The attached DOCX labeled `CLINICPILOT LOVABLE TO CODEX 25.docx` extracted as the prior exact SQL review document, not the actual migration completion/post-check report.

Codex performed live QA anyway.

Result: pass for the approved additive Phase 1B migration scope.

Verified:

- Dashboard loads with real metrics (`Total Leads 20`, `Conversion Rate 15%`, `Revenue (MTD) $0`, Recent Leads populated).
- Leads loads and shows `17` active pipeline leads.
- Patients loads with populated patient records.
- Appointments loads and shows `29 total appointments`.
- Payments loads with invoice/payment rows.
- Communication Hub loads.
- Automation Center loads with `Professional` and `7 / 13 Active`.
- Settings still renders.
- No `No Plan` state observed.
- No visible permission-denied/missing-table/settings errors observed in the checked routes.

Read-only API shape check:

- `clinic_id` is selectable on 20 of the 23 expected tables.
- `internal_channels`, `internal_messages`, and `internal_channel_members` could not be verified through anon REST because of the known pre-existing `internal_channel_members` RLS recursion.

Ross later provided the correct Lovable completion evidence:

- All 23 tables have `clinic_id`.
- All 23 tables have `0` NULL `clinic_id` rows.
- Row counts were unchanged.
- 23 `idx_<table>_clinic_id` indexes exist.
- 23 new FKs to `public.clinics(id)` exist.
- Linter warnings remain pre-existing permissive-RLS findings with no Phase 1B-attributable new findings.
- No app code, RLS, Settings, edge functions, sends, workflows, integrations, payments, calendar, or webhooks were touched.

New files:

- `09-exports/request-021-phase-1b-migration-qa-2026-06-25.md`
- `docs/handoffs/Lovable-paste-message-022-phase-1b-evidence-and-app-scope-plan.md`
- `docs/handoffs/Lovable-paste-message-023-phase-1b1-app-scope-plan.md`

Current next step: send Request 023 to Lovable in Plan mode only for Phase 1B.1 app-code planning. Do not approve app-code build until Lovable provides exact files, sequencing, QA, and rollback.

## 2026-06-25 Request 024 Phase 1B.1a Active Clinic QA

Ross approved and published Lovable's narrowed Phase 1B.1a active-clinic app-code slice.

Lovable reported:

- new `src/hooks/useActiveClinic.tsx`,
- `ClinicProvider` wrapper in `AppLayout`,
- Leads create path stamps `clinic_id`,
- Patients create path stamps `clinic_id`,
- no Appointments, Payments, Messages, Settings, RLS, migrations, edge functions, workflows, integrations, or useSubscription edits.

Codex retested the live app.

Result: failed / follow-up required before Phase 1B.1b.

Verified:

- Dashboard hard reload renders real data.
- Leads page renders.
- Add Lead with blank email/phone is rejected by current validation, so Lovable's blank-contact QA step is not valid unless validation is intentionally changed.
- Add Lead with safe `example.com` QA email succeeds.
- Leads total increased from `17` to `18`.
- New lead row appeared: `QA TEST 1B1A LEAD 20260625-1255`.
- Patients page renders.
- Add Patient with blank email/phone is rejected by current validation.

Blocking issue:

- Add Patient with safe `example.com` QA email is blocked by the new active-clinic guard.
- The UI shows `No active clinic` and `No active clinic selected. Contact an admin.`
- The same blocker repeats after reloading `/patients` and retrying.

New files:

- `09-exports/request-024-phase-1b1a-active-clinic-qa-2026-06-25.md`
- `docs/handoffs/Lovable-paste-message-025-phase-1b1a-patient-active-clinic-fix.md`

Current next step: send Lovable handoff 025 as a custom fix request. Do not proceed to Phase 1B.1b until Patients create succeeds and Lovable provides SQL evidence that both Lead and Patient inserts are stamped with the pilot `clinic_id`.

## 2026-06-25 Request 025 Phase 1B.1a Fix Retest

Ross published Lovable's Phase 1B.1a patient active-clinic fix.

Lovable reported the root cause:

- `ClinicProvider` was mounted inside `AppLayout`.
- Page components such as Patients called `useActiveClinic()` before rendering `AppLayout`, so the hook ran outside the provider tree.
- LeadFormDialog worked because it was a child component rendered inside `AppLayout`.

Lovable reported the fix:

- moved `ClinicProvider` to wrap `Routes` in `src/App.tsx`,
- removed duplicate provider from `AppLayout`,
- added loading guards to Patients and LeadFormDialog,
- no RLS, migration, edge function, workflow, useSubscription, or other module changes.

Codex retested the live app.

Result: partial pass / workflow safety follow-up required.

Verified:

- Dashboard hard reload renders real metrics.
- New Lead create succeeds:
  - `QA TEST 1B1A LEAD FIX 20260625-1439`
  - `cpx.test+1b1a-lead-fix-20260625-1439@example.com`
  - Leads active count increased from `18` to `19`.
- New Patient create succeeds:
  - `QA TEST 1B1A PATIENT FIX 20260625-1441`
  - `cpx.test+1b1a-patient-fix-20260625-1441@example.com`
  - UI showed `Success` and `Patient added successfully`.
- The previous Patient `No active clinic selected. Contact an admin.` blocker did not appear.

Safety issue:

- Automation Center Activity Logs showed new/recent activity after the QA lead creation:
  - `Completed` - `Smart Follow-up Sequence` - `1 minute ago`
  - `Failed` - `Lead Acknowledgment` - `1 minute ago`
- Codex did not click any send/test/payment/calendar/workflow/integration action.
- This appears to be automatic workflow activity from creating the QA lead, so Codex cannot certify no workflow side effects.

New files:

- `09-exports/request-025-phase-1b1a-fix-retest-2026-06-25.md`
- `docs/handoffs/Lovable-paste-message-026-phase-1b1a-workflow-safety-followup.md`

Current next step: send Lovable handoff 026 in Plan mode only. Do not proceed to Phase 1B.1b until Lovable explains the workflow activity and proposes a safe test-data strategy.

## 2026-06-25 Request 026 Phase 1B.1a Safety QA

Ross approved and published Lovable's Phase 1B.1a workflow-safety patch after exact SQL/function review.

Lovable reported:

- `is_test` added to Leads and Patients,
- existing QA rows backfilled,
- Lead Acknowledgment trigger now short-circuits for QA/test leads,
- Smart Follow-up trigger now short-circuits for QA/test leads,
- Lead and Smart Follow-up edge functions now have direct-invocation guards,
- Lead and Patient create forms auto-flag QA rows.

Codex retested the live app.

Result: pass for the tested UI and Activity Logs safety scope.

Verified:

- Automation Center Activity Logs baseline had no fresh workflow rows; newest rows were about 5 hours old.
- Created QA lead:
  - `QA TEST SAFETY 20260625-A`
  - `cpx.test+safety-A@example.com`
  - Leads active count increased from `19` to `20`.
- Created QA patient:
  - `QA TEST SAFETY PT 20260625-A`
  - `cpx.test+safety-pt-A@example.com`
  - Patient appeared in the Patients list.
- Rechecked Automation Center Activity Logs after creating both records.
- No fresh Lead Acknowledgment, Smart Follow-up, Appointment Confirmation, or other workflow rows appeared.
- Dashboard, Leads, Patients, Appointments, Payments, Communication Hub, Automation Center, and Settings rendered in a smoke pass.

Known note:

- Codex still cannot independently run authenticated SQL from the browser environment, so DB-level `is_test` and `clinic_id` assertions rely on Lovable's SQL evidence plus UI/Activity Log behavior.

New file:

- `09-exports/request-026-phase-1b1a-safety-qa-2026-06-25.md`

Current next step: Phase 1B.1a can be treated as passed for the tested scope. Ask Lovable for a Plan-mode Phase 1B.1b proposal covering Appointments and Payments active-clinic stamping only, with no live send/payment/calendar behavior.

## 2026-06-25 Request 028 Phase 1B.1b QA

Ross approved and published Lovable's Phase 1B.1b active-clinic stamping build for Appointments and Payments.

Lovable reported:

- Appointments create path stamps `clinic_id`,
- RescheduleDialog has active-clinic readiness guard,
- QuickBookingSheet stamps `clinic_id` and auto-flags test appointments from test patients,
- CreateInvoiceForm stamps `clinic_id` on payments and payment_items.

Codex retested the live app.

Result: pass for the tested UI and Automation Center Activity Logs scope.

Verified:

- Automation Center Activity Logs baseline had no fresh workflow rows.
- Created TEST appointment:
  - `QA TEST 1B1B APPOINTMENT 20260625-A`
  - `cpx.test+1b1b-appt-A@example.com`
  - `QA TEST 1B1B Consultation`
  - June 25, 2026 at 3:45 PM
- Appointment count increased from `29` to `30`.
- New appointment showed `Pending` and `TEST`.
- Toast explicitly included `(TEST - no sends)`.
- Created QA invoice:
  - `INV00017`
  - patient `QA TEST SAFETY PT 20260625-A`
  - description `QA TEST 1B1B invoice for clinic_id stamping`
  - amount `$1.00 CAD`
  - status `pending`.
- Pending Payments and Outstanding Balance increased by `$1.00`.
- Rechecked Automation Center Activity Logs after QA; no fresh workflow rows appeared.
- Dashboard, Appointments, Payments, Patients, Automation Center, and Settings rendered in smoke testing.

No payment link, Stripe checkout, send button, email, SMS, calendar, webhook, or integration action was clicked.

Known note:

- Codex still cannot independently run authenticated SQL from the browser environment, so DB-level `clinic_id` assertions rely on Lovable's implementation claim plus successful UI behavior and visible Activity Logs safety check.

New file:

- `09-exports/request-028-phase-1b1b-appointments-payments-qa-2026-06-25.md`

Current next step: Phase 1B.1b can be treated as passed for the tested scope. Ask Lovable for a Plan-mode Phase 1B.1c proposal covering messages, scheduled_messages, and conversation_notes active-clinic stamping only. Continue keeping live-send and Communication Hub send actions out of scope until separately reviewed.

## 2026-06-25 Request 031 Phase 1B.1c Internal Messages QA

Ross approved and published Lovable's revised Phase 1B.1c build after scheduled-message paths were removed from scope.

Lovable reported:

- `ConversationNotesPanel` stamps `clinic_id` with active-clinic readiness guard,
- `InternalChat` stamps `clinic_id` on `internal_messages` and `internal_channels` inserts,
- no `scheduled_messages`, live sends, payment links, edge functions, RLS, migrations, or external channels were touched.

Codex retested the live app.

Result: partial fail / follow-up required.

Verified:

- Communication Hub renders.
- Internal Chat tab renders.
- Staff member `Kizha Kaye` appears.
- Automation Center Activity Logs stayed quiet after the failed internal-chat attempt; newest visible workflow rows remained about 6 hours old.
- No live sends, payment links, calendar writes, workflows, or external-channel actions were triggered.

Issues:

- Clicking a visible external conversation still does not open the detail pane, so `ConversationNotesPanel` could not be reached for UI QA.
- Clicking `Kizha Kaye` in Internal Chat still shows `Failed to create direct message channel`.
- Console shows `Error fetching channels: Object`.
- No internal channel opens, so Codex could not send a safe internal-only test message.

New files:

- `09-exports/request-031-phase-1b1c-internal-messages-qa-2026-06-25.md`
- `docs/handoffs/Lovable-paste-message-032-phase-1b1c-internal-chat-followup.md`

Current next step: send Lovable handoff 032 in Plan mode only. Do not proceed to scheduled messages, email intake, chatbot/API intake, or Automation Center builds until internal chat/channel creation is fixed and QA passes.

## 2026-06-26 Request 032 Internal Chat Fix Plan Review

Ross provided Lovable's Phase 1B.1c internal chat fix plan.

Lovable diagnosed:

- `internal_channel_members` RLS recursion causes `Error fetching channels: Object`,
- direct-message channel creation fails because the new `internal_channels` row has no member rows before `.select().single()`,
- adding the other staff member to a DM is blocked by the current self-only `internal_channel_members` insert policy.

Codex agreed with the direction but did not approve the plan as-is because the proposed SQL needs tightening before it is run.

Required revisions:

- use a safer one-argument `is_internal_channel_member(channel_id)` helper that checks `auth.uid()` internally,
- explicitly verify the caller is a member of `current_clinic_id()` inside `create_dm_channel`,
- make `internal_messages` insert policy require `clinic_id` to match the referenced channel's `clinic_id`,
- use `DROP POLICY IF EXISTS` where appropriate,
- provide revised exact SQL before build approval.

New handoff:

- `docs/handoffs/Lovable-paste-message-033-phase-1b1c-sql-review-response.md`

Current next step: send handoff 033 to Lovable in Plan mode only. Do not approve the internal chat SQL/RPC build until Lovable provides revised exact SQL for Codex review.

## 2026-06-26 Request 033 Internal Chat Fix QA

Ross approved and published Lovable's revised internal chat SQL/RPC fix.

Lovable reported:

- migration applied,
- `InternalChat.tsx` updated to use the new RPC,
- clinic-scoped initialization added.

Codex retested the live app.

Result: pass for the tested Internal Chat fix scope.

Verified:

- Communication Hub loads.
- Internal Chat tab loads.
- Group channels now render: `All Staff`, `Doctors`, and `Front Desk`.
- No console errors appeared after the internal chat test.
- Clicking `Kizha Kaye` created/opened `DM: Kizha Kaye`.
- Sent safe internal-only message `QA TEST INTERNAL CHAT 20260626-A`.
- Message appeared in the DM thread with timestamp `10:41:49 AM`.
- Automation Center Activity Logs stayed quiet after the message; newest visible workflow rows remained `7 days ago`.
- No live SMS, email, WhatsApp, Messenger, Viber, Telegram, payment, Stripe, calendar, scheduled-message, or Automation Center test-send action was triggered.

Remaining issues:

- Automation Center/header plan state showed `No Plan` and `7 / 5 Active` during this pass.
- External conversation selection still does not open the detail pane, so `ConversationNotesPanel` remains untested from the UI.
- DB-level row verification still needs Lovable/Supabase SQL evidence.

New files:

- `09-exports/request-033-phase-1b1c-internal-chat-fix-qa-2026-06-26.md`
- `docs/clinicpilotx-current-build-control-map.md`
- `docs/qa/communication-hub-internal-chat-human-qa-script.md`

Updated:

- `docs/clinic-knowledge-base-roadmap.md`
- `docs/dr-hong-demo-roadmap.md`

Current next step: document the current build control map for Ross, then prepare the next Lovable Plan-mode request. Recommended next build planning target is clinic workspace/setup plus per-clinic Knowledge Base, because this is required for the Dr. Hong pilot and for email/chatbot automations to use the right clinic facts safely.

## 2026-06-26 Phase 1B.1c SQL Evidence Accepted

Lovable provided SQL evidence for the internal chat QA row:

- `internal_channels` DM row exists for `DM: Kizha Kaye`,
- DM row has pilot clinic id `8ed615bf...7db3`,
- two `internal_channel_members` rows exist: caller and Kizha,
- `internal_messages` row exists for `QA TEST INTERNAL CHAT 20260626-A`,
- message row has the same pilot clinic id,
- zero new rows appeared in `messages`, `scheduled_messages`, `workflow_executions`, `automation_logs`, `email_delivery_logs`, and `reminders`.

Codex rechecked the live UI:

- Internal Chat still renders.
- `DM: Kizha Kaye` persists.
- `QA TEST INTERNAL CHAT 20260626-A` persists in the DM thread.
- Automation Center Activity Logs remain quiet; newest visible workflow rows are still `7 days ago`.

Result: Phase 1B.1c can be treated as passed for the tested scope.

Next planning step:

- Clinic Workspace Setup + Per-Clinic Knowledge Base.
- UX direction: do not add Knowledge Base as a main left-nav item yet; place setup/admin controls under Settings, with a top-bar clinic/workspace selector for switching clients.

New handoff:

- `docs/handoffs/Lovable-paste-message-034-clinic-workspace-setup-knowledge-base-plan.md`

## 2026-06-26 Request 034 Clinic Workspace Plan Review

Ross provided Lovable's Clinic Workspace Setup + Per-Clinic Knowledge Base plan.

Codex reviewed it and found the product direction strong:

- no new main left-nav item,
- top-bar ClinicSwitcher concept,
- Settings > Clinic Workspace placement,
- Phase A setup UI and structured metadata,
- Phase B/C knowledge source uploads/indexing deferred,
- live integrations and send-capable paths out of scope.

Codex did not approve the build yet because the plan includes migrations, RLS policies, grants, enum checks, and table changes without exact SQL.

Answers to Lovable's open questions were documented:

- do not extend `clinic_role` blindly; provide current enum/type evidence first,
- use integer cents plus currency column from day one, default CAD for the pilot clinic,
- show Knowledge Base Sources disabled with a "Coming in Phase B" banner.

New handoff:

- `docs/handoffs/Lovable-paste-message-035-clinic-workspace-exact-sql-request.md`

Current next step: send handoff 035 to Lovable in Plan mode only. Do not click the approve/build button until Lovable returns exact forward SQL, rollback SQL, schema pre-checks, RLS policies, grants, frontend file list, and Codex reviews them.

## 2026-06-27 Request 035 Clinic Workspace Exact SQL Review

Ross provided Lovable's exact SQL response for Clinic Workspace Setup + Per-Clinic Knowledge Base Phase A.

Codex reviewed the SQL and did not approve build yet.

The product direction remains approved:

- no new main left-nav item,
- Settings > Clinic Workspace placement,
- Phase A setup UI and structured metadata only,
- Phase B/C knowledge sources, uploads, crawling, embeddings, email AI sorting, chatbot/API intake, and live integrations out of scope.

Blocking SQL/RLS concerns:

- Lovable proposed adding a new `clinics` UPDATE policy "alongside existing ones" and described it as tightening access. In Postgres/Supabase, permissive policies are OR'd together, so adding another policy does not tighten access if an older broader UPDATE policy still exists.
- Need current `public.clinics` and `public.services` policy evidence.
- Need revised SQL that drops/replaces any broader clinic UPDATE policy if required.
- Need rerun-safe service constraints, triggers, and policies.

New handoff:

- `docs/handoffs/Lovable-paste-message-036-clinic-workspace-sql-review-fixes.md`

Current next step: send handoff 036 to Lovable in Plan mode only. Do not approve the build until Lovable provides revised exact SQL and policy evidence.
