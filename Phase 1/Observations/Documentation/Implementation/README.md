# Intelex Technical Development Task List

## 1. Document Control Information

| Field | Value |
|---|---|
| Client / Project | NDT / Integra Observations Harmonization |
| Source Gap Analysis | `observations_gap_analysis_report_system_change_only.md` |
| Source Configuration Package | `Observations App Config(v1.0.0.0).ipack` |
| Prepared For | Intelex Configuration / Development Team |
| Prepared By |  |
| Date | 2026-06-15 |

## 2. Purpose

This document converts the Observations Gap Analysis, current-state Observations `.ipack` review, and subsequent implementation decisions into an executable Intelex technical development task package. The solution focuses on refining the Observations application so Hazard ID becomes the active HSE observation pathway, Quality Observation is removed from active Observations intake, Hazard ID receives a new stage-based workflow, and workflow reminder/escalation notifications are configured.

## 3. Assumptions and Scope Notes

- The uploaded `.ipack` package represents the baseline current-state Observations configuration.
- The current-state package includes both `Quality Observation` and `Hazard ID`, but the future-state direction is to remove Quality Observation from active Observations intake and retain Hazard ID as the active HSE observation concept.
- Historical Quality Observation records must be preserved unless a separate approved data strategy authorizes migration, deletion, or archival.
- Lookup values should not be deleted or carelessly recaptioned where historical records may exist. Values should be hidden, deactivated, or made unavailable for future use unless master-data governance approves another approach.
- The final Quality destination, such as NCR or another Quality application pathway, is outside the scope of this Observations task list.
- Hazard ID workflow will be newly configured using stage-based tasks: `Draft`, `Review`, and `Closed`.
- The `Draft` stage is owned by the creating user and due three calendar days after initial record creation.
- The `Review` stage is owned by the `HSE Manager` role and due three calendar days after entering Review.
- Approval from Review closes the record.
- Rejection from Review returns the record to Draft and requires review comments.
- Review comments must be prominently displayed in Draft when a record has been returned from Review.
- Responsible users must be able to create Event Action Plan records at all workflow stages.
- The source for a responsible user’s immediate supervisor must be confirmed before escalation notifications are configured.
- Removed tasks are intentionally omitted from this package: `TASK-OBS-007`, `TASK-OBS-008`, `TASK-OBS-009`, `TASK-OBS-013`, `TASK-OBS-014`, and `TASK-OBS-015`.

## 4. Technical Development Task Index

| Task Number | Task Name | Application | Theme | Task File |
|---|---|---|---|---|
| TASK-OBS-001 | Retire Active Quality Observation Intake from Observations | Observations | Cleanup, Decommissioning, and Legacy Quality Observation Handling | [Open task](tasks/TASK-OBS-001_Retire_Active_Quality_Observation_Intake_from_Observations.md) |
| TASK-OBS-002 | Convert Quality Observation Views to Historical / Read-Only Access Where Required | Observations | Cleanup, Decommissioning, and Legacy Quality Observation Handling | [Open task](tasks/TASK-OBS-002_Convert_Quality_Observation_Views_to_Historical_Read_Only_Access_Where_Required.md) |
| TASK-OBS-003 | Deactivate `Quality` from Active Safe/Unsafe/Quality Classification Use | Observations | Data Model and Lookup Configuration | [Open task](tasks/TASK-OBS-003_Deactivate_Quality_from_Active_Safe_Unsafe_Quality_Classification_Use.md) |
| TASK-OBS-004 | Export and Document Current Hazard ID Lookup Values for Harmonization | Observations | Data Model and Lookup Configuration | [Open task](tasks/TASK-OBS-004_Export_and_Document_Current_Hazard_ID_Lookup_Values_for_Harmonization.md) |
| TASK-OBS-005 | Implement Approved Hazard ID Lookup Harmonization | Observations | Data Model and Lookup Configuration | [Open task](tasks/TASK-OBS-005_Implement_Approved_Hazard_ID_Lookup_Harmonization.md) |
| TASK-OBS-006 | Add Hazard / Near Miss / Incident Definition Guidance to Hazard ID Intake | Observations | Form Layout and User Experience | [Open task](tasks/TASK-OBS-006_Add_Hazard_Near_Miss_Incident_Definition_Guidance_to_Hazard_ID_Intake.md) |
| TASK-OBS-010 | Configure Hazard ID Navigation Under Approved HSE / Incident Management Context | Observations | Navigation and Cross-Application UX | [Open task](tasks/TASK-OBS-010_Configure_Hazard_ID_Navigation_Under_Approved_HSE_Incident_Management_Context.md) |
| TASK-INC-001 | Add Hazard ID Entry Point to Incident Management HSE Navigation | Incident Management | Cross-Application User Experience | [Open task](tasks/TASK-INC-001_Add_Hazard_ID_Entry_Point_to_Incident_Management_HSE_Navigation.md) |
| TASK-OBS-011 | Redesign Observations Security Groups for HSE Ownership Model | Observations | Security, Roles, and Permissions | [Open task](tasks/TASK-OBS-011_Redesign_Observations_Security_Groups_for_HSE_Ownership_Model.md) |
| TASK-OBS-012 | Secure Historical Quality Observation Access Separately from HSE Hazard ID Access | Observations | Security, Roles, and Permissions | [Open task](tasks/TASK-OBS-012_Secure_Historical_Quality_Observation_Access_Separately_from_HSE_Hazard_ID_Access.md) |
| TASK-OBS-016 | Update Mobile Observations Experience for HSE-Only Intake | Observations | Mobile or Offline Behavior | [Open task](tasks/TASK-OBS-016_Update_Mobile_Observations_Experience_for_HSE_Only_Intake.md) |
| TASK-OBS-017 | Configure Hazard ID Draft Workflow Stage | Observations | Workflow and Status Logic | [Open task](tasks/TASK-OBS-017_Configure_Hazard_ID_Draft_Workflow_Stage.md) |
| TASK-OBS-018 | Configure Hazard ID Review Workflow Stage | Observations | Workflow and Status Logic | [Open task](tasks/TASK-OBS-018_Configure_Hazard_ID_Review_Workflow_Stage.md) |
| TASK-OBS-019 | Configure Hazard ID Closed Workflow Stage | Observations | Workflow and Status Logic | [Open task](tasks/TASK-OBS-019_Configure_Hazard_ID_Closed_Workflow_Stage.md) |
| TASK-OBS-020 | Configure Hazard ID Workflow Due Date Reminder and Escalation Notifications | Observations | Notifications and Email Templates | [Open task](tasks/TASK-OBS-020_Configure_Hazard_ID_Workflow_Due_Date_Reminder_and_Escalation_Notifications.md) |

## 5. Cross-Application Dependencies

| Dependency | Impact |
|---|---|
| Incident Management | Hazard ID may be surfaced under Incident Management or a consolidated HSE navigation context while remaining technically in Observations. This affects menu structure, permissions, and user guidance. |
| NCR / Quality Application | Quality Observation is expected to move out of Observations, but the target Quality intake design is outside this Observations task list and must be confirmed separately. |
| Action Plans / Event Action Plans | Responsible users must be able to create related Event Action Plan records in Draft, Review, and Closed. Permissions and related-record configuration must be validated across the workflow. |
| Employee / Supervisor Hierarchy | Overdue escalation notifications depend on a confirmed source for the responsible user’s immediate supervisor. |
| Mobile Profiles | Mobile Hazard ID and Work Observation views must be updated alongside desktop navigation, workflow, picklist, and security changes. |
| Security Groups | `HSE Manager` must exist or be created before Review-stage assignment, workflow actions, and notification recipients can be fully configured. |

## 6. Open Questions for Build Planning

| ID | Open Question | Build Impact |
|---|---|---|
| OQ-001 | What are the final approved user-facing definitions for Hazard ID, Near Miss, and Incident? | Required before finalizing Hazard ID intake guidance. |
| OQ-002 | Should Hazard ID remain visible under Observations, move visually under Incident Management, or appear in both places? | Required before finalizing navigation and cross-application access. |
| OQ-003 | Should the Quality Observation object be hidden, retired, preserved read-only, or repurposed? | Required before finalizing legacy Quality Observation view and security behavior. |
| OQ-004 | Which Hazard ID fields constitute the “main detail section” that must be completed in Draft? | Required before configuring Draft requiredness and submit validation. |
| OQ-005 | Should the existing `Reviewer Comments` field be reused for rejection comments, or should a new `Review Comments` field be created? | Required before configuring rejection requiredness and returned-Draft display. |
| OQ-006 | Should the HSE Manager be assigned as a named user, role queue, group, or dynamically derived responsible party? | Required before configuring Review-stage responsibility and notifications. |
| OQ-007 | What is the approved source for the responsible user’s immediate supervisor? | Required before configuring escalation notifications. |
| OQ-008 | If Review is assigned to the `HSE Manager` role rather than a named user, whose supervisor should receive escalation emails? | Required before supervisor escalation logic can be completed. |
| OQ-009 | Can Event Action Plans be created after the Hazard ID is Closed? | Required before finalizing Closed-stage related-record permissions. |
| OQ-010 | Should Closed Hazard ID records ever be reopened? | Required before confirming whether reopen workflow actions are excluded. |
| OQ-011 | Which Hazard ID picklist values should be added, hidden, retained, or recaptioned? | Required before implementing lookup harmonization. |
| OQ-012 | Should reminder and escalation recurrence use calendar days or business days? | User requirement states calendar days; confirm no exception is required for weekends/holidays. |

## 7. Suggested Build Sequencing

1. Confirm unresolved architecture and configuration decisions: Quality Observation retirement model, Hazard ID navigation location, HSE Manager role model, supervisor hierarchy source, review comment field decision, and Event Action Plan behavior in Closed.
2. Complete `TASK-OBS-004` lookup export and harmonization decision matrix.
3. Retire active Quality Observation intake through `TASK-OBS-001` and `TASK-OBS-002`.
4. Update Safe/Unsafe/Quality active value handling through `TASK-OBS-003`.
5. Implement approved Hazard ID taxonomy through `TASK-OBS-005`.
6. Add Hazard / Near Miss / Incident guidance through `TASK-OBS-006`.
7. Configure Hazard ID navigation through `TASK-OBS-010` and, if approved, `TASK-INC-001`.
8. Configure security and role model through `TASK-OBS-011` and `TASK-OBS-012`.
9. Update mobile experience through `TASK-OBS-016`.
10. Build Hazard ID workflow stages: `TASK-OBS-017` Draft, `TASK-OBS-018` Review, and `TASK-OBS-019` Closed.
11. Configure workflow reminder and escalation notifications through `TASK-OBS-020`.
12. Perform end-to-end regression testing across Hazard ID creation, due dates, approval/closure, rejection comments, Event Action Plan creation, security, mobile, email notifications, and historical Quality Observation access.

## 8. Configuration Items That Appear Already Satisfied

| Item | Current-State Note |
|---|---|
| Hazard ID object | Hazard ID already exists in the Observations configuration. |
| Hazard ID fields | Baseline includes fields such as reporter, reviewer, severity, type, steps taken, action/follow-up, Action Plan, reviewer comments, and close date. |
| Quality Observation object | Exists and can be preserved for historical access instead of being rebuilt. |
| Lookup/admin objects | Existing lookup structures provide a starting point for Hazard Type, Observation Area, Severity, Steps Taken, Safe/Unsafe/Quality, and related configuration. |
| Observations security groups | Existing `Observations Admin`, `Observations Supervisor`, and `Observations Reporter` groups provide a starting point for the future HSE security model. |
| Mobile view profiles | Mobile configuration exists and can be modified rather than built from scratch. |
| Date validation | Existing validation prevents future-dated Observations/Hazard ID dates and should be preserved unless future design changes require otherwise. |

## 9. Out-of-Scope or Deferred Items

- Building the future Quality/NCR intake path is out of scope for this Observations-only task list.
- Migrating historical Quality Observation records is out of scope unless a separate approved data strategy is provided.
- Creating new Incident, Near Miss, NCR, Finding, or Inspection workflows is out of scope unless future requirements explicitly require those changes.
- External integrations, HRIS synchronization, ERP integration, and data-warehouse feeds are out of scope based on the current package review.
- Recaptioning historical lookup values is deferred until master-data governance approves the exact historical reporting impact.
- Reopen logic for Closed Hazard ID records is not included unless explicitly approved.
- Escalation logic for role-based Review assignment remains dependent on a confirmed supervisor-resolution rule.