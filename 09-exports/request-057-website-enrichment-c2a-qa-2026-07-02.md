# Request 057 - Website Enrichment C2a QA

Date: 2026-07-02
App: https://clinic-pilot-x.lovable.app
Lovable project: 8b4d9031-af8d-4faf-81d3-135c41ad73b7
Pilot clinic: Dr. Colin Hong (Pilot)

## Scope

Lovable implemented Website Enrichment C2a plus Branding/logo upload.

Reported implementation:

- Added crawl/AI metadata columns to site enrichment tables.
- Added `clinics.logo_path`, `clinics.logo_updated_at`, and `clinics.enrichment_ai_enabled`.
- Created private `clinic-branding` storage bucket with clinic-scoped RLS.
- Added `supabase/functions/site-enrichment-scan/index.ts`.
- The scanner is bounded to 15 pages, depth 3, 8 seconds per page, and 55 seconds wall clock.
- Scanner uses same-host `www`/apex normalization, honors robots.txt, skips login/portal/checkout paths, and stores no full HTML, only capped cleaned summaries.
- Rule extraction is always available; AI extraction is optional and gated by clinic setting.
- Branding form now has PNG/JPG/WEBP logo upload, rejects SVG, and suggests colors from raster preview without auto-saving.

## Codex QA Performed

### Publish

Codex published the Lovable build using `Publish` -> `Update`.

### Workspace smoke

Result: Pass.

Verified live:

- `/workspace` loads for the authenticated pilot clinic.
- Main sidebar and dedicated Workspace left rail are both present.
- `Auto-Fill From Website` remains the first Workspace Home block.
- Guardrails are visible: draft only, human review required, no sends, no automation.
- Workspace left rail includes Home, Business profile, Branding & logo, Hours of operation, Services & pricing, Team & roles, Knowledge FAQs, Knowledge sources, AI guardrails, Integrations status, and Email inbox.

### Real website scan

Test URL:

`https://www.drcolinhong.com`

Result: Pass for first C2a pilot scan.

Observed flow:

- Entering the URL enabled the scan action.
- Clicking `Scan website` changed the button to `Scanning website...`.
- Scan completed and navigated to `Workspace > Knowledge sources`.
- Import run appeared for `https://www.drcolinhong.com`.
- Run showed `15%` completeness and `15p` pages.
- Draft facts appeared with source URLs, snippets, confidence, extractor, and review actions.
- Facts remained review-gated and were not automatically approved or applied.

Extracted draft facts observed:

- `profile.name` via rule extractor, 50% confidence, needs review.
- `profile.phone` via rule extractor, 60% confidence, needs review.
- `profile.email` via rule extractor, 60% confidence, needs review.
- `social.social_facebook` via rule extractor, 80% confidence, needs review.
- `social.social_youtube` via rule extractor, 80% confidence, needs review.
- `social.social_instagram` via rule extractor, 80% confidence, needs review.
- `social.social_linkedin` via rule extractor, 80% confidence, needs review.

Safety observed:

- No facts were approved during QA.
- No lead was created from the scan.
- No email, SMS, call, calendar, payment, chatbot, or workflow action was triggered from the UI flow.
- Review actions remained manual: Approve, Reject, Delete draft.
- AI extraction was presented as optional with cost/credit warning; it was not enabled during this QA pass.

### Branding/logo UI

Result: Pass for visible UI scope.

Verified live at `Workspace > Branding & logo`:

- `Clinic logo` upload area exists.
- Copy says PNG, JPG, or WEBP only, up to 2 MB.
- Copy explicitly says SVG uploads are not accepted.
- Logo is described as stored privately per clinic.
- Primary Color, Secondary Color, Currency, and Brand Voice fields remain present.
- Save action remains present.

No real logo file was uploaded during this pass.

### Console

Result: Pass after reload.

Initial browser logs contained stale Lovable preview/HMR errors from the build environment. After reloading the live app and waiting for clinic context, no recent live console errors were observed.

## Notes / Minor Polish

- The import run label showed `reviewed` while extracted facts were still `needs_review`. The safety model still behaved correctly, but the label may confuse users. Suggested future polish: use `Awaiting review` or similar when a run has pending draft facts.
- The first `profile.name` fact appears to come from `og:site_name / <title>` and should be reviewed by a human before approval.
- C2a implemented a stricter 15-page single-function scan instead of the earlier 40-page multi-function plan. This is acceptable for pilot safety and speed.

## Current Status

Website Enrichment C2a is live and passed first functional QA for a public Dr. Hong website scan.

Next recommended step:

- Review the extracted facts with Ross/assistant and approve/reject them manually.
- Then continue with Email Inbox / Email AI Sorting Phase A/B safe demo work.
- Do not connect a real inbox, enable AI extraction, approve facts into chatbot/email/voice use, or activate automations until separately approved.
