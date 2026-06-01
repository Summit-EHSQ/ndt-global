---
adr: ADR-003
title: Define Hazard, Near Miss, and Incident as Distinct HSE Event Buckets
status: accepted-in-principle
date: 2026-05-29
deciders:
  - Dave McLean
  - Niall Walsh
  - Brett Corpe
  - John Blackham
  - Michael Barthelmess
  - Øyvind Heimli
consulted:
  - Tucker White
informed:
  - Branka Vidovic
---

# ADR-003: Define Hazard, Near Miss, and Incident as Distinct HSE Event Buckets

## Context and Problem Statement

The HSE reporting model needs clear definitions so that workers know whether to submit a Hazard ID, near miss, or incident. The discussion identified overlap between observations, near misses, and incidents, especially where a condition could have led to harm but did not.

The solution requires practical definitions that can be used in form guidance, training, routing, and reporting.

## Decision Drivers

- Reduce confusion at the point of submission.
- Support consistent reporting and analytics.
- Avoid unnecessary conversion logic between Hazard ID, near miss, and incident.
- Keep the reporting model understandable for frontline users.
- Preserve different workflows for different kinds of HSE events.

## Considered Options

1. **Allow users to choose freely among Hazard ID, near miss, and incident without strong definitions**
   - Reduces upfront design effort.
   - Increases inconsistent reporting.

2. **Define three distinct buckets based on event occurrence and impact**
   - Gives users practical decision criteria.
   - Supports cleaner reporting and workflow routing.
   - Requires training and clear captions/help text.

3. **Use one HSE intake form and classify records later**
   - Simplifies intake.
   - Requires review triage and possible reclassification.
   - Was not preferred due to the desire to avoid added review burden.

## Decision Outcome

Use three distinct HSE reporting buckets:

- **Hazard ID:** A condition, act, or situation was observed, but no event occurred.
- **Near Miss:** An event occurred, but no injury, damage, spill, or other impact resulted.
- **Incident:** An event occurred and caused an impact.

The exact user-facing wording can be refined, but the conceptual model should guide configuration and training.

## Consequences

- Form captions, help text, and training material should reinforce these distinctions.
- Hazard ID does not require automatic conversion to incident if definitions are clear.
- Near miss and incident remain part of Incident Management.
- Hazard ID remains a related but distinct HSE reporting concept.
- Edge cases may still require reviewer judgment.

## More Information

The meeting recognized that terminology may need to be adapted for regional and industry-specific usage, but the three-bucket model was accepted as a practical foundation.

---
