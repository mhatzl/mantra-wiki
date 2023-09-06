# wiki.ref_list.manual: Mark requirements to require manual verification

Some requirements may require manual verification, because it is either not possible to trace them in code,
or they cannot be verified automatically.
Therefore, it must be possible to mark requirements with `manual`, because *mantra* itself cannot detect
if a requirement cannot be traced, or it is not implemented.

Once a requirement is marked as `manual`, *mantra* must not remove this flag even if references are found,
because the requirement may still require manual verification.
To show that references were found, the counter must be added after the flag.

The `manual` flag may be set per entry in the *references* list.
The list may be created manually, because *mantra* would only create the list if it found references in code. 

**Example:**

```
# my_req: Requirement must be manually verified

**References:**

- in branch main: manual

# other_req: Requirement must be manually verified, but is also referenced in code

**References:**

- in branch main: manual + 1
```

Created in response to [issue #4](https://github.com/mhatzl/mantra/issues/4).
