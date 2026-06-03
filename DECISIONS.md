# ClinicPilotX Decisions

## 2026-05-27

- Treat `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX` as the official local ClinicPilotX workspace.
  - Rationale: It matches the numbered Buzzooka Workspace product structure already present on the external drive.

- Do not use or compare the separate `D:\BUZZOOKA WORKSPACE\Products\ClinicPilot X` folder unless Ross explicitly asks.
  - Rationale: Ross instructed Codex not to compare this project to older ClinicPilot work unless requested.

- Audit Lovable before approving new build work.
  - Rationale: The project is reportedly 70-80% complete, but current structure, backend, real vs mock data, auth, integrations, and incomplete features must be verified before changing anything.

- Prioritize product/dashboard functionality before marketing website work.
  - Rationale: Real client testing and launch require the core operational product to be itemized, verified, and stabilized first.

- Do not activate paid integrations without Ross approval.
  - Rationale: Keep costs controlled and avoid accidental billable service usage.

- GitHub is intended to become the online source of truth, with the external-drive folder as working backup/mirror.
  - Rationale: Codex, Lovable, Ross's PC, and Ross's laptop need a shared source of truth.

## 2026-06-02

- Confirmed `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX` is the official workspace for the new ClinicPilotX project.
  - Rationale: Ross confirmed this is the current project folder created by Codex for the new official run.

- Treat `D:\BUZZOOKA WORKSPACE\Products\ClinicPilot X` as old/reference-only material, not the active project.
  - Rationale: Ross clarified this folder contains work from the wrong Lovable project and should not drive the new project.

- Do not use Markdown files from the old/reference folder as the source of truth for the new project.
  - Rationale: Those `.md` files are prior Codex-generated project-management history for the wrong project.

- Only user-provided source materials from the old/reference folder may be considered as optional reference, especially Word/PDF/office documents or marketing/product explanation materials.
  - Rationale: Product explanation and marketing source material may still be valuable, but old project-management decisions should not contaminate the new official project.

## 2026-06-03

- Do not reinstall n8n as the immediate first move.
  - Rationale: current deployed app evidence points to Supabase tables plus Edge/server functions as the live automation layer; no direct n8n references were found in the frontend bundle. n8n can be introduced later if it solves a specific orchestration need.

- Treat Automation Center testing as high-risk until sandbox/live credential status is confirmed.
  - Rationale: deployed code can invoke email, SMS, payment-link, AI, and appointment-confirmation functions.
