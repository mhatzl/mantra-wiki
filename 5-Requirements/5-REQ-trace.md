# `trace`: Trace requirements

Tracing requirements down to code level provides better overview of the project status,
and helps with impact analysis. It is also mandatory to achieve certain certifications.

Focus is on traces between requirements and code,
but a requirement hierarchy may be passed to *mantra*
to detect transitive relations between requirements and artifacts.

## `trace.id`: Use the requirement ID for traces

The requirement ID must be used for tracing, because the ID uniquely identifies a requirement.

## `trace.origin`: Origin of requirement traces

To know where a trace is located, the file path and line number must be stored.
This information helps developers with project navigation and is needed for *coverage* analysis.

## `trace.multiple`: Trace more than one requirement at same origin

More than one requirement may affect the same code.
Therefore, it must be possible to specify more than one requirement at the same origin.

## `trace.collect`: Collect requirements traces

It must be possible to collect requirements traces.

### `trace.collect.general`: Collect traces from text-based files

If no language specific feature is defined to trace requirements for a text-based file,
the following pattern must be detected:

```
[req(<requirement IDs>)]
```

**Note:** `<requirement IDs>` is used as placeholder for the actual IDs to trace with IDs being separated by `,`.

**Examples:**

```
[req(req_id)]
[req(first_id, second_id)]
```

### `trace.collect.ast`: Collect traces from an abstract syntax tree

An AST should be used to restrict trace detection for programming languages.

**Rationale:**

Only requirements traces intended by developers should be detected, because falsely detected traces
result in unreliable trace data.
Therefore, traces found in commented code should be ignored,
and language features should be used to further restrict trace detection.

#### `trace.collect.ast.rust`: Collect traces from Rust code

The following patterns must be recognized as requirements trace in Rust code:

```rust
#[req(some_id)]
fn foo() {}
```

```rust
#[requirements(some_id)]
fn foo() {}
```

```rust
#[mod_path::req(some_id)]
fn foo() {}
```

```rust
fn foo() {
    reqcov!(some_id)
}
```

```rust
fn foo() {
    mod_path::reqcov!(some_id)
}
```

### `trace.collect.extern`: Add external traces

It must be possible to add external traces to *mantra*, because annotations in code
might not be possible.
e.g. In case code was already certified before, adding annotations would change the code, which would require re-certification. 

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

## `trace.ident`: Optional associated identifier of a trace

A trace set in a programming language may be linked to an item.
An identifier that uniquely identifies this item may be stored together
with the trace to improve the readability of the traceability report,
and to improve static coverage analysis.

**Example:**

```rust
#[req(spanning_trace)]
fn some_fn() {
    // ...
}
```

## `trace.span`: Optional associated span of a trace

A trace set on a code block in a programming language affects all lines of the code block.
This code block line span must be stored in *mantra* to connect code coverage data with traces.

**Example:**

The trace spans all three lines of the `some_fn` function.

```rust
#[req(spanning_trace)]
fn some_fn() {
    // ...
}
```
