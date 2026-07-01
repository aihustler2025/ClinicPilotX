# Request 055 - Workspace IA/UX D1 QA

Date: 2026-07-02

App: https://clinic-pilot-x.lovable.app

Lovable project: 8b4d9031-af8d-4faf-81d3-135c41ad73b7

## Scope

Workspace IA/UX cleanup after Site Import Assistant C1.

Primary product correction: make `Auto-Fill From Website` the first obvious Workspace action, reduce the double-left-navigation problem, and slim the main sidebar so daily work stays visible.

## Lovable Build Summary

Lovable reported D1 as frontend-only:

- `/workspace` first visible block changed to `Auto-Fill From Website`.
- Persistent Workspace secondary left rail replaced with horizontal section chips plus breadcrumb/prev-next on section pages.
- Main sidebar slimmed to daily work modules.
- Staff, Auto-Assignment, Subscription, Settings, and Profile moved to the header account menu.
- Direct routes preserved.
- No migrations, RLS, edge functions, inbox, crawler, AI extraction, sends, workflows, payments, or integrations touched.

## Publish Note

Initial QA showed the live published app still had the old Workspace.

Root cause: Lovable preview had the D1 changes, but the published `.lovable.app` URL still needed `Publish` -> `Update`.

Codex clicked `Publish`, then the blue `Update` button. The publish dialog then showed `Up to date`.

## Live QA Result

Result: Pass for tested D1 scope.

Verified on the live published app after update:

- `/workspace` loads behind authenticated session.
- First visible Workspace block is `Auto-Fill From Website`.
- The copy explains that ClinicPilotX can draft Business Profile, Hours, Services, and FAQs from the website, with human review before anything is published.
- Guardrail chips are visible:
  - `DRAFT ONLY`
  - `HUMAN REVIEW REQUIRED`
  - `NO SENDS`
  - `NO AUTOMATION`
- Existing site import draft status appears: `1 import run on this clinic`.
- `Open review queue` routes to `/workspace?section=knowledge-sources`.
- Setup checklist remains available as `Review & finish your setup`.
- Main sidebar now shows:
  - Workspace
  - Dashboard
  - Leads
  - Patients
  - Appointments
  - Communication Hub
  - Video Consultation
  - Payments & Billing
  - Analytics & Reporting
  - Automation Center
- Main sidebar no longer shows:
  - Staff Management
  - Auto-Assignment Rules
  - Subscription
  - Settings
  - Profile
- Header account menu opens from the avatar and contains:
  - Profile
  - Settings
  - Team & access
  - Billing & subscription
  - Logout
- Direct preserved routes still load:
  - `/staff`
  - `/auto-assignment`
  - `/subscription`
  - `/settings`
  - `/profile`
- Workspace deep link `/workspace?section=business-profile` loads the Business profile editor.
- Settings compatibility path `/settings?tab=clinic-workspace&section=business-hours` still loads Business Hours.

## Layout Verification

DOM inspection on `/workspace` showed:

- Main content uses a single-column `max-w-5xl mx-auto` Workspace layout.
- Workspace section navigation is a horizontal scrollable chip row:
  - class evidence included `overflow-x-auto` and `flex gap-2 pb-2 min-w-max`.
- No old persistent Workspace aside was present in the content area.
- The only detected `ASIDE` in the DOM was Lovable's `Edit with` overlay, not a ClinicPilotX navigation rail.

## Mobile QA Limitation

The current in-app browser control session did not expose a working viewport resize capability after the browser reconnection, so Codex did not honestly complete a real phone-width visual QA for D1.

Mobile behavior remains a follow-up check for the next browser session or a Lovable evidence request.

## Safety

Codex did not click `Create draft from website` during this D1 QA pass, so no new site import run or fact was intentionally created.

D1 was frontend IA/navigation only. No live sends, workflows, inbox connections, crawler, AI extraction, payments, calendar writes, or integrations were triggered by this QA.

## Remaining Follow-Ups

- Complete a real mobile-width QA pass for Workspace D1.
- Decide whether D2 should improve the Workspace section forms visually or whether to move next into Dr. Hong demo data population.
- Do not approve actual website crawling / AI extraction until a separate C2 plan is reviewed.
