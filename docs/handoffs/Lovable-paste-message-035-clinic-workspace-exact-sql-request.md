# Lovable Paste Message 035 - Clinic Workspace Exact SQL Request

Date: 2026-06-26

Use this in Lovable Plan mode only. Do not build yet.

```text
Codex reviewed the Clinic Workspace Setup + Per-Clinic Knowledge Base plan.

Directionally approved:
- No new main left-nav item.
- Top-bar ClinicSwitcher concept is correct.
- Settings > Clinic Workspace is the correct placement.
- Phase A should focus on setup UI + structured metadata only.
- Phase B/C knowledge sources, file uploads, URL crawling, embeddings, email AI sorting, chatbot/API intake, and live integrations remain out of scope.

Do not build yet. Do not run SQL yet.

Because this plan includes migrations, RLS policies, grants, enum checks, and table changes, Codex needs the exact SQL before Ross approves the blue build button.

Please revise and respond in Plan mode only with:

1. Exact forward SQL migration.
2. Exact rollback SQL migration.
3. Current schema pre-checks:
   - current clinic_members.role type and allowed values,
   - whether owner/admin values already exist,
   - current services columns/indexes/unique constraints,
   - current clinics columns,
   - current helper functions available for platform admin / clinic role checks.
4. Exact RLS policies for every new/changed table.
5. Exact grants.
6. Exact frontend file changes.
7. QA plan.
8. Confirmation that no live integrations, edge functions, scheduled_messages, send paths, email AI sorting, chatbot/API intake, Stripe, Google Calendar, or Automation Center workflow behavior will be touched.

Answers to Lovable's open questions:

1. clinic_role enum:
   - Do not extend the enum blindly.
   - First provide the current enum/type evidence.
   - If owner/admin already exist, use them.
   - If they do not exist, propose the smallest exact enum migration and explain whether it can be safely rolled back.

2. Services & Pricing currency:
   - Use integer cents plus a currency column from day one.
   - Default currency should be CAD for Dr. Colin Hong / current pilot clinic.
   - Keep the design multi-clinic/multi-country ready.

3. Knowledge Base > Sources:
   - Show the Sources sub-tab disabled with a clear "Coming in Phase B" banner.
   - It should help Ross and future clients understand where uploads/URLs will go later without pretending the feature is ready.

Scope clarification:
- Keep this as Phase A only.
- It is acceptable to create forms for Business Profile, Branding, Business Hours, Services & Pricing, FAQs, AI Guardrails, and a read-only Team/Integrations status area.
- It is not acceptable to build file upload, URL crawling, AI indexing, embeddings, live inbox connection, chatbot binding, SMS/email sending, calendar writes, payment links, or scheduled messages in this phase.

UX clarification:
- Keep the left sidebar unchanged.
- Put Clinic Workspace in Settings.
- Add top-bar ClinicSwitcher only if it is safe and does not break existing active-clinic behavior.
- If ClinicSwitcher is too much for this phase, propose splitting it into Phase A1 after the Settings-based workspace setup lands.

Please respond with revised exact SQL and implementation plan only. Do not build until Codex reviews the exact SQL.
```
