# ClinicPilotX Project Takeover Operating Model

Date: 2026-06-11

## Purpose

This document defines how Codex should manage ClinicPilotX going forward.

ClinicPilotX is not a blank n8n project. It is an existing Lovable-built product that is already partially complete and must be audited, stabilized, documented, and extended carefully.

Codex's role is project manager, technical auditor, documentation keeper, QA lead, and automation architect. Lovable is the primary build partner for the app. GitHub is the project memory and source of truth.

## Ross's Work System

Ross works across multiple devices:

- Office PC.
- Travel laptop.
- Future/other Codex sessions.

The project must be able to resume from any device or thread by reading the GitHub repo.

GitHub is the brain:

- `AGENTS.md`: rules for Codex and future AI agents.
- `STATUS.md`: current state and where work left off.
- `TASKS.md`: master task list and roadmap.
- `PRODUCT_SPEC.md`: verified product behavior, modules, workflows, and architecture.
- `DECISIONS.md`: durable decisions and rationale.
- `CHANGELOG.md`: history of changes.
- `docs/handoffs/`: structured messages to/from Lovable and future Codex sessions.
- `09-exports/`: QA reports, workflow inventories, test plans, and export-ready documentation.

Google Drive/cloud storage should hold large raw client assets, images, videos, approvals, exports, and deliverables. GitHub should hold text/code/project memory, not heavy asset libraries.

## Source Of Truth

Official GitHub repo:

`https://github.com/aihustler2025/ClinicPilotX`

Laptop local clone:

`C:\Users\user\Documents\ClinicPilotX`

PC mirror referenced by earlier handoffs:

`D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`

Important: do not confuse this with older/wrong ClinicPilot folders or repos unless Ross explicitly asks for old-reference recovery.

## Known Product Context

ClinicPilotX is the mothership product for clinic operations and growth automation. It includes:

- Main CRM/dashboard.
- Lead management.
- Patient management.
- Appointment management.
- Communication Hub.
- Automation Center.
- Payments and billing.
- Analytics and reporting.
- Staff management.
- Subscription/add-ons.
- Settings/integrations.
- Future chatbot.
- Future mobile app.
- Future external API.
- Separate or partially built marketing website that may need to coordinate with the dashboard.

The future chatbot, mobile app, and APIs should connect back into ClinicPilotX rather than becoming isolated products. Leads and interactions from those channels should be stored in the central CRM/backend.

## Current Known App Details

Dashboard app:

`https://clinic-pilot-x.lovable.app`

Lovable project ID:

`8b4d9031-af8d-4faf-81d3-135c41ad73b7`

Known Supabase project ref:

`imuyfbvsombbpgdgkhrb`

Current evidence points to standalone Supabase for database/auth/API plus Lovable-managed deployment/secrets. Lovable must still confirm the exact Lovable Cloud/Supabase relationship.

## Current Known Dashboard Modules

Existing modules to audit and manage:

- Dashboard.
- Leads.
- Patients.
- Appointments.
- Communication Hub.
- Video Consultation.
- Payments & Billing.
- Analytics & Reporting.
- Staff Management.
- Automation Center.
- Auto-Assignment Rules.
- Subscription.
- Settings.
- Profile.

Known verified issues:

- Auto-Assignment Rules references `assignment_rules`, but the table is missing or unavailable in Supabase schema cache.
- Internal chat tables have an RLS recursion error.
- Subscription display can be inconsistent between `Professional` and `No Plan`.
- Video Consultation appears incomplete / coming soon.
- Main Profile route appears incomplete / coming soon.
- Some operational Supabase tables may be too publicly readable through anon access.
- Automation testing is high-risk until live vs sandbox credentials are confirmed.

## Automation Direction

Automation must be audited in this order:

1. Understand current Lovable/Supabase Automation Center.
2. Confirm which workflows are real, mocked, configured, enabled, and logged.
3. Confirm credential/secrets/sandbox status.
4. Map old n8n workflows as reference blueprints only.
5. Decide workflow-by-workflow whether production belongs in Lovable/Supabase, n8n, or both.

Local n8n is installed on the laptop for review/testing/import only:

- Container: `clinicpilotx-n8n`
- Local URL: `http://localhost:5678`
- Persistent volume: `clinicpilotx_n8n_data`

Local n8n must not become production infrastructure for client-facing ClinicPilotX workflows.

## Known Automation Center Rows

Known rows from prior audit:

- Lead Scoring & Assignment.
- Multi-Channel Sync.
- Lead Acknowledgment.
- WhatsApp Business Integration.
- AI Voice Agent - Inbound.
- Facebook Messenger Bot.
- Advanced Lead Nurture AI.
- Smart Follow-up Sequence.
- AI Voice Agent - Outbound.
- Follow-up After Visit.
- Follow-Up Sequences.
- No-Show Recovery.
- Payment Receipt.
- Payment Reminder Sequence.
- Appointment Confirmation.
- Appointment Reminders.
- Predictive Booking Suggestions.
- Daily AI Briefing.
- Weekly Performance Report.

These must be verified in the live dashboard before any build decisions.

## Lovable Coordination Rules

Ross communicates with Lovable manually unless a direct connector can perform a safe read-only project check.

Codex should:

1. Audit and decide what needs to be asked.
2. Create a precise Lovable prompt in `docs/handoffs/` when long.
3. Give Ross the exact short message to paste into Lovable.
4. Review Lovable's response.
5. Verify claims through app behavior, database evidence, code, screenshots, or logs.
6. Only then approve build work.

Do not approve new Lovable build work until the current dashboard/backend/project structure is audited.

## Required Live Audit Plan

Codex must perform or coordinate a click-by-click authenticated audit:

1. Dashboard metrics and data source.
2. Leads CRUD, filters, export, scoring, assignment, conversion to patient.
3. Patients CRUD, record model, appointment linkage.
4. Appointments create/edit/status/calendar/reminder/payment request.
5. Communication Hub external inbox, quick responses, AI suggestions, internal chat.
6. Payments and billing records, invoice/payment link flow, Stripe safety.
7. Analytics and reporting visual quality/export accuracy.
8. Staff management roles and permissions.
9. Automation Center workflow configs, enabled status, logs, and safe-testing protocol.
10. Auto-Assignment Rules backend fix.
11. Subscription state and entitlements.
12. Settings integrations, email logs, audit logs, profile/signature behavior.

If browser control is not available, Codex should ask Ross for screenshots or a controllable browser session instead of guessing.

## Working Session Protocol

At the start of a session:

1. Pull/read the official GitHub repo.
2. Read `AGENTS.md`, `STATUS.md`, `TASKS.md`, `PRODUCT_SPEC.md`, and this operating model.
3. Check the current Lovable app/project state.
4. Continue from the highest-priority open task.

During work:

1. Prefer audit and verification before build requests.
2. Keep changes small and documented.
3. Do not use paid services or live credentials without Ross approval.
4. Preserve credential safety.
5. Treat old folders/repos as reference-only unless explicitly approved.

Before ending a session:

1. Update `STATUS.md`.
2. Update `TASKS.md`.
3. Update `PRODUCT_SPEC.md` if behavior was verified.
4. Update `CHANGELOG.md` for meaningful changes.
5. Commit and push to GitHub.
6. Tell Ross exactly what was done and what is next.

## Immediate Next Steps

1. Complete an authenticated live dashboard audit.
2. Send Lovable handoff 003 for project/backend/marketing-site clarification.
3. Build a module readiness matrix.
4. Build an Automation Center workflow readiness matrix.
5. Confirm Supabase/Lovable Cloud/secrets/GitHub connections.
6. Decide first safe client-test path only after dashboard/backend safety is understood.
