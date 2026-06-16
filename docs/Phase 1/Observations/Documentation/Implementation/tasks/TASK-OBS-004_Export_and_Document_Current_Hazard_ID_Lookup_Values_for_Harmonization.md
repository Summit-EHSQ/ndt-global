## TASK-OBS-004: Export and Document Current Hazard ID Lookup Values for Harmonization

| Field | Value |
|---|---|
| Application | Observations |
| Theme | Data Model and Lookup Configuration |
| Task Number | TASK-OBS-004 |

### Task Name

Export and Document Current Hazard ID Lookup Values for Harmonization

### Task Description

Prepare the Hazard ID taxonomy for NDT / Integra harmonization before any lookup value changes are made.

### Specific Technical Changes Required

- Export current values for `Hazard Type`, `Observation Area`, `Severity`, `Steps Taken`, `Safe/Unsafe`, and any Hazard ID-related lookup fields.
- Include current value name, internal identifier/key if available, active/inactive status, sort order, color or severity formatting where applicable, and count of historical records using each value if query access is available.
- Identify duplicate, overlapping, or legacy values for business review.
- Produce a configuration decision matrix with actions: `Retain`, `Add`, `Hide/Deactivate`, `Recaption`, or `Requires Decision`.
- Do not implement recaptioning or deletion during this task.
- Flag values used by reports, filters, action handlers, or mobile views.

### Unit Tests

- Confirm each exported lookup list matches the values visible in the admin/configuration UI.
- Confirm at least one sample Hazard ID record using each high-use value still opens successfully.
- Confirm the export includes internal identifiers or stable references where available.
- Confirm values used in reports or filters are flagged in the decision matrix.
- Confirm no lookup values are changed, hidden, or deleted as part of this task.

### Source Gap / Requirement Reference

GAP-006; REQ-008

### Configuration Impact Area

Administrative Configuration / Master Data / Reporting Impact Analysis

### Dependencies / Sequencing Notes

Must be completed before `TASK-OBS-005`.
