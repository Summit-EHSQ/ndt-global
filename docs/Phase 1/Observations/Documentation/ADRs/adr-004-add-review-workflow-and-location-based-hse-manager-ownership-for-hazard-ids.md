---
adr: ADR-004
title: Add Review Workflow and Location-Based HSE Manager Ownership for Hazard IDs
status: accepted-in-principle
date: 2026-05-29
deciders:
  - Dave McLean
  - Niall Walsh
  - John Blackham
  - Lisa McLaughlin
  - Brett Corpe
  - Øyvind Heimli
consulted:
  - Tucker White
  - Michael Barthelmess
informed:
  - Branka Vidovic
---

## ADR-004: Add Review Workflow and Location-Based HSE Manager Ownership for Hazard IDs

### Context and Problem Statement

The out-of-the-box observation model was described as primarily a data capture mechanism without a strong review workflow. NDT’s current process expects submitted observations to be reviewed by the relevant HSE manager before they are visible or processed more broadly and before actions are assigned.

The existing Integra configuration includes review-related fields, but the meeting suggested that the process should be more explicitly represented as workflow.

### Decision Drivers

- HSE needs quality control over incoming hazard submissions.
- Submitted records should have clear ownership.
- Reviewers need to validate the submission and assign appropriate actions.
- The process should support location-based responsibility.
- Multiple possible reviewers may exist for a location.

### Considered Options

1. **No formal review workflow**
   - Simpler configuration.
   - Leaves ownership and follow-up unclear.
   - Does not match NDT’s current process.

2. **Submitter assigns actions directly at intake**
   - Allows fast capture when the action is obvious.
   - May assign work to the wrong owner or due date.
   - Does not provide HSE review control.

3. **Submitted Hazard IDs route to a location-based HSE manager role for review**
   - Aligns with NDT’s process.
   - Provides review and action assignment control.
   - Requires role mapping by location.

### Decision Outcome

Add a review workflow for Hazard ID records. Submitted records should route to the HSE manager role associated with the relevant location. The reviewer validates the submission and assigns follow-up actions as needed. Where multiple HSE managers are assigned, the process may allow the first available reviewer to take action.

### Consequences

- Hazard ID requires workflow configuration beyond simple record capture.
- A location-based HSE manager role must be maintained.
- Notifications should be sent to the appropriate reviewer role.
- Records will have clearer status and ownership.
- The process better supports governance but adds configuration complexity.

### More Information

The review model was demonstrated using a configured workflow example. The group indicated that this model better matched the desired process than the current simple submission model.

---
