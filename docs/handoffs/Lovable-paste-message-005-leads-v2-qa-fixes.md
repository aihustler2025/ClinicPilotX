# Lovable Paste Message 005 - Leads v2 QA Fixes

Mode: Plan first. Do not build until Ross returns your plan to Codex for review.

Please review the published Leads v2 QA results and propose the smallest safe fix plan.

GitHub source:

https://github.com/aihustler2025/ClinicPilotX/blob/main/09-exports/controlled-crm-test-log-2026-06-11.md

Specific live QA finding:

- Test lead: `CPX TEST Leads V2 20260611-19504`
- Email: `cpx.test+leads-v2-20260611-19504@example.com`
- Initial created state: `NEW LEAD` and `Cold`
- Action tested: edited only the notes field
- Actual result: status stayed `NEW LEAD`, but temperature changed from `Cold` to `Hot`
- Expected result: editing safe fields such as notes/service/contact details must not change status, temperature, score, created_at, or conversion fields unless an explicit scoring/status action or approved automation event occurs.

Please investigate why temperature still changes after a notes-only edit. In your plan, identify whether the cause is:

- frontend payload still sending a temperature/score field,
- database trigger/function still recalculating on lead updates,
- updated_at/date ordering causing the row to display updated fields incorrectly,
- activity/logger side effect,
- or another cause.

Also include two small UX fixes if they are low-risk:

- Invalid phone input such as `5551234567` should show a clear visible validation message instead of leaving the user unsure why Create Lead did not complete.
- U.S./Canada-style display should move closer to `+1 (213) 555-0199` while retaining E.164 storage, for example `+12135550199`.

Do not add live integrations. Do not send email/SMS/calls. Do not activate workflows. Do not create storage buckets for files/photos yet.

Please respond with a concise plan, touched files/components/tables/functions, and exact QA steps you will run after build.
