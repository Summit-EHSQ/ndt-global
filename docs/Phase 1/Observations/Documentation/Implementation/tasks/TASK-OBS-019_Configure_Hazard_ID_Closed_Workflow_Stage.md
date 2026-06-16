## TASK-OBS-019: Configure Hazard ID Closed Workflow Stage

| Field | Value |
|---|---|
| Application | Observations |
| Theme | Workflow and Status Logic |
| Task Number | TASK-OBS-019 |

### Task Name

Configure Hazard ID Closed Workflow Stage

### Task Description

Configure the Hazard ID `Closed` stage reached when the HSE Manager approves the record. Closed records should preserve the submitted Hazard ID details, review outcome, review comments if present, and related Event Action Plan records. Responsible or authorized users must be able to create related Event Action Plan records in Closed if post-closure action planning is required.

### Specific Technical Changes Required

- Create or configure `Closed` as the terminal Hazard ID workflow stage.
- Configure the `Approve` action from Review to transition the record to Closed.
- Configure Closed-stage form behavior so submitted Hazard ID details are read-only for standard users.
- Show review outcome information and reviewer comments where appropriate.
- Confirm whether Closed records can be reopened; if not, do not configure a reopen action.
- Confirm whether Event Action Plan records may be created after closure.
- If post-close action planning is required, allow authorized/responsible users to create related Event Action Plan records in Closed.
- If post-close action planning is not required, make Action Plan sections read-only in Closed.
- Confirm Closed records remain visible in historical/list views and reports.
- Ensure Closed-stage permissions prevent unauthorized edits to core Hazard ID and review fields.

### Unit Tests

- Approve a Review-stage Hazard ID and confirm it enters `Closed`.
- Confirm standard users cannot edit core Hazard ID details after closure.
- Confirm review outcome information is visible on the Closed record.
- Confirm reviewer comments remain visible if entered before closure or during prior review activity.
- Confirm no reopen action is available unless explicitly approved.
- Confirm authorized users can create a related Event Action Plan in Closed if post-close action planning is required.
- Confirm unauthorized users cannot edit closed Hazard ID fields.
- Confirm Closed records appear in the appropriate Hazard ID inventory/reporting views.
- Confirm Closed records no longer appear in active Draft or Review work queues unless intentionally included.

### Source Gap / Requirement Reference

Updated user workflow requirement; Hazard ID approval and closure behavior

### Configuration Impact Area

Workflow / Closed-State Form Behavior / Action Plans / Security / Reporting

### Dependencies / Sequencing Notes

Depends on `TASK-OBS-018`. Requires decision on whether Action Plans may be created after closure and whether any reopen behavior is required.
