# Request 058 Website Enrichment C2b QA - 2026-07-02

## Scope

Website Enrichment C2b deepened `Auto-Fill From Website` beyond the C2a 15-page first pass.

Tested live app:

`https://clinic-pilot-x.lovable.app/workspace?section=enrichment-review`

Pilot clinic:

`Dr. Colin Hong (Pilot)`

Public site scanned:

`https://www.drcolinhong.com`

## What Lovable Built

- Sitemap-first same-site public crawl.
- Sliced crawl processing with resume support.
- Review Center with category rail and source/origin badges.
- Fact version history support.
- Missing-materials checklist for later assistant accuracy.
- Draft AI guardrails surface separate from live guardrails.
- Cancel/stale-run/error visibility for enrichment runs.
- Conservative extraction categories so article/knowledge pages are not treated as confirmed services.

## QA Path

1. Published Lovable C2b build to the live `.lovable.app` site.
2. Loaded `/workspace` and confirmed the preferred two-left-panel Workspace layout remained intact.
3. Confirmed `Auto-Fill From Website` stayed as the first Workspace Home block.
4. Opened `Site enrichment review`.
5. Started a safe public-site scan for `https://www.drcolinhong.com`.
6. Verified the first C2b run exposed a crawl-resume bug: it stalled at `crawling`, `20 pages`, `sitemap.xml`.
7. Sent Lovable a focused fix request for sliced crawl resume/status handling.
8. Published the fix and re-QA'd.
9. Verified the resumed run reached `awaiting_review`, `120 pages`, `4508 URLs discovered`, `slice 6`.
10. Found extraction-quality issue: `/learn/` and `/uncategorized/` article URLs were being emitted as service facts.
11. Sent Lovable a focused category/extraction fix request.
12. Published the fix and re-QA'd.
13. Found a regression: fresh scan stopped at `1 page`, `1 URL discovered`, `0% complete`, with no facts.
14. Sent Lovable a focused discovery-regression fix request.
15. Published the final fix and re-QA'd the live Review Center.

## Final Verified Live Result

Latest live Review Center after final publish:

- Run status: `awaiting_review`.
- Completeness: `35% complete`.
- Pages fetched: `120 pages`.
- URLs discovered: `4546 URLs discovered`.
- Slice count: `slice 6`.
- Source discovery: `sitemap.xml`.
- Visible draft categories:
  - Profile: `7 draft`.
  - Hours: `5 draft`.
  - Social: `4 draft`.
  - Services: `0 draft` after conservative pollution fix.
- Latest scan detected page categories: `faq`, `team`, `other`, `contact`, `pricing`, `knowledge`.

Verified draft facts remain `needs_review` and show:

- origin badge: `FOUND ON CLINIC WEBSITE`,
- target category such as `PROFILE` or `HOURS`,
- extractor type `RULE`,
- confidence,
- target table hint,
- source URL,
- snippet,
- `Approve`, `Reject`, `Delete draft`, and `Version history` actions.

## Extracted Draft Examples

Profile facts visible from the homepage:

- `name`.
- `phone`.
- `email`.
- `address_line1`.
- `city`.
- `region`.
- `postal_code`.

Hours facts visible from the homepage:

- `mon`.
- `tue`.
- `wed`.
- `thu`.
- `fri`.

The visible source snippet includes the public website text containing:

`Phone:(416) 222-6986 Mon-Fri (10am - 6pm) info@drcolinhong.com 302 Sheppard Ave W, North York, ON M2N 1N5`

## Fixes Requested During QA

### Crawl Resume Fix

Problem:

- The first published C2b scan stalled at `crawling`, `20 pages`, and did not resume.

Lovable fix evidence:

- The stuck run had `pages_fetched=20`, `slice_count=1`, and a large remaining queue.
- After fix/resume, it completed to the configured 120-page cap with `slice_count=6`.
- Review Center now surfaces stale/failure/cancel information.

### Extraction Quality Fix

Problem:

- `/learn/` and `/uncategorized/` article URLs were being emitted as service facts.

Lovable fix evidence:

- Knowledge/article paths are no longer emitted as service facts.
- Homepage contact/hours/address extraction was added.

### Discovery Regression Fix

Problem:

- After extraction-quality fix, a fresh scan returned only `1 page`, `1 URL`, `0% complete`, and no facts.

Lovable root cause:

- Sitemap child URLs were being fetched with mixed `http`/`www` forms and a too-low sitemap file cap.
- A challenge-like homepage response could be treated as a completed page.

Lovable fix evidence:

- Discovery now normalizes same-site sitemap URLs back to requested host/protocol.
- Sitemap traversal capacity was raised.
- Queueing is independent from category rules.
- Challenge-like page responses are retried with a browser-style user agent.
- Fresh scan reached `120 pages`, `4546 URLs`, and `slice 6`.

## Safety Verification

Lovable reported zero side-effect rows after the final scan in:

- workflow executions,
- email delivery logs,
- scheduled messages,
- scheduled confirmations,
- leads,
- payments,
- appointments,
- messages.

Codex visible QA also confirmed:

- no facts were automatically approved,
- no facts were automatically applied to live clinic profile/services/hours,
- no leads were created through the visible flow,
- no sends/workflows/automations were triggered through the visible flow,
- no real inbox, OAuth, chatbot grounding, embeddings, SMS/calls, payments, or calendar writes were connected.

## Result

Pass for C2b safe website-enrichment infrastructure after follow-up fixes.

C2b is now good enough for Ross/assistant to review website-sourced draft facts manually. It is not yet a complete service/pricing/FAQ knowledge-base importer.

## Remaining Limitations / Next Work

- Services are now conservative and show `0 draft` rather than polluted article-derived service facts. Next pass should identify true service/procedure pages without treating education/blog articles as services.
- Pricing facts remain `0 draft`; if pricing is hidden or separate, Ross/assistant must provide pricing source material or URLs.
- FAQ facts remain `0 draft`; future phase should generate FAQ candidates only with clear source/origin labels and human approval.
- Team/provider facts remain `0 draft`; future phase should map provider/team website pages separately from app staff accounts.
- Contact and Locations category counts remain `0` even though address fields appear under Profile. Future polish can route address facts into a clearer Locations review target if desired.
- Do not enable optional AI extraction, external research, chatbot/email/voice grounding, real inbox ingestion, or automated fact approval without a separate reviewed plan.
