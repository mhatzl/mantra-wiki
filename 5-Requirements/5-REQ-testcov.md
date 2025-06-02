# `testcov`: Collect test and coverage data

As a product owner, I want to ensure that implemented requirements are covered by tests,
because this is required by safety-critical standards and improves software quality.
To represent this information in traceability reports, *mantra* must be able to store this data.

## `testcov.test_run`: Store test run data

Multiple tests may be grouped inside one test-run.
This is similar to a *testsuite*, but test-runs cannot be nested,
and represent the actual execution of a *testsuite*.

This allows to store metadata for test-runs.
e.g. enabled feature flags, target the tests were run on, ...

The test-run metadata is programming language, domain, and company specific,
so it must be possible to store arbitrary information in *mantra*,
but still be able to access the data for the report generation.

## `testcov.test_case`: Store test case data

The information if a test case was executed successfully, failed, or skipped must be stored
in reference to a test-run, because the state of a test case is important for quality assurance.
The origin of a test case must also be stored, which at least includes the filepath and line number
the test case is defined at. An optional identifier for the test case may also be stored.

## `testcov.cov`: Store coverage data

Code coverage data must be associated with test-runs or test cases to know if a
requirement was successfully covered by one or more tests.

Detecting if a requirement was covered by a test is possible my mapping
the line spans of linked traces with the covered lines of the test.

**Note:** Preferably, the code coverage data should be linked per test case to get the most
accurate requirement coverage, but not all test tools and formats support this fine grain coverage control.

### `testcov.cov.lines`: Store line coverage data

It must be possible to store the line coverage of a specific test case or test-run,
because this information is important for safety-critical certifications.

### `testcov.cov.condition`: Store condition coverage data

It must be possible to store the condition coverage of a specific test case or test-run,
because this information is important for safety-critical certifications.

### `testcov.cov.mcdc`: Store modified condition decision coverage data

It must be possible to store MCDC data of a specific test case or test-run,
because this information is important for safety-critical certifications.

### `testcov.cov.mul_condition`: Store multiple condition coverage data

It must be possible to store the multiple condition coverage of a specific test case
or test-run, because this information is important for safety-critical certifications.

### `testcov.cov.fn`: Infer function coverage data

It must be possible to infer the function coverage of a specific test case or test-run
based on the line coverage data and collected function information during trace collection.

## `testcov.static_approx`: Statically approximated requirement coverage

It should be possible to use static code analysis to approximate requirement coverage of test cases
without executing the test case.
This improves *mantra*'s usability, because covered requirements could already be
displayed while writing a test case.
