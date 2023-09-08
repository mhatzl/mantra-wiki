# release.checklist: Checklist for requirements marked with *manual* flag

As a product owner, I want that mantra generates a checklist that contains all requirements marked with the *manual* flag,
because I want to make sure that all of those *manual* requirements are verified before a release is published.

To keep the report compact, it should only list the requirement title, and link to the wiki entry.
The link to the wiki should be an optional argument, because the wiki might not be accessible outside an organization.

**Note:** Because high-level requirements may not be marked as *manual*, but some sub-requirements of it might be,
the list is flattened for all requirements, and only requirements marked with *manual* are included in the list.

**Example:**

```
**Requirements requiring *manual* verification for release v1.1.0:**

- [ ] man_id: Some security concerns ([wiki-link](URL))
- [ ] req_id.sub_req: Some UX thing ([wiki-link](URL))
```

Created in response to [issue #5](https://github.com/mhatzl/mantra/issues/5).
