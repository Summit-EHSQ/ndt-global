# TASK-OBS-011: Redesign Observations Security Groups for HSE Ownership Model

| Field | Value |
|---|---|
| Application | Observations |
| Theme | Security, Roles, and Permissions |
| Task Number | TASK-OBS-011 |

## Task Name

Redesign Observations Security Groups for HSE Ownership Model

## Task Description

Update Observations security so access aligns to HSE Hazard ID ownership and no longer grants broad mixed Quality/HSE access by default. Existing Observations security groups should be reused where practical but revised to support the future HSE ownership model.

## Specific Technical Changes Required

- Review current permissions assigned to `Observations Admin`, `Observations Supervisor`, and `Observations Reporter`.
- Define future HSE roles such as HSE Hazard Reporter, HSE Hazard Supervisor / Reviewer, and HSE Observations Admin.
- Create or confirm the `HSE Manager` role/group required for Hazard ID Review-stage responsibility.
- Remove or restrict Quality Observation create/edit permissions from HSE reporter/supervisor roles.
- Preserve historical Quality Observation read permissions only for approved roles.
- Grant Hazard ID create/read/edit permissions according to role responsibilities.
- Grant Review-stage permissions to the `HSE Manager` role.
- Align module tab and view visibility with the selected navigation model.
- Document any users/groups that require migration from old Observations groups to new or revised HSE groups.

## Unit Tests

- Log in as HSE Reporter and confirm the user can create Hazard ID records.
- Confirm HSE Reporter cannot create Quality Observation records.
- Log in as HSE Manager and confirm the user can access Review-stage Hazard ID records.
- Confirm HSE Manager can approve or reject records only in the appropriate workflow stage.
- Log in as Quality-only user and confirm the user does not receive unnecessary Hazard ID access.
- Log in as Observations Admin and confirm admin can access required support/configuration views.
- Confirm hidden navigation links are not accessible through direct URL for unauthorized roles.

## Source Gap / Requirement Reference

GAP-007; REQ-007; Updated workflow requirement

## Configuration Impact Area

Security Groups / Roles / View Permissions / Object Permissions / Workflow Permissions

## Dependencies / Sequencing Notes

Depends on decisions for Quality retirement, Hazard ID navigation placement, and final `HSE Manager` role membership. Must be completed before UAT.
