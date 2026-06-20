# Patient Profile Booking / Delete QA - 2026-06-20

## Scope

Codex performed a fresh Patients profile QA pass focused on:

- Creating a disposable dummy patient.
- Opening the patient profile side panel.
- Testing `Book Appointment` from the profile.
- Testing delete cancel/confirm behavior only on the disposable dummy patient.

Safety boundary:

- Dummy data only.
- TEST appointment mode only.
- No live calls.
- No live messages.
- No payments.
- No workflow activation.

## Disposable Test Patient

Created successfully:

- Name: `CPX TEST Disposable Patient Delete QA 20260620`
- Email: `cpx.test+delete-qa-20260620@example.com`
- Phone: `2135550199`
- Displayed phone after save: `+1 (213) 555-0199`
- Patient ID shown in profile: `#PT00028`

Result: pass.

## Patient Profile Panel

Opened the profile panel by clicking the patient name.

Verified:

- Profile side panel opens.
- Contact details show correct email and formatted phone.
- Notes display the dummy QA note.
- Profile actions are visible: `Call`, `Message`, `Video`, `Edit`, `Book Appointment`.
- Appointments tab initially showed `No appointments found`.

Result: pass for read-only profile display.

## Book Appointment From Patient Profile

Clicked `Book Appointment` from the patient profile.

Verified:

- Browser navigated to `/appointments`.
- `Book New Appointment` modal opened.
- Selected patient was prefilled as `CPX TEST Disposable Patient Delete QA 20260620 (#PT00028)`.
- Patient information was prefilled.
- TEST checkbox was checked before submit.
- TEST warning text was visible: no SMS, email, payment, or workflow sends should fire even if Automation Center workflows are active.

Result: partial pass with blocking save bug.

## Appointment Save Bug

Entered:

- Service: `CPX TEST Profile Booking Regression 20260620`
- Date: default `June 20th, 2026`
- Time: `15:30`
- Consultation type: `In-Person`
- Fee: `0`
- Notes: `Controlled QA booking from patient profile. TEST mode on. No live sends.`

Observed:

- First submit showed `Invalid time format (HH:MM)`.
- Inspecting the form after the first submit showed the native time input value was blank.
- Codex re-entered `15:30` and verified the time input value was `15:30`.
- Second submit still showed `Invalid time format (HH:MM)`.
- Modal stayed open.
- Appointment count stayed `27`.
- The test appointment was not created.

Expected:

- A native `input[type="time"]` value of `15:30` should pass validation if the expected format is `HH:MM`.
- A valid TEST appointment should save, show a success toast, increase the appointment count, appear in the list with a TEST badge, and remain safe from live sends.

Status: fail / blocking for patient-profile booking regression.

## Delete Patient QA

After returning to Patients, the page briefly showed `No Plan` and `No patients found`.

Reload restored:

- `Professional` plan state.
- Full Patients list.
- Disposable patient row.

Codex filtered Patients to the disposable patient and opened its row action menu.

Verified actions:

- `View Details`
- `Edit Patient`
- `Delete Patient`

Clicking `Delete Patient` triggered the native browser confirmation dialog. As in the previous pass, the native confirmation froze the browser automation connector before Codex could safely dismiss or accept the dialog.

Codex did not intentionally accept deletion.

Status: delete is guarded, but cancel/confirm behavior remains unverified because the native browser confirm blocks reliable QA automation.

Expected:

- Replace native browser confirm with an in-app confirmation modal/dialog.
- Cancel should close the modal and leave the patient row intact.
- Confirm should delete only the selected disposable patient and show clear success/failure feedback.
- Delete should never affect unrelated patient records.

## Additional Reconfirmed Issue

The subscription/data-load flicker still occurs:

- Patients briefly showed `No Plan`.
- Patients list briefly showed `No patients found`.
- Reload restored `Professional` and the real patient list.

This remains a separate known issue.

## Recommendation

Create a Lovable plan-mode fix request for:

1. Patient-profile `Book Appointment` time validation/save bug.
2. Replacing native patient delete confirm with an in-app confirmation modal.
3. Keeping all appointment QA rows in TEST mode with no live sends.

