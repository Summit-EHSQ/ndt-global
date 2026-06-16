## TASK-OBS-020: Configure Hazard ID Workflow Due Date Reminder and Escalation Notifications

| Field | Value |
|---|---|
| Application | Observations |
| Theme | Notifications and Email Templates |
| Task Number | TASK-OBS-020 |

### Task Name

Configure Hazard ID Workflow Due Date Reminder and Escalation Notifications

### Task Description

Configure automated email notifications for Hazard ID workflow due dates and overdue escalation. For each active workflow stage, the responsible user should receive reminder notifications one day before the due date and on the due date. If the record becomes overdue, the responsible user should receive an overdue-specific reminder one day after the due date and every other day after that until the record is closed. If the record reaches three days overdue, the responsible user’s immediate supervisor should receive an escalation notification at the three-day overdue mark and every other day thereafter until the record is closed.

### Specific Technical Changes Required

- Create or update Hazard ID workflow email templates for pre-due reminder, due-today reminder, overdue responsible-user reminder, and supervisor escalation.
- Configure notification logic for each active Hazard ID workflow stage: `Draft` and `Review`.
- Send stage reminder notifications to the current responsible user for the active stage.
- For Draft-stage records, send reminders to the creating user / current Draft responsible user.
- For Review-stage records, send reminders to the HSE Manager responsible user or role recipient, based on the final assignment model.
- Configure the pre-due notification to trigger when the stage due date is one calendar day away.
- Configure the due-today notification to trigger on the stage due date.
- Configure overdue responsible-user notification to trigger one calendar day after the due date.
- Configure recurring overdue responsible-user notification every other calendar day after the first overdue reminder while the record remains open and overdue.
- Configure supervisor escalation notification to trigger when the record is three calendar days overdue.
- Configure recurring supervisor escalation every other calendar day after the first escalation while the record remains open and overdue.
- Configure all overdue reminder and escalation conditions to stop once the Hazard ID reaches `Closed`.
- Confirm the source for the responsible user’s immediate supervisor, such as Employee Profile supervisor, manager field, or another approved employee hierarchy field.
- If the Review stage is assigned to a role rather than a named user, confirm how supervisor escalation should work for role-based responsibility.
- Include key email merge fields where available: Hazard ID record number/name, current workflow stage, responsible user, due date, days overdue, link to the Hazard ID record, location / area, and reporter or creator.
- Use distinct subject lines for normal reminders versus overdue/escalation notifications.
- Ensure notifications do not send for legacy Quality Observation records.
- Ensure notifications do not send for Closed Hazard ID records.
- Document notification schedules, recipients, templates, and stop conditions.

### Unit Tests

- Create a Draft-stage Hazard ID with a due date two days in the future and confirm no reminder is sent yet.
- Adjust or simulate the due date to one day before due date and confirm the responsible user receives the pre-due reminder.
- Simulate the due date and confirm the responsible user receives the due-today reminder.
- Simulate one day after the due date while the record remains in Draft and confirm the responsible user receives the overdue reminder.
- Simulate three days after the due date while the record remains in Draft and confirm the responsible user’s immediate supervisor receives the escalation notification.
- Confirm overdue responsible-user reminders repeat every other day after the first overdue reminder while the record remains open.
- Confirm supervisor escalation reminders repeat every other day after the three-day overdue mark while the record remains open.
- Submit the record to Review and confirm Draft-stage reminder logic no longer applies.
- Confirm Review-stage reminders are sent to the HSE Manager responsible party according to the configured assignment model.
- Approve the record to Closed and confirm all reminder and escalation notifications stop.
- Reject a Review-stage record back to Draft and confirm reminder logic resets or recalculates based on the Draft-stage due date.
- Confirm no reminder or escalation notifications are sent for Closed records.
- Confirm no reminder or escalation notifications are sent for legacy Quality Observation records.
- Confirm email content includes the record link, stage, due date, and overdue language where applicable.
- Confirm escalation email is sent to the correct immediate supervisor based on the approved supervisor source.

### Source Gap / Requirement Reference

Updated user workflow notification requirement

### Configuration Impact Area

Notifications / Email Templates / Workflow Due Dates / Escalations / Employee Hierarchy / Security

### Dependencies / Sequencing Notes

Depends on `TASK-OBS-017`, `TASK-OBS-018`, and `TASK-OBS-019` because workflow stages, due dates, responsible-party assignment, and closure conditions must exist before reminder and escalation logic can be configured. Also depends on confirmation of the source field for the responsible user’s immediate supervisor. If Review responsibility remains role-based rather than user-based, escalation logic must be confirmed before build.
