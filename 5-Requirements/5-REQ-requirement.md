# `req`: Requirements

Requirement information must be stored in *mantra*, and it must be possible to uniquely identify them,
because requirements are a fundamental part of *mantra*, and identification is needed to trace/verify requirements.

## `req.id`: Requirement ID

Every requirement must have a unique ID assigned to it,
because some way of identification is needed to reference requirements.

**Note:** The ID should already tell developers what the requirement is roughly about to help identify the correct requirement to trace.

### `req.id.sub_req`: Sub-requirements for high-level requirements

- **Parents:** [`req.id`, `req.hierarchy`]

Requirement IDs should allow to create simple requirement hierarchies that are easy to understand and navigate,
because most systems/projects have high-level requirements that are then broken up into smaller low-level requirements.

**Implementation details:**

Sub-requirement IDs may be separated by `.` from parent IDs.
This creates the impression of a *dot-notation* used in many programming languages,
which should improve familiarity for developers.

**Example:** `parent_req.sub_req`

**Note:** IDs should not contain whitespace to improve the readability of this *dot-notation*.

### `req.id.restrictions`: Restrict allowed characters to use for IDs

- **Parents:** [`req.id`, `trace.collect.auto.pattern`, `req.id.sub_req`, `req.collect.wiki`, `report.formats`]

An ID must not contain the characters `.`, `"`, `'`, `,`, `` ` ``, `;`, `<`, `>`.

- `.` is used to create requirement hierarchies (see [req("req.id.sub_req")])
- `"` is used to wrap requirement IDs in *mantra*'s common trace pattern (see [req("trace.collect.auto.pattern")])
- `'` could be confused with double quotes
- `,` is used to set multiple IDs in one trace (see [req("trace.collect.auto.pattern")])
- `` ` `` is used to wrap IDs in Wikis based on Markdown syntax (see [req("req.collect.wiki")])
- `;` is used as separator between requirement IDs and trace properties in *mantra*'s common trace pattern (see [req("trace.collect.auto.pattern")])
- `<`, `>` would potentially break the HTML report without sanitizing every ID (see [req("report.formats")])

## `req.hierarchy`: Requirements hierarchy

It must be possible to store a requirements hierarchy in *mantra*,
because hierarchical relations between requirements is common in projects.

### `req.hierarchy.mult_parents`: Allow multiple parents for one requirement

It must be possible to set multiple parent requirements, because it might not always
be feasible to create single-parent hierarchies.
e.g. API-Authentication may affect multiple routes.

#### `req.hierarchy.mult_parents.wiki`: Specify multiple parents in the Markdown wiki format

- **Parents:** [`req.hierarchy.mult_partens`, `req.properties.wiki`]

Multiple parents may be specified using the key `Parents` in the property list.
The key is case insensitive and must allow the case insensitive alias `Parent`.

The value must be a comma-separated list of requirement IDs that is enclosed in square brackets.
Each ID in the list must either be enclosed in verbatim ticks, or given as Markdown hyperlink
where the text content only consists of the requirement ID which must be enclosed in verbatim ticks.

**Example:**

```
Parents: [`req.hierarchy.mult_parents`, [`req.properties.wiki`](<link to requirement>)]
```

### `req.hierarchy.no_cycle`: Prevent cyclical hierarchies

A requirement hierarchy must not contain cycles, because this would break transitive relations.

## `req.origin`: Save the origin of a requirement

As a product owner or developer, I want to know where a requirement is defined,
in case I want to modify the requirement, or find out more about it.

### `req.origin.wiki`: Origin of a requirement in the Markdown wiki format

- **Parents:** [`req.origin`, `req.collect.wiki`]

The origin of a requirement in a Markdown wiki is defined as follows:

- Filepath relative from the root directory set in `mantra.toml` to the Markdown file that defines the requirement
- Line number of the first line of the heading that defines the requirement
- **Optional:** Prefix set in `mantra.toml` that is added to the relative filepath

#### `req.origin.wiki.github`: Origin-URL of a requirement for GitHub wiki

Due to GitHub wiki treating every file in the wiki as a top-level page independent of the folder structure,
the origin filepath might not correctly point to a requirement in the hosted wiki on GitHub.
Therefore, *mantra* must construct and store this URL in addition to the actual origin information.

An additional optional prefix must available in the `mantra.toml` file that points
to base URL of the rendered wiki.

**Warn:** New GitHub wiki versions might change this behavior.

### `req.origin.extern`: Origin of a requirement using external sources

- **Parents:** [`req.origin`, `req.collect.extern`]

Many requirements management tools are either web-based or provide a service that links a URI to a requirement.
Therefore, *mantra* must allow to store a URI as origin for externally defined requirements.

## `req.title`: Save the title of a requirement

- **Parents:** [`req`, `report`, `safety.change`]

The title of a requirement must be stored in *mantra*,
because it likely provides a better overview compared to the ID of a requirement,
but is shorter than the description.

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

- **Parents:** [`req.collect`, `req.id`, `req.properties`, `req.title`, `req.description`, `qa.ux`]

A simple Markdown based approach to define requirements must be supported,
to prevent the need for additional tools to define and manage requirements.
One Markdown file should allow to define multiple requirements,
to prevent the creation of many files containing only a few sentences,
which would likely lead to worse project navigation.
The approach must also allow to set the same information that may be given in the `exchange.requirements.schema`, to serve as a proper alternative to external requirements management tools.

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

#### `req.collect.wiki.filter`: Use ignore files to restrict the search for Markdown files

Many repositories contain files and folders that should be ignored when searching for requirement definitions.
e.g. build outputs, git folder, ...

Most projects already use `.gitignore` files to exclude those files and folders.
Therefore, mantra must adhere to settings of a `.gitignore` file that is found in the current or parent directories of a repository.
Additionally, mantra must offer `.ignore` files to specify files and folders that must be ignored in addition to the `.gitignore` file.

Besides `.ignore`, it must also be possible to use `.reqignore` files to be more strict with ignores for mantra,
when searching for Markdown files.

**Note:** The `.git` folder must always be ignored, because it cannot hold valid requirement definitions.

### `req.collect.extern`: Collect requirements from external sources

- **Parents:** [`req.collect`, `exchange.requirements.schema`]

Collect externally defined requirements from files that adhere to the schema defined in `exchange.requirements.schema`.

*mantra* must be able to collect external requirements from the following file formats:

- JSON

*mantra* may support to collect external requirements from the following file formats:

- RON (Rust Object Notation)
- TOML

## `req.manual`: Mark requirements to require manual verification

It must be possible to flag requirements to require manual verification,
because such requirements might not be traceable to specific lines in related artifacts,
or automated testing might not be enough or not possible.

### `req.manual.wiki`: Mark requirements in Markdown wiki to require manual verification

- **Parents:** [`req.manual`, `req.properties.wiki`]

It must be possible to mark requirements to require manual verification in the Markdown wiki format.

**Implementation Details:**

The case insensitive key `Manuel Verification` may be used to mark requirements to require manual verification
using case insensitive `true` or `false` as values.

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

The case insensitive key `Deprecated` may be used to mark requirements as deprecated
using case insensitive `true` or `false` as values.

```
# `req_id`: Some Requirement

- **Deprecated**: true
```

##### `req.deprecate.versioned`: Deprecate requirements only in specific project versions

Deprecation must be possible per project version, because newer versions may deprecate a requirement,
but the requirement may still be valid in older versions.

TODO: explain in more detail
