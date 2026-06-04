# ClinicPilotX GitHub + Laptop + Local n8n Transfer Plan

Date: 2026-06-04

## Decision

No paid hosting will be purchased for n8n right now.

Rejected for now:

- Hostinger renewal
- n8n Cloud paid/trial path
- Oracle Cloud Always Free
- Any new paid VPS

Accepted path:

- GitHub becomes the shared source of truth.
- PC D-drive remains the local working mirror.
- Laptop clones from GitHub.
- Laptop runs n8n locally only for review/testing/importing old workflows.
- Old n8n JSON exports are used as blueprints, not blindly trusted production automations.

## Current GitHub State

Official repo needed:

`aihustler2025/ClinicPilotX`

Current status:

- `aihustler2025/ClinicPilotX` does not exist yet.
- `aihustler2025/clinicpilot-x` exists, but it is the old/wrong project history and must not be used as the official source of truth.

## What Ross Should Do Now

Create a new GitHub repo manually:

1. Open `https://github.com/new`
2. Owner: `aihustler2025`
3. Repository name: `ClinicPilotX`
4. Visibility: `Private` is recommended because project docs may include product strategy, workflows, and integration details.
5. Do not initialize with README.
6. Do not add `.gitignore`.
7. Do not add a license.
8. Click Create repository.
9. Send Codex the new repo URL.

Expected URL:

`https://github.com/aihustler2025/ClinicPilotX`

## What Codex Will Do After Repo Exists

On the PC:

1. Add GitHub remote to the official local repo.
2. Push local `main` to GitHub.
3. Verify GitHub contains the memory/docs files.
4. Keep GitHub as the source of truth.

Official local PC repo:

`D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`

## Laptop Setup

On the laptop:

1. Install/open Codex.
2. Make sure Git is installed.
3. Create or open the same Buzzooka workspace structure if possible.
4. Clone the new GitHub repo.
5. Use the laptop as the local n8n review machine.

Recommended laptop folder:

`D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`

If the laptop does not have a D drive, use the closest matching workspace folder and document it in `STATUS.md`.

## n8n Local Review Plan

Use local n8n on the laptop for review/testing only.

Purpose:

- Import old n8n JSON workflows.
- View workflow diagrams.
- Understand triggers and integrations.
- Map old workflows to current ClinicPilotX Automation Center.

Do not connect live credentials yet.

Do not activate live sends/calls.

Do not run workflows that send SMS, email, VAPI calls, payment links, WhatsApp messages, Messenger messages, or calendar invites until sandbox credentials and cost controls are confirmed.

## Old n8n Workflow Files

Reference-only local folder on the PC:

`D:\BUZZOOKA WORKSPACE\Products\ClinicPilot X\04-automations\old-n8n-workflows`

Found files:

- `Daily data sending to clinic member.json`
- `Email Agent.json`
- `My workflow.json`
- `NOTIFICATION.json`
- `outbound calling Voice workflow.json`
- `outbound reachout.json`
- `SMS  messages.json`
- `[VAPI] inbound calling scenario.json`
- `services credentials.json`

The credentials file should remain sealed unless Ross explicitly approves a secure credentials review.

## B-Drive Mirror

After GitHub is connected, create a B-drive mirror only as a backup copy.

Rules:

- GitHub is the source of truth.
- D-drive is the active PC working mirror.
- B-drive is backup only.
- Do not manually edit the B-drive copy unless recovering from failure.

## Immediate Next Step

Create the official GitHub repo:

`aihustler2025/ClinicPilotX`

Then send Codex the repo URL so Codex can push the existing official project memory/docs.

