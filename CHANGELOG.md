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
