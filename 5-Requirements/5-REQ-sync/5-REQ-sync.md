# sync: Synchronize wiki, implementation, and tests

**References:**

- in branch main: 6 (6 direct)

[mantra](https://github.com/mhatzl/mantra) must offer a `sync` command to synchronize reference counts
between requirements in the wiki, and references in implementation and tests.
Maintaining them manually is infeasible.

Created in response to [issue #1](https://github.com/mhatzl/mantra/issues/1).

## Implementation details

**Information needed for synchronization:**

- Location of implementation and test content

  Both implementation and tests must be in the same location,
  because reference counts are not distinguished between implementation and tests.

  **Note:** [mantra](https://github.com/mhatzl/mantra) must have read access in this location to search for references.

- Location of requirements

  Only the section in the wiki that contains the requirements is of interest,
  because [mantra](https://github.com/mhatzl/mantra) is only concerned about
  the requirement ID and the *references* list of requirements.

  **Note:** [mantra](https://github.com/mhatzl/mantra) must have write access in this location to update the *references* list.

- Wiki-URL prefix for requirements

  The prefix that must be set for every wiki-link of a reference to correctly point to the requirement in the wiki.

  **Note:** This setting is more specific to the kind of wiki, because GitHub for example flattens folders,
  making every file available at the root level of the wiki.

- Optional: Wiki-kind

  The kind of supported wikis that is used to store requirements.
  Needed because wikis might need to be handled differently.

  **Note:** Use the GitHub wiki as default.

A high-level flow on how to implement synchronization is described in [DR-20230823_2](6-DR-20230823_2). 

## Sub-requirements

- [req:sync.ci](5-REQ-sync.ci#syncci-ci-support-for-mantra-sync)
