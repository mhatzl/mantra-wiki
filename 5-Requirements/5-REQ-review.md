# `review`: Review

Provide a way to manually verify requirements and tests,
because not everything can be automated.

## `review.id`: Identification of a review

A review in *mantra* must be uniquely identified by the name
and UTC datetime of the review, because some form of identification is required for a review to be referencable in a traceability report.

**Note:** It is assumed that a name and UTC datetime is enough to uniquely identify a review.

## `review.reviewer`: Reviewer of a review

Every review must contain a list of reviewers that were involved in the review, because this is essential information for a any review.

## `review.description`: Description of a review

Every review may contain a general description
to provide additional context about the review.

## `review.verify_req`: Verify requirements

- **Parents:** [`review`, `req.id`]

It must be possible to manually verify requirements,
because some may not be traceable to specific text lines,
or some requirements may explicitly require manual verification.

In *mantra*, requirements may be manually verified in reviews,
using the requirement ID to refer to the requirement.

Additional information about the verification may be described
in a comment next to the requirement ID.
This option is especially important in safety-critical domains,
where such information is needed for qualification.

## `review.test_case_state`: Override state of a test case

- **Parents:** [`review`, `testcov.test_case.state`]

It must be possible to override the state of a test case
stored in *mantra*, because e.g. during semi-automatic testing,
a tester may determine that a test was not passed even though
test execution succeeded, or a test that failed during
automatic testing passed during manual testing.

A comment must always be mandatory in this case.

## `review.coverage`: Override coverage data

- **Parents:** [`review`, `testcov.cov`]

It must be possible to override the coverage state of specific code lines,
because some defensive code might never be reached.

It must be possible to override the coverage state of specific
conditions, because some defensive code might never be reached.

A comment must always be mandatory in this case.
