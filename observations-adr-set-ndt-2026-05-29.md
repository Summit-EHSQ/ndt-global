# Observations Application ADR Set

Source transcript: `NDT call 05.29.docx`  
Meeting date: 2026-05-29  
Scope: Observations / Hazard ID future-state design

---

# Suggested ADR List

| ADR | Title | Decision Captured |
|---:|---|---|
| ADR-001 | Separate HSE and Quality into Distinct Solution Streams | Capture the architectural decision to move away from a blended Observations model and maintain distinct HSE and Quality process streams. |
| ADR-002 | Retain Hazard ID as the Primary HSE Observation Concept | Capture the decision that the Observations application scope should center on Hazard ID-type reporting, rather than work observations or quality observations. |
| ADR-003 | Define Hazard, Near Miss, and Incident as Distinct HSE Event Buckets | Capture the conceptual model used to distinguish Hazard IDs from near misses and incidents. |
| ADR-004 | Add Review Workflow and Location-Based HSE Manager Ownership for Hazard IDs | Capture the decision that submitted Hazard IDs should enter a review workflow owned by the relevant location-based HSE manager role. |
| ADR-005 | Align Hazard Follow-Up Actions with Incident Action Plan Patterns | Capture the decision to align Hazard ID follow-up action handling with the broader Incident Management action plan model. |
| ADR-006 | Handle Cross-Domain HSE/Quality Cases as Separate but Related Records | Capture the decision that mixed HSE/Quality cases should remain separate records with a practical association path, rather than being tightly integrated by default. |
| ADR-007 | Do Not Implement Automatic Conversion from Hazard ID to Incident | Capture the decision not to build automated Hazard ID-to-Incident conversion logic because clear definitions and reviewer judgment are preferred for low-frequency edge cases. |

---

# ADR-001: Separate HSE and Quality into Distinct Solution Streams

```yaml
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
```

## Context and Problem Statement

The existing configuration uses the Observations application for more than one conceptual purpose. Hazard ID is used for HSE-related proactive hazard reporting, while the work observation capability has been re-captioned and repurposed as a Quality Observation mechanism.

The future-state NDT Global solution needs to support both HSE and Quality processes, but the discussion identified different ownership models, regulatory drivers, reporting needs, and user expectations for each domain. A blended HSE/Quality observation model creates ambiguity for workers, reviewers, and reporting consumers.

## Decision Drivers

- Workers need a clear and intuitive path for submitting HSE versus Quality matters.
- HSE and Quality have different management teams, process owners, review patterns, and compliance expectations.
- Reporting should avoid unnecessary blending of HSE and Quality data.
- Existing Integra usage was partly shaped by prior licensing and implementation constraints that should not necessarily drive the future-state architecture.
- The future-state model should support global alignment while still accommodating regional regulatory differences.

## Considered Options

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

## Decision Outcome

Adopt a separated HSE and Quality solution model. Users should see distinct HSE and Quality streams in navigation and application structure. HSE matters should be driven toward the HSE incident/hazard process area, while Quality matters should be driven toward the Quality non-conformance process area.

This decision is accepted in principle, with some details dependent on the follow-on NCR/CAPA design session.

## Consequences

- The Observations application should no longer be treated as a blended HSE/Quality container in the future state.
- Quality Observation functionality will likely be removed from the Observations user experience, retired, hidden, migrated, or re-expressed through the Quality process stream.
- Hazard ID remains the main candidate for the HSE observation-style process.
- User training and navigation design should emphasize the domain split.
- Existing data and historical usage must be handled carefully to avoid changing the meaning of past records.

## More Information

This decision was reinforced during the meeting summary, where the target model was described as two streams: HSE/safety and Quality. The exact Quality-side implementation is intentionally out of scope for this Observations ADR set and should be addressed in the NCR/CAPA design ADRs.

---

# ADR-002: Retain Hazard ID as the Primary HSE Observation Concept

```yaml
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
```

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

# ADR-003: Define Hazard, Near Miss, and Incident as Distinct HSE Event Buckets

```yaml
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
```

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

# ADR-004: Add Review Workflow and Location-Based HSE Manager Ownership for Hazard IDs

```yaml
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
```

## Context and Problem Statement

The out-of-the-box observation model was described as primarily a data capture mechanism without a strong review workflow. NDT’s current process expects submitted observations to be reviewed by the relevant HSE manager before they are visible or processed more broadly and before actions are assigned.

The existing Integra configuration includes review-related fields, but the meeting suggested that the process should be more explicitly represented as workflow.

## Decision Drivers

- HSE needs quality control over incoming hazard submissions.
- Submitted records should have clear ownership.
- Reviewers need to validate the submission and assign appropriate actions.
- The process should support location-based responsibility.
- Multiple possible reviewers may exist for a location.

## Considered Options

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

## Decision Outcome

Add a review workflow for Hazard ID records. Submitted records should route to the HSE manager role associated with the relevant location. The reviewer validates the submission and assigns follow-up actions as needed. Where multiple HSE managers are assigned, the process may allow the first available reviewer to take action.

## Consequences

- Hazard ID requires workflow configuration beyond simple record capture.
- A location-based HSE manager role must be maintained.
- Notifications should be sent to the appropriate reviewer role.
- Records will have clearer status and ownership.
- The process better supports governance but adds configuration complexity.

## More Information

The review model was demonstrated using a configured workflow example. The group indicated that this model better matched the desired process than the current simple submission model.

---

# ADR-005: Align Hazard Follow-Up Actions with Incident Action Plan Patterns

```yaml
---
adr: ADR-005
title: Align Hazard Follow-Up Actions with Incident Action Plan Patterns
status: accepted-in-principle
date: 2026-05-29
deciders:
  - Dave McLean
  - Niall Walsh
  - John Blackham
  - Lisa McLaughlin
consulted:
  - Tucker White
  - Brett Corpe
  - Michael Barthelmess
informed:
  - Branka Vidovic
---
```

## Context and Problem Statement

The current Hazard ID action plan model differs from the Incident Management action plan model. NDT requested consistency with the Incident Management approach, especially for how actions are created, assigned, and managed.

The discussion distinguished between submitter-provided immediate action information and reviewer-assigned formal follow-up actions.

## Decision Drivers

- Users benefit from consistent action plan fields and layout across HSE processes.
- HSE managers need control over who owns corrective actions and due dates.
- Most hazards may have a simple action path, but the process must support formal assignment.
- The action model should avoid records sitting in the system without ownership.
- The design should remain consistent with Incident Management where practical.

## Considered Options

1. **Keep the current Hazard ID action plan configuration**
   - Avoids configuration change.
   - Leaves inconsistency with Incident Management.

2. **Allow submitters to create the primary action plan during initial submission**
   - Captures action details quickly.
   - May not match NDT’s review and assignment model.

3. **Use reviewer-owned action assignment with Incident-aligned action plan structure**
   - Supports HSE manager control.
   - Aligns with Incident Management.
   - Requires workflow and form updates.

## Decision Outcome

Align Hazard ID follow-up actions with the Incident Management action plan pattern where practical. Submitters may capture what was observed and any immediate steps taken, but formal follow-up actions should be reviewed and assigned by the responsible HSE manager during the review workflow.

## Consequences

- Hazard ID forms and action grids may require configuration changes.
- The HSE manager review step becomes central to action assignment.
- The user experience should distinguish between immediate action taken and assigned follow-up action.
- Reporting on actions should become more consistent across HSE processes.

## More Information

The group discussed that most hazards may only require one action, but NDT’s process expects HSE review before formal action assignment.

---

# ADR-006: Handle Cross-Domain HSE/Quality Cases as Separate but Related Records

```yaml
---
adr: ADR-006
title: Handle Cross-Domain HSE/Quality Cases as Separate but Related Records
status: accepted-in-principle
date: 2026-05-29
deciders:
  - Dave McLean
  - John Blackham
  - Niall Walsh
  - Michael Barthelmess
  - Brett Corpe
consulted:
  - Øyvind Heimli
  - Tucker White
informed:
  - Branka Vidovic
---
```

## Context and Problem Statement

Some events may involve both HSE and Quality aspects. An HSE near miss or incident may reveal an underlying quality or engineering non-conformance. The system needs a way to preserve the relationship between these processes without over-engineering integration for rare scenarios.

The discussion identified that such cases are important but likely infrequent.

## Decision Drivers

- HSE and Quality processes should remain distinct because they have different ownership and treatment paths.
- Some investigations need to reference or trigger work in the other domain.
- Direct automated linkage may not be justified if the scenario is rare.
- The system should not prevent users from associating related records.
- Configuration effort should be proportional to expected usage.

## Considered Options

1. **No relationship between HSE and Quality records**
   - Simplest configuration.
   - Fails to support important cross-domain investigations.

2. **Manual/action-driven association between records**
   - Allows cross-domain follow-up.
   - Avoids heavy integration.
   - Relies on users and investigators to manage the relationship.

3. **Direct relationship grid between incidents/near misses and NCRs**
   - Provides stronger traceability.
   - Adds configuration complexity.
   - May not be justified unless cross-domain cases are common.

4. **Automated creation of NCRs from HSE records**
   - Reduces manual steps.
   - Adds significant complexity.
   - Not justified based on expected frequency.

## Decision Outcome

Handle cross-domain HSE/Quality cases as separate but related records by default. When an HSE investigation identifies a Quality issue, an action can be assigned to create or manage the related NCR. The originating HSE record may remain open until the related Quality process reaches an appropriate point, depending on investigator judgment.

Direct system-enforced linkage or automated NCR creation should not be implemented unless future analysis shows that cross-domain cases are frequent enough to justify the effort.

## Consequences

- The solution supports rare but significant cross-domain cases without excessive complexity.
- Investigators must understand how to create and track related records.
- Manual traceability may be weaker than a direct object relationship.
- If cross-domain cases become common, a future enhancement may add direct record relationships or completion dependencies.

## More Information

A direct relationship model was discussed as technically feasible, including pre-population and workflow blocking, but was not recommended unless the relationship occurs frequently enough to justify the investment.

---

# ADR-007: Do Not Implement Automatic Conversion from Hazard ID to Incident

```yaml
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
```

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
