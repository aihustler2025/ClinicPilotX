# Request 053 Email Inbox Phase B Setup UX QA

Date: 2026-07-01

## Scope

Phase B turns `Workspace > Email inbox` from a test-only classifier surface into a visible subscriber setup flow for the Dr. Colin Hong pilot.

This phase is setup UX only. It does not connect a real inbox, OAuth, forwarding provider, inbound webhook, SMS, calls, calendar writes, payments, attachment ingestion, or workflow triggers.

## Build Summary From Lovable

Lovable built:

- `clinic_email_connections`
- `email_intake_audit`
- nullable `email_intake.connection_id`
- `GuardrailBanner`
- `SetupChecklist`
- `ConnectionMethodPicker`
- `ForwardingSetup`
- `ConnectionStatusCard`
- `HelpInstructions`
- updated `EmailIntakePage.tsx`
- updated `useEmailIntake.ts`

Lovable confirmed:

- no new edge functions
- no OAuth
- no inbound webhook
- no outbound sends
- no workflow-function changes
- no change to `trigger_calculate_lead_score`

## Codex QA Actions

Tested in the Lovable in-app browser preview after publish.

Verified:

- `Workspace > Email inbox` renders.
- Guardrail banner is visible:
  - Read-only pilot
  - No sends
  - Human review required
  - No workflow triggers
  - No automation
- Header/status card renders real counters.
- Setup wizard renders:
  - Step 1. Choose connection method
  - Step 2. Verify mailbox / forwarding
  - Step 3. Run safe test scan
  - Step 4. Review classifications
  - Step 5. Approve leads manually
  - Step 6. Enable automation
- Gmail / Google Workspace and Microsoft 365 / Outlook are labelled planned / pilot approval required.
- Help tabs render for:
  - Gmail
  - Google Workspace
  - Microsoft 365 / Outlook
  - GoDaddy email
  - SiteGround email
  - cPanel / hosting mail
  - Forwarding-only
  - Concierge
- Step 3 still exposes the Phase A paste classifier and sample library.
- Step 4 still exposes the review queue with the existing Phase A Jane Doe and SEO Vendor rows.
- Step 6 remains locked.

## First QA Blocker

Clicking `Forwarding / intake address > Choose` did not change the method from `None yet`.

Codex sent a focused Lovable fix request.

Lovable found the root cause:

- `useCreateConnection` awaited `supabase.auth.getUser()`.
- That network call failed with `TypeError: Failed to fetch`.
- The insert was aborted before it ran.

Fix from Lovable:

- `src/pages/email-intake/useConnections.ts`
  - replaced `getUser()` with cached `getSession()`.
- `src/pages/email-intake/EmailIntakePage.tsx`
  - added a toast when a non-manager clicks Choose.
  - made choosing the already-selected method a no-op.

Lovable confirmed no edge functions, OAuth, sends, workflows, RLS, or migrations were touched by the fix.

## Post-Fix QA

Verified after publishing the fix:

- Clicking Forwarding works.
- Method shows `Forwarding`.
- Status shows `draft`.
- Badges show `Read-only` and `Automation off`.
- Step 1 shows `Done`.
- Forwarding card shows selected/reconfigure state.
- Step 2 opens Forwarding setup.
- Step 2 clearly states the intake address is placeholder-only and real intake domain is deferred.
- Step 2 states no mailbox writes, no auto-replies, no automation, and human review required.

## Lovable Read-Only SQL Evidence

Lovable reported:

- Exactly one `clinic_email_connections` row for the Dr. Colin Hong pilot clinic.
- Clinic id: `8ed615bf...`
- Method: `forwarding`
- Status: `draft`
- `read_only = true`
- `automation_enabled = false`
- `mailbox_hint = null`
- `intake_address = intake+8ed615bf@in.[pilot-domain]`
- Existing Phase A `email_intake` rows remain `connection_id = NULL`.
- `email_intake_audit = 0` rows after this specific post-fix QA, because Codex only selected the connection method and did not re-run classify/approve/spam actions.

Side-effect counts for the last 24 hours:

| Table | Rows created |
| --- | ---: |
| `workflow_executions` | 0 |
| `automation_logs` | 0 |
| `email_delivery_logs` | 0 |
| `reminders` | 0 |
| `scheduled_messages` | 0 |
| `messages` | 0 |
| `scheduled_confirmations` | 0 |
| `call_logs` | 0 |

## Result

Pass for the tested Phase B setup UX scope.

The Email Inbox setup is now visible enough for a product demo, while still safe. It is not a real connected inbox yet.

## Next Recommended Step

Prepare Dr. Hong demo data:

- populate approved/sanitized workspace profile details,
- add services and pricing guidance,
- add FAQs,
- add policies/disclaimers and AI guardrails,
- paste/import sanitized customer-care email samples into Email Inbox,
- manually review classifications and approve test leads.

Do not connect the real customer-care mailbox, OAuth, forwarding, inbound webhook, PHI-containing live ingestion, attachments, auto-replies, SMS/calls, calendar writes, or workflow triggers until separately approved.
