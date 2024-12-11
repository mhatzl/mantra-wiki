# `qa`: Quality Assurance

*QA* requirements help to ensure a high quality.

**Note:** General *QA* requirements affect the overall architecture and implementation of a project, because they are not specific to a feature/functionality.
Therefore, these requirements must be considered for every existing or new feature/functionality, as long as these *QA* requirements are *active*.

**Note:** Only general *QA* requirements should be part of this requirement group. *QA* requirements that are specific to a requirement group should be added to a *qa* requirement subgroup for this feature.


## `qa.DoD`: Have a "Definition of Done" for requirements

A "Definition of Done" is used to ensure consistent quality for new implementations.
Issues may add additional content to the general "Definition of Done".

## `qa.pipeline`: Pipeline to ensure a high library quality

A QA pipeline that is run on every PR and push to *main* ensures higher code quality.\
Running pipeline steps in a defined sequence prevents unnecessary checks, which improves sustainability (see: [req(qa.sustain)](#qasustain-consider-sustainability-during-design-and-development)).

### `qa.pipeline.1_style`: Ensure consistent formatting

`cargo fmt` is used to ensure consistent code styling, and reduces review times, because code can be formatted automatically.

### `qa.pipeline.2_lint`: Ensure good coding standard

`cargo clippy` is used to as linter to ensure good code quality.

### `qa.pipeline.3_build`: Ensure *mantra* builds

`cargo build` is used to ensure that the code still compiles.

### `qa.pipeline.4_tests`: Ensure tests still pass

`cargo test` is used to run all *mantra* tests.

## `qa.sustain`: Consider sustainability during design and development

Sustainability should be considered during design decisions and development, to reduce unnecessary waste of resources.
e.g. reduce execution of unnecessary workflow steps on PRs

**Note:** Also during development, because e.g. CI/CD-pipelines may unnecessarily waste resources.

## `qa.tracing`: Set requirement traces in code

Requirements for *mantra* should be traced to locations that implement, affect, or test the requirement,
because this allows to use *mantra* for the development of *mantra* itself.

## `qa.ux`: Experience using *mantra*

Using *mantra* must be simple and as little distracting as possible for developers and requirement engineers.
Therefore, the user experience must be considered during development, especially on user-facing functionality.

Created in response to [issue #1](https://github.com/mhatzl/mantra/issues/1).
