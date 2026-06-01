---
adr: ADR-007
title: Do Not Implement Automatic Conversion from Hazard ID to Incident
status: accepted-in-principle
date: 2026-05-29
deciders:
  - Dave McLean
  - Niall Walsh
  - John Blackham
consulted:
  - Tucker White
  - Brett Corpe
  - Michael Barthelmess
  - Øyvind Heimli
informed:
  - Branka Vidovic
---

# ADR-007: Do Not Implement Automatic Conversion from Hazard ID to Incident

## Context and Problem Statement

The future-state HSE reporting model distinguishes between Hazard IDs, near misses, and incidents. During the discussion, the question was raised whether a submitted Hazard ID could or should automatically trigger creation of an EHS incident if the reviewer determines that the record was misclassified or should be handled through the Incident Management process.

The existing platform includes some conversion logic between near misses and incidents, but not an equivalent out-of-the-box conversion path from Hazard ID to incident. Implementing that type of conversion would require additional custom logic and configuration effort.

The meeting discussion indicated that this scenario appears to be low-frequency, and that clearer definitions between Hazard ID, near miss, and incident should reduce the need for automated conversion.

## Decision Drivers

- Hazard ID, near miss, and incident should remain distinct HSE event categories.
- Clear user-facing definitions should reduce misclassification at intake.
- Reviewer judgment can handle the occasional misclassified Hazard ID.
- Custom conversion logic would add cost, complexity, and maintainability burden.
- The expected frequency of Hazard IDs needing conversion to incidents does not justify significant automation effort.

## Considered Options

1. **Implement automatic conversion from Hazard ID to Incident**
   - Could streamline misclassified or escalated cases.
   - Would require custom logic because the platform does not provide the same standard conversion path for Hazard ID to Incident.
   - Likely poor value if the scenario is rare.

2. **Allow reviewers to manually create an Incident when needed**
   - Keeps the Hazard ID and Incident models distinct.
   - Avoids unnecessary automation complexity.
   - Requires reviewer judgment and manual follow-up in rare cases.

3. **Rely on clear definitions and training to prevent most misclassification**
   - Reduces the need for conversion.
   - Supports simpler workflow boundaries.
   - Does not eliminate all edge cases.

## Decision Outcome

Do not implement automatic conversion from Hazard ID to Incident as part of the Observations design.

If a Hazard ID is reviewed and determined to require Incident Management handling, the reviewer should address it through a manual process, such as creating the appropriate incident record and managing any required follow-up outside of automated conversion logic.

The primary control for this issue should be clear definitions, training, and review workflow rather than custom automation.

## Consequences

- The Observations/Hazard ID process remains simpler and more maintainable.
- The distinction between Hazard ID, near miss, and incident remains clear.
- Rare misclassification scenarios will require manual reviewer intervention.
- The project avoids spending configuration budget on low-frequency conversion logic.
- If future usage shows frequent Hazard ID-to-Incident escalation, this decision can be revisited.

## More Information

This ADR complements ADR-003, which defines Hazard ID, near miss, and incident as distinct HSE event buckets, and ADR-004, which introduces review workflow and HSE manager ownership for Hazard IDs.
