# ClinicPilotX Tasks

Last updated: 2026-05-27

## In Progress

- Audit current Lovable project before approving new build work.
- Create or connect the official ClinicPilotX GitHub repository.

## Pending

- Send first Lovable audit/intake message.
- Save Lovable response in `docs/handoffs/` using the required naming pattern.
- Review Lovable response and identify claims that require verification.
- Verify project URLs, routes, backend connection, auth, database tables, roles, and integrations.
- Create first QA checklist in `09-exports/` after Lovable returns enough project detail.
- Document verified modules in `PRODUCT_SPEC.md`.
- Create a blank GitHub repo or provide the existing official repo URL/full name.
- Add GitHub remote to local repo and push `main`.

## Blocked

- GitHub push and GitHub handoff links are blocked until an official repo exists and the local folder has a configured remote.
- Creating a GitHub repo directly from this shell is blocked because `gh` is not installed.

## Completed

- 2026-05-27: Confirmed external drive and Buzzooka Workspace location.
- 2026-05-27: Confirmed official local product folder at `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`.
- 2026-05-27: Created/updated required memory files.
- 2026-05-27: Created required `docs/handoffs/` and `09-exports/` folders.
- 2026-05-27: Prepared first Codex-to-Lovable audit/intake handoff.
- 2026-05-27: Initialized local Git repo on `main` and committed the official project memory baseline.

## Added 2026-06-02

- [x] Confirm official workspace is `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`.
- [x] Confirm old/reference folder is not the active project.
- [x] Inventory old/reference folder for non-Markdown source files.
- [x] Record rule: do not use old/reference `.md` files as source of truth.
- [ ] Create or connect new GitHub repo named `ClinicPilotX` for the official project.
- [ ] Get access to the new Lovable preview/project.
- [ ] Perform live QA across every left-navigation module/page.
- [ ] Ask Lovable for current project inventory, backend/database structure, auth roles, routes, real vs mock data, integrations, and known gaps.
- [ ] Build a QA/bug tracker in `09-exports/` after first live walkthrough.

## Source Review Tasks Added 2026-06-02

- [x] Review provided Word/PDF/XLSX ClinicPilot source materials.
- [x] Save source-material review in `09-exports/`.
- [x] Add durable product concepts to `PRODUCT_SPEC.md` as reference-only until verified against the live Lovable app.
- [ ] Compare live Lovable modules against source-material feature map.
- [ ] Convert verified modules into official `PRODUCT_SPEC.md` entries after QA.

## Live App QA Tasks Added 2026-06-02

- [x] Resolve deployed app Lovable project ID.
- [x] Confirm protected routes redirect to login without session.
- [x] Identify backend Supabase project from deployed bundle.
- [x] Inventory deployed app routes/nav from bundle.
- [x] Perform read-only anon Supabase table accessibility checks.
- [x] Identify Automation Center workflow rows and safe status summary.
- [x] Create Lovable handoff 002 with backend/security questions.
- [ ] Get valid admin login/session for `https://clinic-pilot-x.lovable.app`.
- [ ] Click-test Dashboard.
- [ ] Click-test Leads create/edit/delete/convert/persistence.
- [ ] Click-test Patients create/edit/persistence.
- [ ] Click-test Appointments create/status/reminder/payment request/persistence.
- [ ] Click-test Communication Hub external messages and internal chat after RLS issue is resolved.
- [ ] Click-test Video Consultation and define compliant future-state requirements.
- [ ] Click-test Payments & Billing without activating paid integrations.
- [ ] Click-test Analytics & Reporting and define visual upgrade plan.
- [ ] Click-test Staff Management and roles.
- [ ] Click-test Automation Center workflows without triggering paid sends/calls.
- [ ] Review Lovable response to handoff 002.
- [ ] Approve or revise RLS/security fix plan before build mode.

## Platform Investigation Tasks Added 2026-06-03

- [x] Attempt to connect to Ross's authenticated in-app browser session.
- [x] Document browser-control connector blocker.
- [x] Deep-audit deployed app bundle for backend/function/table references.
- [x] Confirm no direct n8n references in deployed frontend bundle.
- [x] Summarize Automation Center workflow configuration keys and UI coverage.
- [x] Check whether official `aihustler2025/ClinicPilotX` GitHub repo exists.
- [ ] Create/connect official `ClinicPilotX` GitHub repo.
- [ ] Get Codex-controllable authenticated app access for UI QA.
- [ ] Confirm Supabase Edge Function list and secrets/sandbox status with Lovable/Supabase.
- [ ] Confirm whether public anon RLS exposure is intentional.
- [ ] Fix internal chat RLS recursion after approved plan.
- [ ] Resolve missing `assignment_rules` and `signatures` schema issues.
- [ ] Prepare Automation Center safe-testing protocol before clicking test-send actions.
- [ ] Decide whether to keep Supabase Edge Functions only or add fresh n8n after core audit.
## Authenticated QA Tasks Added 2026-06-03

- [x] Restore Codex-controllable authenticated app access using Chrome QA browser plus Playwright.
- [x] Create simple Playwright/Chrome QA tutorial for Ross.
- [x] Perform authenticated read-only navigation across all left-nav routes.
- [x] Capture authenticated route screenshots and JSON notes locally.
- [x] Save first authenticated platform audit in `09-exports/`.
- [x] Verify Automation Center Activity Logs tab opens.
- [x] Verify Communication Hub External Messages and Internal Chat tabs open.
- [x] Verify Appointments Calendar View opens.
- [x] Verify Settings tabs open.
- [ ] Deep-test Leads create/edit/delete/convert/persistence in a controlled test-data pass.
- [ ] Deep-test Patients create/edit/persistence in a controlled test-data pass.
- [ ] Deep-test Appointments create/status/reminder/payment request/persistence without paid sends.
- [ ] Audit Automation Center workflow configs and create safe-testing protocol before clicking send/test actions.
- [ ] Investigate `assignment_rules` missing table/schema error.
- [ ] Investigate subscription state inconsistency between `Professional` and `No Plan`.
- [ ] Investigate Hostinger account for old n8n data/workflows before deciding whether to recreate n8n.
- [ ] Research cheapest viable n8n hosting path using current SiteGround/available hosting constraints.
## n8n Recovery Tasks Added 2026-06-03

- [x] Inspect Hostinger hPanel visible status without clicking renew/payment actions.
- [x] Confirm old Hostinger VPS is offline and renewal would not be cheap.
- [x] Inventory local old n8n workflow exports without opening credential contents.
- [x] Create `09-exports/n8n-hostinger-recovery-options-2026-06-03.md`.
- [ ] Map each old n8n workflow to current ClinicPilotX Automation Center workflows.
- [ ] Determine which automations can stay in Supabase/Lovable functions.
- [ ] Determine which automations still require n8n.
- [ ] If n8n is required, evaluate local dev import, n8n Cloud trial, Oracle Always Free, or low-cost VPS with billing guardrails.
- [ ] Do not renew Hostinger unless local exports are proven incomplete or missing critical data.
## GitHub / Laptop Transfer Tasks Added 2026-06-04

- [x] Create official GitHub repo `aihustler2025/ClinicPilotX`.
- [x] Verify old lowercase repo `aihustler2025/clinicpilot-x` is not the official project.
- [x] Connect official D-drive local repo to new GitHub remote.
- [ ] Push local `main` to GitHub.
- [ ] Verify required memory/docs files exist on GitHub.
- [ ] Clone official GitHub repo onto laptop.
- [ ] Set up laptop local n8n for workflow import/review only.
- [ ] Copy or commit old n8n workflow exports into an approved reference folder after credential-safety review.
- [ ] Create B-drive backup mirror after GitHub push is verified.
## Laptop n8n Transfer Tasks Added 2026-06-05

- [x] Verify GitHub remote is connected and `main` tracks `origin/main`.
- [x] Create laptop Codex handoff/master prompt for local n8n setup.
- [x] Clone official GitHub repo onto laptop at `%USERPROFILE%\Documents\ClinicPilotX`.
- [x] Verify Git is installed on laptop.
- [x] Check whether Docker Desktop is installed on laptop.
- [ ] Install Docker Desktop on laptop if missing.
- [ ] Run local n8n Docker container on laptop as `clinicpilotx-n8n`.
- [ ] Verify `http://localhost:5678` opens on laptop.
- [ ] Create local-only n8n owner account.
- [ ] Copy old non-credential n8n workflow JSON files to laptop.
- [ ] Import workflows into local n8n and keep inactive.
- [ ] Create imported workflow inventory and ClinicPilotX Automation Center mapping.
- [ ] Decide workflow-by-workflow: Supabase/Lovable rebuild, n8n retained, or discard.
- [x] Create laptop local n8n setup status report in `09-exports/`.
## Lovable Architecture Tasks Added 2026-06-05

- [x] Revise laptop handoff to include Lovable Cloud/Supabase and marketing website context.
- [x] Clarify that laptop paths are repo-relative after cloning GitHub, not PC D-drive paths.
- [x] Draft Lovable clarification handoff for main dashboard, marketing website, backend, hosting, Supabase, Lovable Cloud, and GitHub connections.
- [ ] Ask Lovable to identify the main CRM/dashboard project ID, backend, Supabase connection, Lovable Cloud status, hosting status, and GitHub connection.
- [ ] Ask Lovable to identify the separate marketing website project ID, URL, backend status, hosting status, and merge readiness.
- [ ] Decide how marketing website and dashboard should be connected: same Lovable app, linked apps, subdomain structure, or future merge.
- [ ] Document chatbot, mobile app, external API, and integration roadmap in PRODUCT_SPEC.md after core dashboard audit.
- [ ] Confirm which automations should run in Lovable Cloud/Supabase versus n8n.
