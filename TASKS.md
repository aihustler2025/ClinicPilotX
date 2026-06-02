# ClinicPilotX Tasks

Last updated: 2026-05-27

## In Progress

- Audit current Lovable project before approving new build work.
- Create or connect the official ClinicPilotX GitHub repository.

## Pending

- Send first Lovable audit/intake message.
- Save Lovable response in `docs/handoffs/` using the required naming pattern.
- Review Lovable response and identify claims that require verification.
- Verify project URLs, routes, backend connection, auth, database tables, roles, and integrations.
- Create first QA checklist in `09-exports/` after Lovable returns enough project detail.
- Document verified modules in `PRODUCT_SPEC.md`.
- Create a blank GitHub repo or provide the existing official repo URL/full name.
- Add GitHub remote to local repo and push `main`.

## Blocked

- GitHub push and GitHub handoff links are blocked until an official repo exists and the local folder has a configured remote.
- Creating a GitHub repo directly from this shell is blocked because `gh` is not installed.

## Completed

- 2026-05-27: Confirmed external drive and Buzzooka Workspace location.
- 2026-05-27: Confirmed official local product folder at `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`.
- 2026-05-27: Created/updated required memory files.
- 2026-05-27: Created required `docs/handoffs/` and `09-exports/` folders.
- 2026-05-27: Prepared first Codex-to-Lovable audit/intake handoff.
- 2026-05-27: Initialized local Git repo on `main` and committed the official project memory baseline.

## Added 2026-06-02

- [x] Confirm official workspace is `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`.
- [x] Confirm old/reference folder is not the active project.
- [x] Inventory old/reference folder for non-Markdown source files.
- [x] Record rule: do not use old/reference `.md` files as source of truth.
- [ ] Create or connect new GitHub repo named `ClinicPilotX` for the official project.
- [ ] Get access to the new Lovable preview/project.
- [ ] Perform live QA across every left-navigation module/page.
- [ ] Ask Lovable for current project inventory, backend/database structure, auth roles, routes, real vs mock data, integrations, and known gaps.
- [ ] Build a QA/bug tracker in `09-exports/` after first live walkthrough.

## Source Review Tasks Added 2026-06-02

- [x] Review provided Word/PDF/XLSX ClinicPilot source materials.
- [x] Save source-material review in `09-exports/`.
- [x] Add durable product concepts to `PRODUCT_SPEC.md` as reference-only until verified against the live Lovable app.
- [ ] Compare live Lovable modules against source-material feature map.
- [ ] Convert verified modules into official `PRODUCT_SPEC.md` entries after QA.

## Live App QA Tasks Added 2026-06-02

- [x] Resolve deployed app Lovable project ID.
- [x] Confirm protected routes redirect to login without session.
- [x] Identify backend Supabase project from deployed bundle.
- [x] Inventory deployed app routes/nav from bundle.
- [x] Perform read-only anon Supabase table accessibility checks.
- [x] Identify Automation Center workflow rows and safe status summary.
- [x] Create Lovable handoff 002 with backend/security questions.
- [ ] Get valid admin login/session for `https://clinic-pilot-x.lovable.app`.
- [ ] Click-test Dashboard.
- [ ] Click-test Leads create/edit/delete/convert/persistence.
- [ ] Click-test Patients create/edit/persistence.
- [ ] Click-test Appointments create/status/reminder/payment request/persistence.
- [ ] Click-test Communication Hub external messages and internal chat after RLS issue is resolved.
- [ ] Click-test Video Consultation and define compliant future-state requirements.
- [ ] Click-test Payments & Billing without activating paid integrations.
- [ ] Click-test Analytics & Reporting and define visual upgrade plan.
- [ ] Click-test Staff Management and roles.
- [ ] Click-test Automation Center workflows without triggering paid sends/calls.
- [ ] Review Lovable response to handoff 002.
- [ ] Approve or revise RLS/security fix plan before build mode.
