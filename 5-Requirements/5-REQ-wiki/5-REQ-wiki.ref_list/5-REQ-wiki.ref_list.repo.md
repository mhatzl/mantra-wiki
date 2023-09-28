# `wiki.ref_list.repo`: Handle multiple repositories for one wiki

**References:**

- in branch [main](https://github.com/mhatzl/mantra/tree/main): 14

Many wikis must handle multiple repositories, because the System may not be created in a monolith repository.
Therefore, each entry in the *references* list may add `in repo <repository name>` before the branch name.

**Example:**

```
**References:**

- in repo mantra-actions in branch main: 3
```
