# ClinicPilotX Controlled CRM Test Log

Date: 2026-06-11

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
| Patient | `CPX TEST Lead June 11` / `cpx.test+lead-20260611@example.com` | Created through lead conversion and verified in Patients | Keep temporarily for downstream appointment testing. |

## Module Test Results

| Module | Test | Result | Notes |
| --- | --- | --- | --- |
| Leads | Create dummy lead | Pass | Created `CPX TEST Lead June 11`; total leads increased from 11 to 12 and New Leads increased from 5 to 6 immediately after creation. |
| Leads | Search dummy lead | Pass | Search for `CPX TEST Lead June 11` filtered the table to only the dummy lead and hid unrelated leads such as Sarah Martinez. |
| Leads | Edit dummy lead | Pass with concern | Edit dialog prefilled existing values and saved changes. Service changed to `CPX TEST Botox Consultation - Edited`. Concern: after saving, status changed from `NEW LEAD` to `CONTACTED` and temperature changed from cold to hot without an explicit status/temperature edit. |
| Leads | View Details | Pass | Details dialog opened for the dummy lead. It showed status, temperature, response time, score area, contact info, service requested, notes, created/updated timeline, and buttons for Call, Email, Message, Edit Lead, Calculate Score, Mark as Lost, and Convert to Patient. No live communication buttons were clicked. |
| Leads | Convert to Patient | Pass | Conversion showed success text: `CPX TEST Lead June 11 has been converted to a patient`. Lead count returned to the prior value and search no longer found the lead in the default active lead list. |
| Leads | Status filter pills | Pass with concerns | All/New/Contacted/Qualified/Booked/Lost/Show Converted pills were clickable and changed table/filter state. Concern: summary cards still show overall counts rather than filtered counts. `Show Converted 0` displayed confusing count behavior, including Total Leads changing to 14 while the table showed no rows. |
| Leads | Export | Needs human download verification | Export appears as a single button with no visible scope/format selector. Codex in-app browser cannot inspect downloaded files directly. Human QA should confirm whether it exports all leads or current filters and what columns/file type are included. |
| Patients | Verify converted patient | Pass with concern | Patient appeared in Patients search with name, email, phone, active status, 0 visits, and $0.00. Concern: page header briefly showed `No Plan` before returning to `Professional`. |
| Appointments | Book dummy appointment | Fail / inconclusive | Booking form listed the converted patient, auto-filled patient contact fields, accepted service/fee/notes, and accepted time after direct time-field fill. After submit, modal closed but no success message appeared, total remained 26, and the `CPX TEST Appointment Audit` record was not visible in the appointment list. |
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

Editing a lead's service/notes appears to trigger status/temperature changes. Confirm whether this is expected lead scoring behavior or a bug before documenting it as final user behavior.

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
