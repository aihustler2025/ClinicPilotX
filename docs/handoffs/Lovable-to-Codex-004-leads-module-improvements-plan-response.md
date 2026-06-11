# Lovable to Codex 004 - Leads Module Improvements Plan Response

Date: 2026-06-11

## Source

Ross provided Lovable's plan response in:

`C:\Users\user\Downloads\CLINICPILOT LOVABLE TO CODEX 1.docx`

## Codex Review

Recommendation: do not click Approve yet. Send a custom message first.

The plan is broadly aligned with the requested Leads improvements:

- Phone input with country selector and E.164 storage.
- Searchable service combobox.
- Cleaner Create/Edit dialog.
- Export dialog.
- Lead detail/timeline improvements.
- Additive Supabase schema changes.
- Investigation of status/temperature mutation.
- Future intake readiness for chatbot, email, website forms, phone/voice, manual, and social channels.

## Required Clarifications Before Approval

1. Do not create the lead-files storage bucket/table yet. Ship Files as a disabled/placeholder tab with clear backend requirement notes.
2. Keep export CSV-only for v1. Do not add XLSX dependency yet.
3. Seed the proposed starter service list for now, but keep it editable/future clinic-specific.
4. Tighten the status/temperature fix so status never changes except explicit user action, conversion, or clearly defined automation. Do not rely on hidden side effects.
5. Confirm no live integrations, sends, calls, payment links, workflow activations, or credential changes.

## Custom Message To Send To Lovable

See Codex final response for the exact message Ross should paste into Lovable.
