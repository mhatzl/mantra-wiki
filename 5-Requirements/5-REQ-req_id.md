# `req_id`: Requirement ID

Every requirement must have a unique ID assigned to it,
because some way of identification is needed to reference requirements.
The ID should already tell developers what the requirement is roughly about to help identify the correct requirement to trace.

Created in response to [issue #1](https://github.com/mhatzl/mantra/issues/1).

## `req_id.sub_req_id`: Sub-requirements for high-level requirements

Requirement IDs must be structured in a way that allows to create requirement hierarchies,
because most systems/projects have high-level requirements that are then broken up into smaller low-level requirements.

Created in response to [issue #1](https://github.com/mhatzl/mantra/issues/1).

**Implementation details:**

Sub-requirement IDs are separated by `.` from parent IDs.
This creates the impression of a *dot-notation* used in many programming languages,
which should improve familiarity for developers.

**Example:** `parent_req.sub_req`

## `req_id.restrictions`: Restrict allowed characters to use for IDs

An ID must not contain the characters `.`, `"`, `,`, `` ` ``, `[`, `]`, `(`, `)`, `{`, `}`.

- `.` is used to create requirement hierarchies
- `"` is used to wrap IDs in traces in case some characters are not allowed in programming languages (see [req(trace.special_chars)])
- `,` is used to set multiple IDs in one trace (see [req(trace.detect)])
- `` ` `` is used to wrap IDs in Wikis based on Markdown syntax (see [req(extract.wiki)])
- Grouping characters `[`, `]`, `(`, `)`, `{`, `}` would interfere with trace syntax (see [req(trace.detect)])
