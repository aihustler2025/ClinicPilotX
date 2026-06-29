# Lovable Paste Message 043 - Subscription Display Regression After Auto-Assignment QA

Please read this focused QA follow-up and respond in Plan mode only. Do not build yet.

Codex QA passed the Auto-Assignment Phase A follow-up CRUD fixes, but found a subscription display regression after the publish.

## What Passed

Auto-Assignment now works for the tested scope:

- `/auto-assignment` loads.
- Creating a rule updates the list/count immediately and persists after reload.
- Active/inactive toggle updates and persists after reload.
- Staff max conversations saves to the new clinic-scoped setting and persists after reload.
- Delete has a labelled in-app confirmation, Cancel preserves the rule, Delete removes it immediately and after reload.
- No browser console warnings/errors were observed during final Auto-Assignment checks.
- No fresh Automation Center workflow rows appeared from the Auto-Assignment QA.

## Blocking Regression

The authenticated live app is showing `No active plan` again:

- `/auto-assignment` header shows `No active plan`.
- `/automation` shows `Current Plan: No active plan`.
- `/subscription` shows `Current Plan: No active plan`.
- `/subscription` still lists `Professional` under available plans, but not as the current plan.
- `/automation` shows `4 / 5 Active`, which appears to be the wrong entitlement path for the pilot clinic.

This conflicts with the earlier Request 040 QA pass, where Codex confirmed:

- Dashboard/header showed `Professional`.
- Automation Center showed `Professional`.
- Subscription page showed `Current Plan: Professional` and `Status: Active`.

## Required Plan

Please diagnose and propose the smallest safe fix to restore the pilot clinic subscription display across:

- shared header chip,
- Automation Center current plan and workflow entitlement count,
- Subscription page current plan card,
- Auto-Assignment page header/chrome.

Please include:

1. Likely root cause.
2. Exact files/tables/policies/functions to inspect.
3. Whether the Auto-Assignment follow-up changed anything that could affect active clinic or subscription context.
4. Whether this is frontend context, RLS/read access, subscription query shape, active clinic lookup, or seeded data mismatch.
5. Exact intended code/SQL changes before build.
6. QA checklist proving the app shows Professional again on Dashboard, Auto-Assignment, Automation Center, and Subscription.

## Safety / Out Of Scope

Do not touch live sends, SMS, email, payment, calendar, webhooks, API keys, workflow execution, or integration credentials.

Do not start visual refresh Phase B yet.

Do not start Dr. Hong email AI sorting yet.
