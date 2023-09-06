# sync.ci: CI support for *mantra sync*

**References:**

- in branch main: 1 (1 direct)

[mantra](https://github.com/mhatzl/mantra) must offer the possibility to automate
synchronization between wiki, implementation, and tests, because it is infeasible to do manually.

Created in response to [issue #11](https://github.com/mhatzl/mantra/issues/11).

## Implementation details

To keep the implementation similar to local synchronization, git should be used in the ci-actions
to make external git repositories local.
