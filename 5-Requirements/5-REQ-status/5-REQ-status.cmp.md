# status.cmp: Compare status of two branches in the wiki

**References:**

- in branch [main](https://github.com/mhatzl/mantra/tree/main): 6

As a product owner, I want to compare the wiki state of two branches,
because it helps to detect outstanding work.
e.g. not all *active* requirements of `feature-branch-x` are *active* in `main`.

**Note:** Only show differences between branches to keep the output compact.

**Example:**

```
**Wiki differences between `branch-a` and `branch-b`:**

| REQ-ID | branch-a | branch-b      |
| ------ | -------- | ------------- |
| req_id | ready    | active        |
| man_id | manual   | manual-traced |
```

**Note:** `manual-traced` means the requirement has the *manual* flag, but also has references in the project.

Created in response to [issue #17](https://github.com/mhatzl/mantra/issues/17).
