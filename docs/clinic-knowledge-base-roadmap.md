# ClinicPilotX Clinic Knowledge Base Roadmap

Last updated: 2026-06-25

## Purpose

Each ClinicPilotX subscriber should eventually have a clean, per-clinic Knowledge Base that stores the business facts AI workflows can safely use.

This is not part of the current Phase 1B.1 active-clinic build. It is parked here so the product direction is not lost.

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

Recommended sections:

- Overview
- Website Sources
- Uploaded Files
- Services & Pricing
- FAQs
- Business Hours
- Policies
- Provider Bios
- Brand Voice
- AI Guardrails
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

Avoid copying any competitor's exact design. Use ClinicPilotX's own visual system and keep it consistent with the current clean dashboard style.

## Reference Screenshots From Ross

Ross shared screenshots on 2026-06-25 from an ElevenLabs Knowledge Base workflow as a general product reference, not as a design to copy.

Local screenshot references:

- `C:\Users\user\OneDrive\Pictures\Screenshots\Screenshot 2026-06-25 123031.png`
- `C:\Users\user\OneDrive\Pictures\Screenshots\Screenshot 2026-06-25 123009.png`
- `C:\Users\user\OneDrive\Pictures\Screenshots\Screenshot 2026-06-25 123108.png`
- `C:\Users\user\OneDrive\Pictures\Screenshots\Screenshot 2026-06-25 123048.png`

Useful ideas to remember later:

- top-level source actions such as Add URL, Add Files, Create Text, and Create Folder,
- drag-and-drop upload modal,
- parent folder selection,
- accepted file-type chips,
- source list with search and filters,
- document preview panel,
- source metadata such as sharing status, document ID, created date, last updated date, size, index status, and dependent agents/workflows,
- update source, download/source file, and edit actions.

Important: use these only as inspiration for product planning. Do not copy the exact ElevenLabs layout, wording, visual hierarchy, or styling.

## AI Safety Requirements

Knowledge Base content should support medical/cosmetic clinic workflows, but AI must stay cautious:

- AI should not diagnose.
- AI should not guarantee outcomes.
- AI should not quote prices as final unless the clinic marks them as approved/fixed.
- AI should escalate urgent or medical-risk messages.
- AI should identify uncertainty and route to staff.
- AI should cite or link the source internally for staff review where possible.

## Future Lovable Prompt Draft

Use this later, not during the current Phase 1B.1 work:

```text
Please plan a ClinicPilotX per-clinic Knowledge Base module in Plan mode only.

The Knowledge Base should let each subscriber/clinic upload and manage business facts that AI workflows can safely use. It should support website URLs, service-page URLs, sitemap URLs, manual text, PDFs, DOCX, TXT/Markdown, FAQs, services/pricing, hours, policies, provider bios, brand voice, and AI guardrails.

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

Plan only. Do not build yet.
```
