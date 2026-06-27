# Clinic Workspace Phase A Human QA Script

Date: 2026-06-27

## Purpose

Use this checklist to manually test the Clinic Workspace setup area.

This is the setup area where a clinic owner/admin enters the clinic's business facts, services, FAQs, and AI safety rules.

## Safety Rules

Do not click:

- send email,
- send SMS,
- send reminder,
- Google Calendar connect/write,
- Stripe/payment link,
- workflow test-send,
- chatbot/API/webhook actions,
- file upload unless Ross explicitly approves.

Use only obvious QA/test values.

## Where To Go

Open:

`https://clinic-pilot-x.lovable.app/settings?tab=clinic-workspace`

Expected:

- You should be on Settings.
- The `Clinic Workspace` tab should be selected.
- Clinic Workspace should not appear as a main left-nav menu item.

## Test 1 - Navigation

Click each Clinic Workspace sub-section:

- Overview
- Business Profile
- Branding
- Business Hours
- Services & Pricing
- Team & Roles
- Knowledge: FAQs
- Knowledge: Sources
- AI Guardrails
- Integrations Status

Expected:

- Each section opens.
- The URL updates with `section=...`.
- No page crashes.
- No permission error appears.

## Test 2 - Business Profile

Go to:

`Business Profile`

Enter harmless QA values, for example:

- Legal Name: `QA TEST Clinic Profile`
- Tagline: `QA TEST tagline`
- Description: `QA TEST description`
- Country: `Canada`
- Region: `Ontario`
- Postal Code: `QA-TEST`

Click `Save`.

Expected:

- You see a saved/success toast.
- Reload the page.
- The values remain.

## Test 3 - Services & Pricing

Go to:

`Services & Pricing`

Find the blank row with placeholder `New service`.

Add:

- Name: `QA TEST Service`
- Category: `QA`
- Duration: `30`
- Price: `250`
- Currency: `CAD`

Click the plus icon on the same blank row.

Expected:

- You see `Service added`.
- Reload the page.
- The QA service is still there.

Important:

- Do not click the trash icon on real services unless Ross specifically asks you to test deletion.

## Test 4 - Knowledge FAQs

Go to:

`Knowledge: FAQs`

Add:

- Question: `QA TEST FAQ`
- Category: `QA`
- Answer: `QA test answer`

Click `Add FAQ`.

Expected:

- You see `FAQ added`.
- Reload the page.
- The FAQ remains visible/editable.

## Test 5 - Knowledge Sources

Go to:

`Knowledge: Sources`

Expected:

- It says `Coming in Phase B`.
- It should not ask you to upload real files yet.

## Test 6 - AI Guardrails

Go to:

`AI Guardrails`

Enter harmless QA values:

- Tone: `Friendly and cautious QA test`
- Forbidden topics: `diagnosis, guaranteed outcomes`
- Escalation email: `qa@example.com`
- Required disclaimer: `General information only`
- Escalation rule: `Escalate medical-risk questions to staff`

Click `Save`.

Expected:

- You see `AI guardrails saved`.
- Reload the page.
- The values remain.

## Test 7 - Team & Roles

Go to:

`Team & Roles`

Expected:

- It shows current team members.
- It says this section is read-only.
- It should not let you accidentally change roles here.

## Test 8 - Integrations Status

Go to:

`Integrations Status`

Expected:

- It shows integration status.
- Do not connect or test any live integration.
- Make a note if any label looks confusing, such as saying `Configured` when you are not sure it is truly connected.

## Test 9 - Overview

Go to:

`Overview`

Expected:

- The setup checklist should show progress.
- It should not permanently show `0 of 6` if you already saved profile/services/FAQs/guardrails.

Known issue:

- It may briefly show the wrong number while loading. Report if it stays wrong.

## Pass / Fail Notes

Record:

- date and time,
- browser used,
- tester name,
- what passed,
- what failed,
- screenshots of any error.
