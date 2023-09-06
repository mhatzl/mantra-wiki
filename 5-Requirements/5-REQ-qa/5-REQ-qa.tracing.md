# qa.tracing: Use requirement IDs in [mantra](https://github.com/mhatzl/mantra)

**References:**

- in branch main: 1

Requirement IDs should be set in [mantra](https://github.com/mhatzl/mantra) at file locations, where the requirement is implemented,
or where it affected the design of the implementation. 
To ignore references, use `[mantra:ignore_next]` before the ID.
IDs must be set using the syntax `[req:my_req_id]`.

**Note:** This helps with traceability between requirements and implementation.
