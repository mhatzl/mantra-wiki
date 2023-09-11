# release: Release report

**References:**

- in branch [main](https://github.com/mhatzl/mantra/tree/main): 6 (5 direct)
- in branch [sidebar](https://github.com/mhatzl/mantra/tree/sidebar): 6 (5 direct)

As a product owner, I want to get a report of all *active* requirements for a given branch,
because I can show this report to stakeholders as kind of release artifact.

To keep the report compact, it should only list the requirement title, and link to the wiki entry.
The link to the wiki should be an optional argument, because the wiki might not be accessible outside an organization.

**Example:**

```
***Active* requirements in release v1.1.0:**

- req_id: High-lvl requirement ([wiki-link](URL))
  - req_id.sub_req: Sub-lvl requireent ([wiki-link](URL))
```

Created in response to [issue #3](https://github.com/mhatzl/mantra/issues/3).

# Sub-requirements

- [req:release.checklist](5-REQ-release.checklist)
