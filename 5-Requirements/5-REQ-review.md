# `review`: Review

Provide a way to manually verify requirements and tests,
because not everything can be automated.

## `review.metadata`: Metadata of a review

Every review must contain a name, date, and the authors of the review.
An optional comment may also be set.

## `review.verify_req`: Verify requirements

It must be possible to verify requirements, because some may not be traceable
to specific text lines, or some requirements may explicitly require manual verification.

## `review.test_state`: Override test results

It must be possible to override a test result stored in *mantra*,
because e.g. during semi-automatic testing, a tester may determine
that a test was not passed even though test execution succeeded,
or a test that failed during automatic testing passed during manual testing. 

A comment is always mandatory in this case.

## `review.coverage`: Override coverage data

It must be possible to override the coverage state of specific code lines,
because some defensive code might never be reached.

It must be possible to override the coverage state of specific conditions,
because some defensive code might never be reached.

A comment is always mandatory in this case.
