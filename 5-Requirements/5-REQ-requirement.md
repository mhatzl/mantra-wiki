# `req`: Requirements

Requirement information must be stored in *mantra*, and it must be possible to uniquely identify them,
because requirements are a fundamental part of *mantra*, and identification is needed to trace/verify requirements. 

# `req.id`: Requirement ID

Every requirement must have a unique ID assigned to it,
because some way of identification is needed to reference requirements.
The ID should already tell developers what the requirement is roughly about to help identify the correct requirement to trace.

Created in response to [issue #1](https://github.com/mhatzl/mantra/issues/1).

## `req.id.sub_req`: Sub-requirements for high-level requirements

- **Parents:** [req(req.id)], [req(req.hierarchy)]

Requirement IDs must be structured in a way that allows to create requirement hierarchies,
because most systems/projects have high-level requirements that are then broken up into smaller low-level requirements.

Created in response to [issue #1](https://github.com/mhatzl/mantra/issues/1).

**Implementation details:**

Sub-requirement IDs are separated by `.` from parent IDs.
This creates the impression of a *dot-notation* used in many programming languages,
which should improve familiarity for developers.

**Example:** `parent_req.sub_req`

## `req.id.restrictions`: Restrict allowed characters to use for IDs

An ID must not contain the characters `.`, `"`, `,`, `` ` ``, `[`, `]`, `(`, `)`, `{`, `}`.

- `.` is used to create requirement hierarchies
- `"` is used to wrap IDs in traces in case some characters are not allowed in programming languages (see [req(trace.special_chars)])
- `,` is used to set multiple IDs in one trace (see [req(trace.detect)])
- `` ` `` is used to wrap IDs in Wikis based on Markdown syntax (see [req(extract.wiki)])
- Grouping characters `[`, `]`, `(`, `)`, `{`, `}` would interfere with trace syntax (see [req(trace.detect)])

## `req.hierarchy`: Requirements hierarchy

It must be possible to store a requirements hierarchy in *mantra*,
because hierarchical relations between requirements is common in projects.

### `req.hierarchy.multiple_parents`: Allow multiple parents for one requirement

It must be possible to set multiple parent requirements, because it might not always
be feasible to create single-parent hierarchies.
e.g. API-Authentication may affect multiple routes.

### `req.hierarchy.no_circle`: Prevent circular hierarchies

A requirement hierarchy must not contain circles, because this would break transitive relations.

## `req.origin`: Save the origin of a requirement

As a product owner or developer, I want to know where a requirement is defined,
because more information about the requirement may be found there.

## `req.collect`: Collect requirements

Requirements may be defined in various project management tools.
It must be possible to collect defined requirements from those tools,
because only collected requirements may be referenced.

### `req.collect.wiki`: Collect requirements defined in Markdown based wikis

IDs of requirements defined matching the following regular expression must be extracted from the content of a wiki:

```
^#{1,6} `(?<req_id>[^`"]+)`: \S+
```

#### `req.collect.wiki.manual_req`: Mark requirements as deprecated

- **Parents:** [req(req.collect.wiki)], [req(req.manual)]

It must be possible to mark requirements to require manual verification in the Markdown wiki format.

**Implementation Details:**

```
# `req_id`: Some Requirement

- **Manual Verification**: true
```

##### `req.collect.wiki.manual_req.versioned`: Deprecate requirements only in specific project versions

Marking requirements to require manual verification must be possible per project version,
because some versions may require a verification, but others might not.

#### `req.collect.wiki.deprecate_req`: Mark requirements as deprecated

- **Parents:** [req(req.collect.wiki)], [req(req.deprecate)]

It must be possible to mark requirements as deprecated in the Markdown wiki format.

**Implementation Details:**

```
# `req_id`: Some Requirement

- **Deprecated**: true
```

##### `req.collect.wiki.deprecate_req.versioned`: Deprecate requirements only in specific project versions

Deprecation must be possible per project version, because newer versions may deprecate a requirement,
but the requirement may still be valid in older versions.

### `req.collect.extern`: Collect requirements from external sources

There are various project management tools, and it is infeasible to implement collectors for each one.
Therefore, a JSON schema must be defined to which tools can export to.

Besides JSON, the schema should also be usable for formats such as YAML, TOML, RON (Rust Object Notation),
because they are similar to JSON and might be preferred by some users.

## `req.deprecate`: Deprecate requirements

It must be possible to deprecate requirements.

## `req.manual`: Mark requirements to require manual verification

It must be possible to flag requirements to require manual verification,
because such requirements might not be traceable to specific lines in related artifacts,
or automated testing might not be enough or not possible.
