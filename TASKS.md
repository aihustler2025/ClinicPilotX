# ClinicPilotX Tasks

Last updated: 2026-06-24

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
- [x] Download and run Docker Desktop installer on laptop.
- [x] Run elevated WSL setup commands for Docker Desktop.
- [x] Restart laptop after Docker/WSL setup.
- [x] Confirm Docker Desktop engine starts successfully.
- [x] Create persistent Docker volume `clinicpilotx_n8n_data`.
- [x] Run local n8n Docker container on laptop as `clinicpilotx-n8n`.
- [x] Verify `http://localhost:5678` opens on laptop.
- [x] Create local-only n8n owner account.
- [x] Create and import first safe local n8n test workflow.
- [x] Verify first imported workflow is inactive.
- [ ] Copy old non-credential n8n workflow JSON files to laptop if Ross can locate/provide them.
- [ ] Import workflows into local n8n and keep inactive.
- [ ] Create imported workflow inventory and ClinicPilotX Automation Center mapping.
- [ ] Decide workflow-by-workflow: Supabase/Lovable rebuild, n8n retained, or discard.
- [x] Create laptop local n8n setup status report in `09-exports/`.
- [x] Create local n8n workflow inventory report.
## Lovable Architecture Tasks Added 2026-06-05

- [x] Revise laptop handoff to include Lovable Cloud/Supabase and marketing website context.
- [x] Clarify that laptop paths are repo-relative after cloning GitHub, not PC D-drive paths.
- [x] Draft Lovable clarification handoff for main dashboard, marketing website, backend, hosting, Supabase, Lovable Cloud, and GitHub connections.
- [ ] Ask Lovable to identify the main CRM/dashboard project ID, backend, Supabase connection, Lovable Cloud status, hosting status, and GitHub connection.
- [ ] Ask Lovable to identify the separate marketing website project ID, URL, backend status, hosting status, and merge readiness.
- [ ] Decide how marketing website and dashboard should be connected: same Lovable app, linked apps, subdomain structure, or future merge.
- [ ] Document chatbot, mobile app, external API, and integration roadmap in PRODUCT_SPEC.md after core dashboard audit.
- [ ] Confirm which automations should run in Lovable Cloud/Supabase versus n8n.

## Project Management Tasks Added 2026-06-11

- [x] Record Ross's BUZZOOKA Work System operating model for ClinicPilotX.
- [x] Clarify Codex role as project manager/auditor/QA/documentation/automation architect.
- [x] Create durable ClinicPilotX takeover operating model document.
- [x] Confirm browser-control path for repeatable dashboard QA.
- [x] Complete first authenticated read-only left-nav dashboard audit.
- [x] Create first module readiness matrix.
- [x] Create first Automation Center workflow readiness notes.
- [ ] Confirm how Lovable responses will be saved back into `docs/handoffs/`.
- [ ] Update Product Spec with verified dashboard module behavior after audit.
- [ ] Retest Settings > Audit Log tab.
- [ ] Open Automation Center Configure panels read-only and document available settings.
- [ ] Create safe controlled test-data plan before CRUD/send/payment testing.
- [ ] Investigate why Automation Center counts differ between earlier 19-row evidence and current `7 / 13 Active` UI.
- [ ] Investigate subscription state inconsistency between `Professional` and `No Plan`.

## Controlled CRM QA Tasks Added 2026-06-11

- [x] Create product/user-guide documentation structure.
- [x] Create controlled test-data plan.
- [x] Create dummy lead.
- [x] Verify dummy lead search.
- [x] Edit dummy lead and verify persistence.
- [x] Test lead View Details.
- [x] Test lead Convert to Patient with dummy record.
- [x] Verify converted patient appears in Patients.
- [x] Attempt dummy appointment booking for converted patient.
- [x] Create Leads human QA script for Ross's assistant.
- [x] Test Leads status filter pills at a first-pass level.
- [x] Create additional dummy leads for chatbot/email intake testing.
- [ ] Investigate why editing dummy lead changed status/temperature automatically.
- [x] Ask Lovable to improve Leads phone input, service selector, export UX, details timeline/files placeholders, and edit safety.
- [x] Publish-test Lovable Leads v2 improvement build.
- [x] Fix remaining Leads temperature mutation: notes-only edit must not change `Cold` to `Hot`.
- [x] Add visible phone validation errors for invalid phone numbers.
- [x] Adjust U.S./Canada phone display toward `+1 (213) 555-0199` while keeping E.164 storage in Lead Details.
- [x] Retest Leads export dialog after the blocking temperature issue is fixed.
- [ ] Investigate Leads `Show Converted` count/table inconsistency.
- [ ] Improve Leads export UX: scope, filters, file type, columns, filename.
- [x] Improve Leads phone input with country picker, auto-formatting, validation, and normalized storage.
- [x] Improve Leads service requested field with searchable service dropdown and custom service support.
- [x] Improve Leads details view with richer timeline/communication/files/follow-up context.
- [ ] Prepare Leads for future chatbot, website contact form, email inquiry, phone, and social intake sources.
- [x] Capture full Leads intake roadmap: email/contact forms, AI filtering, chatbot, SMS, calls, Facebook, WhatsApp, Viber, and social/messaging sources.
- [ ] Design lead intake API/webhook payload contract for chatbot/contact form/email automation.
- [ ] Design AI email/contact-form filtering workflow before building live intake.
- [ ] Define duplicate/spam handling rules for multi-channel lead intake.
- [ ] Map future lead sources to Automation Center controls.
- [ ] Verify Leads export downloaded CSV contents in a normal browser: filename, row count, headers, selected columns, filtered scope, and phone format.
- [x] Investigate why appointment booking closes without visible success or new appointment row.
- [x] Test patient record editing path availability.
- [ ] Retest appointment booking after backend/UI issue is understood.
- [ ] Verify Dashboard and Analytics update after dummy data changes.

## Patients / Appointments QA Tasks Added 2026-06-12

- [x] Open converted dummy patient from Patients list.
- [x] Verify patient detail panel content.
- [x] Check for visible patient edit/update action.
- [x] Test patient-detail `Book Appointment` button without live sends.
- [x] Create Lovable plan-mode handoff for patient edit and appointment booking issues.
- [x] Send Lovable handoff 006 in Plan mode.
- [x] Review Lovable response before approving build.
- [x] After approved build/publish, retest patient edit persistence.
- [x] After approved build/publish, retest patient-detail booking modal.
- [x] After approved build/publish, retest appointment creation persistence and success/error feedback.
- [x] Verify TEST toggle defaults on for patient-detail booking QA path.
- [x] Verify new TEST appointment appears in the Appointments list with TEST badge.
- [x] Verify the new appointment is visible from the patient side.
- [ ] Confirm through Lovable/Supabase code/log review that TEST appointment rows cannot trigger SMS/email/payment/reminder workflows.
- [ ] Retest Appointments calendar view after new test appointment creation.
- [ ] Retest appointment status changes using dummy TEST appointment only.
- [ ] Verify Dashboard and Analytics update after dummy appointment changes.
- [x] Create Patients human QA script for Ross's assistant.
- [x] Create Appointments human QA script for Ross's assistant.
- [x] Document ClinicPilotX phone number standard for UI display and E.164 storage.
- [x] Create Lovable plan-mode handoff for Patients export and shared phone input polish.
- [x] Send Lovable handoff 007 in Plan mode.
- [x] Review Lovable response before approving any Patients module polish build.
- [ ] Improve Patients Add/Edit phone input to match Leads/shared phone standard.
- [ ] Improve Patients export UX to match Leads export dialog pattern.
- [ ] Fully test Patients module as its own module: add, view, edit, export, filters/sort, delete confirmation.
- [x] QA-test Lovable's published Patients phone/export polish build.
- [x] Document failed Patients phone/export QA after publish.
- [x] Create Lovable plan-mode fix request for failed Patients phone/export publish.
- [x] Send Lovable handoff 008 in Plan mode.
- [x] QA-test repeat publish after Lovable response/publish.
- [x] Document repeat failure / likely workstream mismatch after Lovable reported unrelated Financial Transparency / volunteer waiver / handoff docs changes.
- [x] Create Lovable plan-mode fix request 009 for Patients publish mismatch.
- [ ] Send Lovable handoff 009 in Plan mode.
- [ ] Re-approve only after Lovable confirms the correct dashboard project, GitHub repo, publish target, and exact Patients phone/export implementation files.
- [x] Review corrected Lovable Patients phone/export implementation after publish.
- [x] Verify Patients Add/Edit now uses shared phone input.
- [x] Verify Patients Export dialog now exists with scope, row count, and display/E.164 phone columns.
- [x] Create Patients phone/export fix QA report after successful corrected publish.
- [x] Create Lovable handoff 010 for remaining optional-phone/input-mask polish.
- [ ] Send Lovable handoff 010 in Plan mode.
- [x] Send Lovable handoff 010 in Plan mode.
- [x] Retest Lovable's Patients phone polish follow-up after publish.
- [x] Retest Add Lead with blank optional phone.
- [x] Send Lovable handoff 011 in Plan mode.
- [x] Fix Add Patient database permission blocker: `permission denied for function generate_patient_id`.
- [x] Retest Add Patient with valid main phone and blank emergency phone after `generate_patient_id` permission fix.
- [x] Fix optional phone fields so blank optional phones do not default to validation-blocking `+1`.
- [x] Polish Patients Add/Edit U.S./Canada phone input display toward `+1 (213) 555-0199`.
- [x] Verify Patients exported CSV contents in a normal browser that supports downloads.
- [x] Send Lovable handoff 012 in Plan mode.
- [x] Fix invalid Add Patient phone UX so short phone values keep the modal open with visible validation.
- [x] Retest Patients invalid phone UX after Request 012 publish.
- [x] Retest valid Add Patient regression after Request 012 publish.
- [x] Retest Leads invalid phone regression after Request 012 publish.
- [x] Test Patients search, status filters, sort controls, and detail panel in broader Patients QA pass.
- [x] Retest patient-detail `Book Appointment` path after latest Patients phone/export fixes.
- [ ] Fix patient-profile `Book Appointment` time validation bug: valid `15:30` is rejected as invalid `HH:MM`.
- [ ] Test Patients delete cancel behavior on a disposable dummy patient after native confirm is replaced.
- [ ] Test Patients delete confirm behavior only on a disposable dummy patient after Ross approval.
- [x] Create Lovable handoff 013 for patient-profile booking time validation and delete confirmation UX.
- [ ] Send Lovable handoff 013 in Plan mode.
- [ ] Replace native browser delete confirm with an in-app confirmation modal for better admin UX and QA reliability.
- [x] Retest Request 013 after publish.
- [x] Verify patient-profile booking with `15:30` saves as a TEST appointment.
- [x] Verify in-app delete dialog cancel path.
- [x] Verify in-app delete dialog confirm path on disposable patient.
- [ ] Decide safe product behavior for deleting patients with related appointments.
- [ ] Fix stale patient profile panel remaining open after delete.
- [ ] Fix/define related appointment behavior after patient delete.
- [ ] Format appointment row phone display as friendly phone where possible.
- [ ] Format Appointments calendar/detail drawer phone display as friendly phone where possible.
- [ ] Format patient profile appointment time without trailing seconds.
- [ ] Audit Appointments detail actions: Confirm, Cancel, Send Reminder, Add to Google Calendar, with no live sends/calendar writes until approved.
- [x] Create Lovable handoff 014 for patient delete related-record behavior and appointment display polish.
- [x] Send Lovable handoff 014 in Plan mode.
- [x] Approve and publish Lovable Request 014 after revised archive-only plan.
- [x] Partially QA Request 014 appointment list display polish after publish.
- [x] Re-run Request 014 delete/archive branching QA with reliable browser control.
- [x] Verify zero-related patient hard-delete dialog/cancel/confirm behavior.
- [x] Verify related-record patient archive-only dialog/cancel/confirm behavior.
- [ ] Verify stale patient profile panel closes after archive/delete. Current UI covers/blocks row action while profile is open, so the old stale-panel path was not directly reproducible.
- [x] Verify Archived status filter contains archived patient after archive.
- [x] Verify Appointments calendar/detail drawer phone and time formatting after Request 014.
- [x] Create Lovable handoff 015 for Request 014 follow-up polish.
- [x] Send Lovable handoff 015 in Plan mode.
- [x] Fix booking modal disabled patient phone display from raw E.164 to friendly display format.
- [x] Fix appointment drawer patient type label showing `Lead` for patient-created appointments.
- [x] Remove stray `0` text from appointment drawer action area.
- [x] Retest Request 015 after publish.
- [ ] Diagnose Patients `No Plan` / `No patients found` transient state.
- [x] Document patient profile direction for the Patients side panel.
- [ ] Expand Patient Profile QA checklist: profile sections, appointments tab, transactions tab, notes, edit persistence, and future files/communications placeholders.
- [ ] Define patient profile build requirements before connecting Call, Message, Video, files, or live communications.
- [x] Begin broader Appointments module QA with TEST appointments only.
- [ ] Define safe status-action behavior for Appointments `Confirm` and `Cancel`.
- [x] Verify Appointments search, filters, date range, export, list/calendar consistency, and detail drawer behavior.
- [x] Create Lovable handoff 016 for Appointments broader QA fixes.
- [x] Send Lovable handoff 016 in Plan mode.
- [x] Fix Appointments status filter so it includes real statuses such as `Pending` and `Completed`.
- [x] Normalize Appointments status display labels, including `Payment_pending` and `Checked in`.
- [x] Fix Appointments Date Range control so a visible date picker/dialog appears.
- [x] Upgrade Appointments export to a scoped dialog matching Leads/Patients export quality.
- [x] Diagnose and fix Appointments-specific `No Plan` / zero-data flicker.
- [x] Retest Request 016 after publish.
- [ ] Verify Appointments exported CSV file contents through a normal Chrome download path.
- [x] Verify Dashboard and Analytics updates after safe TEST appointment changes.
- [x] Create Dashboard / Analytics QA report.
- [x] Create Dashboard / Analytics human QA script.
- [x] Create Lovable handoff 017 for Dashboard metrics/data-source fixes.
- [x] Send Lovable handoff 017 in Plan mode.
- [x] Diagnose why Dashboard metrics show all-zero/empty data while Leads, Patients, and Appointments contain records.
- [x] Fix Dashboard metric data sources and visible date/scope labels.
- [x] Retest Dashboard / Analytics after Request 017 publish.
- [x] Document Request 017 Dashboard QA result.
- [x] Create controlled TEST-only Appointments status-action QA plan for Confirm and Cancel.
- [x] Test Confirm status change only on a TEST appointment after safety review.
- [x] Test Cancel status change only on a TEST appointment after safety review.
- [x] Document Appointments status-action QA.
- [x] Document Dr. Colin Hong near-term demo roadmap.
- [x] Audit Communication Hub read-only: inbox/messages/internal chat, send buttons, mock vs real data, and safety risks.
- [x] Create Communication Hub human QA script.
- [x] Audit Automation Center read-only with focus on email filtering, lead intake, appointment request handling, and workflow safety.
- [x] Create Automation Center human QA script.
- [x] Create Lovable handoff 018 for Dr. Hong demo foundation.
- [x] Rewrite Lovable handoff 018 to frame ClinicPilotX as a multi-client subscription product, with Dr. Hong as first pilot workspace only.
- [x] Send revised Lovable handoff 018 in Plan mode.
- [x] Approve and publish Phase 1A tenant root foundation after Lovable narrowed scope to additive root tables only.
- [x] QA Phase 1A tenant root foundation after publish.
- [x] Create Lovable handoff 019 for Phase 1A SQL verification and Settings fetch-error follow-up.
- [x] Send Lovable handoff 019 in Plan mode.
- [x] Get Lovable/Supabase SQL confirmation that Phase 1A seeded pilot clinic, members, platform admin, and active clinic profile fields correctly.
- [x] Approve and publish Request 019 frontend-only Settings fix.
- [x] QA Request 019 Settings fix after publish.
- [x] Create Lovable handoff 020 for Settings row missing follow-up.
- [ ] Send Lovable handoff 020 in Plan mode.
- [x] Send Lovable handoff 020 in Plan mode.
- [x] Diagnose and fix Settings page `Settings row missing - contact support` before onboarding/setup work.
- [x] Re-run Settings save/revert QA after the real Settings form renders.
- [x] Confirm `Error fetching settings: Object` no longer appears after visiting Appointments/Automation.
- [x] Create Lovable handoff 021 for Phase 1B planning only.
- [ ] Send Lovable handoff 021 in Plan mode.
- [x] Send Lovable handoff 021 in Plan mode.
- [x] Review exact Phase 1B migration SQL.
- [x] Approve Phase 1B additive migration after exact SQL review.
- [x] QA Phase 1B migration after publish.
- [x] Create Lovable handoff 022 for Phase 1B evidence and Phase 1B.1 app-code planning.
- [ ] Do not send Lovable handoff 022; superseded after correct evidence was provided.
- [x] Get Lovable's actual Phase 1B pre-check and post-check evidence.
- [x] Confirm all 23 tables have non-null `clinic_id` after Phase 1B.
- [x] Confirm all 23 Phase 1B indexes and FKs exist.
- [x] Confirm no new linter findings vs. pre-migration baseline.
- [x] Create Lovable handoff 023 for Phase 1B.1 app-code planning only.
- [ ] Send Lovable handoff 023 in Plan mode.
- [ ] Plan Phase 1B.1 app-code work: active clinic context, insert stamping, and read filtering.
- [ ] Do not approve Phase 1B.1 build until Lovable provides a reviewed app-code plan with exact files, sequencing, QA, and rollback.
- [ ] Design client/clinic account setup requirements for Dr. Colin Hong demo.
- [ ] Design clinic onboarding/setup wizard: profile, logo, website, business hours, services, team, permissions, templates, integrations, and plan gates.
- [ ] Design per-clinic knowledge base for services, FAQs, hours, policies, pricing, provider bios, and AI-safe business facts.
- [ ] Plan Google Calendar connection safely without activating live calendar writes.
- [ ] Design lead intake API/webhook path for external chatbots, ConvoCore, website forms, and future ClinicPilotX chatbot.
- [ ] Design email AI sorting demo using a test inbox before connecting any real client inbox.
- [ ] Keep `Send Reminder` and `Add to Google Calendar` untested until live-send/calendar-write safety is approved.

## Leads v2 Fix QA Tasks Added 2026-06-12

- [x] Approve and publish Lovable's Leads temperature/phone validation fix.
- [x] Retest invalid phone entry with visible inline validation.
- [x] Create a fresh dummy lead after the fix.
- [x] Verify the fresh dummy lead starts `NEW LEAD` and `Cold`.
- [x] Perform notes-only edit and verify status/temperature stay unchanged.
- [x] Verify Timeline records created/edited events.
- [x] Verify Lead Details includes formatted U.S. phone display.
- [x] Decide whether main Leads table should also display formatted phone numbers instead of E.164.
- [ ] Adjust Leads phone field display so U.S./Canada formatting appears as `+1 (213) 555-0199` while typing/displaying, with E.164 storage underneath.
- [ ] Update Leads main table phone display to use friendly formatted phone numbers instead of raw E.164.
- [x] Retest Export dialog UI with scope and column selection.
- [ ] Retest Export downloaded CSV contents in a browser that supports downloads.
