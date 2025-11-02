# `testcov`: Collect test and coverage data

As a product owner, I want to ensure that implemented requirements are covered by tests,
because this is required by safety-critical standards and improves software quality.
To represent this information in traceability reports, *mantra* must be able to store this data.

## `testcov.test_run`: Store test run data

Multiple tests may be grouped inside one test run.
This is similar to a test suite, but test runs represent the execution of a test suite.

### `testcov.test_run.origin`: Store the origin of the test run data

The origin of a test run must be stored in *mantra*, but the storage format should stay flexible to allow different origin variants.
For example, test runs could have local files or URLs as origins.

### `testcov.test_run.id`: Identifier of a test run

The name of the test run must be used as unique identifier.
A test run may be executed multiple times and stored in *mantra*, but only the newest execution of a test run must be used to calculate the latest requirements coverage.

### `testcov.test_run.date`: Date of a test run

A test run represents the execution of a test suite,
so it must store the date and time the test run was executed.

The name of a test run is used as identifier,
and therefore only the newest execution of a test run must be stored.

### `testcov.test_run.metadata`: Metadata of a test run

The test run metadata is programming language, domain, and company specific,
so it must be possible to store arbitrary information in *mantra*,
but still be able to access the data for the report generation.
e.g. enabled feature flags, target the tests were run on, ...

### `testcov.test_run.nested`: Allow nested test runs

- **Parents:** [`testcov.test_run`, `exchange.testcov.test.junit`]

It must be possible to build a hierarchy of test-runs, because well-supported formats like JUnit
allow nested test suites and *mantra* must be able to exchange test data that adheres to the JUnit format.

The number of test cases of a test run must be the sum of all test cases directly linked to the test run
plus the number of test cases of all nested test runs.

However, test runs must only have one parent,
to fit the nested structure of formats like JUnit.
It is also easier to create a usable schema,
by allowing to set a list of test runs as a field in the parent test run.
Taking the approach to express hierarchies from the requirement schema would be harder for test runs, because the id of a test run is more tedious to set manually compared to the requirement id.

**Implementation Details:**

Nested test runs are handled similar to the requirements hierarchy,
by having a test run hierarchy table.

#### `testcov.test_run.nested.no_cycle`: Prevent cyclical dependencies in nested test runs

Cyclical dependencies between test runs must not be allowed and must be prevented in *mantra* internally.

## `testcov.test_case`: Store test case data

A test case must be part of a test run, and must be uniquely identified within the test run.

### `testcov.test_case.state`: State of a test case

The state of a test case must be one of the following:

- `passed`: The test case passed.
- `failed`: The test case failed.
- `skipped`: The test case was skipped.

#### `testcov.test_case.state.reason`: Reason for the state of a test case

For state `skipped`, the reason for skipping the test case must be stored in *mantra* if such a reason exists in the provided data.

#### `testcov.test_case.state.unknown`: Unknown state of a test case

If a test case is not in one of the supported states defined by `testcov.test_case.state`, the state must be makred as `unknown` and the test case treated as failed.

### `testcov.test_case.id`: Identifier of the test case

The name of a test case must be used as unique identifier per test run a test case is linked to.
Testing tools must ensure that the name is unique per test run.

### `testcov.test_case.origin`: Origin of the test case

- **Parents:** [`testcov.test_case`, `trace.origin`]

The origin of a test case consists of the filepath and line number the test case is defined at.
For *mantra* to link traces to test cases, the filepaths of traces and test cases must use the same relative path origin.
Storing filepaths as absolute paths would prevent the database or reports from being portable.

The origin of a trace is its unique identifier, and therefore
the test case origin must also be usable as unique identifier.

### `testcov.test_case.metadata`: Metadata of the test case

The metadata of a test case is programming language, domain, project, and company specific,
so it must be possible to store arbitrary information in *mantra*,
but still be able to access the data for the report generation.
e.g. logs, pre-/post-conditions, description, etc.

## `testcov.cov`: Store coverage data

- **Parents:** [`testcov`, `trace.origin`]

Code coverage data must be associated with test-runs or test cases to know if a
requirement was successfully covered by one or more tests.

**Note:** Preferably, the code coverage data should be linked per test case to get the most
accurate requirement coverage, but not all test tools and formats support this fine grain coverage control.

### `testcov.cov.trace_mapping`: Map traces to code coverage of tests

Detecting if a requirement was covered by a test is possible my mapping
the line spans of linked traces with the covered lines of the test.

#### `testcov.cov.trace_mapping.vcs`: Map trace and code coverage data when knowing the VCS ident

- **Parents:** [`testcov.cov.trace_mapping`, `changes.track.vcs`]

If a VCS identifier is provided for test results and code coverage metrics,
*mantra* must validate that traces were collected for this VCS ident,
and map coverage metrics to entries related to this VCS ident.

#### `testcov.cov.trace_mapping.use_hash`: Map trace and code coverage data when knowing file hashes

If file hashes are provided for test results and code coverage metrics,
*mantra* must validate that traces were collected for those file hashes,
and map coverage metrics to those file entries.

#### `testcov.cov.trace_mapping.no_hash`: Map trace and code coverage data without knowing file hashes

If a file hash is not provided for test results and code coverage metrics,
*mantra* should use the collection timestamps, test run timestamps, spans of detected elements, and statement coverage metrics
to map coverage metrics to the most likely hash of a file.

#### `testcov.cov.trace_mapping.filepath`: Same relative filepath origin

For the trace and code coverage mapping to work, the filepaths of traces and coverage data must use the same relative path origin.
Storing filepaths as absolute paths would prevent the database or reports from being portable.

#### `testcov.cov.trace_mapping.line_nr`: Line numbering

The line numbers for coverage data must start at one for the first line
to match with line numbers of traces.

### `testcov.cov.lines`: Store line coverage data

It must be possible to store the line coverage of a specific test case or test-run,
because this information is important for safety-critical certifications.

### `testcov.cov.branch`: Store branch coverage data

It must be possible to store the branch coverage of a specific test case or test-run,
because this information is important for safety-critical certifications.

See https://www.rapitasystems.com/difference-between-decision-coverage-and-branch-coverage for the difference between branch and decision coverage.

### `testcov.cov.decision`: Store decision coverage data

It must be possible to store the decision coverage of a specific test case or test-run,
because this information is important for safety-critical certifications.

See https://www.rapitasystems.com/difference-between-decision-coverage-and-branch-coverage for the difference between branch and decision coverage.

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
