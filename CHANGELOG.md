# ClinicPilotX Changelog

## 2026-05-27

- Established `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX` as the official local project workspace.
- Expanded project memory files: `AGENTS.md`, `STATUS.md`, `TASKS.md`, `DECISIONS.md`, `CHANGELOG.md`, `PRODUCT_SPEC.md`, and `README.md`.
- Created required `docs/handoffs/` and `09-exports/` folders.
- Prepared first Lovable audit/intake handoff: `docs/handoffs/Codex-to-Dashboard-Lovable-001-project-audit-intake.md`.
- Initialized local Git repo on `main`.
- Created initial baseline commit: `71d4010 Initialize official ClinicPilotX project memory`.
- Recorded GitHub setup blockers: no `gh` CLI installed and no repository connected yet.

## 2026-05-22

- Created initial ClinicPilotX workspace memory skeleton.

## 2026-06-02

- Confirmed official workspace is `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`.
- Marked `D:\BUZZOOKA WORKSPACE\Products\ClinicPilot X` and GitHub repo `aihustler2025/clinicpilot-x` as old/reference-only for this new project.
- Inventoried non-Markdown files in the old/reference folder; no Word/PDF source materials were found.
- Revised first Lovable audit handoff to explicitly avoid old repo/project assumptions.

## 2026-06-02 Source Review

- Reviewed 30 provided ClinicPilot source materials from the old source-document folder.
- Saved source-material review at `09-exports/source-material-review-2026-06-02.md`.
- Added durable product concepts to `PRODUCT_SPEC.md` with an architecture caveat about older n8n/Google Sheets assumptions.

## 2026-06-02 Live App Pre-Login Audit

- Audited deployed app at `https://clinic-pilot-x.lovable.app` without login.
- Resolved Lovable project ID `8b4d9031-af8d-4faf-81d3-135c41ad73b7` and confirmed Lovable connector status `ready`.
- Identified standalone Supabase backend `imuyfbvsombbpgdgkhrb` from deployed bundle.
- Captured route/nav inventory and Supabase table inventory.
- Found public anon readability concerns on operational tables and RLS infinite recursion on internal chat tables.
- Created pre-login inventory report and Lovable handoff 002.

## 2026-06-03 Platform Investigation

- Attempted to connect to authenticated in-app browser session; connector still fails in Windows sandbox.
- Performed deeper deployed-code/backend investigation instead.
- Identified Supabase Edge/server functions referenced by frontend.
- Confirmed no direct n8n references in deployed frontend bundle.
- Summarized Automation Center workflow configuration coverage.
- Saved platform investigation report at `09-exports/platform-investigation-2026-06-03.md`.
## 2026-06-03

- Restored authenticated UI QA path using dedicated Chrome QA browser and Playwright after in-app browser connector failures.
- Added `09-exports/playwright-chrome-qa-tutorial.md` for Ross.
- Added `09-exports/authenticated-platform-audit-2026-06-03.md` with first authenticated module inventory and QA findings.
- Documented verified early bugs: missing `assignment_rules` backend support, inconsistent plan state, Video Consultation/Profile coming soon, and empty Internal Chat state.
## 2026-06-03 n8n Recovery

- Investigated Hostinger status read-only: old VPS is offline and renewal prompt shows approximately `$28.99/mo`.
- Found local old n8n workflow exports for email, SMS/Twilio, VAPI inbound calling, outbound outreach, notifications, and daily reporting.
- Added `09-exports/n8n-hostinger-recovery-options-2026-06-03.md`.
- Recommended not renewing Hostinger until local workflow exports are mapped and proven insufficient.
## 2026-06-04 GitHub Setup

- Verified official GitHub repository `aihustler2025/ClinicPilotX` exists and is empty.
- Added `https://github.com/aihustler2025/ClinicPilotX.git` as the official local repo remote.
- Recorded laptop/local n8n transfer plan and no-paid-hosting decision.
## 2026-06-05 Laptop n8n Handoff

- Added `docs/handoffs/Codex-to-Laptop-Codex-001-clinicpilotx-local-n8n-transfer.md`.
- Confirmed local laptop n8n will be used for review/testing/import only.
- Recorded hybrid automation strategy: Supabase/Lovable for core reliable product automations, n8n for workflow review and optional future orchestration.
## 2026-06-05 Handoff Revision

- Revised laptop Codex handoff to include broader Lovable architecture context.
- Added Lovable Cloud/Supabase preference because Ross's Lovable package includes backend/hosting benefits.
- Added note that a separate partially built marketing website exists in Lovable and may need coordination or merging with the main CRM/dashboard project.
- Clarified that laptop file references are available through the GitHub clone, not through this PC's D-drive.
## 2026-06-05 Laptop Clone and Docker Check

- Cloned the official GitHub repo to `C:\Users\user\Documents\ClinicPilotX`.
- Verified Git is installed on the laptop.
- Confirmed Docker Desktop is not currently installed or available on PATH.
- Added `09-exports/laptop-local-n8n-setup-status-2026-06-05.md`.
- Added Lovable clarification handoff 003 for dashboard, marketing website, Lovable Cloud, Supabase, hosting, GitHub, and Automation Center questions.
- Updated `STATUS.md`, `TASKS.md`, and `PRODUCT_SPEC.md` for the laptop n8n blocker and architecture direction.

## 2026-06-10 Docker Desktop Install Attempt

- Downloaded Docker Desktop for Windows from Docker's official installer URL.
- Ran Docker Desktop installer in per-user mode.
- Verified Docker Desktop and Docker CLI files now exist under `C:\Users\user\AppData\Local\Programs\DockerDesktop`.
- Ran elevated WSL setup commands.
- Docker/n8n remains blocked because WSL 2 reports virtualization is not enabled on this machine.
- Next required step is restart and, if still blocked, enabling CPU virtualization in BIOS/UEFI.

## 2026-06-11 Local n8n Running

- Verified Docker Desktop is running with WSL 2 backend.
- Created persistent Docker volume `clinicpilotx_n8n_data`.
- Started local n8n container `clinicpilotx-n8n` on port `5678`.
- Verified `http://localhost:5678` returns HTTP `200 OK`.
- Confirmed next step is local-only n8n owner account creation, with no live credentials and no active workflows.

## 2026-06-11 First n8n Workflow Import

- Ross completed local n8n owner setup.
- Created `09-exports/n8n-workflows/clinicpilotx-test-lead-intake-webhook.json`.
- Imported `ClinicPilotX - Test Lead Intake Webhook` into local n8n.
- Verified the imported workflow is inactive and uses no credentials.
- Added `09-exports/n8n-local-workflow-inventory-2026-06-11.md`.

## 2026-06-11 Project Manager Reorientation

- Ross clarified that Codex should manage the entire existing ClinicPilotX Lovable project, not begin from n8n or rebuild from scratch.
- Reviewed Ross's BUZZOOKA Work System diagrams and adopted GitHub as cross-device project brain for laptop/PC continuity.
- Added `docs/clinicpilotx-project-takeover-operating-model.md`.
- Updated `AGENTS.md`, `STATUS.md`, and `TASKS.md` with the project-manager operating model and next audit tasks.

## 2026-06-11 Authenticated Dashboard Audit

- Connected browser control to the authenticated in-app browser on the laptop.
- Completed a safe read-only left-navigation sweep of the live ClinicPilotX dashboard.
- Added `09-exports/authenticated-dashboard-module-audit-2026-06-11.md`.
- Verified first module readiness matrix across Dashboard, Leads, Patients, Appointments, Communication Hub, Video Consultation, Payments, Analytics, Staff, Automation Center, Auto-Assignment Rules, Subscription, Settings, and Profile.
- Verified Automation Center Workflows and Activity Logs tabs open, with recent Appointment Confirmation executions visible.
- Recorded safety rule to avoid send/call/payment/workflow actions until credentials and sandbox/live status are confirmed.

## 2026-06-11 Controlled CRM QA

- Added user-guide and QA documentation structure.
- Added controlled dummy-data plan.
- Created and edited dummy lead `CPX TEST Lead June 11`.
- Verified Leads create, search, and edit behavior.
- Added `docs/user-guide/leads.md`.
- Added `09-exports/controlled-crm-test-log-2026-06-11.md`.
- Logged concern that editing a lead appears to change status/temperature automatically.
- Verified Lead Details and Convert to Patient for the dummy lead.
- Verified the converted patient appears in Patients.
- Attempted a dummy appointment booking for the converted patient and logged a likely no-confirmation/no-persistence issue.
- Expanded controlled CRM QA notes for future user-guide/tutorial documentation.
- Added `docs/qa/leads-human-qa-script.md` so Ross's assistant can repeat the Leads test flow.
- Logged Leads status filter and export UX concerns, including confusing `Show Converted` count behavior.
- Added Lovable handoff 004 for Leads module improvements: phone formatting, service selector, source fields, richer details/timeline, export dialog, and future chatbot/email/contact-form intake readiness.
- Added two more controlled dummy leads for future chatbot/email intake testing and confirmed status/temperature can mutate unexpectedly after later lead creation.

## 2026-06-24 Phase 1A Tenant Root QA

- QA-tested Lovable's published Phase 1A tenant root foundation.
- Verified core CRM routes still load after publish and the Dashboard still shows real metrics.
- Verified new tenant root tables exist on the live Supabase project and anonymous reads return no rows.
- Verified new profile columns exist and helper functions return safe anonymous values.
- Logged the remaining Settings fetch error as a blocker before onboarding/setup work.
- Added `09-exports/request-018-phase-1a-tenant-root-qa-2026-06-24.md`.
- Added `docs/handoffs/Lovable-paste-message-019-phase-1a-qa-followup-settings.md`.

## 2026-06-24 Request 019 Settings Fix QA

- QA-tested Lovable's frontend-only Settings fix after publish.
- Confirmed the original indefinite spinner no longer remains forever, but Settings still fails because it renders `Settings row missing — contact support.`
- Confirmed no Settings form controls or tabs render, so the reversible notification toggle/save/revert QA could not be performed.
- Logged that `Error fetching settings: Object` still appears after visiting Appointments/Automation.
- Added `09-exports/request-019-settings-fix-qa-2026-06-24.md`.
- Added `docs/handoffs/Lovable-paste-message-020-settings-row-missing-followup.md`.

## 2026-06-24 Request 020 Settings Grant QA

- QA-tested Lovable's narrowed Settings grant fix after publish.
- Verified Settings now renders the real Settings UI after hard reload.
- Verified the reversible Call Notifications off/save/on/save QA path.
- Verified Audit Log records both settings saves with actor `teambuzzooka@gmail.com`.
- Verified Dashboard, Leads, Patients, Appointments, Payments, Communication Hub, and Automation Center still load.
- Added `09-exports/request-020-settings-grant-qa-2026-06-24.md`.
- Added `docs/handoffs/Lovable-paste-message-021-phase-1b-planning-only.md`.

## 2026-06-25 Request 021 Phase 1B Migration QA

- QA-tested the live app after Ross reported Lovable ran the approved Phase 1B additive migration.
- Verified Dashboard, Leads, Patients, Appointments, Payments, Communication Hub, Automation Center, and Settings still load.
- Verified no visible `No Plan`, permission, missing-table, or Settings errors in the checked routes.
- Confirmed `clinic_id` is selectable through read-only REST on 20 of the 23 expected tables.
- Logged that internal chat tables could not be verified through REST because of the known `internal_channel_members` RLS recursion.
- Received corrected Lovable completion evidence confirming all 23 tables were backfilled with non-null `clinic_id`, row counts were unchanged, and 23 indexes/FKs exist.
- Added `09-exports/request-021-phase-1b-migration-qa-2026-06-25.md`.
- Added `docs/handoffs/Lovable-paste-message-022-phase-1b-evidence-and-app-scope-plan.md`.
- Added `docs/handoffs/Lovable-paste-message-023-phase-1b1-app-scope-plan.md`.

## 2026-06-25 Clinic Knowledge Base Roadmap

- Captured Ross's future per-clinic Knowledge Base requirement.
- Added `docs/clinic-knowledge-base-roadmap.md`.
- Updated `PRODUCT_SPEC.md` and `TASKS.md` so the idea is parked without interrupting Phase 1B.1 work.

## 2026-06-25 Phase 1B.1a Active Clinic QA

- QA-tested Lovable's Phase 1B.1a active-clinic app-code slice after publish.
- Confirmed Lead creation works from the UI with a safe test email.
- Found blocker: Add Patient is blocked by `No active clinic selected. Contact an admin.`
- Added `09-exports/request-024-phase-1b1a-active-clinic-qa-2026-06-25.md`.
- Added `docs/handoffs/Lovable-paste-message-025-phase-1b1a-patient-active-clinic-fix.md`.
