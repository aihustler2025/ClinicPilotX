# Leads v2 Fix QA - 2026-06-12

## Context

Ross approved and published Lovable's Leads v2 QA fix after the previous blocking issue:

- Notes-only lead edits changed a fresh lead temperature from `Cold` to `Hot`.

Lovable reported that it:

- Dropped the leftover `trigger_update_lead_temperature` trigger and old `update_lead_temperature()` function.
- Rewrote `calculate_lead_temperature()` so leads with no engagement return `cold`.
- Backfilled existing leads.
- Added inline phone validation.
- Added U.S./Canada display formatting in `LeadDetailPanel`.

## Test Environment

- Live app: `https://clinic-pilot-x.lovable.app/leads`
- Date: 2026-06-12
- Tester: Codex
- Data type: dummy QA data only
- Live sends/calls/payments: not triggered

## Dummy Lead

- Name: `CPX TEST Leads V2 fixB-678321`
- Email: `cpx.test+leads-v2-fixb-678321@example.com`
- Phone typed: `2135550199`
- Stored/list phone observed: `+12135550199`
- Detail phone observed: `+1 (213) 555-0199`
- Source: `Manual`
- Service: `Skin Care Consultation`

## Results

| Check | Result | Notes |
| --- | --- | --- |
| Invalid phone blocks submit | Pass | `5551234567` showed visible inline validation and dialog stayed open. |
| Valid phone clears validation | Pass | Replacing with `2135550199` cleared the validation message. |
| Create dummy lead | Pass | Creation succeeded after consent checkbox was checked. |
| Initial status/temperature | Pass | New lead appeared as `NEW LEAD` and `Cold`. |
| Notes-only edit safety | Pass | Editing notes only preserved `NEW LEAD` and `Cold`. |
| Timeline created event | Pass | Timeline showed `Lead created`. |
| Timeline edited event | Pass | Timeline showed `Lead edited`. |
| Detail phone formatting | Pass | Detail panel included `+1 (213) 555-0199`. |
| Table phone formatting | Polish issue | Main table still showed `+12135550199`. |
| Export retest | Not tested | Needs a separate focused pass. |

## QA Decision

The blocking Leads v2 temperature mutation bug is resolved for the tested create/edit path. Leads is not fully complete yet, but this specific blocker no longer prevents continuing the controlled CRM audit.

## Next Leads QA Items

- Retest Export dialog and downloaded CSV contents.
- Decide whether the main Leads table should display formatted phone numbers instead of raw E.164.
- Retest converted-lead filter/count behavior.
- Continue patient edit and appointment booking persistence testing.
