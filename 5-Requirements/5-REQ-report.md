# `report`: Reports

As a product owner, I want to be able to generate various reports that show the states of existing requirements,
because these reports help to track project development.

## `report.versioning`: Versioning of reports

- **Parents:** [`report`, `lifecycle.versioning`]

*mantra* must provide options to define what project's and versions must be considered when generating a traceability report.

## `report.project_data`: Show project information in the report

- **Parents:** [`report`, `lifecycle.versioning.id`]

*mantra* must be able to display the following project related information in a report:
- name ... The name of a project
- version ... The version of a project

*mantra* should be able to display the following project related information in a report:
- homepage ... The URL of the homepage of a project
- repository ... The URL of the repository of a project
- license ... The license of a project

*mantra* should allow to display additional metadata
related to a project in custom reports.

## `report.formats`: Supported report formats

The following report formats must be supported by *mantra*:

- Markdown
- HTML
- JSON
- PDF

### `report.formats.json`: JSON report format

The JSON report format must have a fixed schema to ensure stability
for other tools to consume the report.

## `report.custom`: Custom reports

*mantra* is not able to know what information is relevant for projects.
Therefore, *mantra* should provide a way to create custom reports using information collected by *mantra*.
Enough information should be provided by *mantra* per default, so most reports may be created using simple templates.

**Note:** The JSON report format cannot be customized due to requirement `report.formats.json`.

## `report.default`: Default report

A default report must be integrated into *mantra*, so users must not create
their own template.
The default report should cover most requested use cases of a traceability report.

TODO: what is needed to cover most use cases?

## `report.checklist`: Checklist for requirements requiring manual verification

- **Parents:** [`report`, `req.manual`]

As a product owner, I want that mantra generates a checklist that contains all requirements that require manual verification,
because I want to make sure that all of those requirements are verified before a release is published.

**Implementation Details:**

Because high-level requirements may be *traceable*, but some sub-requirements might **not** be,
the list should be flattened, and only *manual* requirements should be included in the list.

**Example:**

```
**Requirements requiring *manual* verification for release v1.1.0:**

- [ ] man_id: Some security concerns ([origin-link](URL))
- [ ] req_id.sub_req: Some UX thing ([origin-link](URL))
```

Created in response to [issue #5](https://github.com/mhatzl/mantra/issues/5).
