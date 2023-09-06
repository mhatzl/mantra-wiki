This section contains requirements for the system.

## Requirements Overview

**High-Level Requirements:**

- [req:qa](5-REQ-qa) ... Contains requirements about general quality assurance
- [req:ref_req](5-REQ-ref_req) ... Contains the requirement to reference requirements 
- [req:req_id](5-REQ-req_id) ... Contains requirements about the requirement ID
- [req:sync](5-REQ-sync) ... Contains requirements about *mantra sync*
- [req:wiki](5-REQ-wiki) ... Contains requirements about the content of the wiki

**Important Requirements:**

- [req:ref_req](5-REQ-ref_req) ... Contains the requirement to reference requirements
- [req:req_id](5-REQ-req_id) ... Contains requirements about the requirement ID
- [req:wiki.ref_list](5-REQ-wiki.ref_list) ... Contains requirements about the structure of the *references* list

## Requirement ID

IDs help to easily reference requirements.
Requirement IDs may be grouped to create a hierarchy of requirements.
IDs of sub-requirements are separated by a dot "." from the parent ID.

**Note:** IDs must not include any whitespace or `-` to keep IDs readable in wiki titles.

**Examples:**

```
my_req
my_req.sub_req
other_req.sub_req.even_lower_req
```

## Requirement structure
### General structure

Requirements should have a consistent structure to improve the readability.

If [mantra](https://github.com/mhatzl/mantra) is used for tracing,
every requirement must start with the heading with the ID assigned to the requirement.
[mantra](https://github.com/mhatzl/mantra) uses a *references* list to trace requirements between the wiki, implementation, and tests.
This list is placed by [mantra](https://github.com/mhatzl/mantra) directly below the requirement heading.

**Note:** *References* lists may be manually modified, but must remain directly below the requirement heading.

**Example:**

```
# req_id: Some title

**References:**

- in branch main: 2

The description of the requirement.
```

## High-level requirements

In addition to the general structure, high-level requirements should contain a section that links to sub-requirements
that are one level *deeper*. This helps with navigation through the wiki.

**Note:** This section should link to sub-requirements independent of their phase, because adapting this section would otherwise be too cumbersome.

**Note:** Linking to sub-requirements that are more than one level *deeper* is also too cumbersome to maintain.

**Note:** To keep pages short, sub-requirements should in general be placed in their own files.

The syntax to reference requirements as defined in [req:qa.tracing](5-REQ-qa.tracing) may be used to link to sub-requirements.
This allows to use [mantra](https://github.com/mhatzl/mantra) to update the links to those sub-requirements.

**Example:**

```
# req_id: Some title

**References:**

- in branch main: 2

The description of the high-level requirement.

## Sub-requirements

- [req:req_id.sub_req_1](5-REQ-req_id.sub_req_1) ... Optional description for this requirement
- [req:req_id.sub_req_2](5-REQ-req_id.sub_req_2) ... Optional description for this requirement
```

## Adding tests to requirements

Tests may be added to the wiki in the form of sub-requirements.
However, creating a sub-requirement for each test case may be too tedious.
In this case it is probably better to create an overall test requirement with `<your_req>.test` as ID.
This requirement may then contain descriptions for multiple test cases, while only requiring to remember one ID.
A "Definition of Done" specific to the requirement may then be defined that enforces that all test cases described in the `.test` ID must be fulfilled.

**Note:** A requirement is **not** considered as high-level requirement if it only contains tests as sub-requirements.

```
# req_id: Some title

**References:**

- in branch main: 12 (2 direct)

The description of the requirement.

## req_id.test: Multiple test cases

**References:**

- in branch main: 10

All test cases in this section must be fulfilled.

### Test case 1

Test something...

### Test case 2

Test something else...
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

   The number of times the requirement is referenced in [mantra](https://github.com/mhatzl/mantra) should be added to the wiki.
   [mantra](https://github.com/mhatzl/mantra) may be used to achieve this.

   **Example:**

   ```
   # my_req: Some implemented requirement
   
   **References:**

   - in branch main: 2
   ```

   For high-level requirements, the number of references is the sum of all sub-requirement references plus the number the requirement is directly referenced.
   To see the number of direct references, `(<Number of references> direct)` is added after the overall number.

   **Example:**

   ```
   # high_level: Some implemented high-level requirement
   
   **References:**

   - in branch main: 4 (1 direct)
   ```

   If it is not possible to reference a requirement, `manual` may be set manually instead of the number of references.
   This marks the requirement as **active**, but requiring manual verification.

   **Example:**

   ```
   # my_req: Requirement that needs manual verification
   
   **References:**

   - in branch main: manual
   ```

   A manually verified requirement may get references in the future.
   The number of references is then added after the `manual` keyword.

   **Example:**

   ```
   # my_req: Requirement that needs manual verification, but is also referenced in code
   
   **References:**

   - in branch main: manual + 3
   ```

5. **deprecated** ... If a requirement is replaced or removed by another requirement, the requirement gets **deprecated**.

   Since the requirement might still be **active** in some branches, `deprecated` must be set manually to the branches
   the requirement is deprecated.

   The requirement must be deleted if the requirement is **deprecated** in all branches, to keep the wiki small.

   **Note:** A link should be added in the **deprecated** requirement, pointing to the new requirement for better traceability.

   **Example:**

   ```
   # my_req: Got deprecated in latest version

   **References:**

   - in branch main: deprecated
   - in branch stable: 2
   ```

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
