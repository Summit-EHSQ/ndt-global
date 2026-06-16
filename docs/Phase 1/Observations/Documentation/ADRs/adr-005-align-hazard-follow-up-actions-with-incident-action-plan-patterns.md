---
adr: ADR-005
title: Align Hazard Follow-Up Actions with Incident Action Plan Patterns
status: accepted-in-principle
date: 2026-05-29
deciders:
  - Dave McLean
  - Niall Walsh
  - John Blackham
  - Lisa McLaughlin
consulted:
  - Tucker White
  - Brett Corpe
  - Michael Barthelmess
informed:
  - Branka Vidovic
---

## ADR-005: Align Hazard Follow-Up Actions with Incident Action Plan Patterns

### Context and Problem Statement

The current Hazard ID action plan model differs from the Incident Management action plan model. NDT requested consistency with the Incident Management approach, especially for how actions are created, assigned, and managed.

The discussion distinguished between submitter-provided immediate action information and reviewer-assigned formal follow-up actions.

### Decision Drivers

- Users benefit from consistent action plan fields and layout across HSE processes.
- HSE managers need control over who owns corrective actions and due dates.
- Most hazards may have a simple action path, but the process must support formal assignment.
- The action model should avoid records sitting in the system without ownership.
- The design should remain consistent with Incident Management where practical.

### Considered Options

1. **Keep the current Hazard ID action plan configuration**
   - Avoids configuration change.
   - Leaves inconsistency with Incident Management.

2. **Allow submitters to create the primary action plan during initial submission**
   - Captures action details quickly.
   - May not match NDT’s review and assignment model.

3. **Use reviewer-owned action assignment with Incident-aligned action plan structure**
   - Supports HSE manager control.
   - Aligns with Incident Management.
   - Requires workflow and form updates.

### Decision Outcome

Align Hazard ID follow-up actions with the Incident Management action plan pattern where practical. Submitters may capture what was observed and any immediate steps taken, but formal follow-up actions should be reviewed and assigned by the responsible HSE manager during the review workflow.

### Consequences

- Hazard ID forms and action grids may require configuration changes.
- The HSE manager review step becomes central to action assignment.
- The user experience should distinguish between immediate action taken and assigned follow-up action.
- Reporting on actions should become more consistent across HSE processes.

### More Information

The group discussed that most hazards may only require one action, but NDT’s process expects HSE review before formal action assignment.

---
