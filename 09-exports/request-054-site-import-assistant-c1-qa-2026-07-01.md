# Request 054 - Site Import Assistant C1 QA

Date: 2026-07-01

## Scope

Website Enrichment / Site Import Assistant C1 was approved, built, published, polished, and QA-tested for the Dr. Colin Hong pilot workspace.

This phase is a safe foundation only. It does not crawl websites, call AI, connect OAuth, read inboxes, send messages, trigger workflows, or activate external providers.

## Visible QA

Path tested in Lovable preview:

`Workspace > Knowledge sources`

Verified:

- `Site Import Assistant` renders under Knowledge sources.
- Guardrail banner is visible: draft only, human review required, no chatbot/email/voice activation until approval.
- The automated button is disabled and now uses the plain-English label `Auto-Fill From Website`.
- The disabled automated button explains that automatic website scanning is coming in a later phase.
- Public-pages-only checkbox is checked and disabled for the future crawler phase.
- Entering `https://www.drcolinhong.com` enables `Create draft run`.
- Creating a draft run works and shows a success toast.
- Adding a manual draft fact works and shows the fact in the review queue.
- Setup completion displays `0 approved / 1 facts`.
- Rejecting the QA fact works; the fact becomes `rejected` and its input becomes disabled.

QA test fact:

`QA TEST Site Import Clinic Name 20260701`

The test fact was rejected, not approved.

## Lovable Evidence

Lovable reported:

- Typecheck clean.
- Initial C1 migration applied.
- UI wired into `Workspace > Knowledge sources`.
- No edge functions, OAuth, external calls, crawler, AI Gateway, sends, workflow triggers, or inbox code were introduced.

Polish fix changed:

- `src/components/settings/clinic/site-import/EnrichmentWizard.tsx`

The disabled automated button label changed from `Run import` to:

`Auto-Fill From Website`

## SQL Evidence From Lovable

QA run:

- `id = 174911db-b4fc-4d0f-a20f-c1a23411993c`
- `clinic_id = 8ed615bf-afd3-4986-86a8-fecec8887db3`
- clinic: `Dr. Colin Hong (Pilot)`
- `root_url = https://www.drcolinhong.com`
- `status = manual_paste`
- `created_at = 2026-07-01 15:06:46Z`

QA fact:

- `id = c656f5c6-8d23-4683-9d0c-7bed7e505f9d`
- `category = profile`
- `field_key = name`
- `value = "QA TEST Site Import Clinic Name 20260701"`
- `status = rejected`
- `applied_to_target = NULL`
- `applied_row_id = NULL`

Clinic name remained unchanged:

`Dr. Colin Hong (Pilot)`

Lovable reported the clinic row `updated_at` predates the QA run, confirming the rejected fact did not modify `clinics.name`.

## Guard Evidence

Lovable reported:

- Same-clinic FK rejected a cross-clinic fact insert with `foreign_key_violation`.
- `site_enrichment_facts_source_same_clinic` uses default `NO ACTION` behavior for source deletion.
- Terminal guard trigger exists:
  - `trg_site_enrichment_facts_terminal_guard`
  - function: `prevent_site_enrichment_fact_terminal_reopen()`
- Terminal guard blocks status changes out of approved/rejected and blocks mutation of approval/apply columns on approved rows.

## Side-Effect Counts

Lovable reported zero rows created during the QA window for:

- `workflow_executions`
- `automation_logs`
- `email_delivery_logs`
- `reminders`
- `scheduled_messages`
- `messages`
- `scheduled_confirmations`
- `call_logs`
- `email_intake`
- leads created from the enrichment path

## Result

Request 054 passes for the safe C1 foundation.

The Site Import Assistant is now ready for manual, owner/admin-reviewed draft knowledge capture.

## Still Not Approved

The following remain parked and require a separate plan/build approval:

- Real website crawling.
- AI extraction from website content.
- Firecrawl or any external crawler provider.
- Lovable AI Gateway/Gemini extraction.
- Real inbox/Gmail/OAuth connection.
- Gmail label writing.
- Automatic lead creation from email or website import.
- Chatbot/voice/email use of imported facts before owner/admin approval.

## Next Recommended Step

Plan C2 carefully:

- Server-side public website scan for approved clinic URLs only.
- Strict public-pages-only behavior.
- Clear crawl limits and robots/legal review.
- AI-generated facts remain `needs_review`.
- No automatic application to workspace fields.
- No chatbot/email/voice use until clinic owner/admin approval.

