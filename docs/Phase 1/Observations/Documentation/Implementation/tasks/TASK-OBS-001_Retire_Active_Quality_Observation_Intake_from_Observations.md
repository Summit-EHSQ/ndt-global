## TASK-OBS-001: Retire Active Quality Observation Intake from Observations

| Field | Value |
|---|---|
| Application | Observations |
| Theme | Cleanup, Decommissioning, and Legacy Quality Observation Handling |
| Task Number | TASK-OBS-001 |

### Task Name

Retire Active Quality Observation Intake from Observations

### Task Description

Remove `Quality Observation` as an active frontline intake path within the Observations application while preserving existing historical records. The future-state Observations model should focus on Hazard ID / HSE observation needs rather than Quality Observation intake.

### Specific Technical Changes Required

- Hide or remove the `Add Quality Observation` tab/menu entry from the Observations module for non-admin users.
- Remove or hide active user navigation to Quality Observation add/detail views where those views are used as Quality Observation intake forms.
- Preserve existing `Quality Observation` records and object configuration for historical access unless a separate approved data-retention or migration strategy directs otherwise.
- Update Observations landing page labels so the primary active intake path points users to `Add a Hazard ID` or the approved HSE Observation / Hazard ID label.
- Restrict direct record creation permissions for `Quality Observation` to admin/support roles only, if object-level security allows this without affecting historical record visibility.
- Add an admin-only note or internal configuration comment identifying `Quality Observation` as legacy/transitional.

### Unit Tests

- Log in as an Observations Reporter and confirm `Add Quality Observation` is no longer visible.
- Log in as an Observations Supervisor and confirm existing Quality Observation records remain accessible if historical read access is required.
- Attempt to create a new Quality Observation as a standard reporter and confirm creation is blocked or the entry path is unavailable.
- Log in as Observations Admin and confirm historical Quality Observation configuration remains accessible for support.
- Confirm `Add a Hazard ID` or the approved HSE entry path remains visible and usable.
- Confirm no historical Quality Observation records are deleted or modified by the configuration change.

### Source Gap / Requirement Reference

GAP-001; REQ-003

### Configuration Impact Area

Forms / Navigation / Security / Historical Data Preservation

### Dependencies / Sequencing Notes

Depends on business confirmation of whether Quality Observation should be hidden, preserved read-only, or fully retired. Complete before active Hazard ID reporting and security cleanup.
