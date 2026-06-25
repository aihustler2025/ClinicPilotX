# Lovable Paste Message 028 - Phase 1B.1b Appointments and Payments Plan

Date: 2026-06-25

Use this in Lovable Plan mode only. Do not build yet.

```text
Codex QA passed Phase 1B.1a for the tested scope after the workflow-safety patch.

Please prepare a Plan-mode proposal for Phase 1B.1b only.

Goal:
Make new Appointments and Payments/Payment Items created from the UI carry the active clinic_id, using the same active-clinic provider/hook pattern that now works for Leads and Patients.

Do not build yet.

Approved planning scope:
- Appointments create/reschedule paths only.
- Payments create/invoice/payment_items paths only.
- Use existing active clinic context.
- Guard submit if active clinic is still loading or missing.
- Preserve existing TEST safeguards on appointments/payments.
- Keep all live-send/payment/calendar behavior disabled during QA.

Files/components to inspect and list in your plan:
- Appointments page create/edit/reschedule paths.
- `src/components/communication/QuickBookingSheet.tsx` if it still creates appointments.
- Any patient-detail Book Appointment path.
- Payment/invoice creation components such as `CreateInvoiceForm.tsx`.
- Any code path that inserts into `appointments`, `payments`, or `payment_items`.

Required plan details:
1. Exact files to edit.
2. Exact insert payload fields to add.
3. Whether each target table already has `clinic_id` and `is_test`.
4. Whether `payment_items` needs explicit `clinic_id` stamping or inherits through parent/payment logic.
5. How QA will create TEST-only appointment/payment records without sending reminders, emails, SMS, payment links, Stripe calls, Google Calendar writes, webhooks, or workflow executions.
6. How you will verify no send-capable side effects fired.
7. Rollback plan.

Out of scope:
- Phase 1B.1c.
- Messages, scheduled messages, conversation notes.
- Communication Hub.
- Automation Center UI.
- Settings.
- Subscription/useSubscription.
- RLS/GRANTs.
- New migrations unless you find a missing required column and explain it first.
- Edge functions.
- Live payment links, Stripe, Google Calendar, email, SMS, Twilio, WhatsApp, Messenger, Viber, Telegram, or voice actions.

Important:
Respond in Plan mode only. Do not build until Codex reviews the exact plan.
```
