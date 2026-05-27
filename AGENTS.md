# ClinicPilotX Agent Instructions

ClinicPilotX is the official Buzzooka product workspace for appointment-based clinics, plastic surgery practices, dental clinics, med spas, beauty/wellness businesses, salons, and other service businesses.

## Source of Truth

- Treat this folder as the official local working mirror: `D:\BUZZOOKA WORKSPACE\02-PRODUCTS\ClinicPilotX`.
- GitHub should become the shared online source of truth once the official repository is created or connected.
- Do not compare this project to any older ClinicPilot project unless Ross explicitly asks.
- Do not delete, overwrite, or merge material from other ClinicPilot folders without explicit approval.

## Current Operating Rules

- Do not build new product functionality until the current Lovable project has been audited.
- Do not assume Lovable is correct. Lovable claims must be verified through code, app behavior, database state, screenshots, logs, or direct project evidence.
- Product/dashboard functionality comes first. Do not start with the marketing website unless Ross redirects the priority.
- Do not activate paid integrations or make billable service changes without Ross approval.
- Keep costs low where possible.
- Keep `STATUS.md` and `TASKS.md` current after meaningful work so a future Codex session can resume without re-explaining context.
- When a module is completed or verified, document its behavior in `PRODUCT_SPEC.md`.
- When QA is needed, create assistant-facing QA docs in `09-exports/`.

## Lovable Coordination

Ross communicates with Lovable manually. Codex writes the prompts/messages; Ross pastes them into Lovable. Ross sends Lovable responses back to Codex for review.

When Ross asks what to send to Lovable, respond in this format:

```text
Mode: Plan or Build
Action: Click Approve or Send Custom Message
Message: exact message to paste into Lovable
```

For long Lovable prompts, create a numbered Markdown handoff in `docs/handoffs/`, commit/push it to GitHub when available, and give Ross a short Lovable message linking to the GitHub file.

Handoff naming pattern:

- `Codex-to-Dashboard-Lovable-001-[short-slug].md`
- `Dashboard-Lovable-to-Codex-001-[short-slug-response].md`

Use the next number each time and keep the sequence clear.

## Folder Conventions

- `AGENTS.md`: instructions for Codex and future AI agents.
- `STATUS.md`: current project state, where work left off, and immediate next steps.
- `TASKS.md`: pending, in-progress, blocked, and completed tasks.
- `DECISIONS.md`: important decisions and rationale.
- `CHANGELOG.md`: major updates over time.
- `PRODUCT_SPEC.md`: verified product features, modules, automations, integrations, and workflows.
- `docs/`: durable supporting documentation.
- `docs/handoffs/`: long Codex-to-Lovable and Lovable-to-Codex messages.
- `09-exports/`: QA scripts, handoff docs, testing docs, and files intended for people outside Codex.
- `app/`: application code only if this folder later owns or mirrors code.
- `prompts/`: reusable prompts that are not one-off Lovable handoffs.
