# `exchange`: Exchange information

As a user, I want to be able to exchange collected information between *mantra* and other tools.

## `exchange.versioned`: Use semantic versioned schemas

All schemas used to exchange information between *mantra* and other tools must follow semantic versioning,
and each schema must include a version field at the top level, so *mantra* or other tools know which version of the schema should be used to exchange information.

## `exchange.requirements`: Exchange requirements

As a user, I want to be able to exchange requirements between *mantra* and other tools,
because requirements are likely stored in other requirements management tools.

### `exchange.requirements.schema`: Schema to exchange requirements information

- **Parents:** [`exchange.requirements`, `req.id`, `req.title`, `req.description`, `req.origin`, `req.hierarchy.mult_parents`, `req.manual`, `req.deprecate`, `req.properties`]

There are various requirements management tools, and it is infeasible to implement collectors for each one.
Therefore, a JSON schema must be defined to which tools can export to.

Besides JSON, the schema should also be usable for formats such as YAML, TOML, RON (Rust Object Notation),
because they are similar to JSON and might be preferred by some users.

The schema must be able to represent the following information per requirement:

- `req.id`: A unique identifier for the requirement.
- `req.title`: A short title for the requirement.
- `req.description`: A detailed description of the requirement.
- `req.origin`: The origin of the requirement.
- `req.hierarchy.mult_parents`: A list of parent requirements.
- `req.manual`: A boolean indicating whether the requirement requires manual verification.
- `req.deprecate`: A boolean indicating whether the requirement is deprecated.
- `req.properties`: A list of properties associated with the requirement.

## `exchange.traces`: Exchange requirement traces

As a user, I want to be able to add or retrieve requirements traces to or from *mantra*,
because traces are either collected externally, or are used in other project analysis tools.

### `exchange.traces.schema`: Schema to exchange trace information

- **Parents:** [`exchange.traces`, `trace.id`, `trace.origin`, `trace.multiple`, `trace.element`]

The schema must be able to represent the following information:

- The filepath and line number of each trace
- The requirement IDs a trace references
- Optional: The ident, type, and line span of the element that is linked to the trace

## `exchange.coverage`: Exchange code coverage and test information

Code coverage and test data is often produced and analyzed by multiple tools.
Therefore, *mantra* must be able to collect and output this information using standardized or well-supported formats.

### `exchange.coverage.collect`: Collect code coverage and test information

Code coverage is often collected by tools specific to programming languages.
The coverage format supported by those tools alone does not satisfy *mantra*'s `CoverageSchema`,
because they are missing related test information.

Consequently, *mantra* must be able to combine information from a combination of provided
code coverage and test report formats to satisfy the information needed by the `CoverageSchema`.
e.g. combine Cobertura coverage and GoogleTest

### `exchange.coverage.output`: Output code coverage and test information

*mantra* must be able to output the collected coverage and test information into standardized or well-supported formats,
because other tools might be used to do further static analysis.

Consequently, *mantra* must be able to split information from the `CoverageSchema` into specific coverage or test formats.
e.g. split information into Cobertura coverage and GoogleTest files
