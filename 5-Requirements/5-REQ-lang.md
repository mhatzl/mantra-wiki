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

These traces have an associated line span of the element the attribute is set on.

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

```rust
#[req(<requirement IDs>; props: "verifies", "satisfies")]
fn foo() {}
```

```rust
#[req(<requirement IDs>; props: "other-prop")]
fn foo() {}
```

**Function-like Macro:**

These traces only link to the line the macro is set at.

```rust
fn foo() {
    satisfy_req!(<requirement IDs>);
    verify_req!(<requirement IDs>);

    satisfy_req!(<requirement IDs>; <some code that is passed through>);
    verify_req!(<requirement IDs>; assert!(cond == true));

    satisfy_req!(<requirement IDs>; props: "other-prop"; assert!(value > 42));
    verify_req!(<requirement IDs>; props: "verifies", "satisfies"); // trace that both verifies and satisfies a requirement

    mod_path::satisfy_req!(<requirement IDs>)
    mod_path::verify_req!(<requirement IDs>)
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
