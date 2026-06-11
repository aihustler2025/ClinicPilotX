# Codex to Lovable 004 - Leads Module Improvements

Date: 2026-06-11
Mode: Build only after Ross approves this prompt in Lovable.

## Context

Ross reviewed the current Leads module and confirmed it is not finished enough for client testing.

ClinicPilotX is being built in Lovable. Keep the current project structure and Supabase/Lovable backend. Do not introduce a paid external backend or paid integration.

Do not activate live email, SMS, calls, payment, chatbot, or social integrations during this work.

## Main Goal

Improve the Leads module so manual lead creation, lead filtering/export, and lead record review feel like a real clinic CRM workflow instead of a basic first draft.

## Required Improvements

### 1. Improve Phone Input

Replace the current plain phone input with a user-friendly international phone field.

Requirements:

- Include country selector/picker with flag or country code.
- Default should be United States/Canada-style `+1`.
- Users should type digits only.
- For `+1`, automatically format as `+1 (555) 123-4567`.
- Do not require the user to type parentheses, spaces, or dashes.
- Store the canonical value in a consistent normalized format, preferably E.164 such as `+15551234567`, while displaying friendly formatting in the UI.
- Validate obvious invalid phone numbers before submission.
- Keep the field usable for other countries with different patterns.

Use a proven library if already available in the project, or add a lightweight maintained phone input/masking library compatible with the existing stack.

### 2. Improve Service Requested

The current free-text `Service Requested` field should become a better service selector.

Requirements:

- Use a searchable dropdown/combobox.
- Include common default services for med spa/plastic surgery/clinic demos, such as:
  - Botox
  - Dermal Fillers
  - Consultation
  - Laser Hair Removal
  - Chemical Peel
  - Microneedling
  - Skin Rejuvenation
  - Facelift
  - Breast Augmentation
  - Hair Transplant
- Allow staff to type a custom service if the service is not listed.
- Store the final selected/typed service cleanly on the lead record.
- Design for future clinic-specific service settings, where each clinic can maintain its own service list.

### 3. Improve Create New Lead Modal

Current fields:

- Full Name
- Email
- Phone
- Service Requested
- Notes

Keep these, but improve the form with:

- Lead Source field with options:
  - Manual
  - Website Contact Form
  - Chatbot
  - Email Inquiry
  - Phone Call
  - Facebook
  - Instagram
  - Referral
  - Other
- Preferred Contact Method:
  - Phone
  - Email
  - SMS
  - WhatsApp or messaging app if already modeled, but do not send anything live.
- Urgency or interest level:
  - Low
  - Medium
  - High
  - Urgent
- Consent/permission note field or checkbox if needed for future messaging compliance.
- Optional tags field, if the existing data model supports tags.

Do not overcomplicate the first version. Keep the modal clean and fast.

### 4. Improve Lead Details

Lead Details should become the central record for everything known about a lead.

Add or improve sections for:

- Contact summary.
- Lead source and intake channel.
- Service interest.
- Current status and temperature.
- Assigned staff.
- Notes.
- Timeline/activity history.
- Communication history.
- Uploaded/shared files or photos, if current storage supports this safely.
- Conversion history if converted to patient.

If files/photos are not currently implemented, add a clear placeholder section or data model note for future build, but do not add unsafe file upload behavior without backend/storage confirmation.

### 5. Timeline Requirement

Every important lead interaction should eventually be visible in a timeline:

- Manual lead created.
- Lead edited.
- Status changed.
- Staff assigned.
- Message/email received.
- Message/email sent.
- File/photo submitted.
- Appointment booked.
- Converted to patient.
- Marked lost.

For this build, implement the timeline only if the backend already supports safe event records. If not, add the UI structure and document the missing backend requirement.

### 6. Export Improvements

Replace the basic one-click Export behavior with an export dialog.

Requirements:

- User can choose export scope:
  - All leads
  - Current filters
  - Selected leads
- User can choose statuses:
  - New
  - Contacted
  - Qualified
  - Booked
  - Lost
  - Converted
- User can choose date range.
- User can choose source.
- User can choose file type:
  - CSV
  - XLSX if already supported
- User can choose columns if practical.
- Show estimated row count before download.
- Use clear filenames, for example `clinicpilotx-leads-new-2026-06-11.csv`.

### 7. Fix Known Leads Bugs / Inconsistencies

Investigate and fix:

- Editing service/notes changed the dummy lead from `NEW LEAD`/cold to `CONTACTED`/hot without explicitly changing status/temperature.
- `Show Converted 0` showed confusing totals and no rows during QA.
- Summary cards show overall counts while status filters are active; decide whether cards should show overall totals or filtered totals, and make the UI label clear.

### 8. Future Intake Sources

Design the Leads module so it can later accept leads from:

- ClinicPilotX chatbot product.
- Website contact form.
- Email inquiry parser/AI triage.
- Phone/voice assistant.
- Manual staff entry.
- Social channels such as Facebook and Instagram.

Do not build the full chatbot/email/social automation in this prompt. Only make the Leads module data/UI ready for those future sources.

## Safety

- Do not send real emails, SMS, calls, WhatsApp/Messenger/Viber messages, or payment links.
- Do not activate workflows.
- Do not add live credentials.
- Use dummy data only.
- Keep existing records intact.

## Acceptance Criteria

- Manual lead creation works with formatted phone input.
- Phone entry accepts digits-only typing and displays clean `+1 (555) 123-4567` formatting.
- Services can be selected from a searchable list or typed as custom.
- Lead source can be set during manual creation.
- Lead details show a more complete CRM record layout.
- Export opens a clear dialog before download.
- `Show Converted` behavior is understandable and consistent.
- Editing lead notes/service does not unexpectedly change status/temperature unless documented intentional logic exists.
- UI remains clean, fast, and mobile-friendly.
