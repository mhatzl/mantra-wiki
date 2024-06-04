# `analyze`: Analyze trace and coverage data

The collected traces and coverage data may be used to analyze various aspects of a project.

## `analyze.not_implemented`: List requirements that are not yet implemented

As a project manager, I want to be able to see a list of requirements that are not yet implemented,
because this provides an overview of the project state.

## `analyze.validate`: Validate trace and coverage data

It must be ensured that the collected trace and coverage data is valid,
because reliable data is required for any useful analysis.

Required checks are added as sub-requirements to this requirement.

### `analyze.validate.traces`: Traced requirements exist

All traces point to existing requirements.

### `analyze.validate.coverage`: Coverage entries point to traces

All coverage entries point to existing traces with matching requirement IDs.

### `analyze.validate.deprecated`: Requirements marked as deprecated exist 

All deprecated requirements point to existing requirements.

### `analyze.validate.manual`: Manual reviews point to existing requirements

All manually verified requirements point to existing requirements.

## `analyze.custom`: Allow custom queries for analyzation

It should be possible to run custom queries against the collected trace and coverage data,
because this allows to define what to analyze per project, without requiring to adapt *mantra*.
