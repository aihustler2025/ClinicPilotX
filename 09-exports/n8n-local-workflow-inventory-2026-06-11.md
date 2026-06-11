# n8n Local Workflow Inventory - 2026-06-11

## Scope

This inventory tracks workflows imported or created in the laptop-local n8n instance for ClinicPilotX review/testing.

Local n8n URL:

`http://localhost:5678`

Local Docker container:

`clinicpilotx-n8n`

Rules:

- Keep workflows inactive unless Ross explicitly approves a test run.
- Do not connect live credentials until the specific integration is approved.
- Do not use laptop n8n as production infrastructure for client-facing ClinicPilotX.
- Use local n8n to prototype, inspect, and map automation logic.

## Imported / Created Workflows

| Workflow | Source file | Active | Credentials | Purpose | Status |
| --- | --- | --- | --- | --- | --- |
| ClinicPilotX - Test Lead Intake Webhook | `09-exports/n8n-workflows/clinicpilotx-test-lead-intake-webhook.json` | No | None | Safe first test workflow that receives lead data by webhook, normalizes fields, and returns a local-test confirmation. | Imported successfully |

## First Workflow Details

Workflow ID:

`clinicpilotx-test-lead-intake-webhook`

Nodes:

- `Receive Test Lead`: POST webhook at `clinicpilotx/test-lead-intake`.
- `Normalize Lead Fields`: maps test payload fields into standard ClinicPilotX lead fields.
- `Return Test Confirmation`: returns a JSON confirmation.

No external services are connected.

No email, SMS, voice, payment, WhatsApp, Messenger, or client-site action is performed.

## Old Workflow Search

Codex searched common laptop locations for non-credential `.json` files:

- `%USERPROFILE%\Documents`
- `%USERPROFILE%\Downloads`
- `%USERPROFILE%\OneDrive`

No obvious old ClinicPilotX n8n workflow exports were found.

One unrelated-looking n8n file was found:

`C:\Users\user\OneDrive\Microsoft Teams Chat Files\n8n_runpod_workflow.json`

This was not imported because it does not appear to be a ClinicPilotX workflow.

Credential-like JSON filenames were excluded from inspection.

## Automation Build Plan

1. Use the current Lovable dashboard audit to identify existing Automation Center workflows and backend behavior.
2. Recover old n8n workflow exports only if Ross can provide them or if they are found in a safe non-credential folder.
3. Build new local n8n prototypes from Ross's descriptions when old exports are unavailable.
4. Test with dummy/test accounts first.
5. Connect one integration at a time only after Ross approves the credential and testing scope.
6. Decide per workflow whether production should run in Lovable/Supabase or later in hosted n8n.

## Likely First Production-Relevant Automation Candidates

- Lead intake from website form or webhook.
- Internal staff notification for new lead.
- Test email acknowledgement to lead.
- Follow-up reminder sequence.
- Appointment request handoff.
- Missed-call or voice-lead intake.
- SMS test notification after Twilio sandbox/limits are confirmed.

## Next Step

Ross should describe the first automation in plain English:

- What starts the automation?
- What information comes in?
- Who should be notified?
- What message should go out?
- What test account/email should be used?
- What should never happen during testing?

Codex will then create or update the n8n workflow directly.
