# qa.tracing: Use requirement IDs in the *project* repository

Requirement IDs should be set in the *project* repository at file locations, where the requirement is implemented,
or where it affected the design of the implementation.
IDs must be set using the syntax `[req:my_req_id]`, with an optional link added with `[req:my_req_id](URI to requirement in the wiki)`.

**Note:** This helps with traceability between requirements and implementation.
