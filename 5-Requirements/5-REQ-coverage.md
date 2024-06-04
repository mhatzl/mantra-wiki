# `coverage`: Collect coverage data for traces

As a product owner, I want to ensure that implemented requirements are tested,
because this helps with certification and improves software quality.

## `coverage.test_relation`: Coverage data must be linked to a test

Coverage data must be associated with tests to know if the related trace
was successfully covered or not.

Code coverage is primarily collected during testing, so this restriction is fine.
If coverage from benchmarks or regular execution must be added to *mantra*,
it may be *wrapped* in a manually created test run.

## `coverage.test_run`: Group tests

Multiple tests may be grouped inside one test-run.
This is similar to a *testsuite*, but test-runs cannot be nested
and represent the actual execution of a *testsuite*.

This allows to store metadata for test-runs.
e.g. enabled feature flags, target the tests were run on, ...

The test-run metadata is programming language, domain, and company specific,
so it must be possible to store arbitrary information in *mantra*,
but still be able to access the data for the report generation.
