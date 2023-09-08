# release.checklist: Checklist for requirements marked with *manual* flag

As a product owner, I want that mantra generates a checklist that contains all requirements marked with the *manual* flag,
because I want to make sure that all of those *manual* requirements are verified before a release is published.

To keep the report compact, it should only list the requirement title, and link to the wiki entry.
The link to the wiki should be an optional argument, because the wiki might not be accessible outside an organization.

**Example:**

```
**Requirements requiring *manual* verification for release v1.1.0:**

- [ ] req_id: High-lvl requirement ([wiki-link](URL))
  - [ ] req_id.sub_req: Sub-lvl requireent ([wiki-link](URL))
```

Created in response to [issue #5](https://github.com/mhatzl/mantra/issues/5).
