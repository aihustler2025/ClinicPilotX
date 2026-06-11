# Leads Module Human QA Script

Status: draft for assistant/human tester confirmation.
Last updated: 2026-06-11.

## Purpose

This script lets a human tester repeat the same controlled Leads checks Codex is performing in the live ClinicPilotX dashboard.

Use only dummy data. Do not use real patient/client data.

## Safety Rules

- Do not click Call, Email, Message, send, payment, or live workflow buttons.
- Do not delete existing records unless Ross explicitly approves cleanup.
- Use clearly marked dummy records.
- Use a plus-address test email if Ross provides an approved inbox, for example `approvedaddress+cpxlead1@gmail.com`.
- If no approved inbox is provided, use `example.com` dummy emails, for example `cpx.test+lead1@example.com`.

## Test Data

Suggested record:

- Full name: `CPX TEST Human Lead 01`
- Email: `cpx.test+human-lead-01@example.com`
- Phone: `+15005550121`
- Service requested: `CPX TEST Human QA Consultation`
- Notes: `Controlled human QA dummy lead. Do not send live communications.`

## Test Steps

### 1. Open Leads

1. Log in to ClinicPilotX.
2. Open `Leads`.
3. Confirm these are visible:
   - Export
   - Refresh
   - Add Lead
   - Total Leads, New Leads, Contacted, Qualified, Avg Score, Unassigned cards
   - Status pills: All Leads, New, Contacted, Qualified, Booked, Lost, Show Converted
   - Search box
   - Filter controls: All Statuses, All Sources, From Date, To Date, All Staff
   - Lead table

Pass if all expected controls are visible.

### 2. Create A Dummy Lead

1. Click `Add Lead`.
2. Enter the test data.
3. Click `Create Lead`.
4. Confirm a success message appears.
5. Confirm the new lead appears in the table.
6. Record whether the Total Leads and New Leads cards changed.

Pass if the lead appears and can be found after creation.

### 3. Search

1. Search for `CPX TEST Human Lead 01`.
2. Confirm only the dummy lead appears.
3. Clear the search.
4. Confirm the normal lead list returns.

Pass if search narrows and clears correctly.

### 4. Edit Lead

1. Open the row action menu for the dummy lead.
2. Click `Edit Lead`.
3. Confirm the form pre-fills the current data.
4. Change service to `CPX TEST Human QA Consultation - Edited`.
5. Add this to notes: `Edited during human QA.`
6. Save.
7. Reopen the lead and verify the changes persisted.
8. Record whether status or temperature changed unexpectedly.

Pass if edited values persist.

Flag if status or temperature changes without the tester changing those fields.

### 5. View Details

1. Open the row action menu for the dummy lead.
2. Click `View Details`.
3. Confirm the details view shows:
   - Lead name
   - Source
   - Status
   - Temperature
   - Contact info
   - Service requested
   - Notes
   - Created/updated timeline
   - Details, Communication, and Activity sections
4. Do not click Call, Email, Message, Calculate Score, or Mark as Lost.
5. Close the details view.

Pass if details match the lead record.

### 6. Status Pills

Click each status pill and record what happens:

- All Leads
- New
- Contacted
- Qualified
- Booked
- Lost
- Show Converted

For each click, record:

- Does the table change?
- Does `Clear Filters` appear?
- Do the table rows match the selected status?
- Do the summary cards still make sense?

Known issue to watch: `Show Converted` may show confusing counts or no rows.

### 7. Filter Controls

Open each filter control and record the options:

- All Statuses
- All Sources
- From Date
- To Date
- All Staff

Apply one safe filter at a time, then clear it.

Pass if filters apply and clear predictably.

### 8. Export

1. Start from All Leads.
2. Click `Export`.
3. Record whether the app:
   - Immediately downloads a file, or
   - Opens an export dialog, or
   - Shows no visible response.
4. If a file downloads, open it and confirm:
   - File type, such as CSV or XLSX.
   - Columns included.
   - Whether it exported all leads or only the current filter.
   - Whether dummy lead data appears when expected.
5. Repeat after selecting `New`.

Current improvement request: Export should let users choose all leads, current filters, selected statuses, date range, columns, and file type before downloading.

### 9. Convert To Patient

Only do this after Ross approves conversion of the human test lead.

1. Open the row action menu.
2. Click `Convert to Patient`.
3. Confirm success message.
4. Search Leads for the lead name and record whether it disappears from the active lead list.
5. Open Patients and search the same name.
6. Confirm the patient exists with matching email and phone.

Pass if patient is created and searchable.

### 10. Findings Format

For each issue, record:

- Module: Leads
- Step number
- Expected result
- Actual result
- Screenshot filename
- Severity: blocker, high, medium, low
- Notes
