# Request 028 Phase 1B.1b Appointments and Payments QA

Date: 2026-06-25

Published app: `https://clinic-pilot-x.lovable.app`

## Scope Tested

Lovable reported Phase 1B.1b was applied across:

- Appointments create path.
- RescheduleDialog readiness guard.
- QuickBookingSheet active-clinic stamping and test auto-flagging.
- CreateInvoiceForm active-clinic stamping for payments and payment_items.

## Result

Pass for the tested live UI and Automation Center Activity Logs scope.

Codex could not independently run authenticated SQL from this environment, so DB-level `clinic_id` assertions still rely on Lovable's implementation claim plus successful UI behavior and no visible side effects.

## Activity Log Baseline

Before creating new records, Automation Center -> Activity Logs showed no fresh workflow rows.

Newest rows were still old:

- `Completed` - `Smart Follow-up Sequence` - about 5-6 hours ago
- `Failed` - `Lead Acknowledgment` - about 5-6 hours ago

## TEST Appointment Created

Created through Appointments -> Book Appointment using manual QA data with the TEST checkbox already checked:

- Patient/name: `QA TEST 1B1B APPOINTMENT 20260625-A`
- Email: `cpx.test+1b1b-appt-A@example.com`
- Service: `QA TEST 1B1B Consultation`
- Date/time: June 25, 2026 at 3:45 PM
- Notes: `Controlled TEST appointment for Phase 1B.1b clinic_id stamping QA. No sends.`

Observed:

- Toast: `Appointment created for QA TEST 1B1B APPOINTMENT 20260625-A on Jun 25, 2026 at 15:45 (TEST - no sends)`
- Appointment count increased from `29` to `30`.
- Today count increased from `0` to `1`.
- Pending count increased from `5` to `6`.
- New appointment appeared at the top of the Appointments table.
- New appointment showed `Pending` and `TEST`.

## QA Invoice Created

Created through Payments & Billing -> New Invoice:

- Patient: `QA TEST SAFETY PT 20260625-A`
- Description: `QA TEST 1B1B invoice for clinic_id stamping`
- Service item: `Follow-up Visit`
- Quantity: `1`
- Price: `$1.00`
- Payment status: `Pending`
- Payment method: `Card`
- Notes: `Controlled TEST invoice for Phase 1B.1b clinic_id stamping QA. No payment link or Stripe call.`

Observed:

- Toast: `Invoice created successfully`
- New invoice appeared at the top of Payments table:
  - Invoice: `INV00017`
  - Patient: `QA TEST SAFETY PT 20260625-A`
  - Amount: `$1.00 CAD`
  - Status: `pending`
- Pending Payments increased from `$2050.00` to `$2051.00`.
- Outstanding Balance increased from `$2050.00` to `$2051.00`.

No payment link, Stripe checkout, send button, email, SMS, calendar, webhook, or integration action was clicked.

## Activity Logs After QA

After creating the TEST appointment and QA invoice, Codex waited and re-opened Automation Center -> Activity Logs.

Newest workflow rows remained old:

- `Completed` - `Smart Follow-up Sequence` - about 6 hours ago
- `Failed` - `Lead Acknowledgment` - about 6 hours ago

No fresh workflow rows appeared for:

- Appointment Confirmation,
- Payment Receipt,
- Payment Reminder Sequence,
- Lead Acknowledgment,
- Smart Follow-up Sequence,
- or any other visible workflow.

## Smoke Test

Codex smoke-rendered:

- Dashboard
- Appointments
- Payments
- Patients
- Automation Center
- Settings

All checked routes rendered.

Console note:

- Existing dialog accessibility warning still appears:
  - `Warning: Missing Description or aria-describedby={undefined} for {DialogContent}.`
- No fatal console error was observed.

## Decision

Phase 1B.1b can be treated as passed for the tested UI and visible safety scope.

Next recommended step: request Plan-mode Phase 1B.1c for messages, scheduled_messages, and conversation_notes active-clinic stamping only. Continue keeping live-send paths and Communication Hub sends out of build scope until separately reviewed.
