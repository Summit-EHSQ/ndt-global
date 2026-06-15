# TASK-INC-001: Add Hazard ID Entry Point to Incident Management HSE Navigation

| Field | Value |
|---|---|
| Application | Incident Management |
| Theme | Cross-Application User Experience |
| Task Number | TASK-INC-001 |

## Task Name

Add Hazard ID Entry Point to Incident Management HSE Navigation

## Task Description

If the approved UX model is “one HSE place to go,” add Hazard ID access under Incident Management or the HSE landing experience while retaining the underlying Observations object. This supports clear separation of HSE and Quality navigation without object migration.

## Specific Technical Changes Required

- Add a menu/tab/link in the Incident Management or HSE navigation area labeled with the approved Hazard ID / HSE Observation term.
- Link the navigation item to the existing Observations Hazard ID add form or approved inventory view.
- Add a `My Hazard IDs` or equivalent link if reporter self-service access is required.
- Confirm the navigation placement does not imply that Hazard ID is an Incident or Near Miss record.
- Apply permission checks so the link is visible only to approved HSE roles.
- Add guidance text in the Incident / HSE landing context distinguishing Hazard ID from Near Miss and Incident.

## Unit Tests

- Log in as an HSE reporter and confirm the Hazard ID link appears in the Incident / HSE navigation area.
- Select the link and confirm the correct Hazard ID form or inventory opens.
- Create a test Hazard ID and confirm it does not create an Incident record.
- Log in as a Quality-only user and confirm the Hazard ID link is not visible unless explicitly approved.
- Log in as an Incident Management admin and confirm the link appears if admin access is expected.
- Confirm the definition guidance is visible from the HSE landing context.

## Source Gap / Requirement Reference

GAP-003; GAP-004; OQ-002

## Configuration Impact Area

Navigation / Cross-Application UX / Security

## Dependencies / Sequencing Notes

Only proceed if the approved architecture decision is to surface Hazard ID under Incident Management or a consolidated HSE navigation context.
