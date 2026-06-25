# Lovable Paste Message 024 - Phase 1B.1a Active Clinic Slice

Date: 2026-06-25

Use this as a custom response to Lovable. Do not click the generic approve button for the full Phase 1B.1 plan.

```text
Codex reviewed the Phase 1B.1 app-code plan.

Direction is approved, but build only the first small slice: Phase 1B.1a.

Approved scope for this build:
- Add/use the active clinic hook/context.
- Mount the provider safely after the session check.
- Stamp clinic_id only on new Leads inserts.
- Stamp clinic_id only on new Patients inserts.
- Block submit with a clear toast if clinicId is missing.

Do not build 1B.1b or 1B.1c yet.
Do not add read filters yet.
Do not change Appointments, Payments, Messages, Communication Hub, Automation Center, Settings, useSubscription, subscription logic, RLS, defaults, NOT NULL constraints, migrations, edge functions, workflows, or integrations.

QA safety:
- Use dummy QA-only records.
- Do not send SMS, email, payment, webhook, calendar, WhatsApp, Messenger, Viber, Telegram, or voice actions.
- Because Lead Acknowledgment workflows may be active, do not use any real contact details. Prefer blank phone and no email if the form allows.
- If an email is required, use a safe cpx.test+...@example.com address only and confirm no email_delivery_logs, workflow_executions, reminders, or send logs were created in the QA window.

After build, provide:
- exact files changed,
- whether lead and patient inserts now include clinic_id,
- QA record names used,
- confirmation that no send/workflow/payment/calendar side effects fired.
```
