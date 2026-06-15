---
adr: ADR-002
title: Retain Hazard ID as the Primary HSE Observation Concept
status: accepted-in-principle
date: 2026-05-29
deciders:
  - Dave McLean
  - Niall Walsh
  - Brett Corpe
  - Michael Barthelmess
  - Øyvind Heimli
  - John Blackham
consulted:
  - Tucker White
informed:
  - Branka Vidovic
---

# ADR-002: Retain Hazard ID as the Primary HSE Observation Concept

## Context and Problem Statement

The Observations application includes multiple concepts, including Work Observation and Hazard ID. The meeting established that NDT’s “See It, Own It, Share It” process maps most closely to Hazard ID-type reporting rather than to a planned supervisor work observation process.

The group did not identify a strong future-state need for the Work Observation object as a standalone proactive supervisor conversation process. Other proactive activities, such as inspections and toolbox talks, are better aligned to other application areas or future phases.

## Decision Drivers

- NDT’s current observation process is primarily hazard and improvement reporting.
- The Work Observation object does not appear to map cleanly to the combined future-state process.
- Hazard ID supports proactive reporting of unsafe conditions, unsafe acts, environmental hazards, and similar HSE concerns.
- Quality observations are expected to move out of the Observations process stream.
- The solution should avoid retaining unused or confusing observation concepts.

## Considered Options

1. **Use both Work Observation and Hazard ID**
   - Preserves the full out-of-box Observations structure.
   - Could support planned supervisor observations.
   - Adds confusion if no discrete work observation program exists.

2. **Use Hazard ID only for the future-state Observations scope**
   - Aligns with NDT’s existing hazard reporting pattern.
   - Simplifies the Observations application.
   - May require hiding or disabling the Work Observation component.

3. **Retire Observations entirely and move all HSE reporting into Incident Management**
   - Provides one HSE reporting destination.
   - May obscure the distinction between hazards and incidents.
   - Requires more significant configuration and navigation changes.

## Decision Outcome

Retain Hazard ID as the primary future-state HSE observation concept. The Work Observation / Quality Observation concept should not remain a central user-facing process unless a clear business program is later identified for it.

## Consequences

- The Observations application may be reduced to Hazard ID functionality only.
- Work Observation functionality may be hidden, disabled, repurposed, or left unused.
- Hazard ID configuration must be harmonized between existing Integra and NDT practices.
- Training and terminology should clarify how Hazard ID relates to near misses and incidents.

## More Information

This decision depends on the broader HSE/Quality stream separation captured in ADR-001. The exact treatment of the retired Quality Observation concept should be handled in the NCR/CAPA design work, not in the Observations ADR set.

---
