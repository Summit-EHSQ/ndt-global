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

## ADR-006: Handle Cross-Domain HSE/Quality Cases as Separate but Related Records

### Context and Problem Statement

Some events may involve both HSE and Quality aspects. An HSE near miss or incident may reveal an underlying quality or engineering non-conformance. The system needs a way to preserve the relationship between these processes without over-engineering integration for rare scenarios.

The discussion identified that such cases are important but likely infrequent.

### Decision Drivers

- HSE and Quality processes should remain distinct because they have different ownership and treatment paths.
- Some investigations need to reference or trigger work in the other domain.
- Direct automated linkage may not be justified if the scenario is rare.
- The system should not prevent users from associating related records.
- Configuration effort should be proportional to expected usage.

### Considered Options

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

### Decision Outcome

Handle cross-domain HSE/Quality cases as separate but related records by default. When an HSE investigation identifies a Quality issue, an action can be assigned to create or manage the related NCR. The originating HSE record may remain open until the related Quality process reaches an appropriate point, depending on investigator judgment.

Direct system-enforced linkage or automated NCR creation should not be implemented unless future analysis shows that cross-domain cases are frequent enough to justify the effort.

### Consequences

- The solution supports rare but significant cross-domain cases without excessive complexity.
- Investigators must understand how to create and track related records.
- Manual traceability may be weaker than a direct object relationship.
- If cross-domain cases become common, a future enhancement may add direct record relationships or completion dependencies.

### More Information

A direct relationship model was discussed as technically feasible, including pre-population and workflow blocking, but was not recommended unless the relationship occurs frequently enough to justify the investment.

---
