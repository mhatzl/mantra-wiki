This section contains requirements for the system.

## Requirements Overview

**High-Level Requirements:**

- [req(analyze)](5-REQ-analyze) ... Contains requirements about analyzing trace and coverage data
- [req(cli)](5-REQ-cli) ... Contains requirements about *mantra*'s CLI
- [req(testcov)](5-REQ-testcov) ... Contains requirements about collecting test and code coverage data
- [req(exchange)](5-REQ-exchange) ... Contains requirements about exchanging information with external tools
- [req(qa)](5-REQ-qa) ... Contains requirements about general quality assurance
- [req(report)](5-REQ-report) ... Contains requirements for reports from collected data
- [req(requirement)](5-REQ-requirement) ... Contains requirements about storing requirement information
- [req(safety)](5-REQ-safety) ... Contains requirements about safety-critical aspects for *mantra*
- [req(trace)](5-REQ-trace) ... Contains requirements about tracing requirements in code

**Important Requirements:**

- [req(analyze)](5-REQ-analyze) ... Contains requirements about analyzing trace and coverage data
- [req(coverage)](5-REQ-coverage) ... Contains requirements about collecting requirement coverage data
- [req(req.id)](5-REQ-requirement) ... Contains requirements about the requirement ID
- [req(trace)](5-REQ-trace) ... Contains requirements about tracing requirements in code

## General requirement structure

Every requirement must start the heading with the ID assigned to the requirement to be able to reference it.
The ID must be wrapped in backticks `` ` ``, to prevent wrongful ID detection.
See [req.collect.wiki](/5-REQ-requirement) for the full specification.

**Example:**

```
# `req_id`: Some title

Some description...
```

## High-level requirements

In addition to the general structure, requirements may contain sub-requirements to create a hierarchy of requirements.
Sub-requirements may be created by *dot-like* notation, starting with the ID of the parent requirement.

**Note:** The heading level should also be increased.

**Example:**

```
# `req_id`: Some title

The description of the high-level requirement.

## `req_id.sub_req`: Sub-requirement title

The description of the sub-requirement.
```

In addition, IDs of parent requirements may be stated in the property section of the requirement.
This allows to add multiple parent requirements.

**Example:**

```
# `req_id`: Some title

- **Parents:** [`parent_1`, [`parent_2`](#link-to-parent-2)]

The description of the requirement that has two parent requirements.
```

## Requirement Phases

A requirement goes through the following phases:

1. **proposed** ... Requirements are **proposed**, by creating feature-request issues

   The issue should be used as a central place to clarify the intent of the feature-request.
   At this stage, the requirement should **not** yet be documented in the wiki, because it is highly likely
   that the content of the requirement will change.

2. **ready** ... Once a requirement has enough information available to be implemented, it may be considered **ready**

   The [Definition of Ready](#definition-of-ready) defines minimum criteria a requirement must fulfill before it may be considered **ready**.
   Before the requirement is implemented, it must be documented in the wiki with a unique ID to be used for tracing.

   To keep the wiki small, requirements should not be documented too far ahead of the planned implementation.
   This also makes it easier to react to changes to the requirement.
   As result, the wiki then only contains implemented or *soon-to-be implemented* requirements.

3. **Optional: declined** ... A requirement in **proposed** or **ready** state may be **declined**, meaning that it will not be implemented

   A **declined** requirement must be removed from the wiki if it already exists.
   This keeps the wiki small, and focused to implemented or *soon-to-be implemented* requirements.

4. **traced** ... When a requirement has at least one trace to an artifact like a code or configuration file, the requirement gets **traced**

   [mantra](https://github.com/mhatzl/mantra) may be used to automate tracing of requirements.

5. **covered** ... If at least one test case exists that covers one or more traces of a requirement, the requirement gets **covered**

   Statement coverage may be collected during test execution to automate the detection of covered requirements.
   By default, covering one line that is linked to a trace of a requirement is enough to consider the requirement **covered**, but more strict criteria may be defined on a project by project basis.

6. **Optional: deprecated** ... If a requirement is replaced or removed by another requirement, the requirement gets **deprecated**

   Note that requirements might still be **active** in some projects, but **deprecated** in others.
   The requirement should be deleted if the requirement is **deprecated** in all projects, to keep the wiki small.

   **Note:** A link should be added in the **deprecated** requirement, pointing to the new requirement for better traceability.

## Definition of Ready

A requirement may be considered **ready** if it fulfills the following statements:

- **General:**

  - It is clear where the requirement must be placed in the wiki
  - The ID for the requirement is decided and unique in the wiki
  - All currently raised concerns by stakeholders are resolved
  - Active quality assurance requirements were considered (see [req(qa)](5-REQ-qa))

- **For high-level requirements:**

  In general, it is difficult to state if a high-level requirement is **ready**,
  because it is mostly implicitly defined by its sub-requirements.

  As a guideline, consider the following statements to determine if a high-level requirement is **ready**:

  - The intent of the requirement is covered by existing sub-requirements
  - All sub-requirements fulfill their Definition of Ready

- **For low-level requirements:**

  - At least one developer understands how to implement it
  - The scope of the requirement is small enough that only few traces to artifacts are needed

  **Note:** If the requirement does not fulfill these statements, consider creating sub-requirements for it.
