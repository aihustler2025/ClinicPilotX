# Playwright + Chrome QA Browser Tutorial

## What Playwright Is

Playwright is a tool that lets Codex control a real web browser.

Think of it like this:

- You open the app in Chrome.
- Playwright acts like a careful tester.
- It can click pages, read text, take screenshots, and check if errors appear.
- It helps us test ClinicPilotX faster than clicking everything by hand.

Playwright does not replace Lovable, Supabase, or the website. It is only a testing helper.

## What We Set Up

We opened a special Chrome window for QA testing.

That Chrome window is connected to Codex through a local browser control port:

`http://127.0.0.1:9222`

That means:

- You can log in normally.
- Codex can attach to the same logged-in window.
- Codex can click through ClinicPilotX after you log in.

## Why This Matters

ClinicPilotX is behind a login screen.

Without a logged-in browser, Codex can only see the login page. With this QA Chrome setup, Codex can see the actual dashboard, modules, settings, automations, and app data that an admin user sees.

## Simple Step-by-Step

1. Open the dedicated Chrome QA browser.
2. Go to `https://clinic-pilot-x.lovable.app`.
3. Log in with the admin account.
4. Leave that Chrome window open.
5. Codex attaches to the browser using Playwright.
6. Codex visits each page, checks what is there, captures screenshots, and records errors.

## What We Tested First

Codex attached to the logged-in Chrome window and confirmed access to:

- Dashboard
- Leads
- Patients
- Appointments
- Communication Hub
- Video Consultation
- Payments & Billing
- Analytics & Reporting
- Staff Management
- Automation Center
- Auto-Assignment Rules
- Subscription
- Settings
- Profile

## Plain-English Summary

Playwright is the QA robot. Chrome is the browser. You log in once, and then Codex can use Playwright to test the app from the inside.

