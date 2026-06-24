# ClinicPilotX Product Spec

Last updated: 2026-06-24

## Product Purpose

ClinicPilotX is a Buzzooka product for appointment-based and service businesses, including clinics, plastic surgery practices, dental clinics, med spas, beauty/wellness businesses, salons, and similar operators.

The product is intended to support real client testing and launch after the current Lovable build is audited, organized, verified, documented, and stabilized.

## Current Verification Status

The Lovable project is reportedly 70-80% complete, but no modules are considered verified yet in this official workspace.

Until the audit is complete, every major claim should be marked as one of:

- `Verified`: confirmed through direct evidence.
- `Claimed by Lovable`: stated by Lovable but not yet independently checked.
- `Mock/demo`: present but using mock, seed, placeholder, or demo data.
- `Incomplete`: partially present but not ready for real client testing.
- `Unknown`: not yet assessed.

## Product Areas To Audit

- Dashboard and analytics
- Admin panel
- User/staff portal
- Client/patient/customer-facing flows
- Appointment management
- Lead capture and CRM workflows
- Communication center
- Automations and reminders
- Calendar integrations
- Payment or subscription integrations
- AI/chatbot/voice workflows
- Settings, roles, and permissions
- Marketing website, only after core product functionality is itemized

## Backend To Audit

- Backend provider: evidence points to standalone Supabase project `imuyfbvsombbpgdgkhrb` plus Lovable-managed deployment/secrets, but Lovable must confirm the exact Lovable Cloud/Supabase relationship.
- Database schema: partially inferred from deployed app behavior and Supabase errors, but not fully verified.
- Auth provider and roles: Supabase auth is evidenced by deployed app behavior; role model still requires verification.
- Integrations: Automation Center and backend functions reference email, SMS, payment, AI, and appointment workflows; sandbox/live credential status must be confirmed before testing.
- Real data vs mock/demo data: partially assessed through authenticated QA, but still requires module-by-module verification.

## Architecture Direction - 2026-06-05

ClinicPilotX should treat Lovable Cloud/Lovable hosting/Supabase as the preferred production path before considering new paid backend or hosting platforms, because Ross already has Lovable package benefits.

Local n8n is approved only for review/testing/import of old workflow blueprints on the laptop. It must not become production infrastructure for commercial ClinicPilotX workflows unless Ross later approves a reliable hosting, monitoring, backup, security, and cost plan.

There may be two Lovable projects:

- Main ClinicPilotX CRM/dashboard.
- Separate partially built ClinicPilotX marketing website.

Do not assume they are merged. Lovable must clarify project IDs, URLs, GitHub connections, Supabase/backends, hosting status, and merge readiness before build decisions.

## Phone Number Standard

ClinicPilotX should store phone numbers in E.164 format for integrations and display them in user-friendly localized format in the UI.

Product requirement:

- U.S./Canada user input: staff can type digits only, such as `5558878888`.
- U.S./Canada display: `+1 (555) 887-8888`.
- Canonical database/API value: `+15558878888`.
- Use libphonenumber-style parsing, formatting, and validation rather than custom regex.
- Reuse the same phone input behavior across Leads, Patients, Staff, Settings, and future intake forms.

Detailed standard:

`docs/phone-number-standard.md`

## Module Registry

First authenticated read-only module audit completed on 2026-06-11. See:

`09-exports/authenticated-dashboard-module-audit-2026-06-11.md`

| Module | Status | Evidence | Notes |
| --- | --- | --- | --- |
| Dashboard | Partially verified | Authenticated browser audit | Loads with dashboard metrics and sections, but metrics need data-source validation. |
| Leads | Partially verified | Authenticated browser audit | 11 leads visible with filters/search/export/Add Lead; CRUD and conversion need controlled test data. |
| Patients | Partially verified | Authenticated browser audit + controlled CRM QA | Patient list, statuses, visits/revenue, search/filter/export/Add Patient visible. Lead-to-patient conversion verified with dummy record. Patient detail edit now exists and persisted notes in QA. |
| Appointments | Partially verified | Authenticated browser audit + controlled CRM QA | List and calendar views open. Patient-detail booking now opens a prefilled appointment form, validates required fields, and successfully saved a TEST appointment with TEST badge. Broader calendar/status/reminder/payment behavior still needs QA. |
| Communication Hub | Partially verified | Authenticated browser audit | External Messages and Internal Chat tabs open; message sending not tested. |
| Video Consultation | Incomplete | Authenticated browser audit | Route shows `Coming Soon`. |
| Payments & Billing | Partially verified | Authenticated browser audit | Payment/invoice UI visible; payment link/Stripe flows not tested. |
| Analytics & Reporting | Partially verified | Authenticated browser audit | Reporting UI visible; values require validation against source data. |
| Staff Management | Partially verified | Authenticated browser audit | Staff list and role controls visible; permissions/invites not tested. |
| Automation Center | Partially verified / high priority | Authenticated browser audit | Workflows and Activity Logs tabs open; activity logs show completed Appointment Confirmation runs. |
| Auto-Assignment Rules | Broken / blocked | Authenticated browser audit | Route remains on `Loading assignment rules...`, consistent with missing/unavailable backend table. |
| Subscription | Partially verified | Authenticated browser audit | Professional plan UI visible; entitlement consistency still suspect. |
| Settings | Partially verified | Authenticated browser audit | General, Notifications, Integrations, Profile, Email Logs verified; Audit Log needs retest. |
| Profile | Incomplete | Authenticated browser audit | Main route shows `Coming Soon`. |

## Automation Center / n8n Blueprint Mapping

## Controlled CRM QA Notes - 2026-06-11

Verified lead lifecycle behavior:

- A manual dummy lead can be created.
- Lead search can isolate that dummy lead by name.
- Lead edit saves service/notes changes.
- Lead Details view opens and shows contact, service, notes, timeline, and action controls.
- Converting a lead to a patient creates a patient record with matching name, email, and phone.

Open product/engineering issues:

- Editing a lead's service/notes and creating later leads changed existing dummy lead status/temperature without an explicit status/temperature edit.
- The app intermittently displays `No Plan` where `Professional` is expected, while still showing protected CRM data.
- Appointment booking for a converted dummy patient did not visibly persist or confirm success.
- Leads `Show Converted` can display confusing count/table behavior and needs clear converted-lead handling.
- Leads export should support explicit export scope, current filters, statuses, date range, source, file type, column selection, estimated row count, and clear filenames.
- Leads manual creation should use a proper international phone input with country selector, digits-only typing, display formatting such as `+1 (555) 123-4567`, and normalized storage.
- Leads manual creation should use a searchable service selector with custom service entry and future clinic-specific service lists.
- Leads should be ready for future intake sources: chatbot, email inquiry parser, website contact forms, phone/voice assistant, manual entry, Facebook, Instagram, and referrals.
- Lead details should become the full record of the relationship, including communication history, uploaded photos/files, timeline activity, staff assignment, follow-up context, and conversion history.

These issues should be clarified or fixed before writing final customer-facing tutorials for lead conversion and appointment booking.

## Leads Published v2 QA - 2026-06-11

After Lovable's Leads improvement build was approved and published, Codex verified the following live behavior:

- Manual lead creation supports expanded lead intake fields: contact info, country-aware phone input, service selector, source, preferred contact, urgency, consent, and notes.
- Phone storage normalizes to E.164, verified with `+12135550199`.
- Service selection saved a catalog value, verified with `Botox`.
- Lead Details now has Overview, Timeline, Comms, Files, and Activity tabs.
- Timeline records created and edited events.
- Files tab is intentionally disabled for now and explains that future file/photo uploads require a storage backend.

Still incomplete:

- A notes-only lead edit changed the test lead temperature from `Cold` to `Hot`. Lead status stayed `NEW LEAD`, but temperature mutation on safe edits is not acceptable for final behavior.
- Invalid phone input needs a visible validation message.
- U.S./Canada display formatting should be improved toward `+1 (213) 555-0199`, while keeping normalized E.164 database storage.
- Export dialog still needs a clean retest after the blocking temperature issue is fixed.

## Leads v2 Fix QA - 2026-06-12

After Lovable's QA fix build was approved and published, Codex retested the live Leads workflow.

Verified final behavior for this pass:

- Invalid phone numbers block lead creation and show an inline validation message.
- Valid U.S. digits can be typed without punctuation and are accepted.
- Manual lead creation still normalizes stored phone data to E.164.
- Lead Details displays U.S./Canada-style phone formatting such as `+1 (213) 555-0199`.
- A newly created lead starts as `NEW LEAD` and `Cold`.
- Editing notes only no longer changes lead status or temperature.
- Timeline records both `Lead created` and `Lead edited` events.

Current Leads status:

- Leads v2 critical temperature mutation blocker is resolved for the tested create/edit path.
- Leads remains `Partially verified`, because export behavior, converted-lead filtering, patient/appointment continuation, and future intake-source readiness still need deeper QA.

Remaining Leads polish:

- The main Leads table still shows E.164 phone values such as `+12135550199`; detail formatting is fixed, but table formatting should be reviewed.
- Invalid-phone helper copy and phone field display should match the preferred U.S./Canada display format.
- Export dialog UI now supports scope, column selection, and estimated row count, but downloaded CSV contents are not yet verified.

## Leads Export QA - 2026-06-12

Codex retested the live Leads export dialog after the Leads v2 fixes.

Verified:

- Export opens a CSV-specific dialog.
- Scope choices include all leads, current filters, and selected-only leads.
- Current filters were selected by default.
- Selected-only was disabled when no rows were selected.
- Column picker includes key lead fields.
- Column toggles work.
- Dialog shows the number of rows that will export.

Still pending:

- Downloaded CSV content verification, including filename, headers, row count, filtered scope, selected columns, and phone format. The Codex in-app browser cannot save downloads, and Chrome extension control was not available in this session.

## Patients / Appointments QA - 2026-06-12

Codex tested the converted dummy patient `CPX TEST Lead June 11`.

Verified:

- Converted patient appears in Patients.
- Patient detail panel opens.
- Detail panel includes patient identity, contact information, medical information, appointments, transactions, notes, and action buttons.

Current issues:

- No clear patient edit/update action is visible from the detail panel.
- Patient-detail `Book Appointment` did not open a booking modal or visible booking state.
- Appointment creation persistence remains suspect from the earlier Appointments module test, where a dummy booking closed the form without visible success or a new row.

Expected future behavior:

- Staff can edit patient details safely from the patient profile.
- Patient edits persist after close/reopen and refresh.
- Patient-detail booking opens a prefilled appointment booking flow.
- Appointment save shows clear success or clear error feedback.
- Booking must not trigger SMS/email/payment/reminder side effects unless explicitly enabled and approved.

## Patients / Appointments Fix QA - 2026-06-12

After Lovable's Patients/Appointments fix was approved and published, Codex retested the converted dummy patient.

Verified:

- Patient detail now includes an `Edit` action.
- Patient notes edit saved and remained visible after reopening the detail panel.
- Patient detail `Book Appointment` now opens a booking modal on `/appointments`.
- The booking modal prefilled the selected patient.
- TEST mode is checked by default in this QA path.
- Required field validation is visible and prevents incomplete appointment creation.
- A valid TEST appointment saved successfully.
- The success toast explicitly stated `TEST - no sends`.
- The Appointments list showed the new row with a `TEST` badge.
- The new appointment details were visible from the patient side.

Current Patients/Appointments status:

- The previously blocking patient edit and patient-detail booking issues are resolved for the tested dummy-data path.
- Patients and Appointments remain partially verified overall until broader calendar, status, reminder, payment, dashboard/analytics, and workflow-safety checks are complete.
- TEST-row automation safety should still be confirmed by Lovable/Supabase code or log review before real client testing with active workflows.

## Patients Module Polish Requirements - 2026-06-12

Patients needs its own module polish pass separate from the patient-to-appointment cross-module workflow.

Required improvements:

- Add Patient and Edit Patient should use the same shared country-aware phone input standard as Leads.
- Staff should type digits only and see friendly U.S./Canada formatting such as `+1 (555) 887-8888`.
- Patient phone values should be stored canonically in E.164 for Twilio/VAPI readiness.
- Patients export should open a scoped export dialog similar to Leads export, with all/current-filter/selected scope, column selection, row count, and clear filename.
- Patients delete must require clear confirmation and should be tested only with dummy records.
- Human QA script exists at `docs/qa/patients-human-qa-script.md`.

## Patients Phone / Export QA Failure - 2026-06-14

After Lovable's Patients phone/export polish build was approved and published, Codex tested the live Patients module and found the requested behavior was not present.

Observed:

- Add Patient phone fields remain plain text inputs.
- Edit Patient phone fields remain plain text inputs.
- Existing E.164 values can still display raw, such as `+15005550111`.
- Patients Export did not open a scoped export dialog.
- Patient list phone formatting remains inconsistent across records.

Status:

- Patients phone/export polish is not complete.
- Patients remains partially verified and requires a Lovable follow-up before deeper Add/Edit/Export human QA can be marked ready.

## Patients Publish Mismatch - 2026-06-14

A repeat publish QA found that Lovable's reported changes did not match the active ClinicPilotX dashboard workstream.

Lovable reported Financial Transparency wording, volunteer waiver language, handoff docs, and an internal `/handoff` page. On the active ClinicPilotX app, `/handoff` returned 404, the claimed docs were not present in the official local GitHub clone, and the Patients phone/export behavior was still unchanged.

Product status remains:

- Patients phone/export polish is incomplete.
- The correct Lovable dashboard project, publish target, GitHub connection, and branch/source context must be confirmed before another Patients build is approved.

## Patients Phone / Export Fix QA - 2026-06-14

After Lovable's corrected Patients phone/export implementation was approved and published, Codex verified that the feature is now landing on the active ClinicPilotX dashboard.

Verified behavior:

- Patients Add/Edit uses the shared international phone input.
- Patient list and detail display U.S./Canada phone values in friendly format, such as `+1 (213) 555-0199`.
- Patient phone values can be entered as digits and saved for integration-ready storage.
- Invalid phone numbers show visible validation.
- Patients Export now opens a scoped CSV dialog with row count and column picker.
- Export columns separate friendly display phone values from canonical E.164 phone values.

Remaining requirements:

- Optional phone fields must not default to `+1` in a way that blocks saving when staff leaves them blank.
- U.S./Canada input display should be polished toward `+1 (213) 555-0199` while typing, not only after save/display.
- Exported CSV file contents still need browser-download verification.

Current status: Patients phone/export is partially verified, not complete.

## Patients Phone Polish QA - 2026-06-19

After Lovable's Patients phone polish follow-up was approved and published, Codex retested the live app.

Verified:

- Patients list/detail can display friendly U.S./Canada numbers such as `+1 (213) 555-0199`.
- Patients Export opens a scoped CSV dialog with row count, selectable columns, and separate display/E.164 phone columns.
- Invalid patient phone entry shows inline validation and blocks submit.
- Leads blank-phone behavior is fixed for the tested path: leaving the phone input at its default `+1` saved a lead with blank phone, not bare `+1`.

Current blocker:

- Add Patient fails with `permission denied for function generate_patient_id`.
- Until this is fixed, Patients Add/Edit/Export phone polish remains partially verified, not complete.

Remaining product requirement:

- Staff-facing U.S./Canada phone input should display as `+1 (213) 555-0199` wherever feasible, while storage remains canonical E.164.
- Invalid phone helper text should use the same friendly example.

## Patients Phone / ID Fix QA - 2026-06-19

After Lovable's Patient ID / phone polish fix, Codex verified the prior blocker is resolved.

Verified:

- Add Patient works for an authenticated staff user.
- Valid main phone plus untouched blank emergency phone saves successfully.
- Patient list displays friendly U.S./Canada phone format.
- Edit Patient shows main phone as `(213) 555-0199` with separate `+1` country chip.
- Blank emergency phone remains blank and does not block Edit Patient save.
- Patients CSV export was downloaded and verified with display/E.164 phone columns and 26 rows.
- Leads blank-phone behavior still passes.

Remaining issue:

- Invalid short Add Patient phone values currently close the modal without visible validation and without creating a visible patient. The modal should remain open and show inline validation.

## Patients Invalid Phone Final QA - 2026-06-19

After Lovable's Request 012 invalid-phone UX fix, Codex verified the final phone-validation gap is resolved.

Verified:

- Add Patient with invalid short phone `123` keeps the modal open.
- Approved helper text appears with `+1 (213) 555-0199`.
- Invalid patient row is not created.
- Valid Add Patient still works with main phone `2135550199` and blank emergency phone.
- Leads invalid-phone behavior also keeps the modal open and shows the same helper.

Current Patients phone/export status:

- Complete for tested Add/Edit/Export/phone-validation paths.
- Still requires separate broader Patients module QA for delete confirmation, filters/sort, detail tabs, and patient-to-appointment downstream workflows.

## Patients Broader Module QA - 2026-06-19

Verified Patients behavior:

- Search can isolate a named patient and hide unrelated patient rows.
- Status filter supports `All Statuses`, `Active`, `Inactive`, and `Archived`.
- Sort supports `Name (A-Z)`, `Recently Added`, `Most Visits`, and `Highest Spent`.
- `Most Visits` and `Highest Spent` sorting behaved plausibly with the visible patient dataset.
- Patient detail panel includes contact information, formatted phone display, summary metrics, medical information, Appointments tab, Transactions tab, and action buttons for `Call`, `Message`, `Video`, `Edit`, and `Book Appointment`.

Current product note:

- Patient delete is guarded by a native browser confirmation. This is safer than instant delete, but a future in-app confirmation modal would be more polished and easier to QA.
- Delete cancel/confirm and patient-to-appointment regression still need a fresh controlled QA pass.

## Patient Profiles And Leads Intake Direction - 2026-06-19

Patient profiles:

- The Patients side panel is the working patient profile surface.
- It should eventually combine identity, contact details, treatment interests, notes, appointments, transactions, files/photos, communication history, and follow-up context.
- `Edit` and `Book Appointment` are near-term safe QA/build areas.
- `Call`, `Message`, and `Video` should remain gated until Communication Hub and Video Consultation workflows are audited.

Leads intake:

- The Leads module is not complete. Current manual-entry improvements are only the foundation.
- Future lead sources include website contact forms, direct email inquiries, AI-filtered inbox intake, chatbot submissions, SMS, phone/AI voice, Facebook, WhatsApp, Viber, and other messaging/social channels.
- All intake channels should normalize phone numbers to E.164 while preserving friendly display formatting.
- Leads should preserve source channel, original message/conversation, preferred contact time, consent/contact permission, AI filtering/classification notes, attachments/photos when available, and timeline history.
- Automation Center should eventually expose settings for enabled channels, AI filtering, staff notifications, auto-assignment, follow-up timing, and channel-specific templates.

Planning document:

`docs/patient-profile-and-leads-intake-roadmap.md`

## Patient Profile Booking / Delete QA - 2026-06-20

Verified:

- Patient profile `Book Appointment` opens the Appointments booking modal.
- The selected patient is prefilled.
- TEST mode is on by default for the patient-profile booking path.
- TEST warning copy is visible.

Current bug:

- A valid native time value `15:30` is rejected with `Invalid time format (HH:MM)`.
- The TEST appointment is not created.
- Patient-profile booking cannot be treated as complete until this is fixed.

Current delete UX note:

- Patients row delete currently uses a native browser confirmation.
- This protects against instant deletion, but it blocks reliable automated QA.
- Product direction is to replace it with an in-app confirmation modal showing the selected patient and explicit Cancel/Delete actions.

## Request 013 Fix QA - 2026-06-20

Verified:

- Patient-profile booking path now works for a TEST appointment using time `15:30`.
- TEST appointment appears in Appointments with a TEST badge.
- Patient profile Appointments tab displays the new appointment.
- Patient delete uses an in-app confirmation dialog with name, email, and patient ID.
- Delete cancel keeps the patient.
- Delete confirm removes the patient from Patients after reload/search.

Open product decision:

- Deleting a patient with related appointments currently leaves the related appointment visible in Appointments with the deleted patient's name and phone.
- ClinicPilotX needs a safe deletion policy before this behavior is treated as complete. Strong candidate: archive/deactivate patients with historical records instead of hard-deleting them.

Polish issues:

- Appointment list phone display can show raw E.164, for example `+12135550199`.
- Appointment calendar/detail drawer can show raw E.164, for example `+150055501111`.
- Patient profile appointment time can show trailing seconds, for example `15:30:00`.
- Appointment detail actions such as `Send Reminder` and `Add to Google Calendar` must remain gated until Appointments/Communication/Integration safety is reviewed.

## Request 014 Partial QA - 2026-06-21

After Lovable's Request 014 publish, Appointments list display polish is partially verified:

- Parseable U.S./Canada appointment phones display in friendly format, for example `+1 (213) 555-0199` and `+1 (500) 555-0111`.
- Appointment list times display as friendly times, for example `3:30 PM` and `2:45 PM`.

Still pending:

- Patient delete/archive branching must be verified directly before the Patients module is considered complete.
- Patients with related appointments/payments should archive rather than hard-delete.
- Patients with no related records may be hard-deleted only after clear in-app confirmation.
- Appointment calendar/detail drawer polish still needs live visual QA.

## Request 014 Live QA - 2026-06-21

Core archive-vs-delete behavior is verified:

- Patients with no related appointments/payments can be hard-deleted only after a clear `Delete patient?` confirmation.
- Patients with related appointments/payments are archived instead of deleted after a clear `Archive patient?` confirmation.
- Related-record archive dialog shows related appointment/payment counts and does not expose a `Delete anyway` option.
- Archived patients are hidden under Active filter and visible under Archived filter.
- Related appointments remain visible after archive to preserve clinic history.

Appointments display polish is verified in list and calendar/detail drawer for tested rows:

- Friendly U.S./Canada phone display.
- Friendly time display without trailing seconds.

Follow-up polish still needed:

- Booking modal disabled patient phone should use friendly display formatting.
- Appointment drawer should label patient appointments as `Patient`, not `Lead`.
- Appointment drawer should not leak stray `0` text near action buttons.
- Patients page entitlement/data-load flicker still needs diagnosis.

## Request 015 Live QA - 2026-06-22

Request 015 resolves the immediate polish issues from Request 014.

Verified:

- Patient-profile `Book Appointment` prefill now displays disabled phone fields in friendly phone format.
- Appointments Calendar View detail drawer uses `Patient` for appointments linked to `patient_id`.
- Appointment drawer no longer leaks a stray standalone `0` around the action button area.
- Appointment list and drawer continue to display friendly phone/time values for tested rows.

Current Appointments status:

- Appointments remains partially verified overall.
- Next QA should focus on Appointments as its own module: safe TEST-only status actions, search, filters, date range, export, calendar/list consistency, detail drawer behavior, and dashboard/analytics impact.
- `Send Reminder` and `Add to Google Calendar` remain gated until live side-effect safety is explicitly approved.

## Appointments Broader QA - 2026-06-23

Appointments remains partially verified.

Verified:

- List View can load real appointments after valid subscription/context state is restored.
- Search can isolate a known appointment.
- Sort options are present and Date Ascending works.
- Calendar View shows expected TEST appointments.
- Calendar drawer displays tested appointment details consistently and safely.

Current Appointments issues:

- CRM route context can still briefly show `No Plan` and zero appointment data.
- Appointment Status filter does not include `Pending`, despite pending appointments being visible and counted.
- Status vocabulary needs normalization across stored values, filters, badges, and summary cards.
- `Date Range` does not expose a visible picker/dialog after click.
- Export is immediate/toast-only and should be upgraded to scoped export UX consistent with Leads and Patients.
- Invalid legacy phone values need a deliberate display fallback/data-quality treatment.

Status/action safety remains gated:

- `Confirm`, `Cancel`, `Send Reminder`, and `Add to Google Calendar` should not be tested or documented as safe until Lovable confirms whether they trigger only local status changes or external sends/calendar writes.

## Request 016 Appointments QA - 2026-06-23

Request 016 resolves the main Appointments polish issues found during broader QA.

Verified:

- Appointments direct load no longer shows the old `No Plan` / `0 total appointments` state before data resolves.
- Appointment Status filter includes real visible statuses, including `Pending`, `Completed`, and `Payment Pending`.
- Status labels are friendlier, including `Payment Pending`.
- Date Range exposes visible presets plus Clear and Apply.
- Appointments Export now uses a scoped export dialog with column picker and row preview.
- Export includes both Display Phone and E.164 Phone columns.
- Invalid legacy phone fallback is visible as `(unverified)`.
- Drawer Confirm/Cancel actions now require confirmation and state that no external SMS/email/calendar/refund action will be sent.
- Send Reminder and Add to Google Calendar are disabled.

Still gated:

- Accepting Confirm/Cancel status changes should be tested only as part of a controlled TEST-only status-action QA plan.
- Reminder, calendar, payment, SMS, email, and workflow paths remain off-limits until explicitly approved.
- Export file contents still need one normal Chrome download verification.

## Dashboard / Analytics QA - 2026-06-24

Dashboard status: partially verified, follow-up required.

Current issue:

- Dashboard shows all-zero/empty-state metrics even though source CRM modules contain data.
- During QA, Dashboard showed `Total Leads 0`, `Leads by Source No leads data available`, and `Recent Leads No leads yet`.
- The Leads module showed `17` total leads with real rows and source/status data.
- The Patients module showed populated patient records.
- The Appointments module showed `29 total appointments`.

Product requirement:

- Dashboard cards must use trustworthy data sources or clearly indicate that a metric is not yet connected.
- Each Dashboard metric must have an obvious scope, such as today, this week, this month, all time, selected date range, current org, or current branch.
- Empty-state copy should not appear when the corresponding module contains records.

Analytics status: partially verified.

- Analytics currently exposes a date range, observed as `Jun 01 - Jun 30`.
- Its `3` appointments value appears plausible for visible June TEST appointments.
- Analytics needs deeper validation after Dashboard data-source/scope logic is clarified.

QA report:

`09-exports/dashboard-analytics-qa-2026-06-24.md`

## Request 017 Dashboard QA - 2026-06-24

Request 017 resolves the main Dashboard metrics issue.

Verified:

- Dashboard waits for session/data readiness and no longer gets stuck in permanent zero/empty-state values.
- Dashboard shows real/scoped metrics:
  - `Total Leads 20`
  - `Today's Appointments 0`
  - `Conversion Rate 15%`
  - `New Patients (this week) 1`
  - `Pending 3`
  - `Completed Today 0`
  - `Cancelled Today 0`
  - `Follow-ups Coming soon`
  - `Revenue (MTD) $0`
- Leads by Source now shows real source counts and sums to total leads.
- Recent Leads now shows actual recent leads.
- The difference between Dashboard total leads and Leads page active pipeline count is explainable by scope: Dashboard appears all-time, while Leads page shows active pipeline leads.
- Dashboard appointment headline counts exclude TEST rows where supported, while the Appointments module still shows TEST rows for QA visibility.

Current Dashboard status:

- Dashboard is partially verified and substantially improved.
- Remaining deeper work includes validating revenue with real paid test/payment-safe records later and adding a future global date range if desired.

QA report:

`09-exports/request-017-dashboard-qa-2026-06-24.md`

## Appointments Status Actions QA - 2026-06-24

Appointments internal status actions are now verified for the tested TEST-only path.

Verified:

- A pending TEST appointment can be confirmed after an in-app confirmation dialog.
- The Confirm dialog explicitly states that no SMS, email, or calendar invite will be sent.
- A confirmed TEST appointment can be cancelled after an in-app confirmation dialog.
- The Cancel dialog explicitly states that no cancellation SMS, email, or refund will be sent.
- After cancellation, the appointment remains visible with the TEST badge and `Cancelled` status.

Still gated:

- Send Reminder.
- Add to Google Calendar.
- Request Payment.
- SMS/email sends.
- Workflows/webhooks.

QA report:

`09-exports/appointments-status-actions-qa-2026-06-24.md`

## Dr. Colin Hong Demo Direction - 2026-06-24

Near-term development should prioritize a useful Dr. Colin Hong demo over lower-priority modules.

Priority order:

1. Communication Hub read-only audit.
2. Automation Center read-only audit focused on email filtering and lead intake workflows.
3. Client/clinic account setup so a clinic can have its own services, pricing, templates, inboxes, chatbot sources, and knowledge base.
4. Lead intake API/webhook path for external chatbots, website forms, and future ClinicPilotX chatbot.
5. Email AI sorting demo using a test inbox first.

Deferred:

- Payments/Billing.
- Video Consultation.
- WhatsApp.
- Messenger.
- Viber.
- Telegram.
- Google Calendar writes.
- Live SMS/calling.

Roadmap:

`docs/dr-hong-demo-roadmap.md`

## Communication Hub Read-Only Audit - 2026-06-24

Communication Hub status: present but incomplete.

Verified:

- The module has two top-level tabs:
  - External Messages.
  - Internal Chat.
- External Messages shows a conversation list with 11 records.
- Visible sample channels include SMS, WhatsApp, and Messenger.
- Visible contact types include Patient and Lead.
- Filters exist for Channel, Date Range, and Contact Type.
- Search can narrow the visible conversation list.

Current issues:

- External conversation rows did not open a readable conversation detail pane during Codex QA.
- Internal Chat direct message creation failed with `Failed to create direct message channel`.
- No visible Email inbox, email triage, or email AI sorting queue exists yet.
- Existing messages appear to be seeded/demo examples until Lovable confirms otherwise.

Product implication:

- Communication Hub is not yet the best place to demo Dr. Hong's email filtering.
- The next step should be Automation Center audit, then a planned Dr. Hong demo foundation covering client setup, test inbox email classification, and lead intake.

QA report:

`09-exports/communication-hub-readonly-audit-2026-06-24.md`

## Automation Center Read-Only Audit - 2026-06-24

Automation Center status: present, partially functional, and high-risk because some workflows are active and send-capable.

Verified:

- Current plan shows `Professional`.
- Workflow count shows `7 / 13 Active`.
- Activity Logs show workflow execution history.
- Active/send-capable workflows include Lead Acknowledgment, Smart Follow-up Sequence, Follow-up After Visit, Follow-Up Sequences, No-Show Recovery, Appointment Confirmation, and Appointment Reminders.

Key findings:

- Lead Acknowledgment has SMS/email templates and test-send buttons.
- Appointment Confirmation has SMS/email templates, timing rules, test-send buttons, and `Executions 21`.
- Smart Follow-up and No-Show Recovery are SMS-style outbound workflows.
- Lead Scoring & Assignment is not configurable yet.
- No visible email AI sorting or inbound email-to-lead workflow exists yet.
- No visible external chatbot/contact-form lead intake workflow exists yet.

Product implication:

- The Dr. Hong demo needs a new planned foundation around inbound intake, not existing outbound send workflows.
- Existing send-capable workflows must remain gated until live/test credential behavior, consent, and TEST suppression are fully verified.

QA report:

`09-exports/automation-center-readonly-audit-2026-06-24.md`

Next Lovable handoff:

`docs/handoffs/Lovable-paste-message-018-dr-hong-demo-foundation.md`

Old n8n workflow exports are reference blueprints only until imported into local n8n and reviewed. Keep all imported workflows inactive.

Initial known old workflow categories:

- Daily clinic/staff reporting.
- Email agent or email automation.
- Notifications.
- Outbound voice calling.
- Outbound reachout/follow-up.
- SMS messaging.
- VAPI inbound calling scenario.

Each workflow should be mapped to one of:

- Rebuild in Lovable/Supabase as app-native production automation.
- Retain as n8n orchestration only after a production-grade n8n plan is approved.
- Discard if obsolete or duplicated by current Automation Center behavior.

## Source Material Review - 2026-06-02

Ross provided old/source ClinicPilot documents from `D:\PROJECTS\CLINICPILOT X (Old)`. These were reviewed as reference material only. Review saved at `09-exports/source-material-review-2026-06-02.md`.

Durable concepts to carry forward into ClinicPilotX:

- AI-powered front desk and growth assistant for clinics and appointment-based service businesses.
- Unified lead capture across email, forms, chatbot, voice/phone, manual entry, social leads, and future messaging channels.
- Fast patient/prospect acknowledgments and staff alerts.
- Leads pipeline with source, status, qualification/classification, and follow-up tracking.
- Appointment request workflow that collects preferred times and supports staff-confirmed scheduling.
- Payment/deposit concept, with paid integrations requiring explicit approval before activation.
- Reminder, no-show, outgoing follow-up, review request, missed-call recovery, and voice assistant concepts.
- PriorityBook scoring/prioritization for high-value or time-sensitive requests.
- Automation Center with per-clinic settings for channels, timing, quiet hours, deposits, reminders, and scoring weights.

Architecture caveat: source docs often assume n8n plus Google Sheets. The current Lovable project must be audited before choosing or changing architecture. Do not assume the old stack is the right stack for the new official build.

## Live App Inventory - 2026-06-02 Pre-Login

Current deployed app: `https://clinic-pilot-x.lovable.app`
Lovable project ID: `8b4d9031-af8d-4faf-81d3-135c41ad73b7`
Backend evidence: standalone Supabase project `imuyfbvsombbpgdgkhrb`.

Current left-nav modules found in deployed bundle:

- Dashboard
- Leads
- Patients
- Appointments
- Communication Hub
- Video Consultation
- Payments & Billing
- Analytics & Reporting
- Staff Management
- Automation Center
- Auto-Assignment Rules
- Subscription
- Settings
- Profile

Status: module presence is verified from the deployed bundle, but live behavior is not yet verified because login is required. See `09-exports/live-app-inventory-prelogin-2026-06-02.md`.
