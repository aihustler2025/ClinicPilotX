# Request 037 - Clinic Workspace Phase A QA

Date: 2026-06-27

## Scope

Ross approved and published Lovable's Clinic Workspace Phase A build.

Lovable reported:

- Typecheck is clean.
- Migration is in.
- RLS was replaced as planned.
- Settings now has a gated Clinic Workspace tab.
- Clinic Workspace sub-nav includes Overview, Business Profile, Branding, Business Hours, Services & Pricing, Team & Roles, Knowledge FAQs, Knowledge Sources, AI Guardrails, and Integrations Status.
- Sections are deep-linkable by `?tab=clinic-workspace&section=...`.
- Editing is restricted to clinic owner/admin or platform admin.

Codex performed live browser QA against:

`https://clinic-pilot-x.lovable.app`

## Result

Pass with follow-up polish required.

Clinic Workspace Phase A is present under Settings, not the main left nav, and the tested editable sections persist after reload.

Do not move to live email inbox connection yet. Next should be a small follow-up for the issues below, then test-inbox email AI sorting planning.

## Verified

### Placement / Navigation

Passed.

- Main left nav was not cluttered with a Knowledge Base item.
- Settings includes a `Clinic Workspace` tab.
- Clinic Workspace sub-nav appears:
  - Overview
  - Business Profile
  - Branding
  - Business Hours
  - Services & Pricing
  - Team & Roles
  - Knowledge: FAQs
  - Knowledge: Sources
  - AI Guardrails
  - Integrations Status
- Direct links using `?tab=clinic-workspace&section=...` load the expected section.

### Business Profile

Passed.

Codex saved QA values:

- Legal Name: `Dr. Colin Hong Plastic Surgery QA`
- Tagline: `QA TEST Workspace Setup 20260627`
- Description: `QA test description entered by Codex on 2026-06-27 to verify Clinic Workspace persistence.`
- Country: `Canada`
- Region: `Ontario`
- Postal Code: `QA-20260627`

Toast shown:

- `Business profile saved`

After reload, the values persisted.

Note: Ross should later replace the QA values with real Dr. Hong clinic data.

### Services & Pricing

Passed.

Existing services loaded, including seeded services such as Botox, Dermal Fillers, Laser Hair Removal, Rhinoplasty Consultation, and Skin Care Consultation.

Codex added:

- Service: `QA TEST Service 20260627`
- Category: `QA`
- Duration: `30`
- Price: `250`
- Currency: `CAD`

Toast shown:

- `Service added`

After reload, the QA service persisted.

### Knowledge FAQs

Passed.

Codex added:

- Question: `QA TEST FAQ 20260627`
- Category: `QA`
- Answer: `QA test answer for Clinic Workspace persistence.`

Toast shown:

- `FAQ added`

After reload, the QA FAQ persisted as editable fields.

### Knowledge Sources

Passed for Phase A placeholder scope.

The page shows:

- `Knowledge Base - Sources`
- `Coming in Phase B`
- copy explaining uploads, URLs, chunking, embeddings, and indexing will come later.

No upload/source ingestion was tested because it is intentionally out of Phase A.

### AI Guardrails

Passed.

Codex saved:

- Tone: `Friendly, cautious, staff-escalating. QA 20260627`
- Forbidden topics: `diagnosis, guaranteed outcomes, emergency medical advice`
- Escalation email: `qa-escalation@example.com`
- Escalation phone: `+1 (416) 555-0199`
- Required disclaimers, escalation rules, after-hours message, and PII handling notes.

Toast shown:

- `AI guardrails saved`

After reload, values persisted.

### Team & Roles

Passed read-only check.

Displayed:

- `teambuzzooka@gmail.com` as `owner`
- `kizha.buzzooka@gmail.com` as `admin`

The section says invite and role management live in Team Management.

### Integrations Status

Rendered.

Displayed:

- Google Calendar - Configured
- Stripe - Not configured
- Email notifications - Configured
- SMS notifications - Configured
- Call notifications - Configured

This needs wording review before client demo, because "Configured" may be confused with "live/verified/connected".

### Overview

Mostly passed.

After saved data loaded, the setup checklist showed:

- `4 of 6 steps complete`

Completed checks included business profile, business hours, service/pricing, FAQ, and AI guardrails state.

Minor issue:

- On one navigation, Overview briefly showed `0 of 6 steps complete` before correcting to `4 of 6` after the workspace data finished loading.
- This should show a loading skeleton or "Checking setup..." instead of a false zero state.

### Smoke Routes

Passed:

- Dashboard
- Leads
- Patients
- Appointments
- Communication Hub at `/communication-hub`
- Settings / Clinic Workspace

Note:

- `/communication` returns 404, but the real route is `/communication-hub`.

### Workflow / External Side Effects

No live sends were triggered by Codex.

Codex did not click:

- send email,
- send SMS,
- calendar connection/write,
- payment link,
- Stripe,
- workflow test-send,
- chatbot/API intake,
- file upload,
- live integration buttons.

Automation Center still showed no visible "just now" / "minutes ago" workflow activity during the workspace QA pass.

Browser console error check:

- No console errors appeared from the Clinic Workspace sections themselves.
- One 404 console error was caused by Codex intentionally checking the wrong route `/communication`; corrected route `/communication-hub` works.

## Issues / Follow-Up

### 1. Services row actions need accessible labels and safer delete UX

Existing service rows use an icon-only trash button with no visible label/tooltip/aria label.

Codex initially clicked an existing service row action while testing and got:

- `Deleted`

The QA service was removed after reload, confirming the button performs delete.

The blank row uses a plus icon and successfully adds services.

Fix requested:

- Add accessible labels/tooltips:
  - `Delete service`
  - `Add service`
- Add a confirmation dialog before deleting an existing service.
- If soft delete/archive exists, prefer archive/inactive over hard delete for real services.

### 2. Overview checklist should not flash false `0 of 6`

The Overview checklist briefly displayed `0 of 6 steps complete` before correcting to `4 of 6`.

Fix requested:

- Show a loading skeleton or `Checking setup...` until workspace metadata, services, FAQs, hours, and guardrails are loaded.

### 3. Integrations Status wording needs safer states

The section currently shows several items as `Configured`.

For a client demo, this should be clearer:

- `Connected and verified`
- `Configured, not tested`
- `Not connected`
- `Coming later`

Do not imply live Google Calendar, SMS, call, or email readiness unless a connection has actually been verified.

### 4. Subscription display remains inconsistent

Header / Automation Center still showed:

- `No Plan`
- `7 / 5 Active`

This is not caused by Clinic Workspace Phase A, but it remains important before plan-gated features are trusted.

### 5. Need Lovable SQL evidence for Phase A rows

Codex verified UI persistence, but still cannot independently run authenticated SQL in the browser.

Need Lovable to provide SQL evidence for:

- pilot clinic row updated values,
- QA service row and `clinic_id`,
- QA FAQ row and `clinic_id`,
- AI guardrails row and `clinic_id`,
- row counts for workflow/send-capable tables remaining unchanged during QA.

## Human QA Script

Created:

`docs/qa/clinic-workspace-phase-a-human-qa-script.md`

## Recommended Next Step

Send a small Lovable follow-up before starting the test inbox email AI build:

`docs/handoffs/Lovable-paste-message-037-clinic-workspace-phase-a-qa-followup.md`

After that:

1. Fill real Dr. Hong business profile / services / FAQs / guardrails.
2. Plan the test-inbox email AI sorting demo.
3. Do not connect Dr. Hong's real inbox until a test inbox workflow is proven safe.
