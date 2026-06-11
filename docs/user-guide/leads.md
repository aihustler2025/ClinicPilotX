# Leads User Guide Draft

Status: working draft from authenticated QA, not final customer documentation.

## What The Leads Module Is For

The Leads module is the clinic's pipeline for new inquiries and prospects. It helps staff capture leads, track status, see lead source, understand service interest, and decide who needs follow-up.

## Verified UI Elements

Verified in the live app on 2026-06-11:

- Total Leads card.
- New Leads card.
- Contacted card.
- Qualified card.
- Average Score card.
- Unassigned card.
- Status filter buttons: All Leads, New, Contacted, Qualified, Booked, Lost, Show Converted.
- Search by name, email, or phone.
- Status, source, date, and staff filters.
- Export, Refresh, and Add Lead buttons.
- Lead table with name, contact, source, service, score, temperature, assigned staff, status, and date.
- Row action menu with View Details, Edit Lead, Convert to Patient, and Delete Lead.

## Manual Lead Creation

1. Open `Leads`.
2. Click `Add Lead`.
3. Enter the lead's full name.
4. Optionally enter email, phone, requested service, and notes.
5. Click `Create Lead`.
6. Confirm the lead appears in the lead table.

Planned improvement: the phone field should format automatically from digits-only input, with a country code picker. For United States and Canada numbers, the display should look like `+1 (555) 123-4567` while storing a normalized number behind the scenes.

Planned improvement: service requested should become a searchable service dropdown/combobox with support for custom services and future clinic-specific service lists.

## Verified Add Lead Fields

- Full Name
- Email
- Phone
- Service Requested
- Notes

## Search

The lead search box can find a lead by name. During testing, searching `CPX TEST Lead June 11` returned only that dummy lead.

## Status Filters

The Leads page includes quick status filters for All Leads, New, Contacted, Qualified, Booked, Lost, and Show Converted.

Working draft note: these filters should let staff focus on a specific pipeline stage. During QA, status filtering changed the visible table and showed `Clear Filters`, but the summary cards continued to show overall counts rather than filtered counts.

Open issue: `Show Converted` displayed confusing count behavior during QA. This needs Lovable review before final documentation.

## Edit Lead

The row action menu includes `Edit Lead`. The edit form prefilled the existing lead values and saved an updated service/notes change.

Open issue: editing the dummy lead changed status/temperature from `NEW LEAD`/cold to `CONTACTED`/hot. This needs confirmation before final documentation.

## View Lead Details

The row action menu includes `View Details`. During testing, the details view showed:

- Lead name, source, status, and temperature.
- Response time and score area.
- Contact information.
- Service requested.
- Lead notes.
- Created and last-updated timeline.
- Details, Communication, and Activity sections.
- Action buttons for Call, Email, Message, Edit Lead, Calculate Score, Mark as Lost, and Convert to Patient.

Safety note: Call, Email, Message, Calculate Score, and Mark as Lost were not clicked during this controlled pass.

Planned improvement: Lead Details should become the complete interaction record for a lead, including timeline, communication history, uploaded/shared photos or files, staff assignment, source, follow-up context, and conversion history.

## Convert Lead To Patient

The row action menu and details view both include `Convert to Patient`.

Verified behavior:

1. A dummy lead was converted to a patient.
2. The app showed success text confirming conversion.
3. The converted lead disappeared from the default active lead search results.
4. The new patient appeared in Patients search with the same name, email, and phone.

Open issue: the final user guide should explain whether converted leads remain accessible through `Show Converted`, and what staff should do if conversion was accidental.

## Not Yet Tested

- Delete Lead.
- Bulk selection/actions.
- CSV import, if available.
- Export file contents by a human tester, because the in-app browser cannot inspect downloaded files directly.
- Staff assignment.
- Lead scoring explanation.
- Lead source automation from chatbot, contact forms, email, or phone.
