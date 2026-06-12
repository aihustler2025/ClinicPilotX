# ClinicPilotX Phone Number Standard

Last updated: 2026-06-12.

## Decision

ClinicPilotX should store phone numbers in E.164 format and display them in a user-friendly localized format.

For U.S. and Canada:

- User types digits only: `5558878888`
- UI display while typing should become: `+1 (555) 887-8888`
- Database/API value should be stored as: `+15558878888`

This gives staff the clean form Ross wants while keeping the data ready for Twilio, VAPI, SMS, voice, and future automation tools.

## Why

E.164 is the right integration format for telephony tools. Twilio documents E.164 as globally unique, starting with `+`, using decimal digits, and limited to 15 digits. Twilio examples include `+14155552671` for a U.S. number.

Google's libphonenumber exists specifically for parsing, formatting, and validating international phone numbers. Its supported behavior includes validation and an `AsYouTypeFormatter`, which is exactly the user experience ClinicPilotX needs.

Reference sources:

- Twilio E.164 glossary: `https://www.twilio.com/docs/glossary/what-e164`
- Google libphonenumber: `https://github.com/google/libphonenumber`

## Product Rules

- Store one canonical value in E.164, for example `+15558878888`.
- Do not store brackets, spaces, or dashes as the canonical database value.
- Display a friendly localized value in UI, for example `+1 (555) 887-8888` for U.S./Canada.
- Let staff type digits only after choosing country.
- Auto-format as the user types.
- Validate using libphonenumber-style metadata, not a hand-written regex.
- Keep country/region as explicit metadata when possible.
- Use the same phone input component across Leads, Patients, Staff, Settings, and any future intake forms.
- Existing records should be normalized carefully, without losing the original raw value if a number cannot be parsed.

## Fields To Prefer

Recommended database/application shape:

- `phone_e164`: canonical value for integrations, such as `+15558878888`
- `phone_country`: ISO country/region code, such as `US` or `CA`
- `phone_display`: optional derived display value, such as `+1 (555) 887-8888`
- `phone_raw`: optional original user-entered text for migration/debug only
- `phone_valid`: boolean validation result if needed

The canonical integration value is `phone_e164`.

## UI Requirement

The phone field should look and behave like this:

1. Country picker with flag and country code.
2. Single phone input next to it.
3. For U.S./Canada, typing `5558878888` displays as `+1 (555) 887-8888`.
4. Staff never need to type parentheses, spaces, or hyphens.
5. Invalid numbers show a clear inline message.

## Current ClinicPilotX Notes

Leads now has a country-aware phone field, but the current visible formatting still needs refinement to match Ross's requested U.S./Canada display exactly.

Patients still needs the same upgraded phone input behavior as Leads. The Add Patient form should not remain on a plain phone input if Leads has the better component.

Patients export should also be upgraded to a scoped export dialog similar to Leads export.
