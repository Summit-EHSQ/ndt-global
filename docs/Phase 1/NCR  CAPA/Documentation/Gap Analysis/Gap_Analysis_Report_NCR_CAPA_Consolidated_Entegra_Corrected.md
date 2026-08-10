# Gap Analysis Report

# 1. Engagement Overview

| Item | Description |
|---|---|
| Application Reviewed | **NCR Capa v1.0.0.0**, including Nonconformance Reporting (NCR), Corrective Action Reporting (CAR), 8D CAR, and Supplier Corrective Action Report (SCAR) |
| Session Type | Two-part future-state gap-analysis and solution-design workshop |
| Transcript Reviewed | **Part 1:** Quality-event intake, observation/NCR routing, triage, classification, root-cause data, customer response, and lower-risk effectiveness review. **Part 2:** NCR-to-CAR escalation, 8D investigation, CAR validation, related events, TIR handling, SAP flat-file integration, and effectiveness review. |
| Current-State Documentation Reviewed | `NCR Capa(v1.0.0.0).ipack`, exported 2026-07-24 from Intelex platform version 6.6.16.2 |
| Primary Business Objective | Harmonize Entegra and NDT quality-event processing in Intelex while retaining necessary business-specific classifications; reduce manual handoffs; route records according to risk; standardize root-cause information; and improve reporting, investigation, and customer-response traceability |
| Key Stakeholders Referenced | Dave McLean, Michael Barthelmess, Niall Walsh, Tucker White, Øyvind Heimli, John, Sonja, Branka, Quality Managers, field personnel, project/account managers, integration/IT team |
| Analysis Date | 2026-07-24 |

The target operating model is a consolidated quality-event intake with differentiated processing based on risk and event type. Employees should be able to report what they know with a small initial data set. Quality personnel then complete triage, calculate or confirm risk, and route the event to a lightweight observation path, a lower-risk NCR path, or a higher-risk CAR/8D investigation.

The workshops also established that NCRs and CARs serve different purposes. The NCR is the initial nonconformance and risk-assessment record. The CAR is the investigative record and may be created from one or more NCRs, from another originating event, or independently. Higher-risk NCRs are expected to require a CAR based on an approved RPN/decision rule.

The principal drivers for change are:

- Process harmonization across historically different Entegra and NDT practices.
- Reduced reliance on email and Quality staff re-entering reports for field users.
- Consistent risk-based routing and enforcement.
- A single, reportable root-cause data structure.
- Better trending for reliability, investment, and resource-prioritization decisions.
- Reuse of NCR data in CAR/8D investigations.
- Structured preservation of Technical Investigation Reports (TIRs).
- Controlled customer-response tracking.
- SAP-derived customer, project, run, and technology metadata.
- Practical effectiveness verification for both frequent and long-tail failures.

# 2. Current-State Solution Summary

## Solution Scope and Architecture

The package contains four workflow-enabled record types:

- **NCR**
- **CAR**
- **8D CAR**
- **SCAR**

CAR, 8D CAR, and SCAR inherit from a shared **CAR Abstract** object. NCR inherits from a **Nonconformance Abstract** object. Shared application dependencies include Quality Comply Framework, Action Plans, Event Framework, Customer Complaint Reporting, Supplier Management Framework, My Tasks Summary, and other system/framework applications.

This shared architecture supports reuse, but changes to common CAR objects, fields, actions, or child records may affect CAR, 8D CAR, and SCAR.

## Workflow Architecture

| Record Type | Current Workflow | Current Assignment Model | Current Transition Controls |
|---|---|---|---|
| NCR | Draft → Triage → Verification → Closed, with Cancelled as a separate outcome | Draft uses Created By; Triage and Verification use Quality Management Role | Cancellation comments and no open Action Plans are required for cancellation. Disposition and Verification Due Date are required before verification. Verified By and Verification Date are required for closure. |
| CAR | Draft → Root Cause & Implementation → Verification of Effectiveness → Closed | Draft uses Reported By; implementation uses Assignee; verification uses Quality Management Role | Open Action Plans block movement to effectiveness verification. Effectiveness result, verification notes, verifier, and verification date are required for closure. “Further Action Required” returns the record to implementation. |
| 8D CAR | Draft → Root Cause & Implementation → Verification of Effectiveness → Closed | Same pattern as CAR | Same broad controls as CAR, with an additional team congratulations notification on closure. |
| SCAR | Draft → Root Cause & Implementation → Verification of Effectiveness → Closed | Same broad pattern as CAR, with helper-based assignee synchronization | Same broad controls as CAR. |

All packaged workflow actions have `RequireSignature = false`.

## Current Intake and Triage

- NCR has an initial Draft stage followed by Quality-led Triage.
- The package contains RPN, Criticality, Severity, Occurrence, and Detection-related configuration.
- NCR RPN is calculated as Severity × Occurrence × Detection.
- NCR Criticality is calculated as Severity × Occurrence.
- CAR Settings and NCR Settings contain RPN and Criticality threshold values.
- The package does not evidence an observation-specific workflow or lightweight observation form.
- The package does not evidence automatic pathway selection among observation, simple NCR, CAR, and 8D based on the configured thresholds.
- Effective security for allowing all employees to initiate NCRs cannot be confirmed from the package alone.

## Current Forms and Child Records

### NCR

The NCR form includes stage-based sections for:

- NCR Details
- Issues
- Disposition Details
- Verification Details

Related/child records include:

- Action Plans
- CAR Event
- NCR Costs
- Related Employees
- Attachments

### CAR / 8D CAR / SCAR

The corrective-action applications contain combinations of:

- Corrective Action Details
- Problem Definition
- Root Cause Analysis
- Team Members
- Action Plans
- Lessons Learned
- Cost
- Related Events
- Effectiveness Review Log
- Verification of Effectiveness
- Attachments

The current CAR-family workflows use three principal stages rather than separate workflow stages for each 8D discipline. The package contains 8D-oriented form content but does not evidence all future validation rules discussed in the workshop.

## Current Assignment and Access Behavior

- NCR Triage and Verification are assigned to Quality Management Role.
- CAR-family implementation work is assigned to an Assignee.
- CAR-family verification is assigned to Quality Management Role.
- Team Members are synchronized through shared CAR behavior.
- The package does not provide sufficient runtime evidence to confirm that adding a Team Member automatically grants the intended record access in every location/security context.
- The package does not establish how Quality Management Role resolves to the local site Quality Manager.

## Current Classification and Root-Cause Support

- The package contains multiple issue-classification lookups and shared Quality Comply lookups.
- Application-specific issue objects exist for areas such as General, Administration, Operations, Data Analysis, and Project Management.
- Root Cause Analysis is available as a child/related record in the CAR-family solution.
- The package does not evidence the agreed three-level **Category → Subcategory → Failure** model with:
  - dependent value filtering,
  - repeatable multiple entries,
  - Primary/Contributing designation,
  - organization/location-specific content,
  - and one consolidated reporting structure across simple NCR and CAR/8D pathways.

## Current Risk and Calculation Behavior

Confirmed calculations and controls include:

- NCR RPN = Severity × Occurrence × Detection.
- NCR Criticality = Severity × Occurrence.
- NCR Days Open calculation.
- NCR cost roll-up from NCR Cost records.
- Quantity validations for NCR and NCR Cost.
- CAR-family Date Reported validation.
- CAR-family prevention of verification while Action Plans remain open.
- Effectiveness-review due date derived from the latest Effectiveness Review Log date or transition date + 3.

The package does not evidence:

- mandatory CAR creation when an NCR exceeds a threshold,
- technology/location-specific threshold matrices,
- deriving CAR risk values from the highest related NCR,
- or requiring an override justification when CAR risk values are changed.

## Current Customer Response Support

The package summary does not evidence the workshop-requested combination of:

- Customer Response Requested,
- Customer Response Expected Date,
- Customer Response Text,
- Customer Submission Date,
- and closure validation tied to customer submission.

## Current Related-Record Behavior

- NCR and CAR-family applications reference related events.
- CAR can be associated with originating events through the Event Framework.
- The configuration supports related-event concepts, but the package does not evidence two distinct future relations:
  - **Originating Event**
  - **Thematically Related CAR**

The package also does not evidence the requested create-CAR-from-NCR action with field prepopulation.

## Current Attachments and TIR Support

- Attachments are enabled and exposed on the CAR-family forms.
- The package does not evidence a dedicated D4 TIR upload field.
- The package does not evidence automatic generation of a TIR document when a CAR is opened.
- The package does not evidence a structured endpoint or document format designed specifically for future AI parsing.

## Current Reporting Support

- Calculated fields and inventory views support basic reporting.
- Workflow transitions provide timestamps that can support start-to-close and stage-duration metrics.
- No approved future KPI catalogue, dashboard specification, or critical day-one report inventory was supplied.
- No evidence was supplied confirming how historical PowerApps/Entegra classifications must appear in future reporting.

## Current Integrations

The package evidences internal Intelex dependencies but no external SAP integration. It does not evidence:

- customer flat-file imports,
- project flat-file imports,
- run ID or technology metadata imports,
- project-selection snapshot behavior,
- or mapped TIR metadata generation.

# 3. Future-State Business Requirements Identified

| Requirement ID | Requirement / Need | Source Evidence | Explicit or Implied | Business Driver |
|---|---|---|---|---|
| REQ-001 | Provide one consolidated quality-event intake while supporting different business-specific classification content for Entegra and NDT. | Part 1, 02:18–04:20 | Explicit | Harmonization; Reporting; Adoption |
| REQ-002 | Route initial reports to a lightweight Observation path or a full NCR path based on initial answers and Quality triage. | Part 1, 04:20–06:26 | Explicit | Usability; Scalability; Process consistency |
| REQ-003 | Keep the Observation path condensed, action-plan driven, and approximately fewer than ten fields, with the ability to escalate/reclassify to NCR. | Part 1, 04:20 | Explicit | Adoption; Efficiency |
| REQ-004 | Avoid repeatedly asking users to select a process path; use entered data and business logic to route records. | Part 1, 06:26 | Explicit | Automation; Consistency |
| REQ-005 | Allow any employee to initiate an NCR, with Quality responsible for completing missing information and triage. | Part 1, 09:16–15:52 | Explicit | Adoption; Governance; Reduced manual handoffs |
| REQ-006 | Require only a minimum initial data set for lower-risk reporting: description, date, department, and location. | Part 1, 38:11 | Explicit | Usability; Adoption |
| REQ-007 | Use Quality-led triage to establish completeness, calculate/confirm RPN, prioritize the case, and select the processing path. | Part 1, 09:16; 25:18; 38:11 | Explicit | Governance; Risk management |
| REQ-008 | Enforce an 8D/CAR investigation when approved RPN or other recurrence/criticality criteria are met. | Part 1, 25:18–36:21; Part 2, 11:59 | Explicit, threshold values pending | Compliance; Consistency; Risk management |
| REQ-009 | Permit lower-risk NCRs to proceed through a simpler corrective-action/verification path and, where justified, close with no additional action after immediate compensating action. | Part 1, 38:11 | Explicit | Proportionality; Efficiency |
| REQ-010 | Capture event classifications for statistics, trending, recurrence detection, and prioritization. | Part 1, 45:39–52:14 | Explicit | Reporting; Reliability; Investment decisions |
| REQ-011 | Support dependent classification choices and business/location-specific content rather than one static enterprise list. | Part 1, 45:39; 01:23:16 | Explicit | Data quality; Harmonization |
| REQ-012 | Separate initial observed issue/effect from final root-cause classification and allow classifications to be refined later. | Part 1, 53:32–01:00:35 | Explicit | Analytical integrity; Data quality |
| REQ-013 | Make 5 Why analysis available but not mandatory for every low-priority NCR. | Part 1, 56:23–01:05:06 | Explicit | Usability; Proportionality |
| REQ-014 | Store final root-cause conclusions in one repeatable root-cause grid regardless of whether the investigation is simple, 5 Why, or 8D. | Part 1, 01:07:17–01:16:19 | Explicit | Single source of truth; Reporting |
| REQ-015 | Use a three-level root-cause model: Category, Subcategory/Process Location, and Failure. | Part 1, 01:10:16 | Explicit | Trending; Reliability; Design FMEA alignment |
| REQ-016 | Allow multiple root causes per event, identify each as Primary or Contributing, and capture free-text context. | Part 1, 01:16:19 | Explicit | Reporting; Investigation quality |
| REQ-017 | Capture a concise customer-facing root-cause statement regardless of processing path. | Part 1, 01:30:27 | Explicit | Customer communication |
| REQ-018 | Add Customer Response Requested, Expected Date, Response Text, and Customer Submission Date fields; require the submission date before closure when a response is required. | Part 1, 01:30:27–01:38:43 | Explicit | Customer governance; Traceability |
| REQ-019 | Quality drafts the customer response; the Project Manager or Account Manager delivers it to the customer. The system must not automatically send the response. | Part 1, 01:30:27 | Explicit | Communication control; Governance |
| REQ-020 | Perform a secondary Quality verification before NCR closure. | Part 1, 01:38:43 | Explicit | Quality assurance; Governance |
| REQ-021 | Make effectiveness evaluation conditional for lower-risk NCRs according to defined criteria rather than mandatory for every case. | Part 1, 01:38:43 | Explicit, criteria pending | Proportionality; Compliance |
| REQ-022 | Report start-to-close and stage-duration KPIs using workflow timestamps. | Part 1, 01:38:43 | Explicit | Performance management |
| REQ-023 | Treat NCR as the initial event/risk record and CAR as the investigative record; permit CARs to exist independently or relate many-to-many with NCRs. | Part 2, 08:01; 26:06 | Explicit | Process design; Recurrence aggregation |
| REQ-024 | Create CARs from NCRs with correlated field prepopulation to avoid manual re-entry. | Part 2, 13:05 | Explicit | Efficiency; Data quality |
| REQ-025 | Reorganize and recaption CAR content to align with an 8D-inspired D1–D7 investigation structure. | Part 2, 13:05–15:00 | Explicit | Methodology alignment; Usability |
| REQ-026 | Keep Quality Manager ownership of the CAR process without an additional CAR triage stage. | Part 2, 15:00 | Explicit | Accountability; Process simplicity |
| REQ-027 | Give CAR Team Members appropriate access to view and work the investigation record. | Part 2, 15:00 | Explicit | Collaboration; Security |
| REQ-028 | Default CAR Severity, Occurrence, and Detection from the highest values among related NCRs; make them read-only by default and require a comment to override. | Part 2, 16:50–26:06 | Proposed compromise with concurrence; final calculation detail pending | Risk governance; Traceability |
| REQ-029 | Support separate relations for Originating Event and Thematically Related CARs. | Part 2, 01:14:25 | Explicit decision | Data integrity; Reporting |
| REQ-030 | Before CAR investigation can progress, require at least one assigned person, complete D2 data, and at least one D3, D4, D5, and D6 record; require a related originating event; do not require cost. | Part 2, 01:18:21 | Explicit | Investigation completeness; Governance |
| REQ-031 | Assign effectiveness verification to the local site Quality Manager through a configurable role model. | Part 2, 01:19:53 | Explicit | Accountability; Security |
| REQ-032 | Provide a dedicated D4 TIR upload location when TIR presence is to be validated, and keep the TIR accessible throughout the CAR. | Part 2, 49:52–58:13 | Explicit direction; mandatory-use rule pending | Knowledge retention; Validation |
| REQ-033 | Preserve TIR content in a consistent, identifiable structure suitable for future AI ingestion and historical investigation search. | Part 2, 49:52–56:21 | Explicit future-readiness requirement | Knowledge management; Future automation |
| REQ-034 | Support generation or availability of a TIR template with available Intelex metadata populated from CAR/project data. | Part 2, 58:13–01:01:34 | Explicit desired behavior; mapping pending | Efficiency; Data quality |
| REQ-035 | Import selected SAP customer, project, run, and technology metadata through flat-file Excel/CSV integration, with business-defined fields and snapshot population when a project is selected. | Part 2, 01:01:34–01:05:33 | Explicit, field list pending | Integration; Efficiency; Master data |
| REQ-036 | Support structured D7 Lessons Learned information and an Effectiveness Review Log. | Part 2, 01:22:00 | Explicit | Knowledge retention; Continuous improvement |
| REQ-037 | Define a practical effectiveness-review model that can address both frequent failures and long-tail/low-frequency validation opportunities. | Part 2, 01:22:00–01:36:45 | Explicit need; final design pending | Risk management; Operational practicality |
| REQ-038 | When a failure recurs after closure, support linking the new NCR/CAR to prior cases and escalating priority/RPN as appropriate. | Part 2, 01:26:47–01:36:45 | Explicit operational expectation; exact rule pending | Recurrence management; Traceability |
| REQ-039 | Use site-level action assignments to drive training follow-up in the LMS rather than tightly coupling action completion to LMS completion in the current scope. | Part 2, 34:36–49:52 | Explicit scope direction | Scope control; Adoption |
| REQ-040 | Preserve workflow timestamps and reporting relationships so originating-event risk and thematic relationships do not contaminate each other’s calculations. | Part 2, 01:14:25 and Part 1, 01:38:43 | Explicit / Implied | Reporting integrity |

# 4. Gap Analysis

| Gap ID | Area | Current-State Behavior | Future-State Requirement | Gap Description | Recommended Change | Configuration vs Customization | Affected Components | Priority | Risk / Complexity |
|---|---|---|---|---|---|---|---|---|---|
| GAP-001 | Observation intake | No observation-specific workflow or condensed observation form is evidenced. NCR begins in Draft and proceeds through Triage. | REQ-002, REQ-003 | The desired lightweight observation path, limited field set, action-driven handling, and escalation to NCR do not exist in the evidenced package. | Design an Observation record type or controlled NCR subtype/path with a condensed form, minimal required fields, action-plan support, closure controls, and a governed conversion/escalation action that preserves history. | Likely configuration plus workflow/business-rule customization | Workflow stages/actions, forms, fields, record type/subtype, Action Plans, notifications, reporting, conversion logic | Critical | High |
| GAP-002 | Automated pathway routing | Threshold fields and RPN calculations exist, but no evidenced rule automatically selects Observation, simple NCR, CAR, or 8D. | REQ-004, REQ-007, REQ-008 | Users/Quality may still make manual and potentially inconsistent routing decisions. | Define a decision table using approved inputs, RPN, recurrence, criticality, technology, and exceptions. Configure routing and prevent incompatible actions once the path is determined, while retaining an auditable Quality override. | Configuration plus workflow scripting/business rules | NCR workflow, CAR/8D creation action, configuration objects, validations, audit/comment fields | Critical | High |
| GAP-003 | RPN threshold governance | Current settings contain RPN/Criticality thresholds, but the package does not evidence the approved threshold values, technology-specific logic, or mandatory CAR enforcement. | REQ-008 | The existing thresholds are not sufficient evidence of the future decision model. | Complete the threshold workshop; document formulas, dimensions, site/technology variations, boundary conditions, override authority, and test cases. Store approved rules in governed configuration objects where practical. | Configuration; customization only if matrix logic exceeds standard configuration | NCR Settings, CAR Settings, risk fields, routing rules, reports | Critical | High |
| GAP-004 | Broad employee initiation | NCR Draft uses Created By, but runtime security and the minimum-entry experience for all employees are not established. | REQ-005, REQ-006 | The target self-service intake may be blocked by permissions, required fields, or form complexity. | Validate role/location security; configure an employee intake view with only Description, Date, Department, Location, and essential context; assign Triage to Quality for completion. | Configuration | Security roles, form/view, required fields, workflow assignment, notifications | High | Moderate |
| GAP-005 | Lower-risk NCR completion path | Current NCR follows Draft → Triage → Verification → Closed, with closure validations. No explicit “no further action after immediate correction” outcome is evidenced. | REQ-009, REQ-020, REQ-021 | Lower-risk records may be over-processed or inconsistently closed. | Add a controlled triage outcome for immediate correction/no further action, requiring rationale and evidence. Define when secondary verification and effectiveness review are required or bypassed. | Configuration plus workflow logic | NCR actions/stages, disposition fields, verification, effectiveness rules, reports | High | Moderate |
| GAP-006 | Initial issue versus final cause | Current issue lookups and root-cause records exist, but the package does not evidence a formal separation and controlled refinement between observed effect and final cause. | REQ-010, REQ-012 | Early reporter classifications may be treated as final cause, degrading analytics. | Separate “Observed Issue/Effect” fields from “Final Root Cause” records. Keep initial classifications editable by authorized Quality users while preserving change history or workflow evidence. | Configuration | NCR fields, root-cause child object, forms, permissions, reporting | High | Moderate |
| GAP-007 | Three-level dependent classification | Multiple lookup objects exist, but no single evidenced Category → Subcategory → Failure dependency model spans all pathways. | REQ-011, REQ-015 | Current lookup structure may not provide the agreed fault-tree behavior or consistent reporting. | Import the PowerApps lists and mapping cardinalities; implement dependent lookups with governance for one-to-many/many-to-many relationships and organization/location applicability. | Configuration; possible custom filtering depending on cardinality | Lookup/configuration objects, forms, child grid, imports, reports | Critical | High |
| GAP-008 | Unified root-cause grid | Root Cause Analysis exists, but the exact future repeatable structure with multiple causes, Primary/Contributing flag, three-level classification, and free-text context is not evidenced. | REQ-013–REQ-017 | Root-cause data could remain split between issue fields, 5 Why, and CAR/8D child records, requiring complex joins and producing inconsistent KPIs. | Extend or replace the existing root-cause child object with one shared model used by simple NCR, 5 Why, CAR, and 8D. Make 5 Why optional but write final conclusions to the same grid. | Configuration plus data-model change; possible customization for cross-application reuse | Root Cause Analysis object, NCR/CAR relations, 5 Why components, forms, reports, migration | Critical | High |
| GAP-009 | Root-cause master-data governance | Current lookups are distributed across application-specific and shared framework objects. Ownership and organization-specific values are not defined. | REQ-001, REQ-011, REQ-015 | Harmonization can either erase valid business differences or preserve duplicate/inconsistent classifications. | Establish global versus business-specific values, data owners, approval process, effective dates, deprecation rules, and reporting crosswalks. | Governance plus configuration | Lookup objects, location/org filters, import templates, reports | High | High |
| GAP-010 | Historical classification migration | No approved migration requirement or mapping from current PowerApps/Entegra values to the future root-cause grid is supplied. | REQ-010, REQ-014–REQ-016 | Historical trending and day-one reports may break or require separate legacy logic. | Inventory critical reports; decide whether to transform historical selections, preserve legacy fields, or provide a reporting crosswalk. Prototype migration using representative records. | Data migration/configuration | Legacy fields, root-cause grid, lookup mappings, reports, ETL/import processes | High | High |
| GAP-011 | Customer response controls | Requested customer-response fields and closure validation are not evidenced in the current package. | REQ-017–REQ-019 | Customer commitments, draft response, delivery ownership, and actual submission date cannot be consistently tracked. | Add the requested fields in Triage/Verification. Conditionally require Expected Date and Submission Date. Configure workflow ownership so Quality drafts the response and the Project Manager or Account Manager is responsible for customer delivery. Configure notifications/tasks without automatic external sending. | Configuration | NCR fields/forms, workflow validations, notifications, reports, security | High | Moderate |
| GAP-012 | NCR-to-CAR creation and prepopulation | Related-event concepts exist, but a create-CAR-from-NCR action with data transfer is not evidenced. | REQ-023, REQ-024 | Quality users must manually re-enter issue, project, customer, location, and risk data, increasing effort and inconsistency. | Add a controlled “Create/Link CAR” action from NCR. Prepopulate approved fields and preserve source links. Support one CAR from multiple NCRs and multiple CARs from one NCR without duplicating or overwriting data. | Configuration plus custom action/business logic | NCR actions, CAR creation, related events, field mappings, permissions, notifications | Critical | High |
| GAP-013 | Mandatory CAR creation | Current RPN calculation does not evidence an enforced requirement to launch/link a CAR above threshold. | REQ-008, REQ-023 | High-risk NCRs may close without the required investigation. | At Triage, block progression or closure when the CAR-required condition is met and no qualifying CAR is linked. Allow only an authorized, commented exception if governance approves one. | Workflow configuration plus validation logic | NCR Triage, CAR relation, RPN fields, exception fields, reports | Critical | High |
| GAP-014 | CAR form and 8D alignment | CAR/8D forms contain investigation content, but the workshop identified recaptioning/reorganization needs and the workflow has only broad stages. | REQ-025, REQ-026 | Users may not experience a clear D1–D7 investigation sequence, even where the data exists. | Map every current field/child grid to D1–D7, remove duplicates, recaption sections, and define which disciplines are form sections versus workflow gates. Retain Quality ownership without adding redundant CAR triage. | Configuration | CAR/8D forms, containers, field captions, workflow actions, permissions | High | Moderate |
| GAP-015 | CAR minimum completion criteria | Current controls focus on open Action Plans and final effectiveness fields. The package does not evidence all agreed D2–D6 minimum record-count and related-event requirements. | REQ-030 | CARs may progress without a complete problem statement, containment, cause analysis, corrective action, preventive action, team assignment, or originating event. | Configure transition validations for at least one assigned person, complete D2, and at least one D3/D4/D5/D6 record. Require Originating Event except for a governed independent-CAR reason. Keep cost optional. | Configuration plus validation rules | CAR workflow actions, Team Members, D2 fields, D3–D6 child objects, Related Events | Critical | High |
| GAP-016 | CAR RPN inheritance and override | No evidenced logic derives CAR Severity/Occurrence/Detection from the highest related NCR values or controls overrides. | REQ-028, REQ-040 | Risk can be re-entered inconsistently, and many-to-many relations complicate source selection and calculation. | Define aggregation precisely—highest component values versus highest complete NCR RPN—and configure default/read-only values. Add an authorized override action with mandatory justification and retain original values. | Custom calculation/business logic plus configuration | CAR risk fields, NCR-CAR relation, override fields/action, audit/reporting | High | High |
| GAP-017 | Originating versus thematic relations | Current related-event support does not evidence separate relation types for origin and thematic similarity. | REQ-029, REQ-040 | Using one relation for both purposes can contaminate RPN derivation, counts, recurrence analysis, and traceability. | Create distinct relations and views: Originating Events and Related/Similar CARs. Restrict RPN derivation to originating NCRs. | Configuration/data-model change | Related-event objects, CAR/NCR forms, calculations, reports | High | Moderate |
| GAP-018 | Team access and local ownership | Team-member synchronization and Quality Management Role exist, but runtime access inheritance and site-local role resolution are not confirmed. | REQ-027, REQ-031 | Team members may lack required access, or verification may route to the wrong Quality group. | Test record-level access for team members; define a location-to-Quality-role mapping; configure assignment fallback and reassignment behavior. | Configuration; possible security customization | Security roles, workflow subjects, Team Members, Location, notifications | High | High |
| GAP-019 | TIR field, validation, and document handling | CAR-family records currently use general attachments. No dedicated D4 TIR field or generated TIR template is evidenced. | REQ-032–REQ-034 | TIRs may be inconsistently named/stored, cannot be conditionally validated, and are harder to ingest for future search/AI. | Add a dedicated D4 TIR document field or child record with document type/status metadata. Keep it visible across CAR stages. Decide whether it is mandatory by CAR type. Configure template generation/population after field mapping is approved. | Configuration plus document-generation customization/integration | D4 form, attachment/document object, validations, template mapping, permissions | High | High |
| GAP-020 | SAP flat-file integration | No external SAP imports are evidenced in the package. | REQ-035 | Customer, project, run, and technology data must be entered manually and may not use authoritative identifiers. | Hold the integration field-definition session. Build governed Excel/CSV imports for agreed endpoints and fields; define keys, frequency, rejection handling, ownership, and project-selection snapshot mapping. | Integration customization plus configuration | Customer/project/technology reference objects, import jobs, CAR/NCR forms, TIR mapping, error logs | Critical | High |
| GAP-021 | Effectiveness review model | Current CAR-family workflow has a simple effectiveness step and log; no recurring scheduled review workflow is evidenced. Lower-risk NCR effectiveness criteria are undefined. | REQ-021, REQ-036–REQ-038 | The solution cannot consistently handle sampled low-risk reviews, scheduled reviews, or long-tail failures without leaving CARs open indefinitely or closing without adequate evidence. | Define case-type/site criteria, closure evidence, review windows, recurrence checks, reopen-versus-new-CAR rules, and ownership. Configure only the recurring reviews the business commits to execute. | Design decision followed by configuration; possible scheduling/report customization | NCR/CAR workflow, Effectiveness Review Log, scheduled notifications, recurrence views, related records | High | High |
| GAP-022 | Process-audit linkage | Current package does not evidence a designed action to trigger or link a process audit for effectiveness verification. | Workshop Part 2, 01:19:53 | The business raised the capability, but timing and whether CAR remains open are undecided. | Treat as an open design option. Define qualifying cases, audit application, trigger timing, ownership, closure dependency, and reporting before implementation. | Pending decision; likely configuration/integration with audit application | CAR verification, audit records, workflow, notifications, reports | Medium | High |
| GAP-023 | KPI and day-one reporting | Workflow timestamps and calculated fields exist, but no approved report/dashboard catalogue or legacy-report mapping is supplied. | REQ-010, REQ-022, REQ-040 | The system may capture data without delivering the required operational, Pareto, stage-time, recurrence, or customer-response reports. | Run a reporting workshop; define KPI formulas, filters, primary-versus-contributing cause views, site rollups, and historical continuity. Build acceptance datasets and reconcile against current reports. | Reporting configuration; possible data-model work | Reports, dashboards, inventory views, root-cause grid, workflow history | High | Moderate |
| GAP-024 | Currency and cost normalization | Current solution captures cost records and rolls up NCR cost, but no evidenced multi-currency model or conversion table exists. | Workshop Part 2, 01:06:15 | Native-currency and USD-normalized reporting was proposed, but cost scope and update frequency are not approved. | Record as a scope decision. If approved, add currency code, native amount, managed exchange-rate table, conversion date/rate, and base-currency calculation. | Pending scope; configuration plus calculation logic | NCR/CAR Cost, configuration object, reports, SAP data | Medium | Moderate |
| GAP-025 | LMS interaction | Action Plans exist, but no direct LMS coupling is evidenced. Workshop direction favors site tasks rather than tight integration. | REQ-039 | Without explicit scope wording, teams may assume automatic enrollment/completion synchronization. | Document LMS automation as out of current scope. Use Action Plans assigned to site owners with LMS reference/evidence fields if needed. | Configuration; no tight integration in current scope | Action Plans, fields, notifications, scope documentation | Low | Low |
| GAP-026 | Auditability and controlled overrides | Core object metadata shows audit disabled; future design includes risk overrides, reclassification, and potentially reopening. | REQ-002, REQ-008, REQ-012, REQ-028, REQ-038 | Important decisions may not have sufficient traceability if changes rely only on current values or comments. | Confirm compliance requirements for field audit, workflow comments, reclassification history, CAR-risk override history, and reopening. Enable or design traceability controls accordingly. | Configuration/governance; customization only if standard audit is insufficient | Audit settings, history fields, workflow comments, reports, security | High | High |

# 5. Open Questions & Follow-Ups

| ID | Open Question | Why It Matters | Recommended Owner |
|---|---|---|---|
| OQ-001 | What exact inputs and thresholds route an event to Observation, simple NCR, CAR, or 8D? | Required to implement deterministic routing and acceptance tests. | Niall Walsh / Michael Barthelmess / NDT-Entegra Quality Leadership |
| OQ-002 | Are thresholds global, technology-specific, site-specific, or based on a matrix of RPN, recurrence, and criticality? | Determines configuration-object design and complexity. | Quality Governance / Solution Architect |
| OQ-003 | What is the approved override process when Quality disagrees with the calculated route? | Needed for governance, permissions, comments, and auditability. | Quality Leadership / Compliance |
| OQ-004 | What security role represents “any employee,” and are there confidential/location-restricted NCR types? | Broad intake must not expose restricted records. | Security Owner / HR / Quality |
| OQ-005 | What exact fields are included in the Observation form and employee NCR intake form? | Needed to meet the under-ten-field usability target without omitting required context. | Process Owner / UX Lead |
| OQ-006 | Is Observation a separate object, an NCR subtype, or a workflow branch? | Affects conversion, numbering, reporting, migration, and complexity. | Solution Architect / Product Owner |
| OQ-007 | What constitutes sufficient immediate compensating action for closure with no further action? | Prevents inconsistent low-risk closure. | Quality Process Owner |
| OQ-008 | What are the three PowerApps classification lists, their identifiers, relationships, and one-to-many/many-to-many rules? | Required to build dependent selections and migration mappings. | Michael Barthelmess |
| OQ-009 | Which classification values are global versus Entegra-, NDT-, technology-, or location-specific? | Determines master-data governance and reporting harmonization. | Data Owner / Quality Governance |
| OQ-010 | Must historical classifications be transformed into the new root-cause grid, crosswalked for reporting, or retained as legacy values? | Determines migration scope and continuity of trend reports. | Tucker White / Reporting Owner / Data Migration Lead |
| OQ-011 | Which day-one reports and KPIs are mandatory? | Drives field design, migration, root-cause structure, and acceptance criteria. | Tucker White / Quality Reporting Owner |
| OQ-012 | For CAR risk inheritance, should the system use the highest complete NCR RPN or independently select the highest Severity, Occurrence, and Detection values across all related NCRs? | The two methods can produce materially different CAR risk values. | Quality Risk Owner |
| OQ-013 | Can a mandatory high-RPN CAR be waived, and by whom? | Determines transition validation, exception tracking, and reporting. | Quality Leadership / Compliance |
| OQ-014 | For independent CARs, what replaces the otherwise mandatory Originating Event? | Needed to reconcile independent CAR support with the agreed related-event validation. | CAR Process Owner |
| OQ-015 | Which NCR fields prepopulate CAR, and which remain synchronized versus snapshot-only? | Prevents unintended updates and data ownership conflicts. | Business Analyst / Solution Architect |
| OQ-016 | Does adding a Team Member grant access through existing security, or is explicit record sharing required? | Must be proven before relying on the collaboration model. | Security Architect / Intelex Technical Lead |
| OQ-017 | How is the local Quality Manager resolved by site, and what is the fallback when no mapping exists? | Determines assignment reliability. | Quality Governance / Security Owner |
| OQ-018 | Is the TIR mandatory for every CAR, only selected CAR types, or only when a technical investigation is performed? | Determines field placement and transition validation. | Michael Barthelmess / CAR Process Owner |
| OQ-019 | What TIR template version, metadata fields, file format, naming convention, and generation mechanism are required? | Needed for document generation and future AI ingestion. | TIR Owner / Integration Lead / Solution Architect |
| OQ-020 | Which SAP fields are required for customers, projects, run IDs, technologies, and related project metadata? | Defines in-scope flat-file interfaces and the approximately ten fields per import. | Niall Walsh / Branka / Business Data Owners |
| OQ-021 | What are the SAP file frequency, keys, delta/full-load method, rejection process, and support ownership? | Required for a supportable integration design. | SAP/Integration Team |
| OQ-023 | Which lower-risk NCRs require effectiveness evaluation, sampling, or no review? | Required to configure a compliant proportional model. | Quality/ISO Process Owner |
| OQ-024 | Are recurring CAR reviews required at 1, 3, 6, and 12 months, or was that only a design option? | Avoids building a schedule the business will not execute. | CAR Process Owner |
| OQ-025 | On recurrence, should the prior CAR reopen, should a new CAR be created, or should the action depend on elapsed time and severity? | Determines workflow, relation, and KPI behavior. | Quality Governance |
| OQ-026 | Should process audits be triggerable from CAR, and must a CAR remain open until the audit is complete? | Determines cross-application design and closure timing. | Audit Process Owner / CAR Process Owner |
| OQ-027 | Is normalized USD cost reporting in project scope? | The workshop identified it as adjacent and potentially a commercial scope change. | Project Sponsor / Commercial Lead |
| OQ-028 | Is audit history required for classification changes, risk overrides, reclassification, relation changes, and reopening? | Core audit is currently disabled. | Compliance / Records Management |
| OQ-029 | Is the packaged NCR reopen action valid against the currently published stages, and should future recurrence use reopening at all? | Existing technical behavior requires validation before reuse. | Intelex Technical Lead / QA Lead |
| OQ-030 | Is SCAR part of the same harmonized design, or will its older published workflow remain distinct? | Shared CAR changes could affect SCAR. | Supplier Quality Process Owner |

# 6. Recommended Next Steps

| Priority | Recommendation | Purpose |
|---|---|---|
| 1 | Complete the internal threshold and routing workshop led by Niall Walsh with Michael Barthelmess and Quality stakeholders. | Approve the decision table for Observation, simple NCR, CAR, and 8D, including overrides and exceptions. |
| 2 | Obtain the three PowerApps lists and relationship mappings from Michael Barthelmess. | Establish the source data for dependent Category/Subcategory/Failure lookups. |
| 3 | Conduct a classification and root-cause data-model workshop. | Finalize observed issue versus final cause, the shared grid, Primary/Contributing logic, 5 Why interaction, organization filtering, and governance. |
| 4 | Conduct a reporting and historical-data workshop led by the Quality reporting owner/Tucker White. | Confirm day-one reports, KPI definitions, historical mapping, and migration requirements. |
| 5 | Prototype the employee intake, Observation path, and Quality Triage form. | Validate the under-ten-field experience, access, routing visibility, and escalation behavior with field users and Quality. |
| 6 | Produce the NCR-to-CAR functional design. | Define mandatory CAR rules, create/link actions, many-to-many behavior, field prepopulation, source ownership, and CAR risk inheritance. |
| 7 | Map and redesign the CAR form against D1–D7. | Recaption/reorganize fields, remove duplication, and define stage-exit validations. |
| 8 | Run a security and assignment proof-of-concept. | Confirm all-employee initiation, Team Member access, local Quality Manager routing, and fallback logic. |
| 9 | Schedule the SAP integration discussion with Niall Walsh, Branka, business data owners, and the integration team. | Finalize imported endpoints, fields, file mechanics, keys, cadence, validation, support, and snapshot behavior. |
| 10 | Finalize the TIR design. | Decide mandatory conditions, dedicated D4 storage, template mapping, document generation, metadata, and future AI-readiness. |
| 11 | Define the effectiveness-review operating model. | Approve conditional low-risk review, recurring CAR reviews, long-tail closure evidence, recurrence searches, and reopen/new-CAR rules. |
| 12 | Review scope boundaries and commercial impacts. | Confirm costs/currency, process-audit linkage, advanced AI similarity, and any integration beyond flat files as in-scope, deferred, or change-controlled. |
| 13 | Build a requirements traceability matrix and risk-based QA plan. | Trace each REQ and GAP to configuration/customization, design decisions, test cases, and business acceptance. |
| 14 | Perform regression analysis across CAR, 8D CAR, and SCAR before modifying shared objects. | Prevent shared CAR Abstract changes from unintentionally altering supplier or existing corrective-action behavior. |

# 7. Assumptions, Risks & Constraints

## Assumptions

- The `.ipack` export is an accurate representation of the current configured solution components included in scope.
- The two workshop transcripts represent the current direction but do not replace formal design approval for unresolved items.
- “Intellect” and “Intellects” in the meeting notes refer to the Intelex solution under review.
- AD references in Part 1 are treated as 8D-style corrective-action investigation references unless the business defines a separate methodology.
- Current Action Plan capability can support single, activity-based, and global action patterns through the dependent Action Plans application; detailed configuration was not fully available in the package.
- The flat-file SAP integration is in scope, but its field list and operating design are not yet approved.
- CARs may be independent even though the workshop also proposed making an Originating Event mandatory; the final design must reconcile this apparent exception.

## Risks

- **Routing risk:** Without approved thresholds and exception logic, automated routing could send events to an inappropriate process or permit inconsistent manual decisions.
- **Adoption risk:** A complex employee intake or mandatory 5 Why analysis would discourage reporting and recreate email/manual handoffs.
- **Data-model risk:** Storing issue and root-cause classifications in multiple locations would impair Pareto analysis, KPI consistency, and future AI use.
- **Master-data risk:** Business-specific picklists may fragment enterprise reporting unless governed mappings and common dimensions are established.
- **Migration risk:** Historical PowerApps/Entegra values may not map cleanly to the new three-level model.
- **Many-to-many risk:** CAR risk derivation becomes ambiguous when multiple NCRs with different risk profiles are linked.
- **Shared-object risk:** CAR, 8D CAR, and SCAR inherit common behavior; changes may have cross-application effects.
- **Security risk:** All-employee reporting and Team Member collaboration require tested location, confidentiality, and record-access controls.
- **Customer-communication risk:** Automatic distribution of draft responses could expose unapproved content; the workshop explicitly rejected premature auto-send behavior.
- **Integration risk:** Flat files introduce timing, duplicate, stale-data, key-matching, rejection, and support concerns.
- **Knowledge-retention risk:** Unstructured TIR attachments will be difficult to classify, validate, search, migrate, or use for future AI analysis.
- **Effectiveness risk:** Long-tail failures may not recur within a practical open-CAR period, making “proof of effectiveness” difficult.
- **Operational-capacity risk:** Recurring reviews and historical-case checks will fail if ownership and workload are not realistic.
- **Reporting risk:** Primary and contributing root causes, originating events, and thematic relations must be modeled distinctly to prevent misleading counts and risk calculations.
- **Auditability risk:** Risk overrides, reclassification, relationship changes, and reopening may not be adequately traceable while core object audit remains disabled.
- **Scope risk:** Cost normalization, process-audit linkage, advanced AI similarity, and tighter LMS automation may trigger design or commercial changes.

## Constraints

- Threshold values, recurrence rules, technology nuances, and approved routing inputs remain undefined.
- The PowerApps category, subcategory, and failure lists and their relationships were not supplied.
- Critical day-one reports and historical-data migration requirements remain unconfirmed.
- SAP import fields, keys, frequency, ownership, and error handling remain undefined.
- The exact TIR template and metadata mapping were not supplied.
- Effectiveness-review cadence and reopen-versus-new-CAR rules remain open.
- Package analysis cannot prove runtime permissions, group membership, notification delivery, scheduled processes, or environment-specific extensions.
- The current scope favors file-based SAP integration and does not include a real-time API design.
- Tight LMS completion integration is not part of the current direction.
- No live foreign-exchange integration was approved.
- Future AI-assisted similarity detection was discussed as a potential enhancement, not a committed current requirement.

## Inferred Analysis

The following are implementation inferences, not newly invented business requirements:

- The lowest-risk implementation path may be to retain NCR as the governed quality-event object and introduce an Observation subtype/branch, but a separate Observation object may offer cleaner security and reporting. This must be decided in design.
- Existing RPN and threshold fields provide a useful foundation, but a single numeric threshold may not support the desired recurrence, criticality, technology, and location nuances.
- The existing Root Cause Analysis child structure should be assessed for extension before creating a new object, because reuse would reduce migration and reporting complexity if it can support the agreed model.
- The NCR-to-CAR action will likely require custom field-mapping logic because the target supports many-to-many relationships and derived risk values.
- CAR risk values should preserve source provenance and calculation timestamp, especially when related NCRs are added or removed after CAR creation.
- A dedicated TIR child/document record may provide stronger metadata, versioning, and AI-readiness than a single generic attachment field, but the simplest compliant design should be selected.
- Scheduled effectiveness reviews should be implemented only after owners commit to acting on them; otherwise they will create overdue noise without improving quality.
- Recurrence analysis will initially depend on disciplined classification. AI similarity may supplement, but should not replace, governed categories and explicit relationships.
- All shared-object changes require regression testing across CAR, 8D CAR, and SCAR, even when the business discussion focuses on NCR and CAR.
