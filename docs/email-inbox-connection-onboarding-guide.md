# ClinicPilotX Email Inbox Connection and Sorting Onboarding Guide

Last updated: 2026-06-30

## Purpose

This guide explains how ClinicPilotX should help a clinic connect email for AI sorting, lead intake, and future communication workflows.

The first pilot clinic is Dr. Colin Hong. The process must also work later for any subscribing clinic that uses Google Workspace/Gmail, Microsoft 365/Outlook, GoDaddy email, cPanel/hosting email, or simple forwarding.

This guide separates two things that must not be mixed up:

- **Inbound sorting:** reading incoming messages, classifying them, applying labels, and creating leads.
- **Outbound sending:** sending replies, follow-ups, reminders, campaigns, or confirmations.

Inbound sorting can be tested before outbound sending exists. Outbound sending requires extra safety, sender-domain verification, consent rules, and approval.

## Current Product Rule

Do not connect a real client inbox until the safe test-intake flow works and Ross approves.

Phase order:

1. Paste/import test emails inside ClinicPilotX.
2. Classify and review test emails.
3. Create test leads only after approval.
4. Suppress send-capable workflows from all test rows.
5. Later, connect a real inbox with OAuth or a forwarding/test-inbox path.
6. Later still, enable outbound sending only after domain/sender verification and workflow safety approval.

## Plain-English Definitions

### Inbox

The email account where messages arrive. Example: a clinic's customer care Gmail inbox.

### MX Records

DNS records that tell the internet where to deliver email for a domain. Google says MX records control where email for a domain is delivered, and Google Workspace uses `smtp.google.com` for current Workspace MX setup. Legacy Google Workspace accounts may still use `aspmx...` records.

### Forwarding

The clinic keeps its normal email, but copies messages to another address, such as a ClinicPilotX intake address or a customer-care inbox.

### Gmail Labels

Gmail labels are better than destructive folders for this workflow. Google explains that Gmail labels can tag and categorize messages, and multiple labels can apply to the same message or thread.

Recommended labels:

- `ClinicPilotX/Lead`
- `ClinicPilotX/Appointment Request`
- `ClinicPilotX/Spam or Solicitation`
- `ClinicPilotX/Questionable`
- `ClinicPilotX/Processed`

### OAuth

A secure "Connect Gmail" or "Connect Microsoft" login flow. The client grants permission without giving ClinicPilotX their password.

### Resend

Resend or similar tools are for sending outbound email from a verified domain or subdomain. Resend says a domain must be added and verified before sending from it. Resend is not the primary tool for reading a Gmail inbox.

## Recommended ClinicPilotX UI

The product should make this feel simple for clinic owners.

Recommended location:

- `Workspace`
- `Integrations`
- `Email Inbox`

Possible sub-sections:

- `Connect Inbox`
- `Label Mapping`
- `AI Sorting Rules`
- `Review Queue`
- `Sync Logs`
- `Outbound Sending` later, disabled until configured

The first version should be clear and calm:

- "Connect Gmail"
- "Connect Microsoft"
- "Use forwarding address"
- "Paste test email"
- "Run test classification"
- "Open review queue"

Do not expose technical words like OAuth, MX, SPF, DKIM, or DMARC as the first thing a clinic sees. Those should be behind help text or an advanced setup section.

## Phase A: Safe Test Intake

This is the build we should approve first.

### What Ross/Codex Does

1. Go to `Workspace`.
2. Open the future `Email Intake` or `Email Inbox` area.
3. Choose `Submit Test Email` or `Paste Email`.
4. Paste:
   - From email.
   - From name.
   - To email.
   - Subject.
   - Body.
   - Received date/time.
5. Click `Classify`.
6. Review the AI classification.
7. Edit extracted fields if needed:
   - patient/lead name,
   - email,
   - phone,
   - requested service,
   - appointment request,
   - message summary,
   - urgency,
   - consent clue.
8. Click one of:
   - `Approve and Create Lead`,
   - `Mark as Spam`,
   - `Needs Human Review`,
   - `Reject`.

### Expected Safety Behavior

- Every test intake row has `is_test = true`.
- Every lead created from a test email has `is_test = true`.
- No email is sent.
- No SMS is sent.
- No call is made.
- No calendar write occurs.
- No payment action occurs.
- No n8n workflow is activated.
- No send-capable workflow fires from the test lead.

### What This Proves

This proves the AI can classify the message and create a usable lead before touching a real inbox.

## Phase B: Dr. Colin Hong Pilot Inbox

Ross's current understanding:

- Public clinic email: `info@drcolinhong.com`.
- Messages are forwarded into a customer-care inbox Ross can access through Gmail / Google Workspace.
- We need to confirm the exact setup before connecting anything live.

### Dr. Hong Investigation Checklist

Before connecting Dr. Hong's real inbox, confirm:

1. What address receives website/contact-form messages?
2. Does `info@drcolinhong.com` forward to a customer-care Gmail/Workspace inbox?
3. Who owns/administers the customer-care inbox?
4. Is it Google Workspace, regular Gmail, Microsoft 365, GoDaddy email, cPanel/hosting email, or something else?
5. Does Ross have permission from the clinic to connect or process this inbox?
6. Can we create test labels in the inbox?
7. Can we create a narrow test label like `ClinicPilotX/Test` and process only messages inside that label first?
8. Should ClinicPilotX only label messages, or also create leads automatically?
9. Who reviews `Questionable` messages?
10. What data should never be sent to AI or logs?

### Suggested Dr. Hong First Live-Adjacent Test

Do not process the whole inbox first.

Safer first test:

1. In Gmail, create labels:
   - `ClinicPilotX/Test`
   - `ClinicPilotX/Lead`
   - `ClinicPilotX/Spam or Solicitation`
   - `ClinicPilotX/Questionable`
   - `ClinicPilotX/Processed`
2. Manually copy or label 10 to 25 old emails into `ClinicPilotX/Test`.
3. Connect ClinicPilotX to read only messages in `ClinicPilotX/Test`.
4. Run classification.
5. ClinicPilotX applies outcome labels.
6. Human checks the results.
7. Only after approval, test lead creation in Dr. Hong's workspace.

This keeps the first real test controlled and reversible.

## Scenario 1: Client Uses Google Workspace / Gmail

Best path: OAuth connection.

### Client Steps

1. Client logs into ClinicPilotX.
2. Goes to `Workspace > Integrations > Email Inbox`.
3. Clicks `Connect Gmail`.
4. Chooses the clinic inbox account.
5. Approves requested access.
6. ClinicPilotX shows a confirmation screen:
   - connected email address,
   - labels it can access/manage,
   - whether lead creation is test-only or live.
7. Client creates or approves the ClinicPilotX labels.
8. Client chooses whether ClinicPilotX can:
   - read selected label only,
   - apply labels,
   - create leads after review,
   - create leads automatically later.

### ClinicPilotX Setup

1. Store the connected account under the active `clinic_id`.
2. Store OAuth tokens securely.
3. Request least privilege:
   - read message metadata/body needed for classification,
   - label management,
   - no sending scope in the first inbound-only phase.
4. Create or verify Gmail labels.
5. Let the clinic choose the source label/query.
6. Show a `Test connection` button.
7. Show sync logs.
8. Keep all classification results scoped to that clinic.

### Notes

Gmail API supports managing labels on messages and threads. Google documents `gmail.labels` for label management and `messages.modify` / `threads.modify` for applying or removing labels.

## Scenario 2: Client Uses Microsoft 365 / Outlook

Best path: Microsoft OAuth connection.

### Client Steps

1. Client logs into ClinicPilotX.
2. Goes to `Workspace > Integrations > Email Inbox`.
3. Clicks `Connect Microsoft 365`.
4. Signs in with the clinic mailbox or admin-approved account.
5. Approves access.
6. Chooses test folder or category first.
7. Runs test classification.

### Alternative Forwarding Path

If the clinic cannot connect Microsoft OAuth yet, use forwarding.

Microsoft documents mailbox forwarding through Exchange Admin Center:

1. Admin opens Exchange Admin Center.
2. Goes to `Recipients > Mailboxes`.
3. Selects the mailbox.
4. Opens `Mailbox > Email forwarding`.
5. Turns forwarding on.
6. Chooses the forwarding address.
7. Optionally keeps a copy in the original mailbox.
8. Saves.

Security note: Microsoft warns that automatic external forwarding can increase takeover risk. Use forwarding only with explicit approval and a controlled destination.

## Scenario 3: Client Uses GoDaddy Email

GoDaddy can mean different things:

- GoDaddy domain only, but email is Google Workspace.
- GoDaddy domain only, but email is Microsoft 365.
- GoDaddy Professional Email.
- GoDaddy hosting/cPanel email.

Do not assume. First identify where email actually lives.

### How To Identify

1. Ask the client: "Where do you log in to read email?"
2. Check MX records for the domain.
3. If MX records point to Google, follow Google Workspace path.
4. If MX records point to Microsoft, follow Microsoft 365 path.
5. If MX records point to GoDaddy or hosting/cPanel, use forwarding or IMAP only if approved.

### Recommended Easy Setup

Preferred:

- Create a forwarding rule from the clinic mailbox to a ClinicPilotX intake address or approved customer-care inbox.

Alternative:

- Use IMAP read access only if OAuth is not available, but avoid storing passwords if possible.

Avoid:

- Asking clients to share raw mailbox passwords.
- Changing MX records unless the goal is to move all clinic email hosting.

## Scenario 4: Client Uses cPanel / Hosting Email

This is common with hosting providers.

### Client Steps

1. Log into hosting/cPanel.
2. Open `Email Accounts` or `Forwarders`.
3. Create a forwarder from the clinic address to the ClinicPilotX intake address or approved customer-care inbox.
4. Keep a copy in the mailbox if the provider supports it.
5. Send a test email from an outside address.
6. Confirm it appears in ClinicPilotX test intake or the connected inbox.

### ClinicPilotX Steps

1. Generate a unique intake address for that clinic, for example:
   - `clinic-abc123@intake.clinicpilotx.com`
2. Show copyable forwarding instructions.
3. Ask the client to send a test message.
4. Detect the test message.
5. Confirm setup.
6. Start with review-only mode.

## Scenario 5: Client Wants Us To Do It For Them

This is likely the best onboarding offer for nontechnical clinics.

### Managed Setup Path

1. Client signs an authorization or confirms in writing that ClinicPilotX/Buzzooka may help configure email intake.
2. Client provides temporary access through one of these safe paths:
   - screen share while they log in,
   - admin invite,
   - OAuth connection,
   - temporary delegated account,
   - forwarding-only instructions.
3. We identify where email is hosted.
4. We avoid changing MX records unless the client explicitly wants email hosting changed.
5. We create labels or forwarding.
6. We send test messages.
7. We show the client the review queue.
8. We leave them with a one-page summary of what was connected.

### What We Should Avoid

- Do not ask for passwords in chat.
- Do not store passwords in project docs.
- Do not connect a live inbox without written approval.
- Do not turn on outbound sends at the same time as inbound sorting.
- Do not delete or archive emails during setup.

## Scenario 6: Outbound Sending Later

Outbound sending is not required for inbox sorting.

Later options:

### Option A: ClinicPilotX Managed Sender

Example:

- From: `notifications@clinicpilotx.com`
- Reply-To: `info@drcolinhong.com`

Pros:

- Easiest demo.
- Less domain setup.

Cons:

- Less branded for the clinic.
- Not ideal for production patient communication.

### Option B: Verified Clinic Sending Domain

Example:

- From: `care@drcolinhong.com`
- or a subdomain like `updates.drcolinhong.com`

Requirements:

- Add sender domain/subdomain in Resend or chosen email provider.
- Add DNS records such as SPF/DKIM/DMARC.
- Verify domain.
- Test deliverability.

Resend recommends verifying domains and often using subdomains for clearer sending reputation separation.

### Option C: Send Through Google/Microsoft

Clinic connects Gmail/Microsoft send permission.

Pros:

- Sends from the real mailbox.

Cons:

- Requires broader scopes.
- Higher compliance/safety requirements.
- Should not be first phase.

## AI Sorting Logic

ClinicPilotX should classify each message as:

- `likely_lead`
- `appointment_request`
- `general_question`
- `spam_or_solicitation`
- `existing_patient`
- `admin_or_vendor`
- `needs_human_review`

For each message, extract:

- name,
- email,
- phone,
- requested service,
- preferred date/time,
- urgency,
- summary,
- language,
- consent clue,
- reason for classification,
- confidence score.

Low-confidence messages go to `Questionable`.

## Feedback Loop

Ross wants the AI to improve over time.

Safe version:

1. Human reviews classification.
2. Human marks it correct or wrong.
3. Human chooses the correct bucket.
4. ClinicPilotX stores the correction as clinic-scoped feedback.
5. Future prompts/rules use that feedback.

Important:

Do not claim the AI "learns automatically" unless there is a real implemented feedback system. Say "ClinicPilotX uses reviewed examples to improve future classification rules."

## Client-Facing Quick Script

Use this with a clinic owner:

> We are going to connect your clinic email for incoming-message sorting only. ClinicPilotX will not send emails, delete emails, archive emails, or contact patients during setup. First, we will test on a small set of messages. The AI will sort messages into Leads, Appointment Requests, Spam/Solicitation, and Questionable. Anything uncertain goes to human review. Once you approve the behavior, we can decide whether to create leads automatically.

## Information To Ask The Client

1. What public email address do patients use?
2. Where do you read that email?
3. Is it Gmail/Google Workspace, Microsoft 365, GoDaddy, cPanel/hosting email, or something else?
4. Who has admin access?
5. Are website contact-form messages forwarded to a different inbox?
6. May ClinicPilotX read selected messages for classification?
7. Should ClinicPilotX only label messages first?
8. Who reviews uncertain messages?
9. Should leads be created only after review?
10. Are there message types ClinicPilotX should ignore?

## ClinicPilotX QA Checklist

Before marking the module ready:

- Test paste/import email.
- Test obvious lead.
- Test appointment request.
- Test spam/sales solicitation.
- Test ambiguous/questionable email.
- Test existing-patient/admin message.
- Confirm no outbound email is sent.
- Confirm no SMS is sent.
- Confirm no call is made.
- Confirm no calendar write occurs.
- Confirm no payment action occurs.
- Confirm no workflow activity appears from test rows.
- Confirm lead creation stamps `clinic_id`.
- Confirm test lead creation stamps `is_test = true`.
- Confirm non-clinic members cannot see the intake rows.
- Confirm mobile layout has no horizontal scroll.
- Confirm human reviewer can correct classification.

## Dr. Hong Next Action

For Dr. Hong, the next practical step is:

1. Build/test the safe paste/import email intake inside ClinicPilotX.
2. Prepare 15 to 25 real-but-approved sample emails from the accessible customer-care inbox.
3. Remove or avoid sensitive patient details unless approved.
4. Run AI classification.
5. Tune buckets and review rules.
6. Only then plan the Gmail-label connection for the customer-care inbox.

## Source Notes

- Google Workspace Help: Set up MX records for Google Workspace.
- Google for Developers: Gmail API label management.
- Microsoft Learn: Exchange Online email forwarding.
- Resend Docs: Managing domains, domain verification, SPF, DKIM.
