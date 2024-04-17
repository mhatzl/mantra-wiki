# `trace`: Trace requirements

Tracing requirements down to code level provides better overview of the project status,
and helps with impact analysis. It is also mandatory to achieve certain certifications.

Only traces at code level are considered, because traces between requirements are already covered by most project management tools.

## `trace.id`: Use the requirement ID for traces

The requirement ID must be used for tracing, because the ID uniquely identifies a requirement.

## `trace.origin`: Origin of requirement traces

To know where a trace is located, the file path and line number must be stored.
This information helps developers with project navigation and is needed for *coverage* analysis.

## `trace.untraceable`: Untraceable requirements

Some requirements cannot be traced, because there is no related artifact a trace could be applied to.
Therefore, it must be possible to specify requirements that need to be traced *manually*.
The required action for *manually* traced requirements may vary between projects.

## `trace.multiple`: Trace more than one requirement at same origin

More than one requirement may affect the same code.
Therefore, it must be possible to specify more than one requirement at the same origin.

## `trace.detect`: How to detect traces

Only traces intended by developers must be detected, because falsely detected traces
result in unreliable trace data.
Therefore, traces found in commented code must be ignored,
and language syntax should be used to further restrict trace detection.

If no language specific syntax can be used to trace requirements,
the following syntax must be used inside comments:

```
[req(<requirement IDs>)]
```

**Note:** `<requirement IDs>` is used as placeholder for the actual IDs to trace with IDs being separated by `,`.

**Examples:**

```
[req(req_id)]
[req(first_id, second_id)]
```

## `trace.special_chars`

In case characters that are part of an ID are not allowed as identifiers in a programming language,
the ID may be wrapped in double quotes `"`. Only the ID part containing the special character(s) must be wrapped.

**Examples:**

```
[req("special-char-id".sub_id)]
```

## `trace.dry_run`: Collect trace data without saving

As a developer, I want to see the impact of a code change to the trace data,
before merging these changes, because this helps to identify if all needed changes were done,
or some were wrongfully introduced.
