# `req`: Requirements

Requirement information must be stored in *mantra*, and it must be possible to uniquely identify them,
because requirements are a fundamental part of *mantra*, and identification is needed to trace/verify requirements.

## `req.id`: Requirement ID

Every requirement must have a unique ID assigned to it,
because some way of identification is needed to reference requirements.
The ID should already tell developers what the requirement is roughly about to help identify the correct requirement to trace.

### `req.id.sub_req`: Sub-requirements for high-level requirements

- **Parents:** [`req.id`, `req.hierarchy`]

Requirement IDs should allow to create simple requirement hierarchies that are easy to understand and navigate,
because most systems/projects have high-level requirements that are then broken up into smaller low-level requirements.

**Implementation details:**

Sub-requirement IDs may be separated by `.` from parent IDs.
This creates the impression of a *dot-notation* used in many programming languages,
which should improve familiarity for developers.

**Example:** `parent_req.sub_req`

### `req.id.restrictions`: Restrict allowed characters to use for IDs

An ID must not contain the characters `.`, `"`, `'`, `,`, `` ` ``, `[`, `]`, `(`, `)`, `{`, `}`.

- `.` is used to create requirement hierarchies
- `"` is used in JSON files to wrap requirement IDs, and to wrap IDs in traces in case some characters are not allowed as part of an identifier in a programming language (see [req(trace.special_chars)])
- `'` could be confused with double quotes
- `,` is used to set multiple IDs in one trace (see [req(trace.detect)])
- `` ` `` is used to wrap IDs in Wikis based on Markdown syntax (see [req(extract.wiki)])
- Grouping characters `[`, `]`, `(`, `)`, `{`, `}` would interfere with trace syntax (see [req(trace.detect)])

**Note:** It is recommended that IDs follow common conventions for identifiers in programming languages to help with traceability in code files.

## `req.hierarchy`: Requirements hierarchy

It must be possible to store a requirements hierarchy in *mantra*,
because hierarchical relations between requirements is common in projects.

### `req.hierarchy.mult_parents`: Allow multiple parents for one requirement

It must be possible to set multiple parent requirements, because it might not always
be feasible to create single-parent hierarchies.
e.g. API-Authentication may affect multiple routes.

#### `req.hierarchy.mult_parents.wiki`: Specify multiple parents in the Markdown wiki format

- **Parents:** [`req.hierarchy.mult_partens`, `req.properties.wiki`]

TODO: explain in more detail

### `req.hierarchy.no_circle`: Prevent circular hierarchies

A requirement hierarchy must not contain circles, because this would break transitive relations.

## `req.origin`: Save the origin of a requirement

As a product owner or developer, I want to know where a requirement is defined,
because more information about the requirement may be found there.

## `req.description`: Save the description of a requirement

- **Parents:** [`req`, `report`, `safety.change`]

The description of a requirement must be stored in *mantra*,
because it improves change detection and enables the creation of more detailed traceability reports.

## `req.properties`: Allow additional properties for requirements

It must be possible to specify additional properties for requirements that are not handled by *mantra*,
because requirements may have properties that are only relevant for a specific project or company.

### `req.properties.wiki`: Specify additional properties for requirements in the Markdown wiki format

- **Parents:** [`req.properties`, `req.collect.wiki`, `req.manual`, `req.deprecate`, `req.hierarchy.mult_parents`]

It must be possible to specify additional properties of requirements in the Markdown wiki format,
because the Markdown wiki format must be feature complete with all other requirement collection approaches.

**Implementation Details:**

Properties of requirements may be added directly after the requirement heading, in the form of a Markdown list of key-value pairs adhering to the following rules:

- Each list entry has a valid key-value pair
- Every key has at least one non-whitespace character and is separated by one colon character from the value
- Each key including the colon separator may be surrounded by two asterisks to make the key bold
- Every value has at least one non-whitespace character
- Value parts of keys that are unknown to `mantra` are parsed following the [Rust Objection Notation](https://github.com/ron-rs/ron)

## `req.collect`: Collect requirements

Requirements may be defined in various project management tools or text files.
It must be possible to collect defined requirements from those tools and files,
because only collected requirements can be linked to other artifacts.

### `req.collect.wiki`: Collect requirements defined in Markdown based wikis

- **Parents:** [`req.collect`, `req.id`, `req.properties`, `req.origin`, `req.description`, `qa.ux`]

A simple Markdown based approach to define requirements must be supported,
to prevent the need for additional tools to define and manage requirements.
One Markdown file should allow to define multiple requirements,
to prevent the creation of many files containing only a few sentences,
which would likely lead to worse project navigation.

Markdown is chosen, because it is a well-known and simple markup language.

**Implementation Details:**

Requirements in Markdown files must adhere to the following rules for *mantra* to detect them:

- Only heading content is searched for the definition of a requirement
- A heading must start with a requirement ID that is enclosed in verbatim ticks
- One colon character is placed after the ending verbatim tick
- One space character separates the colon from the requirement title
- The requirement title contains at least one non-whitespace character
- An optional list of key-value properties may follow the heading
- All following lines are considered part of the requirement description until the next requirement definition is found

**Example:**

```
# `req_id`: Some Requirement Title

This is the requirement description.

# `req_id_2`: Another Requirement Title

- **Key:** "Value"

This is another requirement description.
```

### `req.collect.extern`: Collect requirements from external sources

There are various project management tools, and it is infeasible to implement collectors for each one.
Therefore, a JSON schema must be defined to which tools can export to.

Besides JSON, the schema should also be usable for formats such as YAML, TOML, RON (Rust Object Notation),
because they are similar to JSON and might be preferred by some users.

## `req.manual`: Mark requirements to require manual verification

It must be possible to flag requirements to require manual verification,
because such requirements might not be traceable to specific lines in related artifacts,
or automated testing might not be enough or not possible.

### `req.manual.wiki`: Mark requirements in Markdown wiki to require manual verification

- **Parents:** [`req.manual`, `req.properties.wiki`]

It must be possible to mark requirements to require manual verification in the Markdown wiki format.

**Implementation Details:**

The case insensitive key `Manuel Verification` may be used to mark requirements to require manual verification
using `true` or `false` as values.

**Note:** `Manuel Verification` is quite long, so offer `Manual` as an alternative.

```
# `req_id`: Some Requirement

- **Manual Verification**: true

# `req_id_2`: Another Requirement Title

- **Manual**: true
```

### `req.manual.versioned`: Mark requirements to require manual verification only in specific project versions

Marking requirements to require manual verification must be possible per project version,
because some versions may require a verification, but others might not.

TODO: explain in more detail

## `req.deprecate`: Deprecate requirements

It must be possible to deprecate requirements, because they might be outdated or superseded by newer requirements at some point.

#### `req.deprecate.wiki`: Mark requirements as deprecated

- **Parents:** [`req.deprecate`, `req.properties.wiki`]

It must be possible to mark requirements as deprecated in the Markdown wiki format.

**Implementation Details:**

```
# `req_id`: Some Requirement

- **Deprecated**: true
```

##### `req.deprecate.versioned`: Deprecate requirements only in specific project versions

Deprecation must be possible per project version, because newer versions may deprecate a requirement,
but the requirement may still be valid in older versions.

TODO: explain in more detail
