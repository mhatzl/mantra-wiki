# qa.pipeline: Pipeline to ensure a high library quality

**References:**

- in branch main: 4 (0 direct)

A QA pipeline that is run on every PR and push to *main* ensures higher code quality.\
Running pipeline steps in a defined sequence prevents unnecessary checks, which improves sustainability (see: [req:qa.sustain](5-REQ-qa.sustain#qasustain-consider-sustainability-during-design-and-development)).

## Sub-requirements

- [req:qa.pipeline.1_style](5-REQ-qa.pipeline.1_style#qapipeline1_style-ensure-consistent-formatting)
- [req:qa.pipeline.2_lint](5-REQ-qa.pipeline.2_lint#qapipeline2_lint-ensure-good-coding-standard)
- [req:qa.pipeline.3_build](5-REQ-qa.pipeline.3_build#qapipeline3_build-ensure-evident-builds)
- [req:qa.pipeline.4_tests](5-REQ-qa.pipeline.4_tests#qapipeline4_tests-ensure-tests-still-pass)
