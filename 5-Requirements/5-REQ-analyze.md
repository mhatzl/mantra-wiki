# `analyze`: Analyze collected traceability data

The collected trace, review, test, and coverage data may be used to analyze various aspects of a project.

## `analyze.unimplemented`: List requirements that are not yet implemented

As a project manager, I want to be able to see a list of requirements that are not yet implemented,
because this provides an overview of the project state.

`not yet implemented` in *mantra*'s context refers to requirements that are neither traced nor manually verified.

## `analyze.validate`: Validate collected data

It must be ensured that the collected data is valid,
because reliable data is required for any useful analysis.

### `analyze.validate.store_invalid`: Store invalid data separately

If a trace, test, coverage, or review contains invalid data,
the data must be stored in *mantra* separately to valid content,
but the data should still be available for inspection.
The data must be stored separately, because it must not be considered for analysis of the state of the project.

### `analyze.validate.traces`: Traced requirements exist

A trace is valid if it points to an existing requirement.

### `analyze.validate.coverage`: Coverage entries point to test runs or test cases

A coverage entry is valid if it points to either an existing test run or test case.

### `analyze.validate.deprecated`: Deprecated requirements must not be in use

Deprecated requirements must not be used in a project.
This means that deprecated requirements must not be referenced by any trace or review.

### `analyze.validate.verify`: Verified requirements point to existing requirements

- **Parents:** `analyze.validate`, `review.verify_req`

A manually verified requirement is valid if it points to an existing requirement.

## `analyze.custom`: Allow custom queries for analyzation

It should be possible to run custom queries against the collected trace and coverage data,
because this allows to define what to analyze per project, without requiring to adapt *mantra*.
