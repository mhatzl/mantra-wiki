# `trace`: Trace requirements

Tracing requirements down to code level provides better overview of the project status,
and helps with impact analysis. It is also mandatory to achieve certain certifications.

Focus is on traces between requirements and code,
but a requirement hierarchy may be passed to *mantra*
to detect transitive relations between requirements and artifacts.

## `trace.id`: Use the requirement ID for traces

- **Parents:** [`trace`, `req.id`]

The requirement ID must be used for tracing, because the ID uniquely identifies a requirement.

## `trace.origin`: Origin of requirement traces

To know where a trace is located in a text file, the filepath and line number must be stored.
This information helps developers with project navigation, and is needed for *coverage* analysis
and certification.

The trace origin must be used as unique identifier of a trace,
because filepath and line number is the most basic form of location in a text file.

The line numbers must start at one for the first line in a text file.

**Note:** With *mantra*'s focus on traces between requirements and code, it is assumed that all traces will point to text files,
and therefore using filepath and line number as origin is feasible.

## `trace.mult_reqs`: Trace more than one requirement at same origin

More than one requirement may affect the same code.
Therefore, it must be possible to specify more than one requirement at the same origin.

## `trace.kind`: Kind of a trace

A trace must be assigned to one of the following kinds:

- **Clarifies**

  Traces of kind `clarifies` may be used to link documents, diagrams, or other artifacts
  that provide more details and rationale for the traced requirements.

- **Satisfies**

  Traces of kind `satisfies` may be used to link to code sections or other artifacts
  that implement the traced requirements.

- **Verifies**

  Traces of kind `verifies` may be used to link to tests, assertions, or other artifacts
  that verify the traced requirements.

- **Links**

  Traces of kind `links` may be used to indicate that a trace links to a requirement,
  but does not add any information to clarify, satisfy, or verify the requirement.

## `trace.properties`: Properties of a trace

A trace may have properties that further describe the trace.
*mantra* must be able to store trace properties that are not used by *mantra* itself,
because companies and projects may define their own custom trace properties.

## `trace.collect`: Collect requirements traces

It must be possible to collect requirements traces at least manually and semi-automatically,
because automated collection is not always possible.
Nevertheless, to improve the usability of *mantra*, trace collection should be automated as much as possible.

### `trace.collect.auto.filter`: Use ignore files to restrict the search for traces

Many repositories contain files and folders that should be ignored when searching for traces.
e.g. build outputs, git folder, ...

Most projects already use `.gitignore` files to exclude those files and folders.
Therefore, mantra must adhere to settings of a `.gitignore` file that is found in the current or parent directories of a repository.
Additionally, mantra must offer `.ignore` files to specify files and folders that must be ignored in addition to the `.gitignore` file.

Besides `.ignore`, it must also be possible to use `.traceignore` files to be more strict with ignores for mantra, when searching for traces.

**Note:** The `.git` folder must always be ignored, because it cannot hold valid traces.

### `trace.collect.auto.pattern`: Pattern to detect traces

- **Parents:** [`trace.collect.auto`, `trace.id`, `trace.mult_reqs`, `trace.properties`]

To improve consistency across programming languages on how to specify traces in code,
a default pattern must be defined and the functionality to detect this pattern must be exposed by *mantra* to be usable by third parties.

**Default Pattern Rules:**
- Every requirement ID must be surrounded by double quotes `"`
- One or more requirement IDs may be given and separated by one comma `,` and optional whitespace before and/or after the comma
- After the last requirement ID, trace properties may be set after a semicolon `;`
- One trace property may either be a [JSON5 object](https://spec.json5.org/#objects), [JSON5 array](https://spec.json5.org/#arrays), or [JSON5 strings](https://spec.json5.org/#strings)
- One or more trace properties may be given and separated by one comma `,` and optional whitespace before and/or after the comma

**Examples:**

```
"first-id", "second-id.123"; "critical-property", [123, 456], { some_key: "some value" }
```

### `trace.collect.auto.general`: Collect traces from text-based files

- **Parents:** [`trace.collect.auto`, `trace.kind`]

If no language specific feature is defined to trace requirements for a text-based file,
the following patterns must be detected on a line-by-line basis.

For traces that **clarify** a requirement:

```
[req_note(<requirement IDs>)]
```

For traces that **satisfy** a requirement:

```
[req(<requirement IDs>)]
```

For traces that **verify** a requirement:

```
[req_test(<requirement IDs>)]
```

For traces that **link** to a requirement:

```
[req_link(<requirement IDs>)]
```

**Note:** `<requirement IDs>` is used as placeholder for the pattern defined in [req("trace.collect.auto.pattern")].

**Examples:**

```
[req_note("first_id")]

[req("req_id")]
[req("first_id", "second_id")]

[req_test("req_id")]

[req_link("second_id")]
```

**Rationale:**

`req_note` was chosen for `clarify`, because you *add a note* to a requirement for clarification.

`req` was chosen for `satisfy`, because it is assumed to be the most common trace kind next to `verify`,
and having a short form is faster to write.

`req_test` was chosen for `verify`, because it hints at testing a requirement, which is a form of verification,
but subjectively *sounds* better than `req_verify`.

### `trace.collect.auto.ast`: Collect traces from an abstract syntax tree

**Parents:** [`trace.collect`, `trace.element`]

An AST should be used to restrict trace detection for programming languages.

**Rationale:**

Only requirements traces intended by developers should be detected, because falsely detected traces
result in unreliable trace data.
Therefore, traces found in commented code should be ignored or have restricted detection rules,
and language features should be used to further restrict trace detection.

See [requirement `lang`](5-REQ-lang) for language specific tracing conventions.

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

## `trace.code_block`: Link trace to code block

- **Parents:** [`trace`, `lang.rust.tracing`]

A trace may be linked to a code block that is not an element such as a loop or statement.
Therefore, *mantra* must be able to store code blocks that have no associated identifier or definition.

### `trace.code_block.span`: Associated line span of a code block

A trace set on a code block in a programming language affects all lines of the code block.
This line span must be stored in *mantra* to connect code coverage data with traces.

**Example:**

The trace spans all four lines of the condition.

```rust
// [req("spanning_trace")]
if some_condition {
    // ...
}
```

## `trace.element`: Link trace to code element

- **Parents:** [`trace`, `report`, `coverage`]

A trace set in a programming language may be linked to an element,
to improve the expressiveness of the traceability report and mapping of traces to code coverage.

### `trace.element.ident`: Associated identifier of an element

An identifier that uniquely identifies this element may be stored together
with the trace to improve the readability of the traceability report.

**Example:**

```rust
#[req("spanning_trace")]
fn some_fn() {
    // ...
}
```

### `trace.element.kind`: Optional identifier kind

The kind of the element a trace is linked to should be stored in *mantra*,
to improve static test and coverage analysis. Especially important is the information
if a trace is placed on a test case.

For better interoperability, only the following kinds are allowed with the entry number representing their associated value:

1. `test` ... For a trace to a test case
2. `mod` ... For a trace to a module, package, or other general grouping elements
3. `fn` ... For a trace to a function or method
4. `var` ... For a trace to a variable or static
5. `const` ... For a trace to a constant
6. `type` ... For a trace to a type definition (e.g. `struct`, `enum`, `type`, `class`)
7. `field` ... For a trace to a field or property of a type
8. `trait` ... For a trace to a trait, interface, or other abstract type

The special kind `other` with value `0` is used as a placeholder for elements that do not fit into the predefined categories.

### `trace.element.span`: Associated line span of an element

A trace set on an element in a programming language affects all lines of the element.
This line span must be stored in *mantra* to connect code coverage data with traces.

**Example:**

The trace spans all four lines of the `some_fn` function,
including the attribute macro.

```rust
#[req("spanning_trace")]
fn some_fn() {
    // ...
}
```
