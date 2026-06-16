## TASK-OBS-012: Secure Historical Quality Observation Access Separately from HSE Hazard ID Access

| Field | Value |
|---|---|
| Application | Observations |
| Theme | Security, Roles, and Permissions |
| Task Number | TASK-OBS-012 |

### Task Name

Secure Historical Quality Observation Access Separately from HSE Hazard ID Access

### Task Description

Separate access to legacy Quality Observation records from active HSE Hazard ID access so Quality and HSE ownership remain distinct.

### Specific Technical Changes Required

- Define which roles may view historical Quality Observation records.
- Define which roles may edit historical Quality Observation records, if any.
- Apply object/view permissions to restrict Quality Observation add/edit functions.
- Apply inventory filters or view permissions so HSE active lists exclude legacy Quality records.
- Confirm Quality process owners have the access needed to retrieve historical Quality Observation information until the future Quality pathway is implemented.
- Document any temporary access exceptions.

### Unit Tests

- Log in as HSE Reporter and confirm no Quality Observation create/edit access exists.
- Log in as Quality historical viewer, if configured, and confirm historical Quality Observation records are visible.
- Confirm Quality historical viewer does not gain Hazard ID create/edit access unless separately assigned.
- Confirm Observations Admin can access historical Quality records for support.
- Confirm direct URL access to restricted Quality add/edit views is blocked for standard users.
- Confirm active Hazard ID inventories do not include Quality-only records.

### Source Gap / Requirement Reference

GAP-001; GAP-007; OQ-003

### Configuration Impact Area

Security / Historical Views / Permissions

### Dependencies / Sequencing Notes

Depends on `TASK-OBS-001`, `TASK-OBS-002`, and `TASK-OBS-011`.
