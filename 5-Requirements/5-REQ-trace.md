# `trace`: Trace requirements

Tracing requirements down to code level provides better overview of the project status,
and helps with impact analysis. It is also mandatory to achieve certain certifications.

Focus is on traces between requirements and code,
but a requirement hierarchy may be passed to *mantra*
to detect transitive relations between requirements and artifacts.

## `trace.id`: Use the requirement ID for traces

The requirement ID must be used for tracing, because the ID uniquely identifies a requirement.

## `trace.origin`: Origin of requirement traces

To know where a trace is located in a text file, the filepath and line number must be stored.
This information helps developers with project navigation, and is needed for *coverage* analysis
and certification.

**Note:** With *mantra*'s focus on traces between requirements and code, it is assumed that all traces will point to text files, and therefore using filepath and line number as origin is feasible.

## `trace.multiple`: Trace more than one requirement at same origin

More than one requirement may affect the same code.
Therefore, it must be possible to specify more than one requirement at the same origin.

## `trace.collect`: Collect requirements traces

It must be possible to collect requirements traces at least manually and semi-automatically,
because automated collection is not always possible.
Nevertheless, to improve the usability of *mantra*, trace collection should be automated as much as possible.

### `trace.collect.general`: Collect traces from text-based files

If no language specific feature is defined to trace requirements for a text-based file,
the following pattern must be detected:

```
[req(<requirement IDs>)]
```

**Note:** `<requirement IDs>` is used as placeholder for the actual IDs to trace with IDs being separated by `,` and optional whitespace characters.

**Examples:**

```
[req(req_id)]
[req(first_id, second_id)]
```

### `trace.collect.ast`: Collect traces from an abstract syntax tree

**Parents:** [`trace.collect`, `trace.element`]

An AST should be used to restrict trace detection for programming languages.

**Rationale:**

Only requirements traces intended by developers should be detected, because falsely detected traces
result in unreliable trace data.
Therefore, traces found in commented code should be ignored,
and language features should be used to further restrict trace detection.

#### `trace.collect.ast.rust`: Collect traces from Rust code

**Note:** `<requirement IDs>` is used below as placeholder for the actual IDs to trace with IDs being separated by `,` and optional whitespace characters.

The following patterns must be recognized as requirements traces in Rust code:

**Attribute Macro:**

These traces have an associates line span of the element the attribute is set on.

```rust
#[req(<requirement IDs>)]
fn foo() {}
```

```rust
#[mod_path::req(<requirement IDs>)]
fn foo() {}
```

```rust
#[cfg_attr(<some condition>, mod_path::req(<requirement IDs>))]
fn foo() {}
```

**Function-like Macro:**

These traces only link to the line the macro is set at.

```rust
fn foo() {
    reqcov!(<requirement IDs>)
}
```

```rust
fn foo() {
    mod_path::reqcov!(<requirement IDs>)
}
```

**Traces in Comments:**

These traces have an associated line span of the element the comment is referred to.

```rust
/// [req(<requirement IDs>)]
fn foo() {}
```

For traces in regular line comments, several restrictions apply to prevent false detection:

- Traces must be on a separate commented line without any other content except whitespace
- The line directly below a trace must contain a non-commented element to which the trace is linked to
- The affected line span depends on the non-commented element the trace is linked to

```rust
fn foo() {
    // [req(<requirement IDs>)]
    let x = 5;
}
```

**Note:** Traces in block comments are not supported.

### `trace.collect.extern`: Add external traces

- **Parents:** [`trace.collect`, `exchange.traces.schema`]

It must be possible to manually add external traces to *mantra*, because annotations in code
might not be possible.
e.g. In case code was already certified before, adding annotations would change the code, which would require re-certification.

## `trace.special_chars`

In case a requirement ID has characters that are not allowed as part of identifiers in a programming language,
the ID may be wrapped in double quotes `"`.

**Example:**

```
[req("special-char-id.sub_id")]
```

## `trace.element`: Link trace to code element

- **Parents:** [`trace`, `report`, `coverage`]

A trace set in a programming language may be linked to an element,
to improve the expressiveness of the traceability report and mapping of traces to code coverage.

### `trace.element.ident`: Optional associated identifier of a trace

An identifier that uniquely identifies this element may be stored together
with the trace to improve the readability of the traceability report.

**Example:**

```rust
#[req(spanning_trace)]
fn some_fn() {
    // ...
}
```

### `trace.element.type`: Optional identifier type

The type of the element a trace is linked to should be stored in *mantra*,
to improve static test and coverage analysis. Especially important is the information
if a trace is placed on a test case.

For better interoperability, only the following types are allowed with the entry number representing their associated value:

1. `test` ... For a trace to a test case
2. `mod` ... For a trace to a module, package, or other general grouping elements
3. `fn` ... For a trace to a function or method
4. `var` ... For a trace to a variable or static
5. `const` ... For a trace to a constant
6. `type` ... For a trace to a type definition (e.g. `struct`, `enum`, `type`, `class`)
7. `field` ... For a trace to a field or property of a type
8. `trait` ... For a trace to a trait, interface, or other abstract type

The special type `other` with value `0` is used as a placeholder for elements that do not fit into the predefined categories.

### `trace.element.span`: Optional associated line span of a trace

A trace set on an element in a programming language affects all lines of the element.
This line span must be stored in *mantra* to connect code coverage data with traces.

**Example:**

The trace spans all three lines of the `some_fn` function.

```rust
#[req(spanning_trace)]
fn some_fn() {
    // ...
}
```
