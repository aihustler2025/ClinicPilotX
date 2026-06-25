# Lovable Paste Message 029 - Phase 1B.1c Messages Plan

Date: 2026-06-25

Use this in Lovable Plan mode only. Do not build yet.

```text
Codex QA passed Phase 1B.1b for the tested Appointments and Payments scope.

Please prepare a Plan-mode proposal for Phase 1B.1c only.

Goal:
Make message-related rows created from safe UI paths carry the active clinic_id, without enabling or triggering any live sends.

Planning scope:
- `messages`
- `scheduled_messages`
- `conversation_notes`
- any safe internal note/message creation path that writes to those tables

Files/components to inspect and list in your plan:
- `src/components/appointments/RequestPaymentDialog.tsx`
- `src/components/communication/ScheduleMessageDialog.tsx`
- `src/components/communication/ConversationNotesPanel.tsx`
- any Communication Hub component that inserts into `messages`, `scheduled_messages`, or `conversation_notes`
- any internal chat component that inserts message-like rows, but only inspect and report unless clearly in this scope

Required plan details:
1. Exact files to edit.
2. Exact insert payload fields to add.
3. Whether each target table already has `clinic_id`.
4. Whether each target table has `is_test` or an equivalent safety flag.
5. Which UI actions create rows without sending anything externally.
6. Which UI actions are send-capable and must remain out of scope.
7. How QA can create test rows without sending SMS, email, payment links, webhooks, WhatsApp, Messenger, Viber, Telegram, voice, Stripe, or Google Calendar actions.
8. How you will verify no send-capable side effects fired.
9. Rollback plan.

Out of scope:
- Building anything before Codex reviews this plan.
- Live send actions.
- Request Payment if it creates a payment link or sends anything externally.
- SMS/email/WhatsApp/Messenger/Viber/Telegram/voice.
- Stripe/payment links.
- Google Calendar.
- Edge functions.
- Automation Center UI.
- Settings.
- Subscription/useSubscription.
- RLS/GRANTs.
- New migrations unless you find a missing required column and explain it first.
- Phase 1B.2 read filtering.
- Clinic switcher/onboarding UI.

Important:
Respond in Plan mode only. Do not build until Codex reviews the exact plan.
```
