# `report`: Reports

As a product owner, I want to be able to generate various reports that show the states of existing requirements,
because these reports help to track project development.

## `report.custom`: Custom reports

*mantra* is not able to know what information is relevant for projects.
Therefore, *mantra* should provide a way to create custom reports using information collected by *mantra*.
Enough information should be provided by *mantra* per default, so most reports may be created using simple templates.

Created in response to [issue #3](https://github.com/mhatzl/mantra/issues/3).

## `report.default`: Default report

A default report must be integrated into *mantra*, so users must not create
their own template.
The default report should cover most requested use cases of a traceability report.

## `report.checklist`: Checklist for requirements requiring manual verification

As a product owner, I want that mantra generates a checklist that contains all requirements that require manual verification,
because I want to make sure that all of those requirements are verified before a release is published.

**Note:** Because high-level requirements may be *traceable*, but some sub-requirements might **not** be,
the list should be flattened, and only *manual* requirements should be included in the list.

**Example:**

```
**Requirements requiring *manual* verification for release v1.1.0:**

- [ ] man_id: Some security concerns ([origin-link](URL))
- [ ] req_id.sub_req: Some UX thing ([origin-link](URL))
```

Created in response to [issue #5](https://github.com/mhatzl/mantra/issues/5).

## `report.req_snapshot`: 

Requirement content may change during development, even though the ID remains the same.
Because reports do not include the whole content of a requirement,
it is necessary to specify a *tag* that identifies a snapshot of the requirements
for which the report was generated.
Otherwise, it is not clear if the requirement content got changed since the report was generated.
