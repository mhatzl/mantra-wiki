# check: Validate wiki and references

**References:**

- in branch [main](https://github.com/mhatzl/mantra/tree/main): 6

*mantra* must offer a `check` command to validate the wiki structure, and references in the project.
The command must provide an overview that contains reference count changes, list referenced *deprecated* requirements,
and list the requirements that would become *active*.

The command must not exit on the first error, because multiple references may be wrong,
and having to trigger the command after every fix to discover that there is another error is too tedious.

**Example of a possible overview:**

```
-----------------------------------------------------------
mantra check ran successfully for branch: main

**Checks:**

- No deprecated requirement referenced
- All found references refer to existing requirements

**Found 4 new active requirements:**

- new_reg: 4 (2 direct)
- new_reg.sub: 2
- other_req: 7
- another_req: 3

**Decreased references:**

- some_old_reg: 6 -> 2
- some_qa_reg: 10 -> 5

**Increased references:**

- my_req: 4 -> 7
```

**Example of an unsuccessful run:**

```
mantra check found 5 errors for branch: main

**Failed checks:**

- 4 references refer to deprecated requirements
- 1 reference to non-existing requirement

See log output for more details.

**Found 4 new active requirements:**

- new_reg: 4 (2 direct)
- new_reg.sub: 2
- other_req: 7
- another_req: 3

**Decreased references:**

- some_old_reg: 6 -> 2
- some_qa_reg: 10 -> 5

**Increased references:**

- my_req: 4 -> 7
```

Created in response to [issue #2](https://github.com/mhatzl/mantra/issues/2) and [issue #8](https://github.com/mhatzl/mantra/issues/8).

# Sub-requirements

- [req:check.ci](5-REQ-check.ci)
