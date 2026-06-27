# ClinicPilotX Clinic Knowledge Base Roadmap

Last updated: 2026-06-27

## Purpose

Each ClinicPilotX subscriber should eventually have a clean, per-clinic Knowledge Base that stores the business facts AI workflows can safely use.

This is not part of the current Phase 1B.1 active-clinic build. It is parked here so the product direction is not lost.

## Phase A Status - 2026-06-27

The first Clinic Workspace / Knowledge Base foundation is now live under:

`Settings -> Clinic Workspace`

Phase A includes:

- Business Profile
- Branding
- Business Hours
- Services & Pricing
- Team & Roles read-only view
- Knowledge: FAQs
- Knowledge: Sources placeholder
- AI Guardrails
- Integrations Status

Codex QA verified that Business Profile, Services & Pricing, Knowledge FAQs, and AI Guardrails can save and persist after reload.

Still not built:

- file uploads,
- URL/sitemap ingestion,
- source preview,
- document parsing,
- embeddings/vector storage,
- source approval workflow,
- chatbot consumption,
- email AI sorting consumption.

Next near-term need:

- fill real Dr. Hong pilot clinic facts,
- fix small Clinic Workspace polish issues,
- then plan safe test-inbox email AI sorting using this workspace context.

## Why It Matters

ClinicPilotX will need accurate clinic-specific facts for:

- chatbot answers,
- email AI sorting,
- appointment request handling,
- service/pricing questions,
- staff handoff summaries,
- future voice/VAPI/Twilio agents,
- future website/contact-form lead intake,
- future Automation Center workflows.

The Knowledge Base should prevent one clinic's services, pricing, hours, policies, or brand voice from leaking into another clinic's automation.

Ross clarified on 2026-06-26 that this should become the clinic/subscriber's **single source of truth**. It should eventually power the main ClinicPilotX app, the future ClinicPilotX chatbot, email AI sorting, communication workflows, future mobile app, and future APIs.

Each clinic should be able to update its own truth over time: change pricing, replace old documents, add new service pages, update FAQs, change hours, and mark what is approved for AI use.

## Reference Patterns

Research notes:

- ElevenLabs Knowledge Base supports file, URL, and text inputs for conversational agents, including PDFs, TXT, DOCX, HTML, EPUB, documentation links, product pages, and manual text. It also recommends clear structure, smaller focused documents, regular updates, and using conversation transcripts to identify missing knowledge.
- OpenAI File Search / vector stores parse, chunk, embed, and retrieve files using both semantic and keyword search. The default pattern uses chunking, embeddings, ranking, and configurable retrieval limits.
- Supabase supports file storage with access controls and AI/vector storage patterns through pgvector/vector columns and vector buckets. This fits Ross's preference to use Lovable/Supabase first before unrelated paid platforms.

Useful references:

- ElevenLabs Knowledge Base: `https://elevenlabs.io/docs/eleven-agents/customization/knowledge-base`
- OpenAI File Search / Vector Stores: `https://developers.openai.com/api/docs/assistants/tools/file-search`
- Supabase Vector Columns: `https://supabase.com/docs/guides/ai/vector-columns`
- Supabase Storage: `https://supabase.com/docs/guides/storage`

## Product Surface

Future left-nav or Settings area candidate:

`Clinic Setup -> Knowledge Base`

or:

`Settings -> Clinic Knowledge`

Ross also provided a workspace-switcher reference pattern from BuzzForge. ClinicPilotX should eventually have a similar product concept, adapted to clinics:

- top bar current clinic/workspace selector,
- list of available clinic workspaces,
- create new clinic/workspace action,
- per-workspace profile and knowledge state,
- strict data isolation by `clinic_id`.

This should not be copied visually from BuzzForge, but the product concept is important: Ross should be able to switch between Dr. Colin Hong and future subscribed clinic clients the way the reference app switches between workspaces.

Recommended sections:

- Overview
- Setup Checklist
- Website Sources
- Uploaded Files
- Services & Pricing
- FAQs
- Business Hours
- Policies
- Provider Bios
- Brand Voice
- AI Guardrails
- AI Approved Answers
- Escalation Rules
- Connected Workflows
- Review & Gaps

## Subscriber Onboarding Inputs

During setup, each clinic should be guided to add:

- clinic name,
- logo,
- website,
- primary contact email,
- phone,
- address,
- hours of operation,
- holiday/closure rules,
- service categories,
- services/procedures,
- pricing ranges or consultation-fee guidance,
- provider/staff bios,
- FAQs,
- pre-appointment instructions,
- post-treatment instructions,
- cancellation/no-show policies,
- financing/payment notes,
- parking/location notes,
- brand voice/tone,
- things AI must not say,
- escalation rules for urgent or medical-risk questions.

For medical/cosmetic clinics, the onboarding must clearly separate:

- factual business information AI may use,
- marketing copy that needs staff approval,
- medical/safety rules,
- legal disclaimers,
- topics that must be escalated to a human.

## Supported Source Types

Initial source types to plan:

- Website URL.
- Individual service-page URL.
- Sitemap URL.
- Manual text note.
- PDF upload.
- DOCX upload.
- TXT/Markdown upload.
- FAQ import.
- CSV/service list import, later.

Potential future source types:

- Google Drive folder.
- Website crawler.
- Prior email/chat conversations.
- Approved marketing content.
- Video transcript imports.

Ross's requested user-friendly input modes:

- upload files by drag-and-drop,
- add one URL,
- add multiple URLs,
- add a sitemap,
- create text manually,
- create folders/categories,
- enter FAQs manually,
- enter services and prices manually,
- let AI organize uploaded material into suggested categories for staff approval.

## Storage Direction

Preferred product architecture:

- Store source files in Supabase Storage, scoped by `clinic_id`.
- Store metadata in Postgres tables such as `clinic_knowledge_sources`, `clinic_knowledge_documents`, and `clinic_knowledge_chunks`.
- Store embeddings in Supabase/Postgres with pgvector or Supabase vector storage.
- Keep source text, extracted chunks, review status, source type, source URL, file path, version, and last-refresh timestamp.
- Use RLS so each clinic can access only its own Knowledge Base.

Do not use unrelated paid vector databases until Lovable/Supabase limits are known.

## Suggested Data Model Later

Possible future tables:

- `clinic_knowledge_sources`
  - `id`
  - `clinic_id`
  - `source_type`
  - `title`
  - `url`
  - `storage_path`
  - `status`
  - `last_indexed_at`
  - `created_by`
  - `created_at`
  - `updated_at`

- `clinic_knowledge_chunks`
  - `id`
  - `clinic_id`
  - `source_id`
  - `chunk_text`
  - `embedding`
  - `metadata`
  - `token_count`
  - `created_at`

- `clinic_knowledge_facts`
  - `id`
  - `clinic_id`
  - `category`
  - `question`
  - `answer`
  - `approved`
  - `last_reviewed_at`

- `clinic_ai_guardrails`
  - `id`
  - `clinic_id`
  - `rule_type`
  - `rule_text`
  - `severity`
  - `enabled`

## UX Direction

The interface should feel clean, simple, and operational:

- white/light neutral background,
- compact but readable sections,
- drag-and-drop upload area,
- URL input with Add button,
- source cards with status chips,
- search/filter by source type and status,
- clear upload/indexing states,
- "Needs review" queue,
- "Last updated" timestamps,
- preview drawer for each source,
- warning for unapproved or stale content.

Possible dashboard cards:

- Setup completion.
- Knowledge Base health.
- Number of sources.
- Approved vs needs-review sources.
- Stale sources.
- Missing critical sections, such as hours, services, prices, FAQs, policies, or escalation rules.

Source list columns:

- Source.
- Category.
- Status.
- Last updated.
- Used by workflows/agents.

Example status chips:

- Approved.
- Needs Review.
- Draft.
- Stale.
- Disabled.

Derived insight sections:

- Safe claims.
- Banned claims.
- Price guidance.
- Escalation triggers.
- Missing knowledge gaps.

The AI should not automatically make all uploaded content live. Clinic staff should approve important facts before chatbots or automations rely on them.

Avoid copying any competitor's exact design. Use ClinicPilotX's own visual system and keep it consistent with the current clean dashboard style.

## Reference Screenshots From Ross

Ross shared screenshots on 2026-06-25 from an ElevenLabs Knowledge Base workflow as a general product reference, not as a design to copy.

Local screenshot references:

- `C:\Users\user\OneDrive\Pictures\Screenshots\Screenshot 2026-06-25 123031.png`
- `C:\Users\user\OneDrive\Pictures\Screenshots\Screenshot 2026-06-25 123009.png`
- `C:\Users\user\OneDrive\Pictures\Screenshots\Screenshot 2026-06-25 123108.png`
- `C:\Users\user\OneDrive\Pictures\Screenshots\Screenshot 2026-06-25 123048.png`

Ross shared additional screenshots on 2026-06-26:

- BuzzForge workspace selector and dashboard pattern:
  - `C:\Users\user\OneDrive\Pictures\Screenshots\Screenshot 2026-06-26 101523.png`
  - `C:\Users\user\OneDrive\Pictures\Screenshots\Screenshot 2026-06-26 101544.png`
- BuzzForge Knowledge Base page:
  - `C:\Users\user\Downloads\Knowledge-Base-—-BuzzForge-06-26-2026_10_25_AM.png`
  - `C:\Users\user\Downloads\Knowledge-Base-—-BuzzForge-06-26-2026_10_25_AM (1).png`

Useful ideas to remember later:

- top-level source actions such as Add URL, Add Files, Create Text, and Create Folder,
- drag-and-drop upload modal,
- parent folder selection,
- accepted file-type chips,
- source list with search and filters,
- document preview panel,
- source metadata such as sharing status, document ID, created date, last updated date, size, index status, and dependent agents/workflows,
- update source, download/source file, and edit actions.
- workspace selector for switching between multiple clients/clinics.
- health/status cards that show whether the knowledge base is complete enough to use.
- source approval workflow before AI uses a fact.

Important: use these only as inspiration for product planning. Do not copy the exact ElevenLabs layout, wording, visual hierarchy, or styling.

## AI Safety Requirements

Knowledge Base content should support medical/cosmetic clinic workflows, but AI must stay cautious:

- AI should not diagnose.
- AI should not guarantee outcomes.
- AI should not quote prices as final unless the clinic marks them as approved/fixed.
- AI should escalate urgent or medical-risk messages.
- AI should identify uncertainty and route to staff.
- AI should cite or link the source internally for staff review where possible.
- AI should use a narrower "approved answer set" for patient-facing chatbot/email replies than it uses for staff-facing summaries.
- AI should escalate to staff when a question touches diagnosis, urgent symptoms, complications, medical risk, legal questions, final pricing, or treatment suitability.
- AI should never invent clinic policies or service prices.

## Knowledge Scope Layers

Ross described the need for a larger clinic brain and smaller controlled brains for specific tools.

Recommended layers:

1. Full Clinic Knowledge Base
   - All approved and draft clinic materials.
   - Used by staff/admin review and internal tools.

2. Patient-Facing Approved Knowledge
   - Narrower set of approved answers for chatbot, email replies, and public-facing automation.
   - Excludes unapproved drafts and internal-only notes.

3. Workflow-Specific Knowledge
   - Smaller subsets for a specific automation, such as email lead sorting, appointment request detection, or no-show recovery.

4. Escalation Rules
   - Rules that tell AI when to stop answering and route to staff.

This structure helps protect ClinicPilotX, the clinic, and the patient.

## Future Lovable Prompt Draft

Use this later, not during the current Phase 1B.1 work:

```text
Please plan a ClinicPilotX per-clinic Knowledge Base module in Plan mode only.

The Knowledge Base should let each subscriber/clinic upload and manage business facts that AI workflows can safely use. It should support website URLs, service-page URLs, sitemap URLs, manual text, PDFs, DOCX, TXT/Markdown, FAQs, services/pricing, hours, policies, provider bios, brand voice, and AI guardrails.

It should support a multi-clinic workspace model. Ross should be able to switch between clinic workspaces, and each clinic should have its own isolated knowledge base scoped by clinic_id.

Keep the UI clean, light, organized, and consistent with the current ClinicPilotX dashboard. Do not copy any competitor UI exactly.

Prefer Lovable/Supabase infrastructure first:
- Supabase Storage for source files,
- Postgres metadata tables scoped by clinic_id,
- pgvector or Supabase vector storage for embeddings/chunks,
- RLS isolation per clinic,
- no unrelated paid vector database unless Ross approves.

Please propose:
1. UX layout.
2. Source types.
3. Data model.
4. Upload/indexing workflow.
5. AI safety/approval workflow.
6. How chatbot, email AI sorting, voice, and Automation Center would consume the Knowledge Base later.
7. QA checklist.
8. Risks and open questions.
9. How to separate full internal clinic knowledge from patient-facing approved knowledge.
10. How to support Dr. Colin Hong as the first pilot clinic without making this a one-off custom build.

Plan only. Do not build yet.
```
