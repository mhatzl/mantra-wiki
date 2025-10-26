# `changes`: Detect changes to collected data

It must be possible to detect content changes of collected data,
because it is important to know which requirements, reviews, tests, or traces
might be affected by those changes.

This is especially important in safety-critical domains.

## `changes.authors`: Collect names of authors responsible for the change

It must be possible to store the name of authors responsible for changes in collected data in *mantra*,
because it allows to relate changes to people.
For ease of use, *mantra* must be able to track changes even if no authors are given,
because project changes are commonly tracked in version control systems anyways.

## `changes.comment`: Collect comment explaining a change

It must be possible to store a comment that explains the changes introduced in *mantra* with newly collected data,
because it allows to better understand the changes and their implications.
This comment must be optional, because enforcing it on every change would decrease the ease of use of *mantra*.

## `changes.track`: Track changes to collected data

*mantra* must be able to automatically track changes to collected data,
and provide a history of those changes.

*mantra* should **not** rely on an underlying version control system (VCS),
but may add VCS related information if it is available.

### `changes.track.reqs`: Track changes to requirements

- **Parents:** [`changes.track`, `exchange.requirements.schema`]

*mantra* must be able to automatically track changes
to requirements related information that is part of the requirements schema covered by `exchange.requirements.schema` except the requirement ID.

#### `changes.track.reqs.id`: Hint for changed requirement IDs

- **Parents:** [`changes.track.reqs`, `req.id`]

The requirement ID should **not** be part of tracked changes,
because it is used to uniquely identify requirements.

However, *mantra* should try to detect changes to a requirement ID,
by searching for a requirement with identical information listed in `changes.reqs`.
In case such a requirement exists in the collected data,
this information should be used to provide users
with an option to update previously collected data to the new ID.
This would allow changing requirement IDs without loosing already collected data for a requirement.

**Note:** Users of *mantra* need to know that changing a requirement ID
can only be tracked if no other information of a requirement changes.

### `changes.track.traces`: Track changes to traces

*mantra* must be able to automatically track changes to trace related information mentioned in sub-requirements of `changes.traces`.

#### `changes.track.traces.files`: Track changes to files that contain traces

**Parents:** [`changes.track.traces`,`trace.origin`]

Changes to the file a trace was detected in might affect the trace
itself and must therefore be stored in *mantra*.

**Note:** Detailed changes to a file may not be stored in *mantra*,
to reduce implementation complexity. It is assumed that the file is stored in a version control system (VCS) anyways.

#### `changes.track.traces.elements`: Track changes to elements that contain traces

- **Parents:** [`changes.track.traces`, `trace.element`]

Changes to an element a trace is linked to might for example affect
the calculation for requirements coverage, and must therefore be tracked.
The reason such a change might affect requirements coverage,
is because coverage data is linked to test runs that were executed
at a specific time, and changes for example to an element's line span
makes older coverage data incompatible or not trustworthy.

### `changes.track.test_runs`: Track changes to test runs

**Parents:** [`changes.track`, `exchange.testcov.schema`]

Changes to stored test run data for a specific execution time is suspicious,
because such data should not change after it was stored.
However, manual modification should be allowed,
but require a statement and author explaining the reason for the change.
If no statement and author is provided, the change must be rejected.

The possibly affected data of a test run that can change is the one
defined by the resulting schema for requirement `exchange.testcov.schema`.

### `changes.track.reviews`: Track changes to reviews

**Parents:** [`changes.track`, `exchange.review.schema`]

Changes to stored test run data for a specific execution time is suspicious,
because such data should not change after it was stored.
However, manual modification should be allowed,
but require a statement and author explaining the reason for the change.

The possibly affected data of a test run that can change is the one
defined by the resulting schema for requirement `exchange.testcov.schema`.

## `changes.show`: Visualize detected changes

*mantra* must be able to visualize detected changes
to provide feedback to users.

TODO: define how to visualize changes
