<!--
Delta spec template for a change.

This template demonstrates four types of delta sections. Use them as needed:
- ADDED / MODIFIED / REMOVED / RENAMED
File name and location: openspec/changes/<change-name>/specs/<capability>/spec.md
(`<capability>` matches the directory name in openspec/specs/<capability>/)

Strict format rules (validated by OpenSpec):
- A Requirement sentence MUST contain `SHALL` or `MUST`
- Every Requirement MUST have at least one `#### Scenario:`
- A Scenario MUST use level 4 (`####`); level 3 or a bullet fails silently
-->

## ADDED Requirements

<!-- New behavior. List each new Requirement this change adds to the capability. -->

### Requirement: <!-- requirement name -->
<!-- requirement text — must contain SHALL or MUST -->

#### Scenario: <!-- scenario name -->
- **WHEN** <!-- condition -->
- **THEN** <!-- expected outcome -->

---

## MODIFIED Requirements

<!--
Modify an existing Requirement. **MUST use a normalized header identical to the one in
openspec/specs/<capability>/spec.md** (case-sensitive comparison after trimming), or the
delta apply will fail during archive because it cannot find the matching requirement.

**MUST include the complete modified content** (not just a diff), because OpenSpec archive
applies MODIFIED by replacing the full text.
-->

### Requirement: <!-- header identical to the existing spec -->
<!-- complete modified requirement text — contains SHALL or MUST -->

#### Scenario: <!-- scenario name (may be added or modified) -->
- **WHEN** <!-- condition -->
- **THEN** <!-- expected outcome -->

---

## REMOVED Requirements

<!--
Remove an existing Requirement. MUST include Reason and Migration explanations so reviewers
understand why it is being removed and how existing consumers should migrate.
-->

### Requirement: <!-- header to remove, identical to the existing spec -->

**Reason**: <!-- why it is being removed -->

**Migration**: <!-- how existing callers/dependents should adapt -->

---

## RENAMED Requirements

<!--
Rename a Requirement header. The format is fixed: FROM / TO use code-fenced headers.
If both the name and content change, list the name change in RENAMED **and**
include the complete content under MODIFIED using the **new** header.

Apply order during archive: RENAMED → REMOVED → MODIFIED → ADDED
-->

- FROM: `### Requirement: <Old Name>`
- TO: `### Requirement: <New Name>`
