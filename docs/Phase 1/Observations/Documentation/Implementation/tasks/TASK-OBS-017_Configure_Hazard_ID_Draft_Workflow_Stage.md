## TASK-OBS-017: Configure Hazard ID Draft Workflow Stage

| Field | Value |
|---|---|
| Application | Observations |
| Theme | Workflow and Status Logic |
| Task Number | TASK-OBS-017 |

### Task Name

Configure Hazard ID Draft Workflow Stage

### Task Description

Configure `Draft` as the initial Hazard ID workflow stage. The Draft stage is owned by the creating user and is due three calendar days after initial record creation. In this stage, the creator is responsible for completing the main detail section of the Hazard ID form. If the record is rejected from Review and returned to Draft, the HSE Manager’s review comments must be displayed prominently to the creator. Responsible users must be able to create related Event Action Plan records while the Hazard ID is in Draft.

### Specific Technical Changes Required

- Enable or confirm workflow is enabled on the Hazard ID object.
- Create or configure `Draft` as the initial workflow stage for new Hazard ID records.
- Configure Draft-stage responsibility to the creating user / record creator.
- Configure the Draft-stage due date as three calendar days after initial record creation.
- Configure the Draft form layout to allow the creator to complete the main Hazard ID detail section.
- Configure the main Hazard ID detail fields as editable by the creator during Draft.
- Configure requiredness rules for the main detail section fields needed before submission to Review.
- Add a Draft-stage workflow action such as `Submit for Review`.
- Configure `Submit for Review` to move the record from Draft to Review.
- If the record has been returned from Review, display `Review Comments` or the approved reviewer comment field prominently near the top of the Draft form.
- Make reviewer comments read-only to the creator in Draft.
- Hide reviewer comments in Draft when the record has not yet been rejected, unless the business prefers the field to appear blank.
- Allow the responsible Draft-stage user to create related Event Action Plan records.
- Confirm creator access to existing related Action Plan / Event Action Plan sections from the Draft form.

### Unit Tests

- Create a new Hazard ID as a standard reporter and confirm it enters `Draft`.
- Confirm the Draft responsible user is the creating user.
- Confirm the Draft due date is three calendar days after initial record creation.
- Confirm the creator can edit the main Hazard ID detail section in Draft.
- Attempt to submit the record without required Draft fields and confirm validation prevents submission.
- Complete required Draft fields and confirm `Submit for Review` moves the record to Review.
- Return a record from Review to Draft with review comments and confirm the comments display prominently in Draft.
- Confirm the creator cannot edit the reviewer comments in Draft.
- Confirm reviewer comments are hidden or blank for a Draft record that has never been rejected.
- Confirm the Draft responsible user can create a related Event Action Plan record.
- Confirm unauthorized users cannot edit another creator’s Draft record unless their role allows it.

### Source Gap / Requirement Reference

Updated user workflow requirement; Hazard ID two-stage workflow

### Configuration Impact Area

Workflow / Form Behavior / Required Fields / Assignment / Due Dates / Action Plans / Security

## Dependencies / Sequencing Notes

Requires confirmation of the Hazard ID main detail section fields. Depends on the reviewer comment field decision: reuse existing `Reviewer Comments` or create a new `Review Comments` field.
