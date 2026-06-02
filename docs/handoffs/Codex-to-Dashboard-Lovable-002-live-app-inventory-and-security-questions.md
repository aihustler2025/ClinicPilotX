# Codex-to-Dashboard-Lovable-002: Live App Inventory and Security Questions

Date: 2026-06-02
Project: ClinicPilotX
From: Codex
To: Lovable
Mode: Plan
Purpose: Clarification and audit only. Do not build yet.

## Context

Codex performed a pre-login audit of the deployed app at:

https://clinic-pilot-x.lovable.app

Lovable project ID appears to be:

`8b4d9031-af8d-4faf-81d3-135c41ad73b7`

Codex does not yet have authenticated app access, so live UI click testing is pending. However, Codex reviewed the deployed bundle and performed read-only Supabase anon checks.

## Please Answer These Questions Before Build Work

1. Is the official backend standalone Supabase, Lovable Cloud, or both?
2. Is `https://imuyfbvsombbpgdgkhrb.supabase.co` the official backend for this project?
3. Are integration secrets actually stored in Lovable Cloud secrets, Supabase Edge Function secrets, or somewhere else?
4. Which account should Codex use for admin QA? Ross mentioned `teambuzzooka@gmail.com`; does that account exist and what role does it have?
5. Why are these operational tables readable to the anon role: `clinic_subscriptions`, `email_delivery_logs`, `scheduled_messages`, `workflow_executions`, and `workflows`?
6. Should any of those tables be public? If not, please propose an RLS fix plan, but do not apply it yet.
7. Why do `internal_channel_members`, `internal_channels`, and `internal_messages` return an infinite recursion RLS error involving `internal_channel_members`?
8. Why does the deployed bundle reference `assignment_rules` and `signatures` when Supabase REST says those tables are not in the schema cache?
9. Which left-nav modules are complete, partial, mock/demo, or planned?
10. For Automation Center, which workflow rows are real executable workflows vs placeholder configuration rows?
11. Which automations currently send real emails/SMS/calls/messages?
12. Are any paid integrations active: Stripe, Twilio, VAPI, WhatsApp, Messenger, Viber, Google Calendar, or others?
13. Is the `/video-consultation` route currently implemented beyond a placeholder? Does it include recording, consent, transcript, AI notes, file/photo exchange, and consult sign-off?
14. What should Codex verify first after admin login is available?

## Important Constraints

- Do not build or change anything yet.
- Do not activate paid integrations.
- Do not change RLS until Codex and Ross approve the fix plan.
- Do not expose secrets or patient/lead/message data in your response.
- Product/dashboard functionality takes priority over marketing website work.
