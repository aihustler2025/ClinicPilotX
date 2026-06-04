# ClinicPilotX n8n / Hostinger Recovery Options

Date: 2026-06-03

## Current Hostinger Finding

Hostinger hPanel is accessible in the Chrome QA browser.

Visible account/service status:

- Hostinger account is logged in.
- VPS shown: `srv841701.hstgr.cloud`
- Status shown: offline
- Plan shown: KVM 4
- Renewal prompt shown: 12 days remaining to renew at a discounted rate
- Visible renewal price: `$28.99/mo`

No paid action was clicked.

## Local n8n Export Finding

Old/reference n8n workflow export files already exist locally at:

`D:\BUZZOOKA WORKSPACE\Products\ClinicPilot X\04-automations\old-n8n-workflows`

Found workflow files:

- `Daily data sending to clinic member.json`
- `Email Agent.json`
- `My workflow.json`
- `NOTIFICATION.json`
- `outbound calling Voice workflow.json`
- `outbound reachout.json`
- `SMS  messages.json`
- `[VAPI] inbound calling scenario.json`
- `services credentials.json`

The credentials file was not opened.

Safe workflow metadata:

| Workflow | Active | Nodes | Main systems |
| --- | --- | ---: | --- |
| Daily data sending to clinic member | false | 6 | Schedule, Gmail, Google Sheets |
| Email Agent | true | 9 | Gmail trigger, Gemini, Google Calendar, Google Sheets |
| My workflow | false | 2 | Manual trigger, Google Calendar |
| NOTIFICATION | false | 9 | Schedule, Gmail, Google Sheets, Twilio |
| outbound calling Voice workflow | false | 10 | Schedule, Google Sheets, HTTP requests |
| outbound reachout | false | 18 | Gmail, Google Sheets, Twilio, HTTP requests |
| SMS messages | true | 11 | Twilio trigger, OpenAI/Gemini, Google Calendar, Google Sheets |
| VAPI inbound calling scenario | true | 9 | Webhook, VAPI-style inbound call flow, Gemini, Google Calendar, Google Sheets |

## Official Hosting Facts Checked

SiteGround is probably not suitable for n8n because SiteGround says its Shared and Cloud hosting plans do not support Node.js:

https://www.siteground.com/kb/node-js-available/

n8n self-hosting with Docker Compose expects a server where Docker/Docker Compose can run:

https://docs.n8n.io/hosting/installation/server-setups/docker-compose/

Hostinger VPS backups may exist, but Hostinger says direct backup/snapshot download is not supported; you normally restore/access the VPS and use SFTP for specific files:

https://www.hostinger.com/support/1583232-how-to-back-up-or-restore-a-vps-at-hostinger/

Oracle Cloud has an Always Free tier that can include compute resources, but it requires cloud setup discipline and may still need careful billing guardrails:

https://www.oracle.com/cloud/free/

n8n Cloud offers trials, including Starter/Pro trials with no credit card according to its pricing FAQ, but it is not a long-term free production host:

https://n8n.io/pricing/

## Cheapest Practical Options

### Option 1: Do not use n8n yet

Cost: `$0`

Use the current Lovable/Supabase backend first. The live ClinicPilotX app already references Supabase Edge/server functions and Automation Center workflow tables.

Best for:

- Finishing the product audit.
- Avoiding paid hosting.
- Avoiding duplicate automation architecture.

Risk:

- Some older n8n workflows may need to be rebuilt or mapped into Supabase/Lovable functions later.

Recommendation:

Use this as the default path right now.

### Option 2: Reuse local n8n JSON exports only

Cost: `$0`

Do not run n8n yet. Instead, treat the local JSON files as blueprints. Codex can inspect non-secret workflow structure and map each workflow to the current ClinicPilotX modules.

Best for:

- Preserving old work without paying Hostinger.
- Understanding what was built.
- Planning which automations belong in Supabase Edge Functions, Lovable, or future n8n.

Risk:

- Credentials may be expired, unsafe, or tied to old accounts.
- Old workflow logic may use Google Sheets instead of the current Supabase database.

Recommendation:

Do this immediately.

### Option 3: Run n8n locally only for development

Cost: `$0`

Run n8n on a laptop only when testing/importing workflows.

Best for:

- Importing old JSON workflows.
- Reviewing workflow diagrams.
- Testing without monthly hosting.

Risk:

- Not suitable for live client automations.
- Webhooks only work while the laptop is on unless a tunnel is used.

Recommendation:

Good for review/testing, not production.

### Option 4: Use n8n Cloud trial temporarily

Cost: `$0 short-term`, paid later

n8n Cloud trials can be used to import/review workflows without server setup.

Best for:

- Short-term workflow inspection.
- Avoiding server setup.

Risk:

- Not a permanent free option.
- Must avoid letting trial turn into paid billing without approval.

Recommendation:

Only use if local n8n setup is inconvenient.

### Option 5: Oracle Cloud Always Free VPS

Cost: potentially `$0`

Use Oracle Always Free compute to host Docker/n8n.

Best for:

- A free always-on self-hosting path.

Risk:

- More technical setup.
- Cloud accounts can still create billing risk if configured incorrectly.
- Capacity may vary by region.

Recommendation:

Possible, but only after we finish product audit and add billing guardrails.

### Option 6: Renew Hostinger VPS

Cost: about `$28.99/mo` based on current hPanel prompt

Renew only if the local workflow exports are incomplete and Hostinger is the only place with irreplaceable data.

Best for:

- Recovering old VPS files if absolutely needed.

Risk:

- Not cheap.
- Old VPS may contain outdated or insecure setup.
- Renewing does not guarantee clean n8n recovery.

Recommendation:

Do not renew unless we prove the local exports are insufficient.

## Recommended Next Step

Do not pay for Hostinger yet.

Next action:

1. Inventory the old n8n JSON workflows in detail, excluding credentials.
2. Map each old workflow to the current ClinicPilotX Automation Center.
3. Decide which workflows should be rebuilt as Supabase/Lovable functions and which truly require n8n.
4. Only then decide whether n8n hosting is needed.

