# ClinicPilotX Controlled Test Data Plan

Date started: 2026-06-11

## Purpose

This plan defines how Codex should test the live ClinicPilotX dashboard with safe dummy data.

Ross approved dummy data testing. Even so, Codex should avoid broad wipe/delete actions unless Ross explicitly approves a specific cleanup operation after backup/export.

## Test Data Naming Rules

All test records should be easy to search, audit, and delete later.

Use these prefixes:

- Lead names: `CPX TEST Lead ...`
- Patient names: `CPX TEST Patient ...`
- Appointment notes/services when possible: `CPX TEST ...`
- Emails: `cpx.test+...@example.com` unless Ross provides a real test inbox.
- Phone numbers: use clearly fake/test numbers where the UI accepts them.

## Approved Safe Tests

Approved for this phase:

- Create dummy lead.
- Edit dummy lead.
- Filter/search dummy lead.
- Convert dummy lead only if the UI clearly supports it without sending messages.
- Create dummy patient.
- Edit dummy patient.
- Book dummy appointment.
- Change dummy appointment status.
- Use calendar/list views.
- Create draft invoice only if it does not create/send a Stripe/payment link.
- Open configuration panels read-only.

Not approved without explicit Ross confirmation:

- Send email.
- Send SMS.
- Send WhatsApp/Messenger/Viber.
- Place voice/VAPI calls.
- Create live Stripe payment links.
- Upgrade/downgrade subscription or add paid add-ons.
- Activate workflows.
- Enter live integration credentials.
- Bulk delete or wipe records.

## Test Pass Order

1. Leads.
2. Patients.
3. Appointments.
4. Communication Hub read-only.
5. Payments read-only/draft-only.
6. Automation Center configure panels read-only.
7. Settings read-only plus Audit Log retest.
8. Analytics/Dashboard verification after dummy data exists.

## Cleanup Rule

After each test pass, list created records and decide whether to keep them as reusable demo/test data or delete them.

