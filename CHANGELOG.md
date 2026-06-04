# ClinicPilotX Changelog

## 2026-05-27

- Established `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX` as the official local project workspace.
- Expanded project memory files: `AGENTS.md`, `STATUS.md`, `TASKS.md`, `DECISIONS.md`, `CHANGELOG.md`, `PRODUCT_SPEC.md`, and `README.md`.
- Created required `docs/handoffs/` and `09-exports/` folders.
- Prepared first Lovable audit/intake handoff: `docs/handoffs/Codex-to-Dashboard-Lovable-001-project-audit-intake.md`.
- Initialized local Git repo on `main`.
- Created initial baseline commit: `71d4010 Initialize official ClinicPilotX project memory`.
- Recorded GitHub setup blockers: no `gh` CLI installed and no repository connected yet.

## 2026-05-22

- Created initial ClinicPilotX workspace memory skeleton.

## 2026-06-02

- Confirmed official workspace is `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`.
- Marked `D:\BUZZOOKA WORKSPACE\Products\ClinicPilot X` and GitHub repo `aihustler2025/clinicpilot-x` as old/reference-only for this new project.
- Inventoried non-Markdown files in the old/reference folder; no Word/PDF source materials were found.
- Revised first Lovable audit handoff to explicitly avoid old repo/project assumptions.

## 2026-06-02 Source Review

- Reviewed 30 provided ClinicPilot source materials from the old source-document folder.
- Saved source-material review at `09-exports/source-material-review-2026-06-02.md`.
- Added durable product concepts to `PRODUCT_SPEC.md` with an architecture caveat about older n8n/Google Sheets assumptions.

## 2026-06-02 Live App Pre-Login Audit

- Audited deployed app at `https://clinic-pilot-x.lovable.app` without login.
- Resolved Lovable project ID `8b4d9031-af8d-4faf-81d3-135c41ad73b7` and confirmed Lovable connector status `ready`.
- Identified standalone Supabase backend `imuyfbvsombbpgdgkhrb` from deployed bundle.
- Captured route/nav inventory and Supabase table inventory.
- Found public anon readability concerns on operational tables and RLS infinite recursion on internal chat tables.
- Created pre-login inventory report and Lovable handoff 002.

## 2026-06-03 Platform Investigation

- Attempted to connect to authenticated in-app browser session; connector still fails in Windows sandbox.
- Performed deeper deployed-code/backend investigation instead.
- Identified Supabase Edge/server functions referenced by frontend.
- Confirmed no direct n8n references in deployed frontend bundle.
- Summarized Automation Center workflow configuration coverage.
- Saved platform investigation report at `09-exports/platform-investigation-2026-06-03.md`.
## 2026-06-03

- Restored authenticated UI QA path using dedicated Chrome QA browser and Playwright after in-app browser connector failures.
- Added `09-exports/playwright-chrome-qa-tutorial.md` for Ross.
- Added `09-exports/authenticated-platform-audit-2026-06-03.md` with first authenticated module inventory and QA findings.
- Documented verified early bugs: missing `assignment_rules` backend support, inconsistent plan state, Video Consultation/Profile coming soon, and empty Internal Chat state.
## 2026-06-03 n8n Recovery

- Investigated Hostinger status read-only: old VPS is offline and renewal prompt shows approximately `$28.99/mo`.
- Found local old n8n workflow exports for email, SMS/Twilio, VAPI inbound calling, outbound outreach, notifications, and daily reporting.
- Added `09-exports/n8n-hostinger-recovery-options-2026-06-03.md`.
- Recommended not renewing Hostinger until local workflow exports are mapped and proven insufficient.
