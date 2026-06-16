## TASK-OBS-018: Configure Hazard ID Review Workflow Stage

| Field | Value |
|---|---|
| Application | Observations |
| Theme | Workflow and Status Logic |
| Task Number | TASK-OBS-018 |

### Task Name

Configure Hazard ID Review Workflow Stage

### Task Description

Configure the Hazard ID `Review` stage assigned to the `HSE Manager` role. The stage is due three calendar days after the record enters Review. In this stage, the HSE Manager reviews the submitted Hazard ID and either approves or rejects it. Approval moves the record to Closed. Rejection returns the record to Draft and requires review comments. Responsible users must be able to create related Event Action Plan records while the Hazard ID is in Review.

### Specific Technical Changes Required

- Create or configure `Review` as the second Hazard ID workflow stage.
- Configure Review-stage responsibility to the `HSE Manager` role.
- Create or confirm the `HSE Manager` security role/group exists.
- Configure the Review-stage due date as three calendar days after entering the Review stage.
- Configure the Review-stage form layout for HSE Manager review.
- Make core submitted Hazard ID detail fields visible and read-only to the HSE Manager unless edits by HSE Manager are approved.
- Add or confirm review fields, including `Review Comments` or reuse of existing `Reviewer Comments`.
- Add a Review-stage workflow action such as `Approve`.
- Configure `Approve` to move the record from Review to Closed.
- Add a Review-stage workflow action such as `Reject` or `Return for Revision`.
- Configure `Reject` to move the record from Review back to Draft.
- Configure `Review Comments` as required when executing the rejection action.
- Do not require review comments for approval unless separately approved.
- Ensure rejection comments are retained when the record returns to Draft.
- Allow the responsible Review-stage user to create related Event Action Plan records.
- Confirm the HSE Manager can access existing related Action Plan / Event Action Plan sections from the Review form.

### Unit Tests

- Submit a Hazard ID from Draft and confirm it enters `Review`.
- Confirm the Review responsible party is the `HSE Manager` role.
- Confirm the Review due date is three calendar days after entering Review.
- Log in as an HSE Manager and confirm the user can open the Review-stage record.
- Confirm submitted Hazard ID details are visible to the HSE Manager.
- Approve the record and confirm it moves to `Closed`.
- Submit another Hazard ID to Review and attempt to reject without comments; confirm rejection is blocked.
- Enter review comments and reject the record; confirm it returns to `Draft`.
- Confirm rejection comments are retained after the transition back to Draft.
- Confirm the HSE Manager can create a related Event Action Plan record in Review.
- Confirm non-HSE Manager users cannot approve or reject the Review-stage record.
- Confirm review comments are not required when approving unless separately configured.

### Source Gap / Requirement Reference

Updated user workflow requirement; Hazard ID two-stage workflow

### Configuration Impact Area

Workflow / Assignment / Due Dates / Review Fields / Action Handlers or Validation / Action Plans / Security

### Dependencies / Sequencing Notes

Depends on `TASK-OBS-017`. Requires `HSE Manager` role/group and final decision on reviewer comment field.
