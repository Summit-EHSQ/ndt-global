# Observations Application ADRs

Source transcript: `NDT call 05.29.docx`  
Meeting date: 2026-05-29  
Scope: Observations / Hazard ID future-state design

## Overview

This folder contains separate Markdown Architectural Decision Records (ADRs) for the Observations / Hazard ID future-state design discussion. Each ADR is stored as an individual Markdown file with YAML front matter for easier reuse in a GitHub monorepo.

## ADR Map

| ADR | Title | File | Decision Captured |
|---:|---|---|---|
| ADR-001 | Separate HSE and Quality into Distinct Solution Streams | [`adr-001-separate-hse-and-quality-into-distinct-solution-streams.md`](./adr-001-separate-hse-and-quality-into-distinct-solution-streams.md) | Capture the architectural decision to move away from a blended Observations model and maintain distinct HSE and Quality process streams. |
| ADR-002 | Retain Hazard ID as the Primary HSE Observation Concept | [`adr-002-retain-hazard-id-as-the-primary-hse-observation-concept.md`](./adr-002-retain-hazard-id-as-the-primary-hse-observation-concept.md) | Capture the decision that the Observations application scope should center on Hazard ID-type reporting, rather than work observations or quality observations. |
| ADR-003 | Define Hazard, Near Miss, and Incident as Distinct HSE Event Buckets | [`adr-003-define-hazard-near-miss-and-incident-as-distinct-hse-event-buckets.md`](./adr-003-define-hazard-near-miss-and-incident-as-distinct-hse-event-buckets.md) | Capture the conceptual model used to distinguish Hazard IDs from near misses and incidents. |
| ADR-004 | Add Review Workflow and Location-Based HSE Manager Ownership for Hazard IDs | [`adr-004-add-review-workflow-and-location-based-hse-manager-ownership-for-hazard-ids.md`](./adr-004-add-review-workflow-and-location-based-hse-manager-ownership-for-hazard-ids.md) | Capture the decision that submitted Hazard IDs should enter a review workflow owned by the relevant location-based HSE manager role. |
| ADR-005 | Align Hazard Follow-Up Actions with Incident Action Plan Patterns | [`adr-005-align-hazard-follow-up-actions-with-incident-action-plan-patterns.md`](./adr-005-align-hazard-follow-up-actions-with-incident-action-plan-patterns.md) | Capture the decision to align Hazard ID follow-up action handling with the broader Incident Management action plan model. |
| ADR-006 | Handle Cross-Domain HSE/Quality Cases as Separate but Related Records | [`adr-006-handle-cross-domain-hse-quality-cases-as-separate-but-related-records.md`](./adr-006-handle-cross-domain-hse-quality-cases-as-separate-but-related-records.md) | Capture the decision that mixed HSE/Quality cases should remain separate records with a practical association path, rather than being tightly integrated by default. |
| ADR-007 | Do Not Implement Automatic Conversion from Hazard ID to Incident | [`adr-007-do-not-implement-automatic-conversion-from-hazard-id-to-incident.md`](./adr-007-do-not-implement-automatic-conversion-from-hazard-id-to-incident.md) | Capture the decision not to build automated Hazard ID-to-Incident conversion logic because clear definitions and reviewer judgment are preferred for low-frequency edge cases. |

## Notes

- ADR statuses reflect the meeting outcome and should be updated as decisions are finalized or superseded.
- Quality-side NCR/CAPA decisions are intentionally excluded from this Observations ADR set unless they directly affect Observations / Hazard ID architecture.
- Implementation tasks such as picklist cleanup, UI enhancements, and data migration details should be tracked separately from these ADRs.
