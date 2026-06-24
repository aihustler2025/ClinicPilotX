# ClinicPilotX Controlled CRM Test Log

Date: 2026-06-11

## 2026-06-12 Leads v2 Fix Retest

Dummy lead:

- `CPX TEST Leads V2 fixB-678321`
- `cpx.test+leads-v2-fixb-678321@example.com`

Results:

- Invalid phone validation is now visible and blocks creation.
- Valid U.S. digits create a normalized E.164 phone value.
- New lead started `NEW LEAD` and `Cold`.
- Notes-only edit preserved `NEW LEAD` and `Cold`.
- Timeline showed `Lead created` and `Lead edited`.
- Detail panel showed `+1 (213) 555-0199`.

Decision: previous Leads temperature mutation blocker is resolved for the tested path. Continue Leads export, Patients edit, and Appointments booking QA next.

## 2026-06-12 Leads Export Retest

Result: partially verified.

Verified:

- Leads export now opens an `Export Leads to CSV` dialog.
- Dialog offers `All leads (15)`, `Current filters (15)`, and disabled `Selected only (0)` when no rows are selected.
- `Current filters (15)` is selected by default.
- Dialog offers column toggles for Name, Email, Phone, Source, Service, Status, Temperature, Score, Preferred Contact, Urgency, Notes, and Created.
- Column picker works. Codex unchecked `Phone` and verified it changed to unchecked.
- Dialog showed `15 rows will be exported`.

Not verified:

- Downloaded CSV file contents, because the Codex in-app browser does not support downloads and Chrome extension control was unavailable in this session.

Additional issue reconfirmed:

- Leads briefly showed `No Plan` and 0 leads until the page Refresh control restored `Professional` and 15 leads.

Detailed note: `09-exports/leads-export-qa-2026-06-12.md`.

## 2026-06-12 Patients / Appointments Retest

Dummy patient:

- `CPX TEST Lead June 11`
- `cpx.test+lead-20260611@example.com`
- UI patient ID: `#PT00024`

Verified:

- Patient appears in Patients list.
- Clicking the patient opens the patient detail panel.
- Detail panel shows contact info, medical information, appointments, transactions, and notes.
- No live Call, Message, Video, payment, reminder, or workflow action was triggered.

Issues:

- No visible patient edit/update action was found.
- Clicking `Book Appointment` from the patient detail panel did not open a booking dialog or visible booking state.
- Prior Appointments module booking persistence issue remains open.

Detailed note: `09-exports/patients-appointments-qa-2026-06-12.md`.

## 2026-06-12 Patients / Appointments Fix Retest

Result: pass for the tested fix path.

Dummy patient:

- `CPX TEST Lead June 11`
- `cpx.test+lead-20260611@example.com`
- UI patient ID: `#PT00024`

Verified:

- Patient detail now includes an `Edit` button.
- Editing patient notes saved successfully and persisted after reopening the detail panel.
- Patient detail `Book Appointment` now opens the Appointments booking modal with the selected patient prefilled.
- TEST toggle was checked by default.
- TEST warning text was visible.
- Blank service/time submission stayed in the modal and showed validation errors.
- Valid TEST booking saved successfully.
- Success toast said: `Appointment created for CPX TEST Lead June 11 on Jun 12, 2026 at 14:45 (TEST - no sends)`.
- Appointments total increased to 27.
- Appointment list showed `CPX TEST Appointment Audit 2026-06-12` with date `Jun 12, 2026`, time `2:45 PM`, status `Pending`, and a `TEST` badge.
- Returning to Patients showed the appointment details from the patient side.

No live Call, Message, Video, payment, reminder, SMS, email, or workflow action was triggered.

Detailed note: `09-exports/patients-appointments-fix-qa-2026-06-12.md`.

## 2026-06-14 Patients Phone / Export Polish Retest

Result: fail.

Codex tested the live published Patients module after Ross approved and published Lovable's Patients phone/export polish build.

Findings:

- Add Patient phone fields are still plain inputs, not the shared country-aware phone component.
- Edit Patient phone fields are still plain inputs.
- Existing dummy patient `CPX TEST Lead June 11` still showed raw E.164 `+15005550111` in the edit form.
- Patients Export did not open an export dialog with scope, columns, and row count.
- Patient list phone display remains mixed across friendly, raw E.164, and legacy hyphenated formats.

No new dummy patient was created because the requested form behavior was visibly missing.

Detailed note: `09-exports/patients-phone-export-qa-2026-06-14.md`.

## 2026-06-14 Repeat Patients Publish Retest / Workstream Mismatch

Result: fail / likely project or workstream mismatch.

Ross published after Lovable reported Financial Transparency wording, volunteer waiver language, three handoff docs, and an internal `/handoff` page. Codex checked the active ClinicPilotX app and official repo.

Findings:

- `/handoff` on `https://clinic-pilot-x.lovable.app` returns a 404 page.
- The official local repo does not contain `docs/QA_TESTING.md`, `docs/CONTENT_EDITING.md`, or `docs/RUNBOOK.md`.
- Patients Add form still uses plain phone inputs.
- Patients Export still does not show the expected export dialog.
- Patient phone display remains mixed, including raw values such as `+15005550111`.

No live sends/calls/payments/workflows were triggered.

Detailed note: `09-exports/patients-phone-export-qa-repeat-2026-06-14.md`.

## 2026-06-14 Patients Phone / Export Corrected Publish Retest

Result: partial pass.

Dummy patient created:

- `CPX TEST Patient Phone QA 20260614`

Verified:

- Patients Add/Edit now uses shared country-aware phone inputs.
- Valid U.S. digits were accepted and saved.
- Invalid short phone values show validation.
- The new dummy patient's main phone appears as `+1 (213) 555-0199`.
- Patient detail shows formatted main and emergency phone values.
- Edit Patient prefilled the shared phone inputs with the stored values.
- Patients Export now opens `Export Patients to CSV` with all/current/selected scope, selected-only disabled at 0 selected, row count, and separate display/E.164 phone columns.
- Leads Add Lead still opens with the shared phone input after the import refactor.

Issues:

- Optional Emergency Contact Phone defaults to `+1` and can block saving if staff leaves it untouched.
- While typing, U.S. values display as `+1 213 555 0199` rather than the requested `+1 (213) 555-0199`.
- CSV download contents are still unverified because the in-app browser does not support downloads.

Detailed note: `09-exports/patients-phone-export-fix-qa-2026-06-14.md`.

## 2026-06-19 Patients Phone Polish Retest

Result: partial pass / fail due to Add Patient database permission blocker.

Dummy lead created for regression QA:

- `CPX TEST Lead Blank Phone 20260619`
- `cpx.test+lead-blank-phone-20260619@example.com`

Verified:

- Patients page loads.
- Existing patient list/detail display includes friendly phone formatting such as `+1 (213) 555-0199`.
- Patients Export opens a scoped CSV dialog with row count, column picker, and display/E.164 phone columns.
- Invalid Patients phone input blocks submit and shows inline validation.
- Leads blank-phone regression passes: leaving the Add Lead phone input untouched at `+1` saved the lead with blank phone.

Failed:

- Add Patient with valid main phone and untouched emergency phone failed with `permission denied for function generate_patient_id`.
- Add/Edit Patient phone inputs still show spaced values such as `+1 213 555 0199` inside the form instead of the preferred `+1 (213) 555-0199`.
- Invalid phone helper copy still uses spaced example text.

Not verified:

- Patients exported CSV file contents, because the Codex in-app browser cannot save downloads.

Detailed note: `09-exports/patients-phone-polish-qa-2026-06-19.md`.

## 2026-06-19 Patients Phone / ID Fix Retest

Result: pass for the prior Add Patient blocker and main phone/export paths.

Dummy patient created:

- `CPX TEST Patient ID Fix 20260619`
- `cpx.test+patient-id-fix-20260619@example.com`

Dummy lead created:

- `CPX TEST Lead Blank Phone PostID 20260619`
- `cpx.test+lead-blank-postid-20260619@example.com`

Verified:

- Add Patient with valid main phone `2135550199` and untouched emergency phone saved successfully.
- The previous `permission denied for function generate_patient_id` error did not recur.
- Patient list shows `+1 (213) 555-0199`.
- Edit Patient opens with main phone `(213) 555-0199` and blank emergency phone.
- Edit Patient save succeeds without touching emergency phone.
- Leads blank-phone regression passes and does not store/display bare `+1`.
- Patients export downloaded as `patients-filtered-2026-06-19.csv`.
- CSV row count is 26.
- CSV includes `Phone (Display)`, `Phone (E.164)`, `Emergency Phone (Display)`, and `Emergency Phone (E.164)`.
- New dummy patient CSV row includes `Phone (Display)=+1 (213) 555-0199` and `Phone (E.164)=+12135550199`.
- New dummy patient CSV emergency phone fields are blank.

Remaining issue:

- Invalid Add Patient phone `123` closed the modal without visible validation and did not create a visible patient row. Expected behavior is to keep the modal open and show inline validation.

Detailed note: `09-exports/patients-phone-id-fix-qa-2026-06-19.md`.

## 2026-06-19 Patients Invalid Phone Final Retest

Result: pass.

Patients invalid phone test:

- Full name: `CPX TEST Invalid Phone Final 20260619`
- Main phone: `123`

Verified:

- Add Patient modal stayed open.
- Inline helper appeared with approved example `+1 (213) 555-0199`.
- No invalid patient row was created.

Patients valid regression:

- Created `CPX TEST Patient Valid Phone Final 20260619`.
- Email: `cpx.test+patient-valid-final-20260619@example.com`.
- Main phone saved from `2135550199`.
- Emergency phone left blank.
- Patient row displays `+1 (213) 555-0199`.

Leads invalid regression:

- Full name: `CPX TEST Lead Invalid Phone Final 20260619`.
- Main phone: `123`.
- Lead modal stayed open.
- Inline helper appeared with approved example `+1 (213) 555-0199`.
- No invalid lead row was created.

Detailed note: `09-exports/patients-invalid-phone-final-qa-2026-06-19.md`.

## Patients Broader Module QA - 2026-06-19

Detailed note: `09-exports/patients-broader-module-qa-2026-06-19.md`.

Verified:

- Patients search isolated `CPX TEST Patient Valid Phone Final 20260619`.
- Status filter options are present and `Inactive` filtering worked during this pass.
- Sort options are present and `Most Visits` / `Highest Spent` produced plausible ordering.
- Patient detail panel opened for the dummy patient and showed contact information, formatted phone, summary metrics, Appointments and Transactions tabs, and action buttons.

Delete QA:

- The row action menu exposes `View Details`, `Edit Patient`, and `Delete Patient`.
- `Delete Patient` triggers a native browser confirmation dialog.
- Codex did not intentionally accept the deletion.
- Browser automation became unstable after the native confirmation, so delete cancel/confirm verification and downstream patient-to-appointment regression remain pending.

## Patient Profile Booking / Delete QA - 2026-06-20

Detailed note: `09-exports/patient-profile-booking-delete-qa-2026-06-20.md`.

Created disposable patient:

- `CPX TEST Disposable Patient Delete QA 20260620`
- `cpx.test+delete-qa-20260620@example.com`
- `#PT00028`

Verified:

- Disposable patient creation succeeded.
- Patient phone displayed as `+1 (213) 555-0199`.
- Patient profile side panel opened and showed expected contact details, notes, tabs, and actions.
- `Book Appointment` from profile opened `/appointments` with patient prefilled.
- TEST checkbox was checked and no-send warning was visible.

Failed:

- TEST appointment save failed with `Invalid time format (HH:MM)` even after `15:30` was entered and verified in the native time input.
- Appointment count stayed `27`; appointment was not created.

Delete:

- Disposable patient's row menu showed `View Details`, `Edit Patient`, and `Delete Patient`.
- Clicking `Delete Patient` triggered a native browser confirmation and again froze browser automation before cancel/confirm could be verified.
- Codex did not intentionally accept deletion.

Reconfirmed:

- Patients page can briefly show `No Plan` and `No patients found`; reload restored `Professional` and real patient data.

## Request 013 Fix QA - 2026-06-20

Detailed note: `09-exports/patient-profile-booking-delete-fix-qa-2026-06-20.md`.

Verified:

- Patient-profile `Book Appointment` now opens with patient prefilled.
- TEST checkbox is checked and no-send warning is visible.
- Time `15:30` saves successfully.
- Appointment count increased from `27` to `28`.
- New appointment appears in Appointments with TEST badge.
- Patient profile Appointments tab shows the new appointment.
- Native delete confirm is gone.
- In-app delete dialog appears with patient name/email/ID.
- Cancel closes dialog and leaves patient intact.
- Confirm delete shows success toast and removes the patient after reload/search.

New issues found:

- Stale patient profile panel stays open after deleting the selected patient.
- Related TEST appointment remains visible after deleting the patient.
- Appointment row phone display remains raw E.164 for the test patient.
- Patient profile appointment time displays with trailing seconds.

## Request 014 Partial QA - 2026-06-21

Detailed note: `09-exports/request-014-partial-qa-2026-06-21.md`.

Verified from live Chrome Appointments list:

- `CPX TEST Disposable Patient Delete QA 20260620` displays phone as `+1 (213) 555-0199`.
- `CPX TEST Lead June 11` displays phone as `+1 (500) 555-0111`.
- Appointment list times display as `3:30 PM` and `2:45 PM`, not trailing-second values.

Not verified:

- Zero-related patient hard delete.
- Related-record patient archive-only path.
- Stale panel close after archive/delete.
- Calendar/detail drawer display polish.

No live communication, payment, calendar, workflow, or reminder action was triggered.

## Request 014 Live QA - 2026-06-21

Detailed note: `09-exports/request-014-live-qa-2026-06-21.md`.

Result: pass for core archive-vs-delete behavior.

Verified:

- Zero-related patient `CPX TEST Zero Related Delete QA 20260621` showed `Delete patient?`, Cancel worked, and confirm removed the patient.
- Related-record patient `CPX TEST Archive Related QA 20260621` had a TEST appointment created with TEST checked.
- Related-record delete action showed `Archive patient?`, including `1 appointment` and `0 payments`.
- Archive cancel worked.
- Archive confirm changed status to `archived`.
- Active filter hid the archived patient.
- Archived filter showed the archived patient.
- Related TEST appointment remained visible with friendly phone/time formatting.
- Calendar drawer showed friendly phone/time formatting.

Follow-up issues:

- Booking modal disabled phone field showed raw `+12135550102`.
- Calendar/detail drawer labeled the patient-created appointment as `Lead`.
- Calendar/detail drawer showed stray `0` text near action buttons.
- Patients page still has intermittent `No Plan` / `No patients found` state.

No live communication, payment, calendar, workflow, reminder, or integration action was triggered.

## Request 015 Live QA - 2026-06-22

Detailed note: `09-exports/request-015-live-qa-2026-06-22.md`.

Result: pass for the tested Request 015 polish scope.

Verified:

- Patient-profile `Book Appointment` prefilled an active patient's disabled phone field as `+1 (213) 555-0199`, not raw E.164.
- Appointments list still showed `CPX TEST Archive Related QA 20260621` with friendly phone `+1 (213) 555-0102` and time `3:45 PM`.
- Appointments Calendar View drawer labeled the same appointment as `Patient`, not `Lead`.
- Drawer phone/time remained friendly.
- The stray standalone `0` no longer appeared near the drawer action buttons.

Safety:

- No `Confirm`, `Cancel`, `Send Reminder`, or `Add to Google Calendar` action was clicked.
- No live communication, payment, calendar, workflow, reminder, or integration action was triggered.

## Appointments Broader QA - 2026-06-23

Detailed note: `09-exports/appointments-broader-qa-2026-06-23.md`.

Result: partial pass / follow-up required.

Verified:

- Appointments recovered from transient `No Plan` to `Professional` and `29 total appointments` after routing through Dashboard.
- Search for `Archive Related` narrowed the list to one expected TEST appointment.
- Keyboard clearing search restored the full `All Appointments (29)` list.
- Filter dialog opened with Status, Consultation Type, and Payment Status controls.
- Consultation Type and Payment Status options were present.
- Sort options were present, and `Date Ascending` changed row ordering.
- Calendar View showed June 2026 TEST appointments on June 12, 20, and 21.
- Calendar drawer for `CPX TEST Archive Related QA 20260621` showed `Patient`, `3:45 PM`, `Pending`, `In-Person`, friendly phone, email, and notes.

Issues:

- Initial Appointments load can still show `No Plan`, `0 total appointments`, disabled Refresh, and empty table.
- Appointment Status filter is missing `Pending`.
- Status labels are inconsistent: examples include `Payment_pending` and `Checked in`.
- Date Range expands but no visible picker/dialog appears.
- Export shows `Appointments exported to CSV` toast but no scoped export dialog.
- Some legacy phone values still show invalid/unformatted fallback such as `+1 234567890`.

Safety:

- No `Confirm`, `Cancel`, `Send Reminder`, or `Add to Google Calendar` action was clicked.
- No live communication, payment, calendar, workflow, reminder, webhook, or integration action was triggered.

## Request 016 Appointments QA - 2026-06-23

Detailed note: `09-exports/request-016-appointments-qa-2026-06-23.md`.

Result: pass for tested Appointments UI and safety scope, with CSV download caveat.

Verified:

- Direct `/appointments` navigation used neutral loading and then real appointment data; the old `No Plan` / `0 total appointments` state did not recur during this pass.
- Status filter includes `Pending`, `Completed`, `Payment Pending`, and other aligned statuses.
- `Payment Pending` filter returned the expected Amanda Lee row.
- `Payment Pending` displays as friendly text.
- Date Range exposes presets, Clear, and Apply.
- Export opens `Export Appointments to CSV` with scope, column picker, row count preview, Phone Display, and Phone E.164 columns.
- Legacy phone fallback now shows `+1234567890 (unverified)`.
- Calendar drawer still shows `Patient`, friendly phone/time, and no stray `0`.
- Send Reminder and Add to Google Calendar are disabled.
- Confirm and Cancel show confirmation dialogs that explicitly state no SMS/email/calendar/refund side effects.

Not accepted:

- Confirm status change.
- Cancel status change.
- Request Payment.
- Reminder/calendar/payment/SMS/email/workflow/webhook actions.

Caveat:

- Controlled browser did not capture a CSV download event after `Download CSV`; verify file contents later in normal Chrome.
- Known console error `Error fetching settings: Object` still appears.

## Dashboard / Analytics QA - 2026-06-24

Detailed note: `09-exports/dashboard-analytics-qa-2026-06-24.md`.

Result: partial pass / Dashboard follow-up required.

Verified source module data:

- Leads shows `17` total leads, `9` new, `5` contacted, `3` qualified, and `17` unassigned.
- Patients shows populated patient records and formatted phone values.
- Appointments shows `29 total appointments`, `6` pending, `13` confirmed, and `4` completed.
- Analytics shows range `Jun 01 - Jun 30` and `3` appointments, which appears plausible from the visible June TEST appointments.

Issue:

- Dashboard still shows all-zero/empty-state values including `Total Leads 0`, `Leads by Source No leads data available`, and `Recent Leads No leads yet`.
- This does not match the Leads/Patients/Appointments source modules.

Safety:

- Read-only QA only.
- No live sends, calls, reminders, payments, calendar writes, workflows, webhooks, edits, deletes, or credential actions were triggered.

## Request 017 Dashboard QA - 2026-06-24

Detailed note: `09-exports/request-017-dashboard-qa-2026-06-24.md`.

Result: pass for the tested Request 017 Dashboard scope.

Verified:

- Dashboard no longer stays at all-zero/empty values.
- After auth/data readiness, Dashboard shows `Total Leads 20`, `Today's Appointments 0`, `Conversion Rate 15%`, and real Leads by Source counts.
- Dashboard Recent Leads shows actual lead rows.
- Follow-ups shows `Coming soon`, not a fabricated number.
- Revenue is labeled `Revenue (MTD)` and shows `$0`.
- Leads page active pipeline count remains `17`; Dashboard `20` appears to include converted/all-time leads and is consistent with the source breakdown.
- Appointments page shows `6` pending including TEST rows; Dashboard shows `3` pending, which is plausible because Request 017 excludes TEST rows from headline metrics.

Safety:

- Read-only QA only.
- No live sends, calls, reminders, payments, calendar writes, workflows, webhooks, edits, deletes, or credential actions were triggered.

## Appointments Status Actions QA - 2026-06-24

Detailed note: `09-exports/appointments-status-actions-qa-2026-06-24.md`.

Result: pass for TEST-only internal status actions.

Test appointment:

- `CPX TEST Archive Related QA 20260621`
- `CPX TEST Archive Appointment 20260621`
- TEST badge present.

Verified:

- Confirm safety dialog said no SMS, email, or calendar invite would be sent.
- Accepting Confirm changed status from `Pending` to `Confirmed`.
- Cancel safety dialog said no cancellation SMS, email, or refund would be sent.
- Accepting Cancel changed status from `Confirmed` to `Cancelled`.
- The appointment remains visible in Appointments with status `Cancelled` and TEST badge.
- Pending summary dropped from `6` to `5`.

Safety:

- No Send Reminder, Google Calendar, payment, SMS, email, workflow, webhook, or credential action was triggered.

## Scope

This log records safe dummy-data CRM testing after the first authenticated dashboard audit.

## Current Safety Boundary

- Dummy data is allowed.
- No live sends/calls/payments.
- No workflow activation.
- No subscription changes.
- No global wipe/delete.

## Test Records Created

| Record Type | Name/Identifier | Status | Cleanup Needed |
| --- | --- | --- | --- |
| Lead | `CPX TEST Lead June 11` / `cpx.test+lead-20260611@example.com` | Created, edited, and converted to patient | Lead is no longer visible in the default active lead list after conversion. |
| Lead | `CPX TEST Chatbot Lead 01` / `cpx.test+chatbot-lead-01@example.com` | Created for future chatbot intake testing | Keep temporarily. Do not send live communications. |
| Lead | `CPX TEST Email Lead 01` / `cpx.test+email-lead-01@example.com` | Created for future email inquiry testing | Keep temporarily. Do not send live communications. |
| Lead | `CPX TEST Leads V2 20260611-19504` / `cpx.test+leads-v2-20260611-19504@example.com` | Created after Lovable Leads v2 publish; edited for QA | Keep temporarily. Do not send live communications. |
| Patient | `CPX TEST Lead June 11` / `cpx.test+lead-20260611@example.com` | Created through lead conversion and verified in Patients | Keep temporarily for downstream appointment testing. |
| Appointment | `CPX TEST Appointment Audit 2026-06-12` for `CPX TEST Lead June 11` | Created as TEST appointment after Lovable fix; visible in Appointments and from patient side | Keep temporarily. Do not trigger live reminders/payments/sends. |

## Module Test Results

| Module | Test | Result | Notes |
| --- | --- | --- | --- |
| Leads | Create dummy lead | Pass | Created `CPX TEST Lead June 11`; total leads increased from 11 to 12 and New Leads increased from 5 to 6 immediately after creation. |
| Leads | Create additional dummy leads | Pass with concern | Created `CPX TEST Chatbot Lead 01` and `CPX TEST Email Lead 01`. Concern: after the second new lead was created, `CPX TEST Chatbot Lead 01` changed from `NEW LEAD`/Cold to `CONTACTED`/Hot without an explicit edit. This confirms the status/temperature mutation is not limited to the edit flow. |
| Leads | Search dummy lead | Pass | Search for `CPX TEST Lead June 11` filtered the table to only the dummy lead and hid unrelated leads such as Sarah Martinez. |
| Leads | Edit dummy lead | Pass with concern | Edit dialog prefilled existing values and saved changes. Service changed to `CPX TEST Botox Consultation - Edited`. Concern: after saving, status changed from `NEW LEAD` to `CONTACTED` and temperature changed from cold to hot without an explicit status/temperature edit. |
| Leads | View Details | Pass | Details dialog opened for the dummy lead. It showed status, temperature, response time, score area, contact info, service requested, notes, created/updated timeline, and buttons for Call, Email, Message, Edit Lead, Calculate Score, Mark as Lost, and Convert to Patient. No live communication buttons were clicked. |
| Leads | Convert to Patient | Pass | Conversion showed success text: `CPX TEST Lead June 11 has been converted to a patient`. Lead count returned to the prior value and search no longer found the lead in the default active lead list. |
| Leads | Status filter pills | Pass with concerns | All/New/Contacted/Qualified/Booked/Lost/Show Converted pills were clickable and changed table/filter state. Concern: summary cards still show overall counts rather than filtered counts. `Show Converted 0` displayed confusing count behavior, including Total Leads changing to 14 while the table showed no rows. |
| Leads | Export | Partial pass; CSV download still pending | Export now opens a CSV dialog with scope selection, column picker, and estimated row count. Column toggles work. Codex could not verify the downloaded CSV file because the in-app browser does not support downloads. |
| Leads v2 publish | Create lead with new form | Pass with notes | Created `CPX TEST Leads V2 20260611-19504`. Verified country-aware phone input, digits-only entry, E.164 storage `+12135550199`, service selector value `Botox`, default source `Manual`, initial status `NEW LEAD`, and initial temperature `Cold`. Invalid fake number `5551234567` appeared to fail without a visible validation message. |
| Leads v2 publish | Edit notes-only lead | Fail | Edited only notes on `CPX TEST Leads V2 20260611-19504`. Save succeeded and Timeline logged `Lead edited`, but temperature changed from `Cold` to `Hot`. Status stayed `NEW LEAD`. This contradicts the expected edit-safety behavior. |
| Leads v2 publish | Details tabs | Pass | Lead Details includes Overview, Timeline, Comms, Files, and Activity. Timeline showed `Lead edited` and `Lead created`. Files tab shows disabled future upload/storage placeholder. |
| Leads v2 publish | Export dialog | Not completed | Export could not be fully verified from the active detail-panel state during this pass. Retest after the blocking temperature mutation issue is fixed. |
| Patients | Verify converted patient | Pass with concern | Patient appeared in Patients list/search with name, email, phone, active status, 0 visits, and $0.00. Concern: page header can briefly show `No Plan` before returning to `Professional`. |
| Patients | Open converted patient detail | Pass | Detail panel opened for `CPX TEST Lead June 11` and showed contact info, medical info, appointments, transactions, and notes. |
| Patients | Edit patient path | Fail / missing UX | No obvious `Edit Patient`, `Update`, or `Save` action was visible from the patient detail panel. |
| Patients | Book appointment from patient detail | Fail / no visible response | Clicking `Book Appointment` from the patient detail panel did not open a booking dialog or visible booking state. |
| Appointments | Book dummy appointment | Fail / inconclusive | Booking form listed the converted patient, auto-filled patient contact fields, accepted service/fee/notes, and accepted time after direct time-field fill. After submit, modal closed but no success message appeared, total remained 26, and the `CPX TEST Appointment Audit` record was not visible in the appointment list. |
| Patients/Appointments fix | Edit patient notes | Pass | Patient detail now has an `Edit` button. Notes-only edit saved and persisted after reopening. |
| Patients/Appointments fix | Book appointment from patient detail | Pass | Button opened `/appointments` booking modal with `CPX TEST Lead June 11 (#PT00024)` prefilled. |
| Patients/Appointments fix | Appointment required-field validation | Pass | Blank service/time submission stayed in the modal and showed validation errors. |
| Patients/Appointments fix | Create TEST appointment | Pass | TEST toggle was on by default. Saved appointment showed success toast, increased total appointments to 27, appeared in list with TEST badge, and appeared from the patient side. |
| Communication Hub | Read-only conversation review | Pending | Do not send. |
| Payments | Read-only/draft-only invoice review | Pending | Do not create live payment link. |
| Automation Center | Configure-panel read-only review | Pending | Do not save/send/activate. |
| Settings | Audit Log retest | Pending | Previous capture missed tab. |

## Lead Test Notes

Fields verified in Add Lead/Edit Lead:

- Full Name
- Email
- Phone
- Service Requested
- Notes

User-guide draft note:

To manually add a lead, staff should open Leads, click `Add Lead`, enter at minimum the full name, optionally add email, phone, requested service, and notes, then click `Create Lead`. The new lead appears at the top of the lead table and can be found through the search box.

Open product question:

Editing a lead's service/notes and creating subsequent leads appears to trigger status/temperature changes on existing dummy leads. Confirm whether this is expected lead scoring/status behavior or a bug before documenting it as final user behavior.

## Patient Conversion Notes

The converted patient was verified in Patients by searching for `CPX TEST Lead June 11`. The patient record showed:

- Name: `CPX TEST Lead June 11`
- Email: `cpx.test+lead-20260611@example.com`
- Phone: `+15005550111`
- Status: active
- Visits: 0
- Value: $0.00

## Appointment Booking Notes

Attempted appointment:

- Patient: `CPX TEST Lead June 11 (#PT00024)`
- Service: `CPX TEST Appointment Audit`
- Date: June 11, 2026
- Time: 2:30 PM
- Type: In-Person
- Consultation fee: 0
- Notes: controlled QA dummy appointment note

Result: no visible success confirmation and no visible new appointment row. This should be treated as a blocking UX/data-persistence issue until verified from backend logs or fixed by Lovable.

## Leads UX Improvement Notes

Export should be more explicit and user-friendly. Recommended behavior:

- Clicking `Export` opens an export dialog.
- User can choose `All leads`, `Current filters`, or `Selected leads`.
- User can choose statuses: New, Contacted, Qualified, Booked, Lost, Converted.
- User can choose date range and source.
- User can choose CSV or XLSX.
- User can choose columns.
- Dialog should show an estimated record count before download.
- Exported filename should include scope and date, for example `clinicpilotx-leads-new-2026-06-11.csv`.
