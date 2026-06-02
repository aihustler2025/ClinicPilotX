# Codex-to-Dashboard-Lovable-001: Official ClinicPilotX Project Audit Intake

Date: 2026-06-02
Project: ClinicPilotX
From: Codex
To: Lovable
Mode: Plan
Purpose: Audit/intake only. Do not build yet.

## Context

We are starting the official ClinicPilotX project-management, QA, and launch-prep process.

ClinicPilotX is a Buzzooka product for clinics, plastic surgery practices, dental clinics, med spas, beauty/wellness businesses, salons, and other appointment-based/service businesses.

Important: there is an older GitHub repo named `aihustler2025/clinicpilot-x` and older local material from May 2026. That repo/folder is from the wrong/older project workflow and must not be treated as the current source of truth for this audit.

For this official project, please audit the current Lovable project that this chat belongs to. Do not import assumptions from any old repo, old Markdown docs, old handoffs, or old ClinicPilot/ClinicPilot X project history unless we explicitly provide a specific source file later.

## Strict Instruction

Please do not make code, database, auth, deployment, integration, billing, or configuration changes in response to this message. This is an intake request only.

## Please Reply With The Current Project Facts

Please answer each item clearly and specifically. If you do not know something, say `Unknown` rather than guessing.

1. What is the current Lovable project name?
2. What is the current Lovable project ID?
3. What are the current preview URLs and public URLs, if any?
4. Does this Lovable project contain the dashboard, admin panel, user/staff portal, marketing website, or all of these?
5. Which backend is connected: Supabase, Lovable Cloud, standalone Supabase, or something else?
6. If Supabase is connected, what is the Supabase project ref/name, if available?
7. What database tables currently exist, and what is each table used for?
8. What auth/login setup is currently implemented?
9. What roles or permission levels currently exist?
10. What modules, pages, and routes currently exist?
11. Which modules/pages use real backend data?
12. Which modules/pages still use mock, placeholder, seeded, or demo data?
13. What integrations are currently implemented, partially implemented, or planned? Include email, Gmail/Outlook, Google Calendar, Calendly, Stripe, Twilio, VAPI, n8n, chatbot, WhatsApp, Messenger, Meta/Facebook, OpenAI, and any others.
14. What automations are already built?
15. What automations are planned but not built?
16. What known bugs, warnings, broken flows, console errors, or incomplete features exist right now?
17. Is this Lovable project connected to GitHub?
18. If it is connected to GitHub, what is the repository URL, branch, and sync status?
19. If this project is connected to `aihustler2025/clinicpilot-x`, please say so clearly. Do not assume that repo should remain the official repo.
20. Has the project been published yet?
21. If it has been published, what deployment/public URL is live?
22. What should Codex verify first before approving any new build work?

## Response Format Requested

Please structure your response under these headings:

- Project Identity
- URLs and Publishing
- App Scope
- Backend and Database
- Auth and Roles
- Pages, Routes, and Modules
- Real Data vs Mock Data
- Integrations
- Automations
- Known Issues and Incomplete Features
- GitHub Connection
- Recommended First Verification Steps

## Important Constraints

- Do not build or change anything yet.
- Do not activate paid integrations.
- Do not connect new external services.
- Do not start with the marketing website.
- Product/dashboard functionality should be audited first.
- Be explicit about uncertainty. Codex will verify claims before approving future build work.
