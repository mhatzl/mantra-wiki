# `report`: Reports

As a product owner, I want to be able to generate various reports that show the states of existing requirements,
because these reports help to track project development.

## `report.compact`: Keep reports compact

As a product owner, I want to have small reports that show the most important information at high level,
because I do not want to read 100+ pages every release.
However, I want to be able to get more details manually if I need to.

To keep the report compact, it should only list the requirement title, and link to the origin of the requirement.
The link to the origin should be an optional argument, because it might not be accessible outside an organization.


## `report.release`: Release report

As a product owner, I want to get a report of all *active* requirements for a given project and branch,
because I can show this report to stakeholders as kind of release artifact.

**Example:**

```
***Active* requirements in release v1.1.0:**

- req_id: High-lvl requirement ([requirement origin](URL))
  - req_id.sub_req: Sub-lvl requireent ([sub-req origin](URL))
```

Created in response to [issue #3](https://github.com/mhatzl/mantra/issues/3).

## `report.checklist`: Checklist for *untraceable* requirements

As a product owner, I want that mantra generates a checklist that contains all requirements that are *untraceable*,
because I want to make sure that all of those requirements are verified before a release is published.

**Note:** Because high-level requirements may be *traceable*, but some sub-requirements might **not** be,
the list should be flattened, and only *untraceable* requirements should be included in the list.

**Example:**

```
**Requirements requiring *manual* verification for release v1.1.0:**

- [ ] man_id: Some security concerns ([origin-link](URL))
- [ ] req_id.sub_req: Some UX thing ([origin-link](URL))
```

Created in response to [issue #5](https://github.com/mhatzl/mantra/issues/5).

