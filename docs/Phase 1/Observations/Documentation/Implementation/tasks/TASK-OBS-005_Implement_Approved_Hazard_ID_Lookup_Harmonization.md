# TASK-OBS-005: Implement Approved Hazard ID Lookup Harmonization

| Field | Value |
|---|---|
| Application | Observations |
| Theme | Data Model and Lookup Configuration |
| Task Number | TASK-OBS-005 |

## Task Name

Implement Approved Hazard ID Lookup Harmonization

## Task Description

Apply approved NDT / Integra Hazard ID taxonomy changes after business review. This task must follow lookup export and decision approval because recaptioning existing values can affect historical reporting semantics.

## Specific Technical Changes Required

- Apply only approved lookup changes from the decision matrix produced in `TASK-OBS-004`.
- Add new approved values to `Hazard Type`, `Observation Area`, `Severity`, `Steps Taken`, `Safe/Unsafe`, or other Hazard ID lookup objects as required.
- Hide or deactivate superseded values instead of deleting them where historical records exist.
- Recaption existing values only when explicitly approved and historical reporting impact has been accepted.
- Update sort orders and display colors for severity-style values where applicable.
- Update dependent form filters, view filters, report filters, and mobile profiles to use the approved active value set.
- Document all changed lookup values, including old value, new value/action, effective date, and historical data impact.

## Unit Tests

- Create a new Hazard ID and confirm only approved active lookup values are available.
- Confirm hidden/deactivated values no longer appear for new records.
- Open historical records using hidden/deactivated values and confirm they still display and save as expected.
- Confirm new values appear in the intended order and with the correct severity formatting if applicable.
- Confirm affected inventory/report filters still return records.
- Confirm mobile views use the same active lookup values as desktop views.

## Source Gap / Requirement Reference

GAP-006; OQ-012

## Configuration Impact Area

Picklists / Admin Objects / Views / Reports / Mobile

## Dependencies / Sequencing Notes

Depends on `TASK-OBS-004` and master-data approval for Hazard ID lookup changes.
