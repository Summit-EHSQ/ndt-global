# TASK-OBS-003: Deactivate `Quality` from Active Safe/Unsafe/Quality Classification Use

| Field | Value |
|---|---|
| Application | Observations |
| Theme | Data Model and Lookup Configuration |
| Task Number | TASK-OBS-003 |

## Task Name

Deactivate `Quality` from Active Safe/Unsafe/Quality Classification Use

## Task Description

Prevent `Quality` from being selected for future HSE Hazard ID / Observations records while preserving historical records that already use the value.

## Specific Technical Changes Required

- Locate the existing `Safe/Unsafe/Quality` lookup or equivalent picklist used by Observations.
- Confirm all form fields, filters, action handlers, and reports that reference the `Quality` value.
- Hide, deactivate, or otherwise remove `Quality` from future user selection without deleting the value.
- Confirm current action handler logic that sets `SafeUnsafe` based on severity does not assign or require the `Quality` value.
- Update any form labels that still present the field as `Safe/Unsafe/Quality`; use an approved HSE label such as `Safe/Unsafe` if confirmed.
- Update relevant inventory view filters so active HSE lists do not include records classified as `Quality`, unless specifically viewing legacy/historical records.

## Unit Tests

- Create a new Hazard ID / HSE observation and confirm `Quality` is not available in the classification selection.
- Open an existing historical record with `Quality` selected and confirm the value still displays correctly.
- Save an existing historical `Quality` record without changing the value and confirm the save does not fail.
- Create a record with severity populated and confirm the existing Safe/Unsafe auto-population logic still behaves as expected.
- Confirm active HSE inventory views exclude `Quality` records unless the view is intentionally historical.
- Confirm no lookup value was deleted from the database or configuration export.

## Source Gap / Requirement Reference

GAP-005; REQ-003

## Configuration Impact Area

Fields / Picklists / Business Logic / Reports

## Dependencies / Sequencing Notes

Depends on `TASK-OBS-001`. Do not recaption or delete the value without historical reporting approval.
