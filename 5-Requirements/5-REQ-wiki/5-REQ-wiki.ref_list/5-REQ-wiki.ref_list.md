# wiki.ref_list: *References* list

**References:**

- in branch main: 17 (12 direct)

As a developer, I want to know what requirements are currently *active*,
because I need to know what requirements must be considered during implementation.

As a product owner, I want to know what requirements are currently *active*,
because I want to inform stakeholders about the current state of the system/project.

Created in response to [issue #1](https://github.com/mhatzl/mantra/issues/1).

## Implementation details

It was decided to use the wiki to store this information visible to all that have access to the wiki.
In addition, the information is stored on a *per requirement* basis, to directly see the phase a requirement is in.
For more details see [DR-20230823](6-DR-20230823).

The *references* list must be placed directly after the requirement heading,
so it is easier to find the list using regex.

**Note:** Because markdown is not that strict with blank lines, empty lines between heading and the *references* list should be optional.

**Structure of the *references* list**

```
**References:**

- in branch <branch name>: <reference count for this branch>
- in branch <other branch name>: <reference count for this branch>
```

**Note:** Text inside `<>` is used as placeholder.

## Sub-requirements

- [req:wiki.ref_list.branch_link](5-REQ-wiki.ref_list.branch_link)
