# Codex-to-Laptop-Codex-001: ClinicPilotX Local n8n Transfer

Date: 2026-06-05

## Purpose

This handoff is for the Codex session on Ross's laptop.

The laptop will be used as the local n8n review/testing machine for ClinicPilotX. No paid n8n hosting, n8n Cloud, Oracle Cloud, Hostinger renewal, or new VPS should be used at this stage.

## Official GitHub Repo

Use this repo as the source of truth:

`https://github.com/aihustler2025/ClinicPilotX`

Clone it onto the laptop.

Preferred laptop folder:

`C:\Users\Rosstafari\Documents\ClinicPilotX`

If the Windows username is different, use:

`%USERPROFILE%\Documents\ClinicPilotX`

## First Instructions for Laptop Codex

Read these files first:

- `AGENTS.md`
- `STATUS.md`
- `TASKS.md`
- `DECISIONS.md`
- `PRODUCT_SPEC.md`
- `CHANGELOG.md`
- `09-exports/authenticated-platform-audit-2026-06-03.md`
- `09-exports/n8n-hostinger-recovery-options-2026-06-03.md`
- `09-exports/github-laptop-n8n-local-transfer-plan-2026-06-04.md`

Then continue from the current task list.

## Business/Architecture Decision

ClinicPilotX should use a hybrid automation strategy:

1. Supabase/Lovable handles core product automation that must be reliable for all users.
2. Local n8n is used for review, testing, blueprint import, and automation design.
3. n8n should not become the production dependency for client-facing workflows until hosting, security, backups, monitoring, and cost controls are solved.

Reason:

- Local laptop n8n is useful and free, but it is not production-grade for many clinics.
- A laptop can lose internet, reboot, sleep, change IP, or have webhook problems.
- For commercialization, critical automations should not depend on a personal laptop.
- Old n8n workflows can still save time as blueprints.

## Local n8n Decision

Install n8n locally on the laptop using Docker.

Purpose:

- Import old n8n workflow JSON files.
- Review workflow diagrams.
- Map old workflows to current ClinicPilotX Automation Center.
- Test with dummy data only.

Do not:

- Connect live credentials.
- Activate live Twilio/SMS sends.
- Activate live Gmail sends.
- Activate live VAPI calls.
- Send WhatsApp/Messenger messages.
- Trigger payment links.
- Expose laptop n8n as production infrastructure.

## Install Requirements

Use official docs:

- n8n Docker docs: `https://docs.n8n.io/hosting/installation/docker/`
- Docker Desktop Windows docs: `https://docs.docker.com/desktop/setup/install/windows-install/`

Docker Desktop should use Linux containers/WSL2 if prompted.

## Recommended Local n8n Command

After Docker Desktop is installed and running, open PowerShell and run:

```powershell
docker volume create clinicpilotx_n8n_data
docker run -d `
  --name clinicpilotx-n8n `
  --restart unless-stopped `
  -p 5678:5678 `
  -e GENERIC_TIMEZONE="America/Toronto" `
  -e TZ="America/Toronto" `
  -e N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true `
  -e N8N_RUNNERS_ENABLED=true `
  -v clinicpilotx_n8n_data:/home/node/.n8n `
  docker.n8n.io/n8nio/n8n
```

Then open:

`http://localhost:5678`

Create the first local owner account in n8n.

## Verify n8n

Run:

```powershell
docker ps
docker logs clinicpilotx-n8n --tail 50
```

Expected:

- Container is running.
- Port `5678` is accessible.
- n8n opens in the browser.

## Old n8n Workflow Source

Old/reference workflow exports are currently on the PC at:

`D:\BUZZOOKA WORKSPACE\Products\ClinicPilot X\04-automations\old-n8n-workflows`

Known files:

- `Daily data sending to clinic member.json`
- `Email Agent.json`
- `My workflow.json`
- `NOTIFICATION.json`
- `outbound calling Voice workflow.json`
- `outbound reachout.json`
- `SMS  messages.json`
- `[VAPI] inbound calling scenario.json`
- `services credentials.json`

Do not import or open `services credentials.json` until Ross explicitly approves a secure credentials review.

Recommended safe process:

1. Copy only non-credential workflow JSON files to the laptop.
2. Import each workflow into local n8n.
3. Keep all imported workflows inactive.
4. Document each workflow purpose, trigger, integrations, required credentials, and current ClinicPilotX equivalent.
5. Decide whether to rebuild it in Supabase/Lovable, keep it as n8n, or discard it.

## Current ClinicPilotX Verified State

Live app:

`https://clinic-pilot-x.lovable.app`

Lovable project ID:

`8b4d9031-af8d-4faf-81d3-135c41ad73b7`

Supabase project ref:

`imuyfbvsombbpgdgkhrb`

Known issue:

`Auto-Assignment Rules` is broken because the frontend references `assignment_rules`, but Supabase returns a missing table/schema cache error.

Known issue:

Subscription state sometimes shows `Professional` and sometimes `No Plan` for the same logged-in session.

Coming soon:

- Video Consultation
- Main Profile route

## Immediate Laptop Task List

1. Clone `https://github.com/aihustler2025/ClinicPilotX`.
2. Read the memory files listed above.
3. Install Docker Desktop if not installed.
4. Start local n8n with Docker.
5. Verify `http://localhost:5678` opens.
6. Create a local-only n8n owner account.
7. Import old non-credential n8n workflow JSON files.
8. Do not activate imported workflows.
9. Create an inventory report of imported workflows.
10. Update `STATUS.md`, `TASKS.md`, and `PRODUCT_SPEC.md`.
11. Commit and push changes to GitHub.

## Master Prompt to Paste Into Laptop Codex

```text
We are continuing the official ClinicPilotX project.

GitHub source of truth:
https://github.com/aihustler2025/ClinicPilotX

Clone this repo into:
%USERPROFILE%\Documents\ClinicPilotX

After cloning, read:
- AGENTS.md
- STATUS.md
- TASKS.md
- DECISIONS.md
- PRODUCT_SPEC.md
- CHANGELOG.md
- 09-exports/authenticated-platform-audit-2026-06-03.md
- 09-exports/n8n-hostinger-recovery-options-2026-06-03.md
- 09-exports/github-laptop-n8n-local-transfer-plan-2026-06-04.md
- docs/handoffs/Codex-to-Laptop-Codex-001-clinicpilotx-local-n8n-transfer.md

Your first mission:
Set up local n8n on this laptop using Docker Desktop, for review/testing only.

Rules:
- Do not buy hosting.
- Do not use n8n Cloud.
- Do not use Oracle Cloud.
- Do not renew Hostinger.
- Do not activate paid integrations.
- Do not connect live credentials unless Ross explicitly approves.
- Do not import/open services credentials JSON unless Ross explicitly approves.
- Keep workflows inactive until reviewed.
- Keep GitHub updated after meaningful documentation changes.

Install/verify steps:
1. Check whether Git is installed.
2. Check whether Docker Desktop is installed.
3. If Docker is missing, guide Ross through installing Docker Desktop for Windows from official Docker docs.
4. Once Docker is running, create a persistent n8n Docker volume.
5. Run n8n as container name clinicpilotx-n8n on port 5678.
6. Verify http://localhost:5678 opens.
7. Create a local-only n8n owner account.
8. Ask Ross to provide/copy the old non-credential n8n workflow JSON files.
9. Import the old workflows into local n8n but keep them inactive.
10. Create an inventory report mapping each imported n8n workflow to ClinicPilotX Automation Center.
11. Update STATUS.md, TASKS.md, PRODUCT_SPEC.md, and 09-exports.
12. Commit and push changes to GitHub.

Business guidance:
Use n8n locally to preserve and understand old automations. Do not make the commercial ClinicPilotX app depend on laptop-hosted n8n for production. For launch, core automations should eventually run inside reliable hosted backend infrastructure, likely Supabase/Lovable functions first, with n8n used where it clearly saves time and can be hosted safely later.
```

