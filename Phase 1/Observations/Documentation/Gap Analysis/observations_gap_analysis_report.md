# Gap Analysis Report

# 1. Engagement Overview

| Item | Description |
|---|---|
| Application Reviewed | Intelex Observations application, including Quality Observation, Work Observation / safe and unsafe observation views, Hazard ID, and related configuration objects. |
| Session Type | Gap analysis / requirements alignment workshop for Observations in the context of NDT and Integra process harmonization. |
| Transcript Reviewed | `NDT call 05.29.docx`. |
| Current-State Documentation Reviewed | `Observations App Config(v1.0.0.0).ipack`, parsed as the baseline current-state configuration package. |
| Primary Business Objective | Align the future-state Observations model with the combined organization’s HSE observation and hazard-reporting needs while clarifying boundaries with adjacent Quality, Incident, NCR, and Inspection processes. |
| Key Stakeholders Referenced | Dave McLean, Niall Walsh, John Blackham, Tucker White, Brett Corpe, Øyvind Heimli, Michael Barthelmess, Branka Vidovic, Lisa McLaughlin. |
| Analysis Date | 2026-06-15 |

This report compares the baseline Observations configuration package against the requirements and architectural direction discussed in the workshop. The methodology and report structure follow the uploaded Intelex Gap Analysis Report Generator instructions, which require comparison of current Intelex configuration against future-state workshop requirements and identification of gaps, configuration changes, risks, assumptions, and open questions. fileciteturn3file13

The central business driver is enterprise harmonization after integration of two operating models. Integra’s current Observations design uses the application for both Hazard ID and Quality Observation use cases, while the future direction discussed in the workshop favors a clearer separation between HSE and Quality process areas, with Quality-related observations removed from Observations scope and Hazard ID retained as the observation concept for conditions or behaviors that have not yet produced an incident or near miss. fileciteturn3file19

# 2. Current-State Solution Summary

The uploaded baseline package is `Observations App Config`, version `1.0.0.0`, exported from source owner `EntegraTest` on 2026-06-01 with platform version `6.6.16.2`. The package includes configuration for the Observations module and related dependencies including Action Plans, EHS Incident Management, Event Framework, Fragment Application, System Objects, and WCB Claims Management.

## Current Application Architecture

The current baseline Observations configuration contains the following primary objects:

| Object / Component | Current-State Purpose |
|---|---|
| Quality Observation | Captures quality-related observations, improvement opportunities, recognition, and related follow-up information. |
| Hazard ID | Captures observed hazards / conditions using severity, safe/unsafe classification, type, steps taken, action plan, reviewer fields, and close date. |
| Observation | Abstract / shared observation object with Quota reference and incident-management observation views. |
| Follow Up | Lookup / configuration object for follow-up types. |
| Steps Taken | Lookup / configuration object for steps taken. |
| Discussions | Lookup / configuration object for discussions. |
| Topics Discussed | Lookup / configuration object for topics discussed. |
| Observation Area | Lookup / configuration object for area classification. |
| Comfort Level | Lookup / configuration object for comfort level. |
| Hazard Severity / Observation Severity | Severity classification objects. |
| Action Plan | Related action plan object reference. |

## Workflow Architecture

No published workflow is configured on the main Observations objects in the parsed baseline package. `Quality Observation`, `Hazard ID`, and `Observation` do not show a configured `PublishWorkflowId`. The current model therefore appears primarily form-, view-, lookup-, action-plan-, and validation-driven rather than workflow-stage-driven.

Current validation rules identified in the baseline include:

| Object | Validation |
|---|---|
| Quality Observation | Date & Time of Observation must be on or before Today. |
| Hazard ID | Date & Time of Hazard ID must be on or before Today. |
| Lookup / configuration objects | Unique Name validations on several lookup/configuration objects. |

## Current Approval and Assignment Logic

The baseline package does not show a formal workflow approval model for Quality Observation or Hazard ID. Assignment / accountability appears to be supported through fields and related components rather than workflow stages. Relevant fields include:

| Object | Assignment / Responsibility-Relevant Fields |
|---|---|
| Quality Observation | Observer, Observed, Employee Location, Observed Employee’s Location, Department, Action Plan, Task List, Follow Up, PAR/CAPA Required? |
| Hazard ID | Incident Reporter, Reviewed By, Action Plan, Actions/Follow Up, Step Taken, Steps Taken, Reviewer Comments, Hazard ID Closed On |

## Current UI Behavior

The baseline package includes configurable views and tabs that expose Observations concepts separately within the Observations module. Key views include:

| Area | Current Views / Tabs |
|---|---|
| Hazard ID | Add a Hazard ID, Hazard ID List, My Hazard IDs, Hazard ID detail and inventory views, mobile profiles. |
| Work / Quality Observation | Add Quality Observation, Observation List, My Observations, Safe Observation detail, Unsafe Observation detail, Work Observation detail and inventory views, mobile profiles. |
| Incident-Management Observation | EHSIncidentMang_Observation_Inventory and EHSIncidentMang_Observation_Detail views. |
| Settings | Lookup-management views for Discussions, Task List, Step Taken, Severity, Follow Up, Comfort Level, Hazard Type, Specific Location, Observation Area, Topics Discussed. |

## Current Data Model and Lookup Values

The current configuration includes several lookup sets that will require harmonization before enterprise rollout.

| Lookup / Configuration Object | Current Values Identified |
|---|---|
| Safe/Unsafe/Quality | Safe, Unsafe, Quality |
| Observation Severity | Low, Medium, High, Critical |
| Severity Type | Observation, HazardID |
| Observation Purpose | Improvement Opportunity, Recognition |
| Observation Subtype | External Audit, Employee Audit, ADFP, Internal Audit |
| Observation text / type | Inadequate Procedure, Audit, Spot Check, Part Failure |
| Department | Operations, Project Management, Engineering, Continuous Improvement, Admin, Data Analysis, Account Management, QHSE |
| Follow Up | Change request, PAR / NCR, On the spot discussion, Individual training, Team training, Reward / recognition, Stop Work, Other |
| Steps Taken | Change request, Individual training, Stop Work, Team training, Reward / recognition, PAR / NCR, Other, On the spot discussion |
| Quota | Accepted, Rejected, Non Approved, Approved |

## Reporting Support

The package provides inventory views for Hazard ID, My Hazard IDs, Work Observation, My Work Observations, lookup objects, and incident-management observation views. No dedicated KPI dashboards, cross-process reports, or harmonized enterprise analytics were identified in the package.

## Child Objects and Related Records

The baseline includes references to Action Plan, Task List, Follow Up, Steps Taken, Topics Discussed, Discussions, and child/related records. The application supports related action tracking, but does not appear to enforce workflow closure dependency rules between Observations, NCRs, Incidents, or Near Misses.

## Integrations

No external integration behavior was identified in the baseline package. There are dependencies on other Intelex application areas, including Action Plans and EHS Incident Management, but no external API, HRIS, ERP, or data-warehouse integration configuration was identified in the uploaded package.

# 3. Future-State Business Requirements Identified

| Requirement ID | Requirement / Need | Source Evidence | Explicit or Implied | Business Driver |
|---|---|---|---|---|
| REQ-001 | Establish clear definitions separating Hazard ID, Near Miss, and Incident. | The workshop defined a hazard as something noticed before an event occurred, a near miss as something that occurred without injury/impact, and an incident as something where impact occurred. fileciteturn3file0 | Explicit | User adoption, governance, classification consistency |
| REQ-002 | Retain Hazard ID as the primary Observations concept for unsafe conditions / acts and potentially safe or positive observations where no impact has occurred. | Dave summarized that the remaining Observations concept would be Hazard ID, driven by observed unsafe acts/conditions or possibly safe/kudos acts where no impact occurred. fileciteturn3file0 | Explicit | Process simplification, HSE reporting |
| REQ-003 | Move quality-related observations out of Observations and into a quality-focused NCR / quality application pathway. | The transcript states that if quality is taken out of Observations and put into NCR, the remaining Observations concept is Hazard ID. fileciteturn3file2 | Explicit | HSE / Quality separation, process governance |
| REQ-007 | Preserve clear visual and navigational separation between HSE and Quality. | Stakeholders agreed that Quality and HSE should be separated for user clarity and organizational ownership; Dave summarized the intended two-stream model. fileciteturn3file17 fileciteturn3file19 | Explicit | Adoption, organizational alignment, reporting |
| REQ-008 | Harmonize NDT and Integra terminology and lookup values before changing existing picklists. | Dave’s action was to extract Hazard ID picklist values for harmonization, warning that existing data should be protected by hiding values rather than breaking historical records. fileciteturn3file11 | Explicit | Master-data governance, reporting consistency |
| REQ-016 | Ensure the future-state design supports safety, environmental, and security-related observations where appropriate. | Øyvind asked whether Hazard ID includes environment and security, and John stated Hazard ID has been used for those conditions unless severe enough to be near miss or incident. fileciteturn3file12 | Explicit | EHS scope clarity |
| REQ-018 | Provide clear user-facing entry paths so frontline users do not need to understand back-end object complexity. | Stakeholders emphasized that workers need obvious paths such as Observations, Inspections, NCR, and Incidents; confusing navigation would hurt adoption. fileciteturn3file17 | Implied | Usability, adoption |

# 4. Gap Analysis

The gaps below are limited to items that require an actual Intelex system, configuration, security, navigation, form, lookup, or reporting change in the Observations-related solution at this time. Process-only decisions, deferred items, licensing questions, and “do not build” recommendations have been removed from the gap table.

| Gap ID | Area | Current-State Behavior | Future-State Requirement | Gap Description | Recommended Change | Configuration vs Customization | Affected Components | Priority | Risk / Complexity |
|---|---|---|---|---|---|---|---|---|---|
| GAP-001 | Quality Observation placement | Quality Observation exists inside the Observations application and uses fields such as Safe/Unsafe/Quality, Observation Purpose, Observation Subtype, Department, PAR/CAPA Required?, Follow Up, and Steps Taken. | Quality-related observations should no longer be treated as an Observations application intake path; Observations should focus on Hazard ID / HSE observation needs. | The current baseline mixes Quality Observation with HSE Observations, conflicting with the agreed direction to separate Quality and HSE for navigation, ownership, and reporting. | Hide, retire, or make the Quality Observation entry path read-only from the Observations user experience once the approved Quality destination is confirmed outside this Observations gap analysis. Preserve historical Quality Observation records in place unless a separate data strategy approves another approach. | Observations configuration change. | Quality Observation object, Work Observation views, Add Quality Observation tab, Safe/Unsafe/Quality lookup, Observations reports. | Critical | Moderate |
| GAP-002 | HSE / Quality navigation | Current Observations app exposes both Hazard ID and Quality Observation concepts in the same module. | Users should see distinct HSE and Quality streams. | Current UI can confuse users and blur organizational ownership. Stakeholders explicitly favored visually and functionally separating quality and HSE. | Adjust landing-page/tab structure so HSE users access Hazard ID / HSE observation records through an HSE context and Quality users access quality intake through a Quality context outside Observations. | Configuration; possible menu/tab restructuring. | Module tabs, configurable views, landing pages, security groups, reports. | High | Moderate |
| GAP-003 | Hazard ID relationship to Incident Management | Baseline includes Hazard ID views under Observations and also includes EHSIncidentMang observation views, but Hazard ID remains in Observations. | Hazard ID may remain technically in Observations but potentially appear as a component/tab within Incident Management for a “one HSE place to go” experience. | The current application boundary may not align with desired user experience. However, transcript indicates the object can remain in Observations while surfaced in Incident Management. | Evaluate and configure Hazard ID navigation under the HSE / Incident Management user experience while keeping the underlying object in Observations if that is the approved UX model. Align security so users receive the required Hazard ID access through the chosen HSE navigation model. | Configuration; security model update; no object migration required. | Hazard ID views, Incident Management tabs, Observations security groups, EHSIncidentMang_Observation views. | High | Moderate |
| GAP-004 | Hazard / Near Miss / Incident definitions | Current baseline has Hazard ID and Incident Management dependencies but does not enforce or display agreed definition boundaries. | Users need clear criteria: hazard = noticed before event, near miss = event occurred without impact, incident = impact occurred. | Without embedded definitions, users may misclassify conditions, near misses, and incidents. | Add user guidance, help text, intake labels, or decision prompts to the relevant entry points. Confirm whether form-level guidance is sufficient or whether any validation logic is required. | Configuration; possible UI content / form guidance. | Hazard ID detail view, Incident intake, Near Miss intake, help text, training materials. | High | Low |
| GAP-005 | Safe / Unsafe / Quality lookup | Current Safe/Unsafe/Quality lookup contains Safe, Unsafe, Quality. | Quality should not be a Hazard ID / Observations classification in the future HSE stream. | The current lookup embeds Quality into Observations, which conflicts with the future separation model. | Remove Quality from active future use by hiding/deactivating rather than deleting if historical records exist. Recaption only with explicit confirmation due to historical data impact. | Configuration / master-data governance. | Safe/Unsafe/Quality lookup, Quality Observation views, reports, historical records. | High | Moderate |
| GAP-006 | Hazard ID taxonomy harmonization | Baseline contains current Hazard ID fields and lookup objects, but NDT terminology and “See It, Own It, Share It” naming need alignment. | Hazard ID picklist values and terminology need harmonization across NDT and Integra. | Current values may not match future enterprise taxonomy. Recaptioning existing values could alter historical reporting semantics. | Export Hazard ID lookup values, conduct harmonization workshop, decide add/hide/recaption rules, and document historical reporting impact before configuration changes are made. | Configuration; data governance. | Hazard Type, Observation Area, Severity, Steps Taken, Safe/Unsafe, reports. | High | Moderate |
| GAP-007 | Security roles | Baseline includes Observations Admin, Observations Supervisor, and Observations Reporter groups. | Future model requires Quality and HSE ownership separation and possibly HSE-context access to Hazard ID. | Current security groups are Observations-centric, not clearly aligned to future Quality vs HSE ownership. | Redesign security roles for HSE Hazard ID users, admins, supervisors/reviewers, and reporters. Avoid granting quality users unnecessary HSE access and vice versa. | Configuration / security model redesign. | Security groups, module tabs, views, record permissions, workflow assignments. | High | Moderate |
| GAP-008 | Reporting separation and consolidated analytics | Current inventory views support list reporting but not clearly separated enterprise analytics. | Business needs HSE reporting that is separated from Quality reporting and aligned to the future Hazard ID model. | Current mixed Observations model risks confusing metrics, especially if Quality remains a Safe/Unsafe/Quality value. | Separate HSE hazard metrics from Quality observation/improvement metrics by retiring Quality from active Observations use, updating inventory views, and aligning reports to the approved Hazard ID taxonomy. | Reporting configuration; possible view/report updates. | Inventory views, dashboards, reports, lookup values. | High | Moderate |


# 5. Open Questions & Follow-Ups

| ID | Open Question | Why It Matters | Recommended Owner |
|---|---|---|---|
| OQ-001 | What is the final approved future-state definition for Hazard ID, Near Miss, Incident, NCR, Finding, and Improvement Opportunity? | These definitions drive intake design, workflow routing, reporting, and user training. | Business process owners: HSE, Quality, Compliance |
| OQ-002 | Should Hazard ID remain visible under Observations, move visually under Incident Management, or appear in both places? | Determines navigation, security, and user adoption model. | Solution Architect / HSE process owner |
| OQ-003 | Should the Quality Observation object be hidden, retired, preserved read-only, or repurposed? | Prevents accidental loss of current use cases and historical data. | Quality process owner / Intelex admin |
| OQ-012 | Which Hazard ID picklist values should be added, hidden, retained, or recaptioned? | Recaptioning affects historical records; deleting values may break data integrity. | Master-data governance lead |
| OQ-013 | Is “See It, Own It, Share It” a user-facing label to retain for Hazard ID? | NDT users may recognize this terminology better than “Hazard ID.” | HSE change-management lead |
| OQ-014 | Are positive / safe observations or recognition records in scope for Hazard ID? | Transcript mentions possible safe/kudos observations but does not finalize how they should be captured. | HSE process owner |

# 6. Recommended Next Steps

| Priority | Recommendation | Purpose |
|---|---|---|
| Critical | Conduct a joint HSE / Quality process-definition workshop. | Finalize definitions for Hazard ID, Near Miss, Incident, Finding, NCR, Improvement Opportunity, and Quality Observation replacement. |
| Critical | Confirm future-state architecture decision: Quality to NCR, Hazard ID retained as HSE observation concept. | Locks the design foundation before configuration changes begin. |
| High | Export and harmonize Hazard ID lookup values. | Align NDT and Integra taxonomy while protecting historical data. |
| High | Prototype revised navigation separating HSE and Quality streams. | Validate user experience before changing menus, tabs, and security roles. |
| High | Perform security-role review. | Align Observations Admin/Supervisor/Reporter roles with future HSE and Quality ownership. |
| Medium | Develop user-facing guidance and intake labels. | Reduce misclassification and improve adoption for frontline workers. |

# 7. Assumptions, Risks & Constraints

## Assumptions

- The uploaded `.ipack` package represents the baseline current-state Observations configuration.
- No formal workflow exists on the parsed Quality Observation, Hazard ID, or Observation objects because no `PublishWorkflowId` was present for those objects in the package.
- The future-state direction is not fully finalized but strongly favors moving quality-related observations into NCR and retaining Hazard ID as the remaining Observations concept.
- Historical records exist in the current Observations application; therefore, lookup changes should avoid deletion or careless recaptioning.

## Risks

- **Classification risk:** Users may continue misclassifying quality issues, hazards, near misses, incidents, findings, and improvement opportunities if definitions are not embedded in forms and training.
- **Historical reporting risk:** Recaptioning existing lookup values could alter the meaning of prior records.
- **Adoption risk:** If HSE and Quality navigation is not intuitive, frontline users may select the wrong entry path or avoid reporting.

## Constraints

- Existing data in Observations constrains lookup deletion and recaptioning.

## Inferred Analysis

- The most sustainable architecture is to treat Observations as an HSE Hazard ID / proactive condition-reporting capability and treat Quality Observation as a legacy / transitional construct.
- Hazard ID should remain lightweight and action-oriented, with clear escalation/reference guidance rather than heavy conversion automation.
- A formal master-data governance decision is required before any lookup recaptioning, hiding, or consolidation.
