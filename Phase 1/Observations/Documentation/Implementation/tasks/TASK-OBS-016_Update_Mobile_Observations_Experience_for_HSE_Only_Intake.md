# TASK-OBS-016: Update Mobile Observations Experience for HSE-Only Intake

| Field | Value |
|---|---|
| Application | Observations |
| Theme | Mobile or Offline Behavior |
| Task Number | TASK-OBS-016 |

## Task Name

Update Mobile Observations Experience for HSE-Only Intake

## Task Description

Align mobile Observations navigation and forms with the future HSE-focused Hazard ID model. The current package includes mobile view profiles, so mobile must be updated consistently with desktop changes.

## Specific Technical Changes Required

- Review mobile profiles for Hazard ID detail, Hazard ID inventory, Work Observation detail, and Work Observation inventory.
- Remove or restrict mobile Quality Observation add/edit access for standard users.
- Ensure mobile Hazard ID add/detail forms show approved definition guidance.
- Update mobile labels to the approved Hazard ID / HSE Observation term where applicable.
- Ensure mobile picklists reflect approved active Hazard ID values after harmonization.
- Confirm mobile inventory views exclude Quality Observation records from active HSE lists.

## Unit Tests

- Log in on mobile as an HSE reporter and confirm the Hazard ID / HSE entry path is visible.
- Confirm mobile does not show active Quality Observation add access for standard users.
- Create a mobile Hazard ID and confirm it appears in desktop Hazard ID inventory.
- Confirm mobile guidance text is visible and legible.
- Confirm mobile picklists exclude hidden/deactivated values.
- Confirm mobile security matches desktop access rules.

## Source Gap / Requirement Reference

GAP-001; GAP-002; GAP-004; GAP-005

## Configuration Impact Area

Mobile Views / Forms / Picklists / Security

## Dependencies / Sequencing Notes

Depends on `TASK-OBS-003`, `TASK-OBS-005`, `TASK-OBS-006`, `TASK-OBS-010`, and `TASK-OBS-011`.
