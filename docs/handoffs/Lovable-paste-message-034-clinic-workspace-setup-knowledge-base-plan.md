# Lovable Paste Message 034 - Clinic Workspace Setup and Knowledge Base Plan

Date: 2026-06-26

Use this in Lovable Plan mode only. Do not build yet.

```text
Codex QA passed Phase 1B.1c Internal Chat for the tested UI and SQL-evidence scope.

Please prepare a Plan-mode proposal for the next product foundation step:

Clinic Workspace Setup + Per-Clinic Knowledge Base.

Important product context:
- ClinicPilotX is a multi-client subscription product.
- Dr. Colin Hong is the first active/pilot client workspace, not a one-off custom build.
- We need to start storing real clinic setup information for Dr. Hong safely, while keeping the design reusable for future subscribed clinics.
- Do not connect live email, SMS, WhatsApp, Messenger, payment, calendar, or chatbot credentials in this phase.
- Do not build yet. Plan only.

UX placement requirement:
- Do NOT add a new main left-nav item for Knowledge Base yet.
- Do NOT clutter the current CRM left sidebar.
- Preferred UX direction:
  1. Add a top-bar clinic/workspace selector near the current app identity/header area, similar in concept to a workspace switcher.
  2. Add a clinic admin setup area under Settings, likely as a new Settings tab or Settings section named something like:
     - Clinic Workspace
     - Clinic Setup
     - Clinic Profile
  3. Inside that admin setup area, use tabs or sections for:
     - Overview / Setup Checklist
     - Business Profile
     - Branding
     - Business Hours
     - Services & Pricing
     - Team / Roles
     - Knowledge Base
     - AI Guardrails
     - Integrations Status
  4. Optionally show a Dashboard setup card or quick action for owners/admins, but keep the main left nav focused.

Role/access requirement:
- Platform admin can see/manage all clinic workspaces later.
- Clinic owner/admin can manage their clinic setup and Knowledge Base.
- Staff should not see admin-only setup controls unless their role allows it.
- If detailed role enforcement needs more backend work, state exactly what is needed.

Knowledge Base goal:
Each clinic needs a single source of truth that ClinicPilotX AI/automation can safely use later.

It should eventually support:
- website URL,
- sitemap URL,
- service-page URLs,
- manual text,
- PDFs,
- DOCX,
- TXT/Markdown,
- FAQs,
- services and pricing,
- hours of operation,
- provider bios,
- clinic policies,
- cancellation/no-show rules,
- financing/payment notes,
- location/parking notes,
- brand voice,
- AI guardrails,
- escalation rules.

For this planning phase, please propose a staged implementation:

Phase A - Setup UI and metadata only:
- Let admin enter/edit clinic profile fields.
- Let admin enter business hours.
- Let admin enter services/pricing manually.
- Let admin enter FAQs manually.
- Let admin enter AI guardrails/escalation rules.
- Store all rows scoped by clinic_id.
- No AI indexing yet unless already safe/simple.

Phase B - Knowledge sources:
- Add URL/file/text source management.
- Supabase Storage for files.
- Source status: Draft, Needs Review, Approved, Stale, Disabled.
- Source categories: Services, FAQ, Hours, Pricing, Policies, Provider Bio, Brand, Legal/Safety, Other.

Phase C - AI-ready indexing later:
- Extract text/chunks.
- Embeddings/vector storage if using Supabase/pgvector or Lovable-supported path.
- Approval workflow before patient-facing AI can use the facts.
- Separate full internal knowledge from patient-facing approved knowledge.

Data model planning:
Please inspect current schema and propose exact tables/columns if needed. Suggested concepts:
- clinic_profiles or extend clinics
- clinic_business_hours
- clinic_services
- clinic_faqs
- clinic_knowledge_sources
- clinic_knowledge_facts
- clinic_ai_guardrails

Required plan details:
1. Best UX placement and route structure.
2. Exact files/components likely to edit.
3. Exact database changes needed, if any.
4. Whether existing clinic tables can be reused.
5. How the UI will behave for platform admin vs clinic owner/admin vs staff.
6. How this fits Dr. Colin Hong as the first active client workspace.
7. What fields we can store immediately for Dr. Hong.
8. What should wait until email/chatbot automation.
9. QA plan.
10. Rollback plan.

Out of scope:
- Live email inbox connection.
- Email AI sorting build.
- Chatbot/API intake build.
- Live SMS/email/WhatsApp/Messenger/Viber/Telegram sends.
- Stripe/payment links.
- Google Calendar writes.
- Edge functions that send externally.
- scheduled_messages.
- Major Phase 1B.2 read-filtering work unless you identify a small blocker and explain it first.

Important:
Respond in Plan mode only. Do not build until Codex reviews and Ross approves.
```

