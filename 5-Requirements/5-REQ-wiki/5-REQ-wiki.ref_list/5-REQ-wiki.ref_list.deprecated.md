# wiki.ref_list.deprecated: Mark requirements as *deprecated* in specific branches

**References:**

- in branch [main](https://github.com/mhatzl/mantra/tree/main): 4
- in branch [sidebar](https://github.com/mhatzl/mantra/tree/sidebar): 4

It must be possible to explicitly mark requirements as *deprecated*,
because *mantra* cannot know if 0 references means *ready* or *deprecated*.

Requirements may not be *deprecated* in all branches, because LTS versions may have to support a requirement for a longer period.
This requires that each entry in the *references* list must individually be marked as *deprecated*.

*mantra* must then ensure that no references to a *deprecated* requirement is found in the given project. 

To mark an entry as *deprecated*, set `deprecated` instead of the counter.

**Example:**

```
**References:**

- in branch main: deprecated
- in branch stable: 2
```

This example defines that the requirement is *deprecated* in the main branch, but is still *active* in stable.

Created in response to [issue #7](https://github.com/mhatzl/mantra/issues/7).
