# Codex-to-Dashboard-Lovable-003: Project, Backend, Marketing Site, and Lovable Cloud Clarification

Date: 2026-06-05

## Purpose

Before Ross approves new ClinicPilotX build work, please clarify the exact Lovable project structure, backend setup, hosting setup, Supabase connection, GitHub connection, and marketing website relationship.

ClinicPilotX appears to include:

1. A main CRM/dashboard app.
2. A partially built marketing website that may be in a separate Lovable project.

Do not merge, rebuild, or restructure anything yet. This is an audit/intake request only.

## Known Current Details

Known dashboard app:

`https://clinic-pilot-x.lovable.app`

Known Lovable dashboard project ID:

`8b4d9031-af8d-4faf-81d3-135c41ad73b7`

Known Supabase project ref found from deployed app evidence:

`imuyfbvsombbpgdgkhrb`

Official GitHub repo for project memory/documentation:

`https://github.com/aihustler2025/ClinicPilotX`

Ross has a Lovable package that includes Lovable Cloud/back-end/hosting benefits. We want to use the existing Lovable/Lovable Cloud/Supabase value before considering any unrelated paid backend or hosting options.

## Questions To Answer

### Main CRM/Dashboard Project

1. Confirm the exact Lovable project ID for the main ClinicPilotX CRM/dashboard.
2. Confirm the exact live URL and preview URL for the main CRM/dashboard.
3. Confirm whether this project is currently connected to GitHub. If yes, provide the repo URL and branch.
4. Confirm whether this project is using Lovable Cloud, standalone Supabase, or both.
5. Confirm whether Supabase project `imuyfbvsombbpgdgkhrb` is the intended production backend for the dashboard.
6. Confirm what Lovable Cloud backend/hosting benefits are active for this project.
7. Confirm where integration secrets currently live: Lovable secrets, Supabase secrets, both, or neither.
8. Confirm whether current backend functions are Lovable-managed, Supabase Edge Functions, or another mechanism.

### Marketing Website Project

1. Confirm whether the partially built ClinicPilotX marketing website is a separate Lovable project.
2. If separate, provide the Lovable project ID.
3. Provide the marketing website URL or preview URL.
4. Confirm whether it has its own backend/Supabase connection.
5. Confirm whether it is connected to GitHub. If yes, provide the repo URL and branch.
6. Confirm whether it should eventually be merged into the dashboard project, linked as a separate app/site, or deployed as a separate marketing domain/subdomain.
7. Identify any risks or blockers for coordinating the marketing website with the dashboard app.

### Automation and Backend Direction

1. Confirm which current Automation Center workflows are implemented in the app/backend today.
2. Confirm which workflows are only UI/mock/demo.
3. Confirm whether app-native automation should run through Lovable Cloud/Supabase for production.
4. Confirm whether n8n is currently connected anywhere in the live dashboard project.
5. Confirm whether any current workflow actions can trigger real email, SMS, payment links, VAPI calls, WhatsApp, Messenger, or other paid/live integrations.
6. Identify all places where sandbox/live credential status must be checked before Codex performs testing.

### Known Issues To Address Later

Please confirm the correct backend fix plan for these verified issues:

1. `Auto-Assignment Rules` references `assignment_rules`, but the backend returns a missing table/schema cache error.
2. Subscription state can appear inconsistent as `Professional` versus `No Plan` in the same logged-in session.
3. `Video Consultation` and the main `Profile` route are currently coming soon.

## Response Format Requested

Please answer with:

- Dashboard project details.
- Marketing website project details.
- Backend/Supabase/Lovable Cloud details.
- GitHub connection details.
- Hosting/deployment details.
- Automation Center implementation status.
- Paid/live integration safety notes.
- Recommended next audit steps before build mode.
