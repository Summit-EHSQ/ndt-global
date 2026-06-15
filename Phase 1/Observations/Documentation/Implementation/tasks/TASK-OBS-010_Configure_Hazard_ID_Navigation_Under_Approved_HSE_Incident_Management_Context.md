# TASK-OBS-010: Configure Hazard ID Navigation Under Approved HSE / Incident Management Context

| Field | Value |
|---|---|
| Application | Observations |
| Theme | Navigation and Cross-Application UX |
| Task Number | TASK-OBS-010 |

## Task Name

Configure Hazard ID Navigation Under Approved HSE / Incident Management Context

## Task Description

Surface Hazard ID in the approved HSE navigation context, potentially under Incident Management, while keeping the underlying object in Observations if that remains the approved architecture.

## Specific Technical Changes Required

- Confirm approved navigation model: Observations only, Incident Management only, or both Observations and Incident Management.
- If approved, add or expose Hazard ID add/list/my-list tabs within the Incident Management or HSE navigation area.
- Reuse existing Hazard ID views where possible rather than duplicating object configuration.
- Ensure links point to the existing `Hazard ID` object and approved add/detail/inventory views.
- Hide duplicate/conflicting navigation entries if the approved model requires a single HSE entry point.
- Update security so users accessing Hazard ID through Incident Management have appropriate Observations object/view permissions.
- Validate existing Incident Management Observation views to determine whether they should be retained, renamed, hidden, or linked.

## Unit Tests

- Log in as an HSE reporter and confirm Hazard ID is accessible from the approved HSE / Incident Management navigation location.
- Create a Hazard ID from the new navigation location and confirm the record is saved on the existing Hazard ID object.
- Confirm the same record appears in the approved Hazard ID inventory.
- Confirm users without Hazard ID access do not gain access through the new navigation link.
- Confirm there are no duplicate confusing add paths unless dual placement is intentionally approved.
- Confirm existing Observations Hazard ID links still work or are hidden according to the approved model.

## Source Gap / Requirement Reference

GAP-003; OQ-002

## Configuration Impact Area

Cross-Application Navigation / Views / Security

## Dependencies / Sequencing Notes

Depends on final decision for whether Hazard ID remains in Observations, is surfaced under Incident Management, or appears in both places. Coordinate with the Incident Management configuration owner.
