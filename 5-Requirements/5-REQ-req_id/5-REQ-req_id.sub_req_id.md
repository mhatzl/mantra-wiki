## `req_id.sub_req_id`: Sub-requirements for high-level requirements

**References:**

- in branch main: 5

Requirement IDs must be structured in a way that allows to create requirement hierarchies,
because most systems/projects have high-level requirements that are then broken up into smaller low-level requirements.

Created in response to [issue #1](https://github.com/mhatzl/mantra/issues/1).

## Implementation details

Sub-requirement IDs are separated by `.` from parent IDs.
This creates the impression of a *dot-notation* used in many programming languages,
which should improve familiarity for developers.

**Example:** `parent_req.sub_req`
