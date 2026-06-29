# Request 042 - Auto-Assignment Phase A QA

Date: 2026-06-29

## Scope

Ross approved and published Lovable's standalone Phase A Auto-Assignment fix.

Lovable reported:

- migration created `assignment_rules` with clinic-scoped RLS,
- migration added `profiles.max_active_conversations`,
- Auto-Assignment page scopes queries by `clinic_id`,
- loading state now clears,
- Retry appears on error instead of spinning forever.

## Result

Partial pass / follow-up required.

The page is no longer stuck on `Loading assignment rules...`, but several core interactions are still broken or misleading.

## What Passed

### Page Load

Observed on `https://clinic-pilot-x.lovable.app/auto-assignment`:

- Page loads behind authenticated session.
- Header shows `Professional`.
- `Loading assignment rules...` is gone.
- Page shows `Assignment Rules (0)`.
- Page shows `Staff Configuration (2)`.
- Staff rows render:
  - Kizha Kaye / `kizha.buzzooka@gmail.com`
  - `teambuzzooka@gmail.com`
- No console error appeared on initial page load.

### Create Rule Persistence After Reload

Created disposable QA rule:

`QA TEST AUTO ASSIGN 20260629-A`

Observed:

- Toast showed `Rule created successfully`.
- Immediately after save, the page still showed `Assignment Rules (0)` and did not show the new rule.
- After browser reload, the rule appeared and count changed to `Assignment Rules (1)`.

Conclusion: insert persists, but the UI does not refresh/update after create without reload.

### Delete Rule Persistence After Reload

Clicked the rule's icon-only delete action.

Observed:

- Toast showed `Rule deleted successfully`.
- Immediately after delete, the page still showed `Assignment Rules (1)` and the QA rule remained visible.
- After browser reload, the QA rule was gone and count returned to `Assignment Rules (0)`.

Conclusion: delete persists, but the UI does not refresh/update after delete without reload.

### Workflow Safety

Opened Automation Center Activity Logs after the Auto-Assignment QA.

Observed:

- No `just now`, `seconds ago`, or fresh minute-level workflow rows appeared.
- Newest visible rows remained about `10 days ago`.

No email, SMS, call, payment, calendar, webhook, chatbot/API, or workflow test-send action was clicked.

## What Failed

### Toggle Rule Active/Inactive Does Not Work

After creating and reloading the QA rule, Codex clicked the rule's active switch.

Observed:

- Switch remained `aria-checked="true"`.
- Text remained `Active`.
- Coordinate click on the visible switch also did not change state.
- No successful inactive state was observed.

Expected:

- Switch toggles to inactive.
- Row badge/text updates to `Inactive`.
- Value persists after reload.

### Staff Max Conversations Save Does Not Persist

Opened Configure for Kizha Kaye.

Changed Max Active Conversations from `10` to `12` and clicked Save Changes.

Observed:

- Toast showed `Staff settings updated successfully`.
- The row still showed `Max conversations: 10`.
- After browser reload, it still showed `Max conversations: 10`.

Expected:

- Row updates to `Max conversations: 12`.
- Value persists after reload.

### UI Accessibility / Feedback Issues

Observed:

- Rule delete button is icon-only and unlabeled.
- Dialog warning appears in console: `Missing Description or aria-describedby={undefined} for {DialogContent}`.
- Create/delete show success toasts even though the visible list remains stale until reload.
- Staff save shows success even though the changed value does not persist.

## Safety

Codex did not trigger any live integration or Automation Center send/test action.

The disposable QA rule was removed and confirmed gone after reload.

## Recommended Next Step

Send Lovable a focused fix request.

Do not proceed to visual refresh Phase B until Auto-Assignment's core CRUD behavior is actually correct.

Required follow-up:

- fix immediate UI refresh after create/delete,
- fix toggle active/inactive,
- fix staff max-conversations persistence or remove/disable the staff save action until it works,
- add accessible labels/descriptions to the delete action and dialogs,
- keep scope limited to Auto-Assignment only.
