# `exchange`: Exchange information

As a user, I want to be able to exchange collected information between *mantra* and other tools.

## `exchange.traces`: Exchange requirement traces

As a user, I want to be able to add or retrieve requirements traces to or from *mantra*,
because traces are either collected externally, or are used in a later project analysis tool.

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
