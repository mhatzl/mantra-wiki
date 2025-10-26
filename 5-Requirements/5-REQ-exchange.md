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

- **Parents:** [`exchange`, `trace`]

As a user, I want to be able to add or retrieve requirements traces to or from *mantra*,
because traces are either collected externally, or are used in other project analysis tools.

### `exchange.traces.schema`: Schema to exchange trace information

- **Parents:** [`exchange.traces`, `trace.id`, `trace.origin`, `trace.mult_reqs`, `trace.kind`, `trace.properties`, `trace.element`]

The schema must be able to represent the following information:

- The filepath and line number of a trace
- The requirement IDs a trace references
- The kind of a trace
- Optional: Properties of a trace
- Optional: The ident, type, and line span of the element that is linked to the trace

## `exchange.testcov`: Exchange code coverage and test information

- **Parents:** [`exchange`, `testcov`]

Code coverage and test data is often produced and analyzed by multiple tools.
Therefore, *mantra* must allow standardized or well-supported formats as inputs,
and must be able output this information using standardized or well-supported formats.

### `exchange.testcov.schema`: Provide *mantra* specific schema to exchange code coverage and test information

- **Parents:** [`exchange.testcov`, `testcov.test_run`, `testcov.test_case`, `testcov.cov`]

No standardized or well-supported format so far could be found that closely combines code coverage and test information.
Therefore, *mantra* should provide a schema that allows to add coverage data to test runs and/or test cases.

### `exchange.testcov.test`: Exchange test data using standardized or well-supported formats

- **Parents:** [`exchange.testcov`, `testcov.test_run`, `testcov.test_case`]

All standardized or well-supported formats mentioned as sub-requirements
cannot store coverage data alongside the test data.
This has the following implications:

- **Format as Input:**

  If a file adhering to a format mentioned under `exchange.testcov.test` is given
  without additional coverage formats mentioned under `exchange.testcov.cov`,
  no coverage data will be available for the mentioned test suites and test cases.

- **Format as Output:**

  Only stored test data is output.
  Possibly related coverage data is ignored.

#### `exchange.testcov.test.junit`: Exchange test data using the JUnit format

[JUnit XML](https://llg.cubic.org/docs/junit/) is a well-supported format for exchanging test data,
and must therefore be supported as in- and output format for test run and test case information.

The equivalent of a test run in *mantra* in the JUnit format is called test suite.

### `exchange.testcov.cov`: Exchange code coverage data using standardized or well-supported formats

- **Parents:** [`exchange.testcov`, `testcov.cov`]

All standardized or well-supported formats listed as sub-requirements
cannot store test data alongside the coverage data.
This has the following implications:

- **Format as Input:**

  Since *mantra* links coverage data to test data, it is not possible to add coverage data
  without providing related test data that adheres to one of the formats listed in `exchange.testcov.test`.

  An error must be thrown if no test data is provided.

- **Format as Output:**

  Without restricting the output to one or more test runs,
  all stored coverage data is output.

#### `exchange.testcov.cov.cobertura`: Exchange code coverage data using the Cobertura format

[Cobertura](https://github.com/gcovr/gcovr/blob/main/tests/cobertura.coverage-04.dtd)
is a well-supported format for exchanging code coverage data.
However, there seems to be no standardized format for exchanging multiple condition coverage or mc/dc data.
Therefore, *mantra* must only be able to handle `statement`, `condition`, `branch`, and `function` coverage
when exchanging code coverage data using the Cobertura format.

## `exchange.review`: Exchange review data

*mantra* must provide a standardized way to exchange reviews
with third party tools, because reviews may be managed
or further processed by external tools.

### `exchange.review.schema`: Provide *mantra* specific schema to exchange reviews

- **Parents:** [`exchange.review`, `review.id`, `review.author`, `review.description`, `review.origin`, `review.verify_req`, `review.test_case_state`,
`review.coverage`]

The review for manually verifying requirements is fairly specific to *mantra*.
Therefore, *mantra* must provide a JSON schema that allows to exchange review data.

Furthermore, *mantra* must accept reviews adhering to this schema from the following file formats:

- TOML
- JSON
