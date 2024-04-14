This section contains requirements for the system.

## Requirements Overview

**High-Level Requirements:**

- [req:analyze](5-REQ-analyze) ... Contains requirements about analyzing trace and coverage data
- [req:coverage](5-REQ-coverage) ... Contains requirements about collecting requirement coverage data
- [req:deprecate](5-REQ-deprecate) ... Contains requirements about handling deprecated requirements
- [req:extract](5-REQ-extract) ... Contains requirements about extracting requirement IDs
- [req:filter](5-REQ-filter) ... Contains the requirement to ignore files and folders for referencing
- [req:qa](5-REQ-qa) ... Contains requirements about general quality assurance
- [req:report](5-REQ-report) ... Contains requirements for reports from collected data
- [req:req_id](5-REQ-req_id) ... Contains requirements about the requirement ID
- [req:trace](5-REQ-trace) ... Contains requirements about tracing requirements in code

**Important Requirements:**

- [req:analyze](5-REQ-analyze) ... Contains requirements about analyzing trace and coverage data
- [req:coverage](5-REQ-coverage) ... Contains requirements about collecting requirement coverage data
- [req:req_id](5-REQ-req_id) ... Contains requirements about the requirement ID
- [req:trace](5-REQ-trace) ... Contains requirements about tracing requirements in code

## General requirement structure

Every requirement must start the heading with the ID assigned to the requirement to be able to reference it.
The ID must be wrapped in backticks `` ` ``, to prevent wrongful ID detection.

**Example:**

```
# `req_id`: Some title

Some description...
```

## High-level requirements

In addition to the general structure, requirements may contain sub-requirements to create a hierarchy of requirements.
Sub-requirements are created by *dot-like* notation, starting with the ID of the parent requirement.

**Note:** The heading level should also be increased.

**Example:**

```
# `req_id`: Some title

The description of the high-level requirement.

## `req_id.sub_req`: Sub-requirement title

The description of the sub-requirement.
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

4. **active** ... When the implementation of a requirement is merged, the requirement gets **active**

   [mantra](https://github.com/mhatzl/mantra) may be used during testing to check what requirements are covered through tests.

5. **deprecated** ... If a requirement is replaced or removed by another requirement, the requirement gets **deprecated**.

   Note that requirements might still be **active** in some projects, but **deprecated** in others.
   The requirement should be deleted if the requirement is **deprecated** in all projects, to keep the wiki small.

   **Note:** A link should be added in the **deprecated** requirement, pointing to the new requirement for better traceability.

## Definition of Ready

A requirement may be considered **ready** if it fulfills the following statements:

- **General:**

  - It is clear where the requirement must be placed in the wiki
  - The ID for the requirement is decided and unique in the wiki
  - All currently raised concerns by stakeholders are resolved
  - Active quality assurance requirements were considered (see [req:qa](5-REQ-qa))

- **For high-level requirements:**

  - The intent of the requirement is covered by the existing sub-requirements 
  - All sub-requirements fulfill their Definition of Ready

  **Note:** If the requirement does not fulfill these statements, try refining existing sub-requirements, or create additional ones.

- **For low-level requirements:**

  - At least one developer understands how to implement it
  - Implementation is estimated to take less than two weeks for one developer

  **Note:** If the requirement does not fulfill these statements, consider creating sub-requirements for it. 
