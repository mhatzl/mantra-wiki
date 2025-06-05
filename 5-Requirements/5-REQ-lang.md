# `lang`: Conventions for integrated programming languages

Sub-requirements of `lang` define conventions and syntax constructs
that must be followed by users that want to use *mantra*'s built-in
automatic trace, test, and coverage collection for supported programming languages.

## `lang.rust`: Conventions for Rust

Contains conventions for Rust code to allow automated collection of traceability information by *mantra*.

### `lang.rust.tracing`: Rules to detect traces in Rust code

- **Parents:** [`lang.rust`, `trace.collect.auto.ast`]

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
