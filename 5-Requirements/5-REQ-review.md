# `review`: Review

Provide a way to manually verify requirements and tests,
because not everything can be automated.

## `review.verify_req`: Verify requirements

It must be possible to verify requirements, because some may require manual verification.

## `review.test_state`: Override test results

It must be possible to override a test result afterwards,
because e.g. during semi-automatic testing, a tester may determine
that a test was not passed even though test execution succeeded. 

A comment is always mandatory in this case.
