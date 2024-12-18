# `analyze`: Analyze trace and coverage data

The collected traces and coverage data may be used to analyze various aspects of a project.

## `analyze.unimplemented`: List requirements that are not yet implemented

As a project manager, I want to be able to see a list of requirements that are not yet implemented,
because this provides an overview of the project state.

## `analyze.validate`: Validate trace and coverage data

It must be ensured that the collected trace and coverage data is valid,
because reliable data is required for any useful analysis.

If a trace, coverage, or review contains invalid information, it must be stored in *mantra* separately to valid content, because the data must not be considered to
detect the state of a requirement, but the data should still be available for inspection.

Required checks are added as sub-requirements to this requirement.

### `analyze.validate.traces`: Traced requirements exist

All traces point to existing requirements.

### `analyze.validate.coverage`: Coverage entries point to traces

All coverage entries point to existing traces with matching requirement IDs.

### `analyze.validate.deprecated`: Deprecated requirements must not be in use

Deprecated requirements must not be used in a project. This means that deprecated requirements
must not be referenced by any traces, coverage, or reviews. 

### `analyze.validate.verify`: Verified requirements point to existing requirements

- **Parents:** `analyze.validate`, `review.verify_req`

All manually verified requirements point to existing requirements.

## `analyze.custom`: Allow custom queries for analyzation

It should be possible to run custom queries against the collected trace and coverage data,
because this allows to define what to analyze per project, without requiring to adapt *mantra*.
