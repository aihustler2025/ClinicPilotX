# Request 046 - Visual Refresh Phase 1 QA

Date: 2026-06-30
App: https://clinic-pilot-x.lovable.app
Scope: Read-only QA after Lovable Phase 1 visual/chrome refresh publish.

## Lovable Reported Scope

- Added `@fontsource/plus-jakarta-sans` and font imports.
- Updated visual tokens in `src/index.css` and `tailwind.config.ts`.
- Restyled `AppHeader`, `AppSidebar`, `MetricCard`, and `MiniChart`.
- No routes, information architecture, CRM logic, migrations, RLS, edge functions, integrations, live credentials, sends, payments, calendar writes, or Settings > Clinic Workspace changes.

## Desktop QA Result

Result: Pass for desktop/read-only scope.

Verified:

- Dashboard opens behind the authenticated session.
- New slate page background is live: `rgb(248, 250, 252)`.
- Plus Jakarta Sans is applied to body text.
- Header is sticky with backdrop blur.
- Solid indigo logo tile is visible.
- Header/sidebar/navigation still render.
- Sidebar still contains the expected main modules: Dashboard, Leads, Patients, Appointments, Communication Hub, Video Consultation, Payments & Billing, Analytics & Reporting, Staff Management, Automation Center, Auto-Assignment Rules, Subscription, and Settings.
- Dashboard metric cards render with the refreshed card style.
- Dashboard content remains truthful: Follow-ups says `Coming soon`, Revenue shows `$0`, and no fake metrics were introduced during the observed pass.
- Dashboard widgets still render: Upcoming Appointments, Leads by Source, and Recent Leads.
- Automation Center still shows Professional and `7 / 13 Active`.
- Auto-Assignment still loads with `Assignment Rules (0)` and `Staff Configuration (2)`.
- Subscription still shows `Current Plan: Professional` and `Status: Active`.
- Settings still loads.
- Browser console showed no errors or warnings during the dashboard final check.

## Mobile QA Result

Result: Pass with one polish fix required.

Verified at a phone-sized viewport:

- Dashboard renders without an application error.
- Metric cards load after data readiness.
- Metrics and widgets visible after wait: Total Leads, Today's Appointments, Conversion Rate, Total Calls, Upcoming Appointments, Leads by Source, Recent Leads.

Issue found:

- The mobile dashboard has horizontal overflow / a horizontal scrollbar.
- Observed viewport: `390x844`; document client width was `375`, scroll width was `401`.
- This appears to be a shell/header/page-width polish issue from the visual refresh, not a data or backend issue.

## Safety Notes

No workflow toggles, sends, SMS, email, payments, calendar actions, webhook actions, integration connects, or data mutations were triggered during this QA pass.

## Decision

Do not proceed to Phase 2 build yet. Ask Lovable for a small Phase 1 QA fix for the mobile horizontal overflow only, then re-run a quick desktop/mobile smoke QA.
