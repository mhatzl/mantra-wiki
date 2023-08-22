This section contains requirements for the system.

## Requirements Overview

**High-Level Active Requirements:**

{{
  
List and link to the high-level requirements of the system.

}}

[[

- [req:qa](5-REQ-qa) ... Contains requirements about general quality assurance

]]

**Important Active Requirements:**

{{
  
You may also list and link to the most impactful 10 to 20 requirements of the system.

}}

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

   The number of times the requirement is referenced in the *project* repository should be added to the wiki.
   Tools may be used to achieve this.

   **Example:**

   ```
   # my_req: Some implemented requirement
   
   **References**

   - in branch main: 2
   ```

   For high-level requirements, the number of references is the sum of all sub-requirement references plus the number the requirement is directly referenced.
   To see the number of direct references, `(<Number of references> direct)` is added after the overall number.

   **Example:**

   ```
   # high_level: Some implemented high-level requirement
   
   **References**

   - in branch main: 4 (1 direct)
   ```

   If it is not possible to reference a requirement, `manual` may be set manually instead of the number of references.
   This marks the requirement as **active**, but requiring manual verification.

   **Example:**

   ```
   # my_req: Requirement that needs manual verification
   
   **References**

   - in branch main: manual
   ```

   A manually verified requirement may get references in the future.
   The number of references is then added after the `manual` keyword.

   **Example:**

   ```
   # my_req: Requirement that needs manual verification, but is also referenced in code
   
   **References**

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

   **References**

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
