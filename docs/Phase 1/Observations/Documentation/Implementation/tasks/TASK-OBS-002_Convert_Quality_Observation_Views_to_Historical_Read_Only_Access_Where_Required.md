## TASK-OBS-002: Convert Quality Observation Views to Historical / Read-Only Access Where Required

| Field | Value |
|---|---|
| Application | Observations |
| Theme | Cleanup, Decommissioning, and Legacy Quality Observation Handling |
| Task Number | TASK-OBS-002 |

### Task Name

Convert Quality Observation Views to Historical / Read-Only Access Where Required

### Task Description

Update Quality Observation list and detail views so they support historical reference but do not encourage new Quality intake through Observations.

### Specific Technical Changes Required

- Rename relevant Quality Observation inventory views, where appropriate, to include a legacy indicator such as `Legacy Quality Observations` or equivalent approved label.
- Remove create/add buttons from Quality Observation inventory views for non-admin roles.
- Make editable Quality Observation detail sections read-only for non-admin users if historical review access is required.
- Hide or de-emphasize Quality-specific form fields from active Observations navigation, including `PAR/CAPA Required?`, `Observation Purpose`, `Observation Subtype`, and Quality-specific follow-up fields, where these are not needed for historical viewing.
- Confirm whether mobile profiles expose Quality Observation add/detail views.
- Hide or remove mobile add access for Quality Observation if present.
- Keep admin/support access available for troubleshooting, audit, and data correction if approved.

### Unit Tests

- Open the Quality Observation inventory as a reporter and confirm no new-record action is available.
- Open an existing Quality Observation as a reporter and confirm fields are read-only if read-only historical access is required.
- Open the same record as an admin and confirm admin support behavior matches the approved permission model.
- Confirm Quality Observation views are not listed as primary active Observations intake views.
- Confirm mobile navigation does not provide a Quality Observation add path for standard users.
- Confirm historical attachments or related Action Plan links remain visible where they existed before.

### Source Gap / Requirement Reference

GAP-001; OQ-003

### Configuration Impact Area

Views / Forms / Mobile / Security

### Dependencies / Sequencing Notes

Depends on `TASK-OBS-001` and the final decision for whether Quality Observation is hidden, retired, read-only, or repurposed.
