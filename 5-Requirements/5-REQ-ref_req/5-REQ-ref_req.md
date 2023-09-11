# ref_req: Reference requirements

**References:**

- in branch main: 5 (3 direct)
- in branch [sidebar](https://github.com/mhatzl/mantra/tree/sidebar): 5 (3 direct)

It must be possible to reference requirements using their IDs.
Otherwise, semi-automatic tracing is not possible, because [mantra](https://github.com/mhatzl/mantra) cannot determine if a requirement is *active* or not.

The syntax to reference requirements is: `[req:req_id]`

**Note:** `req_id` is used as placeholder, and must be replaced by an existing ID.

Created in response to [issue #1](https://github.com/mhatzl/mantra/issues/1).

## Implementation details

This syntax was chosen, because it should be independent enough in most programming languages that regex can be used to search for references,
while still being able to distinguish an expression from a requirement reference.

Using regex simplifies the implementation effort, because textual files may be searched without the need to first analyze the semantics of a programming language.

## Sub-requirements

- [req:ref_req.ignore](5-REQ-ref_req.ignore)

## ref_req.test: Test requirement referencing

**References:**

- in branch main: 1
- in branch [sidebar](https://github.com/mhatzl/mantra/tree/sidebar): 1

Add a test to make sure that references are found in some content.
