# Gap Analysis Report

## 1. Engagement Overview

| Item | Description |
| --- | --- |
| Application Reviewed | Intelex Observations application |
| Session Type | Gap analysis / requirements alignment session |
| Transcript Reviewed | `NDT call 05.29.docx` |
| Current-State Documentation Reviewed | `Observations App Config(v1.0.0.0).ipack` baseline configuration package |
| Primary Business Objective | Harmonize the future-state use of the Intelex Observations application by separating HSE observation / Hazard ID functionality from quality issue intake, while preserving a governed path for proactive HSE reporting. |
| Key Stakeholders Referenced | Dave McLean, Niall Walsh, John Blackham, Tucker White, Brett Corpe, Øyvind Heimli, Michael Barthelmess, Lisa McLaughlin |
| Analysis Date | June 1, 2026 |

The session focused on how the existing Observations application should be positioned after combining legacy Integra and NDT practices. The major future-state direction is that Observations should no longer serve as a mixed quality and HSE intake area. Quality-related observations should move out of Observations and into the quality process, while Hazard ID remains the relevant Observations concept for HSE-related proactive reporting. The transcript indicates that final configuration decisions for quality handling are dependent on the separate NCR/CAPA design discussion.

## 2. Current-State Solution Summary

The baseline Observations configuration package represents an Intelex Observations application configured with two primary operational concepts: **Quality Observation** and **Hazard ID**.

| Area | Current-State Summary |
| --- | --- |
| Application architecture | Observations is configured as a discrete application with user-facing areas for Quality Observation, Safe Observation, Unsafe Observation, Hazard ID, My Observations, My Hazard IDs, lists, and settings. |
| Primary objects | The package includes `Quality Observation` and `Hazard ID` as the main transactional objects. |
| Supporting objects | Supporting/configuration objects include Hazard Type, Hazard Severity, Observation Area, Comfort Level, Discussions, Follow Up, Steps Taken, Topics Discussed, Action Plan, Job Task, Employee, Event, Event Type, Location, Specific Location, Severity, Incident, Subject, and related abstract action objects. |
| Lookup/configuration data | Lookups include Safe/Unsafe, Observation Severity, Observation Purpose, Observation Subtype, Department, Entegra Steps Taken, Entegra Follow Up, Quota, Severity Type, and Yes/No/Unknown. |
| Workflow architecture | The baseline package does not evidence a full multi-stage workflow for Observations or Hazard ID. The transcript also confirms that observation-style applications can function largely as data-capture tools unless a workflow is configured. |
| Approval/review model | The package includes fields such as Reviewed By, Reviewer Comments, Hazard ID Closed On, PAR/CAPA Required?, Actions/Follow Up, and action-plan relationships, but no complete explicit workflow approval model was evident in the package. |
| Assignment logic | Current assignment appears limited to fields and related action plan objects. There is no confirmed baseline role-driven HSE manager review/assignment workflow. |
| UI behavior | Baseline includes separate tabs for adding Quality Observations and Hazard IDs, plus mobile-facing Safe Observation, Unsafe Observation, Hazard ID, My Observations, and My Hazard IDs tabs. |
| Validations | Date/time validations exist for Observation and Hazard ID requiring the date/time to be on or before today. Several setup/configuration objects enforce Unique Name validation. |
| Automation/action handlers | Baseline action handlers include setting Event Type for Observation and Hazard ID, setting Safe/Unsafe based on severity, and clearing severity when an observation is Safe. |
| Reporting | Inventory/list views exist for observations, hazard IDs, setup objects, and “My” views. No broader KPI/reporting design was evident from the package. |
| Security | Baseline security groups include Observations Admin, Observations Supervisor, and Observations Reporter. |
| Integrations | No external integration behavior was evident in the baseline package. |
| Mobile support | Mobile-specific tabs exist. The session raised additional mobile/user-experience considerations around browser responsiveness, in-app training, and photo attachment. |

Current-state behavior can be summarized as a lightweight Observations application that has been adapted by Integra to support both proactive HSE hazard reporting and quality observation capture. The session confirms that the Work Observation concept had been recaptioned to Quality Observation, changing the domain from Intelex’s original safety/work-observation intent into a quality-focused use case.

## 3. Future-State Business Requirements Identified

| Requirement ID | Requirement / Need | Source Evidence | Explicit or Implied | Business Driver |
| --- | --- | --- | --- | --- |
| REQ-001 | Separate quality and HSE content, user navigation, ownership, and reporting streams. | The group aligned on “a clear delineation between quality and safety related products and content and data,” including user navigation and application layout. | Explicit | Governance, reporting clarity, organizational ownership |
| REQ-002 | Move quality observations / quality issue intake out of Observations and into the Nonconformance process. | The meeting direction was to drive quality-related issues, including existing quality observations and nonconformances, through the nonconformance application. | Explicit, subject to NCR session | Process clarity, quality governance, future-state application separation |
| REQ-003 | Retain Hazard ID as the HSE observation concept for unsafe acts/conditions, safe acts/conditions, or events where no impact occurred. | The future Hazard ID usage was described as observed unsafe/safe acts or conditions where no impact ensued and where the situation was not a near miss. | Explicit | HSE proactive reporting, incident prevention |
| REQ-004 | Consider surfacing Hazard ID within Incident Management rather than exposing Observations as a separate standalone app. | The group discussed that Observations may no longer be user-visible and Hazard ID may become a component of Incident Management. | Explicit / design option | Simplified HSE process structure, application consolidation |
| REQ-005 | Provide HSE manager review / quarantine before submitted observations become visible or actionable. | NDT’s current process sends employee submissions to HSE quarantine; the HSE manager reviews, approves, assigns action owner, and sets due date. | Explicit | Quality control, accountability, appropriate assignment |
| REQ-006 | Add an actual workflow to Hazard ID / HSE observation processing, including review, notification, action assignment, and closure. | The proposed model includes workflow, reviewer notification, review details, action plans, and closure. | Explicit | Governance, traceability, operational control |
| REQ-007 | Use location-based HSE Manager assignment for review routing. | The reviewer is expected to be the HSE manager for the submitting location, with role population on a per-location basis. | Explicit | Regional ownership, assignment accuracy |
| REQ-008 | Harmonize hazard / observation type and category picklists between Integra and NDT. | NDT uses categories such as building security, chemical safety, contractor safety, slips/trips/falls, unsafe behavior, and quality categories that may need cleanup; the team planned to compare and harmonize Intelex values with NDT data. | Explicit | Reporting consistency, master-data governance |
| REQ-009 | Remove or hide quality categories from HSE observation/hazard reporting once quality is moved out of Observations. | NDT noted that quality categories in current observations would be cleaned up and focus would shift to safety/environmental hazard topics. | Explicit | Taxonomy clarity, reporting integrity |
| REQ-010 | Maintain historical data integrity when modifying or recaptioning picklist values. | The session noted that removing values should hide them, while recaptioning must only be done when the concept is truly the same because it affects existing records. | Explicit | Data integrity, auditability |
| REQ-011 | Align Hazard ID action-plan experience with Incident Management action-plan look and feel. | Niall requested that observation action creation be similar to the EHS Incident Management setup in fields, layout, and user perspective. | Explicit | User consistency, adoption |
| REQ-012 | Consider allowing first action details directly on the initial Hazard ID form. | The proposed improvement was to let users enter the first action plan directly on the initial form because most hazards have one action. | Explicit / design option | Usability, reduced clicks |
| REQ-013 | Support photo/document attachment during hazard submission without requiring save-first behavior. | The prototype discussion included documentation added inline “so you don’t have to save it first to get your picture.” | Explicit | Mobile usability, evidence capture |
| REQ-014 | Evaluate mobile-friendly UI and possibly in-app training/multilingual training content. | The team discussed responsive UI, mobile friendliness, in-app training content, and auto-translated training videos. | Implied | Global adoption, multilingual workforce support |
| REQ-015 | Avoid automatic Hazard ID-to-Incident conversion unless the business case is strong. | Hazard-to-incident conversion was technically possible but not considered good value, and NDT could not recall a strong historical use case. | Explicit | Scope control, budget protection |
| REQ-016 | Defer final Observations decisions until the NCR/CAPA session confirms the future quality path. | The meeting noted final Observations decisions depend on the next session about NCR/CAPA and may need revision. | Explicit | Dependency management |

## 4. Gap Analysis

| Gap ID | Area | Current-State Behavior | Future-State Requirement | Gap Description | Recommended Change | Configuration vs Customization | Priority | Risk / Complexity |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| GAP-001 | Application domain separation | Observations currently contains both Quality Observation and Hazard ID concepts. | Separate quality and HSE product/content/data streams. | Current design blends quality and HSE intake in one application, conflicting with the desired future ownership and reporting model. | Remove Quality Observation from the future user-facing Observations model and redirect quality-related intake to the appropriate quality process. | Configuration + navigation/security redesign | Critical | High |
| GAP-002 | Quality Observation positioning | Quality Observation captures quality-related improvement/observation records in Observations. | Quality-related intake should move out of Observations. | Keeping Quality Observation in the Observations app would conflict with the future-state requirement to separate quality and HSE. | Hide or retire Quality Observation entry points for future use; retain historical access/reporting until migration/reporting strategy is decided. | Configuration; data governance | Critical | High |
| GAP-003 | HSE submission review | Baseline Hazard ID appears form/list driven; no complete explicit workflow is evident. | Employee submissions should route to location HSE Manager for quarantine/review before broader visibility/actioning. | Current baseline does not implement NDT’s quarantine review pattern. | Add Hazard ID workflow with Submitted/Pending Review, HSE Review, Action Assignment, Action Completion, and Closure. | Workflow configuration | Critical | Moderate |
| GAP-004 | Assignment logic | Baseline security groups exist, but no confirmed location-based HSE Manager routing was evident. | Reviewer/owner should be location-based HSE Manager, possibly one or more people per location. | Current security/assignment model may not support automatic routing by location. | Add/populate HSE Manager role at location level; configure workflow assignments/notifications based on location. | Configuration; security role design | High | Moderate |
| GAP-005 | Hazard ID visibility control | Current baseline does not evidence quarantine visibility states. | Submitted observations should be controlled until reviewed. | Without quarantine, records may be visible without ownership, appropriateness review, or action accountability. | Add review status/stage and visibility rules; restrict unapproved submissions to HSE reviewers/admins. | Workflow + security configuration | High | Moderate |
| GAP-006 | Action plan creation | Current Hazard ID includes action-plan relationship and Actions/Follow Up text, but action creation may require additional user steps. | Action creation should be consistent with Incident Management and potentially embedded in the initial review/submission flow. | The current flow may add clicks and reduce adoption; unclear ownership after submission was a concern. | Align Hazard ID action plan form with Incident Management action-plan fields/layout; optionally add first-action capture on form. | Configuration; possible action handler/scripting | Medium | Moderate |
| GAP-007 | Picklist taxonomy | Baseline includes Hazard Type, Hazard Severity, Observation Area, Safe/Unsafe, Observation Severity, and related custom lookups. | Harmonized NDT + Integra HSE/environment/security category list. | Current values may not match NDT’s See It / Own It / Share It taxonomy and may include quality categories that should no longer be used in HSE observations. | Export current values, map to NDT values, hide obsolete values, add new distinct values, carefully recaption only true equivalents. | Configuration/data harmonization | High | Moderate |
| GAP-008 | Historical data integrity | Existing values may be recaptioned or removed if not governed. | Existing data must remain auditable and semantically accurate. | Recaptioning values that are not truly equivalent can alter the apparent meaning of historical records. | Use inactive/hidden flags rather than deletion; create new values for new concepts; document value-mapping decisions. | Configuration + data governance | High | Moderate |
| GAP-009 | HSE vs near miss / incident boundary | Hazard ID and near miss/incident definitions require user clarity. Current Hazard ID is used for conditions without injury/property damage and may include security/environment. | Hazard ID should capture observed safe/unsafe conditions where no impact occurred; near miss/incident should remain in Incident Management. | Users may misclassify hazards, near misses, and incidents unless field labels and guidance are clear. | Add landing-page guidance, field help, conditional questions, and training content; consider Incident Management tab placement for Hazard ID. | Configuration + UX content | High | Moderate |
| GAP-010 | Mobile evidence capture | Baseline has mobile tabs, but attachment and responsive browser behavior were raised as needs. | Users should be able to capture photos/documentation easily during hazard submission. | Save-first attachment behavior and non-responsive browser experiences may reduce field adoption. | Validate mobile app and browser UX; configure attachment fields/sections inline where feasible; consider responsive UI enhancements. | Configuration; possible UI customization | Medium | Moderate |
| GAP-011 | In-app guidance/training | Baseline package does not evidence in-app training content. | Global users may need embedded guidance and multilingual support. | Without guidance, users may choose the wrong process or misunderstand Hazard ID boundaries. | Add field help, process guidance, landing-page instructions, and optional embedded training assets. | Configuration/content; possible custom UI | Medium | Moderate |
| GAP-012 | Reporting separation | Baseline list views exist but no enterprise KPI model was evident. | Reporting must separate HSE hazard reporting from quality reporting and support harmonized HSE categories. | Existing mixed Observations data model can distort quality vs HSE metrics. | Define Observations reporting around HSE Hazard ID only; preserve legacy Quality Observation reporting separately. | Reporting configuration + data governance | High | Moderate |

## 5. Workflow & Business Process Impacts

| Workflow / Process Area | Current Behavior | Proposed Future Behavior | Required Workflow Changes | Risks / Considerations |
| --- | --- | --- | --- | --- |
| Quality Observation intake | Quality-related observations can currently be logged in Observations. | Quality-related intake should move out of the Observations application. | Hide/retire Quality Observation entry points for future-state use after the quality-process design is confirmed. | Observations changes depend on the separate NCR/CAPA design outcome. |
| Hazard ID submission | Baseline is primarily form/list based; no full workflow evident. | Employee submits Hazard ID, record enters review/quarantine, HSE Manager reviews. | Add Submitted/Pending Review stage, review action, notifications, and review fields. | Must avoid slowing simple reporting; reviewer workload must be manageable. |
| HSE manager review | Current baseline has reviewer fields but no confirmed routing workflow. | Location HSE Manager reviews appropriateness, assigns action owner, sets due date. | Configure location-based assignment and role population. | Incorrect location hierarchy or missing role data will break routing. |
| Action assignment | Action Plan object exists; current user flow may require save-first creation. | HSE Manager assigns actions during review; optional first action can be captured inline. | Align Hazard ID action plan with Incident Management action-plan pattern; add workflow action creation rules if needed. | Auto-created actions require clear owner/due-date validation. |
| Closure | Hazard ID has closed date and reviewer comments fields. | Closure should occur after review/action completion or rejection as appropriate. | Add closure stage/action, closed date automation, status tracking. | Need definition of when a hazard can close with no action. |
| Rework/rejection | Baseline does not evidence formal return/reject workflow. | Reviewer should be able to reject inappropriate submissions or return for clarification. | Add reject/return actions and notifications. | Overuse may discourage reporting; wording should preserve safety culture. |
| Mobile/photo capture | Mobile tabs exist; photo capture and browser responsiveness need validation. | Field users should attach evidence during submission. | Configure attachment/documentation section inline if possible; test mobile and browser flow. | Mobile/browser differences may require UI customization. |

## 6. Data Model & Configuration Impacts

| Area | Current Configuration | Proposed Need | Recommended Change | Notes / Risks |
| --- | --- | --- | --- | --- |
| Quality Observation object | Exists as primary transactional object in Observations. | No longer primary user-facing quality intake if quality separation is accepted. | Hide/retire entry tabs; retain object for historical access; determine reporting/migration strategy separately. | Do not delete object or values while historical data exists. |
| Hazard ID object | Exists as primary HSE hazard object. | Remains as HSE observation concept, potentially surfaced under Incident Management. | Keep object; adjust navigation, security, workflow, and labels as needed. | Object may still technically live in Observations even if user navigation changes. |
| Hazard Type / category values | Baseline has Hazard Type and other lookup/config objects. | Harmonized NDT + Integra HSE/environment/security category list. | Export, map, hide obsolete values, add new ones. | Recaptioning affects existing records; requires governance. |
| Quality categories in observations | NDT uses some quality categories under improvement observations. | Remove quality categories from future HSE hazard reporting. | Hide/retire quality-oriented values from HSE Hazard ID taxonomy; preserve historical values for legacy records. | Need historical reporting treatment for legacy quality observation data. |
| Safe/Unsafe logic | Baseline action handler sets Safe/Unsafe from severity and clears severity when Safe. | May need to support unsafe, safe, positive/kudos, environmental/security categories. | Revalidate Safe/Unsafe logic against future hazard taxonomy. | Existing automation may not support positive observations or nuanced classifications. |
| Severity | Baseline includes Hazard Severity and Observation Severity. | Severity should drive reporting, review priority, and potentially Hazard ID review expectations. | Harmonize severity definitions with Incident Management where applicable. | Avoid cross-domain severity conflicts. |
| Location | Location and Specific Location objects/fields exist. | Location must drive HSE Manager assignment. | Make location required for submitted hazards; map each location to HSE Manager role. | Missing location data can prevent routing. |
| Action Plan relationship | Hazard ID references Action Plan; Observation references Action Plan. | Consistent action plan behavior with Incident Management. | Align fields, labels, required fields, and display layout. | Event Action Plan and Hazard Action Plan may be related but not identical objects. |
| Attachment/documentation | Attachment behavior not confirmed in baseline; photos raised as needed. | Attach photos/documents inline during hazard submission. | Add/validate attachment section in detail view and mobile view. | Save-first technical behavior may need workaround. |
| Quota | Quota lookup exists in baseline. | Future quota use was not resolved in the retrieved transcript evidence. | Confirm whether quota remains required for future program metrics. | Unused quota fields may confuse users/reporting. |

## 7. Reporting & Analytics Gaps

| Reporting Area | Current Capability | Requested / Needed Capability | Gap | Recommended Solution |
| --- | --- | --- | --- | --- |
| HSE hazard categories | Baseline has Hazard Type/Severity and inventory views. | Report hazards by harmonized HSE/environment/security category. | Current values may not match NDT categories and may include quality categories. | Harmonize hazard category master data before dashboard build. |
| Legacy Quality Observation reporting | Quality Observations currently reside in Observations. | Future Observations reporting should focus on HSE Hazard ID; historical quality observations may still require visibility. | Historical quality observation data and future quality data may be split. | Create legacy Quality Observation view/reporting treatment separate from future HSE Observations reporting. |
| HSE vs Quality dashboards | Current application blends quality and HSE concepts. | Separate HSE and quality reporting ownership. | Mixed data can distort KPI ownership. | Build separate domain dashboards and data definitions. |
| Action closure metrics | Action Plan relationship exists. | Track assigned actions, due dates, completion, overdue status by location/HSE Manager. | Current reporting design not evident. | Add action status dashboards tied to Hazard ID workflow. |
| Adoption / positive reporting | NDT referenced positive IDs and proactive reporting. | Track positive/proactive submissions separately from unsafe conditions if approved. | Safe/Unsafe logic may not provide enough reporting granularity. | Add classification values or reporting flags for positive/kudos/safe observations if approved. |

## 8. Security, Roles & Assignment Impacts

| Area | Current Logic | Future Need | Gap | Recommended Change |
| --- | --- | --- | --- | --- |
| Observations security groups | Baseline includes Observations Admin, Observations Supervisor, Observations Reporter. | Security should align with future HSE Hazard ID use and removal of quality intake from Observations. | Existing Observations groups may not map cleanly to the future separated model. | Redesign role mapping; retire or narrow Observations-specific groups if app is hidden. |
| HSE Manager reviewer | No confirmed baseline HSE Manager assignment workflow. | Route submitted Hazard IDs to location HSE Manager(s). | Missing location-based reviewer assignment. | Add HSE Manager role on location or equivalent assignment matrix. |
| Quality ownership | Quality Observation currently sits in Observations. | Quality team should own quality-process intake outside Observations. | Current Observations ownership may bypass intended quality ownership. | Remove quality submission access from Observations future-state navigation. |
| Submitter visibility | Current behavior may leave submitted records visible without clear status/owner. | Quarantine review before broader visibility, with clear status. | No confirmed visibility control. | Configure workflow statuses and security filters. |
| Incident Management access | Hazard ID may be surfaced in Incident Management. | Incident access should grant appropriate Hazard ID tab/object access. | Object may still live technically in Observations, requiring cross-app permissions. | Add Incident Management tab binding to Hazard ID list and align security. |
| Action owner permissions | Action Plan object exists. | Assigned users must update their actions without gaining excessive admin rights. | Permission model not confirmed. | Validate action-owner edit rights and HSE closure rights. |

## 9. Integration & Migration Considerations

| Area | Current State | Future Need | Recommended Approach | Risk |
| --- | --- | --- | --- | --- |
| Legacy Quality Observation data | Existing Quality Observation records may exist in Observations. | Determine whether to leave historical data in place or migrate/report separately. | Perform data volume/field mapping assessment; choose cutover, archival reporting, or migration. | Moderate to High |
| Legacy Hazard ID data | Existing Hazard ID records may remain in Observations object. | Preserve history while changing navigation/workflow. | Keep object and historical values; use hidden/retired values rather than deletion. | Moderate |
| Picklist migration | Current Intelex values and NDT values need alignment. | Harmonized enterprise HSE taxonomy. | Export current values, compare to NDT list, create mapping workbook, approve adds/hides/recaptions. | Moderate |
| Incident Management relationship | Hazard ID may be presented under Incident Management. | User-facing HSE intake may be consolidated under Incident Management. | Add Incident Management tab/view binding to Hazard ID object; adjust permissions. | Moderate |
| Quality process dependency | Quality observations are expected to move out of Observations. | Observations scope depends on confirmation of future quality process design. | Treat as cross-workstream dependency; do not over-design NCR details in Observations gap analysis. | High |
| Training/localization | No baseline integration evident. | Potential multilingual in-app training or guidance. | Treat as optional adoption enhancement; confirm content ownership and languages. | Low to Moderate |

## 10. Open Questions & Follow-Ups

| ID | Open Question | Why It Matters | Recommended Owner |
| --- | --- | --- | --- |
| OQ-001 | Will the separate NCR/CAPA design confirm that Quality Observation should be retired from future-state Observations use? | Observations redesign depends on whether quality intake definitively moves out of Observations. | Quality process owner / Dave McLean |
| OQ-002 | Should Quality Observation records be migrated, left in Observations as historical records, or reported separately? | Impacts data integrity, reporting continuity, and budget. | Project sponsor / Data migration lead |
| OQ-003 | Should the Observations application be hidden from users, with Hazard ID surfaced through Incident Management? | Determines navigation, permissions, training, and support model. | HSE leadership / Solution architect |
| OQ-004 | What are the final Hazard ID categories and subcategories? | Drives reporting, field behavior, and data harmonization. | HSE leadership / NDT + Integra SMEs |
| OQ-005 | Which values should be hidden, added, or recaptioned in current Hazard Type / category lists? | Recaptioning can change historical reporting meaning. | HSE data governance owner |
| OQ-006 | Should Hazard ID support safe/positive/kudos observations as a distinct classification? | Affects taxonomy, reporting, and Safe/Unsafe automation. | HSE leadership |
| OQ-007 | What is the exact workflow for rejected or inappropriate hazard submissions? | Needed for status model, notifications, and audit trail. | HSE process owner |
| OQ-008 | Who should review Hazard IDs when a location has no populated HSE Manager or multiple HSE Managers? | Prevents workflow routing failures. | Security/admin owner |
| OQ-009 | Are attachments/photos mandatory, optional, or conditional by hazard type/severity? | Impacts field requirements and mobile UI. | HSE process owner |
| OQ-010 | Will Hazard ID action plan fields use the same object/layout as Incident Management Event Action Plan or only a similar design? | Determines configuration complexity and reporting consistency. | Solution architect |
| OQ-011 | Is in-app training/multilingual content in scope for this phase? | Impacts budget and adoption plan. | Project sponsor / Training owner |
| OQ-012 | Is the Quota lookup still needed in the future-state Observations/Hazard ID process? | Unused configuration creates confusion and reporting noise. | HSE process owner |

## 11. Recommended Next Steps

| Priority | Recommendation | Purpose |
| --- | --- | --- |
| Critical | Confirm future-state Observations domain model: Quality intake moves out of Observations; HSE Hazard ID remains. | Establish scope boundary and avoid rework. |
| Critical | Confirm whether Quality Observation will be hidden/retired from user-facing Observations navigation. | Align application structure with REQ-001 and REQ-002. |
| High | Export baseline Hazard ID / Observation picklist values and run taxonomy harmonization workshop with NDT and Integra SMEs. | Decide add/hide/recaption actions while protecting historical data. |
| High | Design Hazard ID workflow with Submitted/Pending Review, HSE Review, Action Assignment, Closure, Reject/Return, and optional Rework. | Replace passive data capture with governed HSE review. |
| High | Define location-based HSE Manager role population and assignment rules. | Enable correct review routing and notifications. |
| High | Prototype user-facing HSE flow, including whether Hazard ID appears under Incident Management. | Validate application placement and worker-facing process flow. |
| Medium | Align Hazard ID action plan layout and behavior with Incident Management action-plan pattern. | Improve consistency and reduce training burden. |
| Medium | Validate mobile submission, photo attachment, and browser/mobile app behavior. | Ensure field usability. |
| Medium | Define historical data strategy for existing Quality Observations and Hazard IDs. | Preserve reporting continuity and auditability. |
| Medium | Build reporting requirements matrix for HSE hazards, legacy quality observations, and action closure. | Ensure dashboards match future ownership and compliance needs. |
| Low | Evaluate optional in-app training and multilingual guidance. | Improve global adoption after core process decisions are finalized. |

## 12. Assumptions, Risks & Constraints

- **Evidence-based conclusion:** The baseline Observations configuration includes Quality Observation and Hazard ID as distinct user-facing concepts, while the session direction is to separate quality and HSE paths.
- **Evidence-based conclusion:** The future quality process is not final within the Observations session and is dependent on the separate NCR/CAPA discussion.
- **Evidence-based conclusion:** HSE Hazard ID should remain available for observed unsafe/safe conditions where no impact has occurred and the situation is not a near miss or incident.
- **Evidence-based conclusion:** NDT’s desired HSE process includes quarantine/review by the HSE Manager, followed by action assignment and due-date determination.
- **Evidence-based conclusion:** Taxonomy harmonization is required, and value recaptioning must be handled carefully because it can affect existing data.
- **Inferred implementation implication:** Retiring Quality Observation from user navigation should be treated as a configuration/navigation and security change, not physical object deletion.
- **Inferred implementation implication:** If Hazard ID is surfaced under Incident Management, the object may still technically remain part of the Observations configuration, requiring cross-application tab/view/security alignment.
- **Inferred risk:** Historical quality observation data may become fragmented from future quality-process data unless a reporting or migration strategy is defined.
- **Inferred risk:** Location-based HSE Manager routing will fail if the location hierarchy or role population is incomplete.
- **Inferred risk:** If quality categories remain available in Hazard ID, future HSE reporting may continue to mix quality and HSE concepts.
- **Constraint:** Automatic Hazard ID-to-Incident conversion is technically possible but likely high effort and low value based on the meeting discussion.
- **Open dependency:** Final removal/retirement of Quality Observation from Observations depends on the agreed NCR/CAPA future-state process, but the Observations gap analysis should not define the NCR workflow itself.
