---
adr: ADR-001
title: Separate HSE and Quality into Distinct Solution Streams
status: accepted-in-principle
date: 2026-05-29
deciders:
  - Dave McLean
  - Niall Walsh
  - John Blackham
  - Tucker White
  - Brett Corpe
  - Michael Barthelmess
  - Øyvind Heimli
consulted:
  - Branka Vidovic
  - Lisa McLaughlin
  - Francisco Duran
informed: []
---

## ADR-001: Separate HSE and Quality into Distinct Solution Streams

### Context and Problem Statement

The existing configuration uses the Observations application for more than one conceptual purpose. Hazard ID is used for HSE-related proactive hazard reporting, while the work observation capability has been re-captioned and repurposed as a Quality Observation mechanism.

The future-state NDT Global solution needs to support both HSE and Quality processes, but the discussion identified different ownership models, regulatory drivers, reporting needs, and user expectations for each domain. A blended HSE/Quality observation model creates ambiguity for workers, reviewers, and reporting consumers.

### Decision Drivers

- Workers need a clear and intuitive path for submitting HSE versus Quality matters.
- HSE and Quality have different management teams, process owners, review patterns, and compliance expectations.
- Reporting should avoid unnecessary blending of HSE and Quality data.
- Existing Integra usage was partly shaped by prior licensing and implementation constraints that should not necessarily drive the future-state architecture.
- The future-state model should support global alignment while still accommodating regional regulatory differences.

### Considered Options

1. **Continue using Observations as a combined HSE and Quality intake area**
   - Preserves the existing Integra configuration pattern.
   - Minimizes immediate configuration change.
   - Continues ambiguity between HSE and Quality use cases.

2. **Separate HSE and Quality visually and procedurally, while still using shared platform capabilities where appropriate**
   - Creates clearer navigation and ownership.
   - Supports domain-specific workflow and reporting.
   - Requires configuration and migration planning.

3. **Create an entirely new application layer for cross-domain HSEQ reporting**
   - Could provide a unified intake experience.
   - Likely adds unnecessary complexity and licensing/configuration effort.
   - Was not strongly supported by the meeting discussion.

### Decision Outcome

Adopt a separated HSE and Quality solution model. Users should see distinct HSE and Quality streams in navigation and application structure. HSE matters should be driven toward the HSE incident/hazard process area, while Quality matters should be driven toward the Quality non-conformance process area.

This decision is accepted in principle, with some details dependent on the follow-on NCR/CAPA design session.

### Consequences

- The Observations application should no longer be treated as a blended HSE/Quality container in the future state.
- Quality Observation functionality will likely be removed from the Observations user experience, retired, hidden, migrated, or re-expressed through the Quality process stream.
- Hazard ID remains the main candidate for the HSE observation-style process.
- User training and navigation design should emphasize the domain split.
- Existing data and historical usage must be handled carefully to avoid changing the meaning of past records.

### More Information

This decision was reinforced during the meeting summary, where the target model was described as two streams: HSE/safety and Quality. The exact Quality-side implementation is intentionally out of scope for this Observations ADR set and should be addressed in the NCR/CAPA design ADRs.

---
