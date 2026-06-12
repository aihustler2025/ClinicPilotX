# Leads Export QA - 2026-06-12

Live app:

`https://clinic-pilot-x.lovable.app/leads`

## Scope

Focused QA pass for the Leads export workflow after Lovable's Leads v2 and QA-fix builds were published.

## Result

Status: partially verified.

The export dialog is materially improved and supports user-facing export choices, but Codex could not verify the downloaded CSV file contents because the Codex in-app browser reports that downloads are not supported. Chrome extension control was not available in this session, so file-content verification remains pending.

## Verified

- Leads page loaded with `Professional` plan after using the page Refresh control.
- Leads page showed 15 total leads during this pass.
- Export button opened an `Export Leads to CSV` dialog.
- Dialog offered export scope choices:
  - `All leads (15)`
  - `Current filters (15)`
  - `Selected only (0)`
- `Current filters (15)` was selected by default.
- `Selected only (0)` was disabled because no leads were selected.
- Dialog offered column selection:
  - Name
  - Email
  - Phone
  - Source
  - Service
  - Status
  - Temperature
  - Score
  - Preferred Contact
  - Urgency
  - Notes
  - Created
- Column toggles are interactive. Codex unchecked `Phone` and verified it changed from checked to unchecked.
- Dialog showed the estimated row count: `15 rows will be exported`.

## Not Verified

- Actual CSV download completion.
- CSV filename.
- CSV header row.
- Whether unchecked columns are excluded from the downloaded CSV.
- Whether `Current filters` exports only the filtered table when filters/search are active.
- Whether phone values in CSV are E.164, formatted display values, or both.

## Additional Issue Reconfirmed

The subscription/data-load flicker still exists. On first reconnect to the Leads page, the app showed `No Plan` and 0 leads. Clicking the page `Refresh` button restored `Professional` state and 15 leads. This should remain open as an app-state consistency issue.

## Recommendation

Do not ask Lovable for another Leads export build yet unless Ross wants the CSV contents verified immediately by manual Chrome download. The UI portion now matches the requested direction well enough to continue QA into Patients edit and Appointments booking persistence.

Before marking Leads export complete, verify with a real browser download:

1. Export all/current-filtered leads.
2. Uncheck one column, such as Phone.
3. Download CSV.
4. Open the CSV.
5. Confirm row count, headers, selected columns, filename, and filtered-scope behavior.
