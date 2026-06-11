# Lovable Paste Message 004 - Leads Module Improvements

Use this in Lovable.

Recommended mode: Plan first.

After Lovable replies with its plan, copy/paste Lovable's response back to Codex before clicking Approve/Build.

## Message To Paste

Please review this as a PLAN first. Do not build until I approve after Codex reviews your plan.

We need to improve the existing ClinicPilotX Leads module. Do not rebuild the app from scratch. Keep the current Lovable/Supabase/backend structure. Do not activate or connect live email, SMS, calls, payment, chatbot, Facebook, Instagram, WhatsApp, Messenger, Viber, or any paid/live integrations.

Main issue: the Leads module is not finished enough for client testing. Please produce a concrete implementation plan for these Leads improvements:

1. Improve the Create New Lead phone field.
- Add a country code selector/picker.
- Default to +1 for United States/Canada.
- User should type digits only.
- For +1 numbers, display as `+1 (555) 123-4567`.
- User should not type parentheses, spaces, or dashes.
- Store a normalized value, preferably E.164 like `+15551234567`.
- Validate obvious invalid numbers.
- Keep it usable for other countries.
- Use an existing/lightweight maintained phone input/masking library if appropriate for this project.

2. Improve Service Requested.
- Replace plain text with a searchable service dropdown/combobox.
- Include starter options: Botox, Dermal Fillers, Consultation, Laser Hair Removal, Chemical Peel, Microneedling, Skin Rejuvenation, Facelift, Breast Augmentation, Hair Transplant.
- Allow custom typed service if not listed.
- Design so future clinic-specific service lists can be managed later.

3. Improve Create New Lead modal without making it cluttered.
Keep Full Name, Email, Phone, Service Requested, Notes.
Add or plan these fields if supported safely:
- Lead Source: Manual, Website Contact Form, Chatbot, Email Inquiry, Phone Call, Facebook, Instagram, Referral, Other.
- Preferred Contact Method: Phone, Email, SMS.
- Urgency/Interest: Low, Medium, High, Urgent.
- Consent/permission note if needed for future messaging compliance.

4. Improve Lead Details.
Lead Details should become the full relationship record:
- Contact summary.
- Lead source/intake channel.
- Service interest.
- Current status/temperature.
- Assigned staff.
- Notes.
- Timeline/activity history.
- Communication history.
- Uploaded/shared files or photos if current storage safely supports it.
- Conversion history if converted to patient.

If files/photos or timeline event storage are not currently safe/supported, do not force it. Instead, identify the missing backend requirement.

5. Timeline direction.
Eventually the timeline should include:
- Lead created.
- Lead edited.
- Status changed.
- Staff assigned.
- Message/email received.
- Message/email sent.
- File/photo submitted.
- Appointment booked.
- Converted to patient.
- Marked lost.

Implement this only if the backend already supports safe event records. Otherwise include it in the plan as a backend requirement.

6. Improve Export.
Replace one-click export with an export dialog:
- Scope: All leads, Current filters, Selected leads.
- Statuses: New, Contacted, Qualified, Booked, Lost, Converted.
- Date range.
- Source.
- File type: CSV, XLSX if already supported.
- Column selection if practical.
- Estimated row count before download.
- Clear filename like `clinicpilotx-leads-new-2026-06-11.csv`.

7. Investigate and fix known Leads bugs.
- Editing service/notes changed dummy lead status/temperature unexpectedly.
- Creating a later dummy lead also changed an earlier dummy lead from NEW LEAD/Cold to CONTACTED/Hot without explicit editing.
- Show Converted showed confusing count/table behavior.
- Summary cards show overall counts while filters are active; make the behavior clear and consistent.

8. Future intake readiness.
Design Leads so it can later receive leads from:
- ClinicPilotX chatbot.
- Website contact form.
- Email inquiry parser/AI triage.
- Phone/voice assistant.
- Manual staff entry.
- Facebook/Instagram/social channels.

Do not build the chatbot/email/social automation in this prompt. Only make the Leads module data/UI ready.

Please respond with:
- Files/components/tables/functions you expect to modify.
- Whether any database migration/schema change is required.
- Whether any new package/library is needed.
- Risks or assumptions.
- A step-by-step build plan.
- How you will test it with safe dummy data.

Do not run live sends, calls, payment links, or workflow activations.
