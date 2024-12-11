# `coverage`: Collect coverage data for traces

As a product owner, I want to ensure that implemented requirements are covered by tests,
because this is required by safety-critical standards and improves software quality.

## `coverage.traces`: Store information about covered traces

- **Related Requirements**: [req(coverage.lines)], [req(trace.span)]

It must be possible to store information about which trace was covered by a specific test case or test-run,
because this information is important to get the requirement coverage.

**Note:** This information may be inferred by combining trace span and line coverage information.

## `coverage.lines`: Store line coverage data

It must be possible to store the line coverage of a specific test case or test-run,
because this information is important for safety-critical certifications.

## `coverage.condition`: Store condition coverage data

It must be possible to store the condition coverage of a specific test case or test-run,
because this information is important for safety-critical certifications.

## `coverage.mcdc`: Store modified condition decision coverage data

It must be possible to store MCDC data of a specific test case or test-run,
because this information is important for safety-critical certifications.

## `coverage.mul_condition`: Store multiple condition coverage data

It must be possible to store the multiple condition coverage of a specific test case
or test-run, because this information is important for safety-critical certifications.

## `coverage.test_relation`: Coverage data must be linked to a test

Coverage data must be associated with test-runs or test cases to know if the related
trace was successfully covered or not.

## `coverage.test_run`: Group tests

Multiple tests may be grouped inside one test-run.
This is similar to a *testsuite*, but test-runs cannot be nested,
and represent the actual execution of a *testsuite*.

This allows to store metadata for test-runs.
e.g. enabled feature flags, target the tests were run on, ...

The test-run metadata is programming language, domain, and company specific,
so it must be possible to store arbitrary information in *mantra*,
but still be able to access the data for the report generation.

## `coverage.static`: Statically analyzed coverage

It should be possible to use static code analysis to detect code coverage of test cases
without executing the test case.
This improves *mantra*'s usability, because covered requirements can already be
displayed while writing a test case.
