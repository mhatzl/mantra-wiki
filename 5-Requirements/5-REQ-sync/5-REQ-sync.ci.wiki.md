# sync.ci.wiki: CI support for *mantra sync* in the wiki repository

As a requirements engineer, I want that references are synchronized automatically with the wiki
after I made changes to the wiki, because I want to make sure that all existing references are still valid.

Created in response to [issue #1](https://github.com/mhatzl/mantra/issues/1).

## Implementation details

The ci-action would be similar to [req:sync.ci.code](5-REQ-sync.ci.code), because references are still taken from implementation and tests side.
However, this ci-action must validate wiki-links for references to requirements inside the wiki.

**Note:** It is not necessary to validate links inside the wiki with [req:sync.ci.code](5-REQ-sync.ci.code),
because links are already validated by the ci-action for this requirement.

**Note:** Validating links inside the wiki with [req:sync.ci.code](5-REQ-sync.ci.code) might even be too complicated,
because ci-actions run on the project may not receive the full wiki content.
