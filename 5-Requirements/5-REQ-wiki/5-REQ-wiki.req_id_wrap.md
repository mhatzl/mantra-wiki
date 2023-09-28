# `wiki.req_id_wrap`: Wrap requirement IDs in backticks

**References:**

- in branch [main](https://github.com/mhatzl/mantra/tree/main): 1

IDs in wiki headings must be wrapped in backticks `` ` `` to prevent regular headings from being detected as requirement ID.
Backticks are used for verbatim formatting, which in addition prevents IDs from being formatted.

**Example:**

```
# `req_id`: This is a new requirement

Description...
```

Created in response to [issue #42](https://github.com/mhatzl/mantra/issues/42).
