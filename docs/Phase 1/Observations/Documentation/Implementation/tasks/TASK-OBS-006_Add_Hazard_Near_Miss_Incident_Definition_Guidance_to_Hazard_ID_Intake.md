## TASK-OBS-006: Add Hazard / Near Miss / Incident Definition Guidance to Hazard ID Intake

| Field | Value |
|---|---|
| Application | Observations |
| Theme | Form Layout and User Experience |
| Task Number | TASK-OBS-006 |

### Task Name

Add Hazard / Near Miss / Incident Definition Guidance to Hazard ID Intake

### Task Description

Add user-facing guidance to reduce misclassification between Hazard ID, Near Miss, and Incident. The form should guide users to select Hazard ID only when a hazard or condition is identified before an event or impact occurs.

### Specific Technical Changes Required

- Add instructional text to the Hazard ID add/detail view near the top of the form.
- Include approved concise definitions for `Hazard ID`, `Near Miss`, and `Incident`.
- Add guidance telling users to use Hazard ID only when no event or impact has occurred.
- Add redirect guidance such as: “If an event occurred without impact, use Near Miss.” and “If impact occurred, use Incident.”
- Confirm whether guidance should be implemented as static form text, help icon text, section text, or a decision prompt.
- Update mobile Hazard ID detail/add view with equivalent concise guidance if mobile intake is in use.

### Unit Tests

- Open the desktop Hazard ID add form and confirm definition guidance appears before or near classification fields.
- Open an existing Hazard ID and confirm the guidance is visible without blocking record review.
- Open the mobile Hazard ID form and confirm guidance is visible or accessible.
- Confirm the guidance does not make unrelated fields required or hidden.
- Confirm the wording uses the approved definitions and labels.

### Source Gap / Requirement Reference

GAP-004; REQ-001

### Configuration Impact Area

Forms / Help Text / Mobile UX

### Dependencies / Sequencing Notes

Depends on confirmation of final definitions for Hazard ID, Near Miss, and Incident.
