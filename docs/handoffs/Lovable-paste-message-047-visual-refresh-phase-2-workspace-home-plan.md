# Lovable Paste Message 047 - Phase 2 Workspace Home Plan Request

Please respond in Plan mode only. Do not build yet.

Codex re-QA passed Phase 1 and the mobile overflow fix:

- Desktop dashboard/header/sidebar visual refresh passed.
- Mobile dashboard horizontal overflow is fixed.
- Dashboard still shows Professional.
- Automation Center still shows Professional and `7 / 13 Active`.
- Auto-Assignment still loads.
- Subscription still shows `Current Plan: Professional` and `Status: Active`.

Now please propose Phase 2 for the subscriber-facing Workspace Home / onboarding experience.

Product goal:

ClinicPilotX is a multi-client subscription product. Each subscriber clinic needs a clear, friendly setup/home area where they can understand and complete their clinic workspace setup without feeling like they are buried in developer/admin Settings.

Please use Lovable's UX/UI judgment. Do not copy the reference designs exactly. Use them only as inspiration for a clean, professional SaaS experience that matches the Phase 1 visual direction.

Phase 2 planning requirements:

1. Recommend the best IA/location for Workspace Home / Clinic Setup:
   - Should it be a dedicated `/workspace` route?
   - Should there be a top-bar clinic/workspace switcher entry point?
   - What should remain in Settings vs move into the workspace setup experience?

2. Propose the subscriber workflow in plain language:
   - Business profile.
   - Branding/logo.
   - Hours of operation.
   - Services and pricing guidance.
   - Team/roles overview.
   - Knowledge FAQs.
   - Knowledge Sources placeholder for the later knowledge base phase.
   - AI guardrails.
   - Integrations status.

3. Keep this plan UI-first and safe:
   - No migrations.
   - No RLS/grant changes.
   - No edge function changes.
   - No workflow execution changes.
   - No sends, payments, calendar writes, live OAuth, or webhook ingestion.
   - No fake production metrics.
   - No live credentials.

4. Explain what files/routes/components you would change in Phase 2 if approved.

5. Include QA steps for Codex after build, including:
   - Desktop smoke.
   - Mobile smoke.
   - Settings deep-link compatibility.
   - Subscription/Professional display check.
   - No workflow/log side effects.

Do not build until Ross/Codex explicitly approve the Phase 2 plan.
