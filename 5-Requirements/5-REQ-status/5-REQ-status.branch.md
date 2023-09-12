# status.branch: See status for one branch in the wiki

**References:**

- in branch [main](https://github.com/mhatzl/mantra/tree/main): 7

As product owner or developer, I want to see an overview of the requirements in the wiki for a specific branch,
because I might only care about the state of this branch.

**Example:**

```
**Wiki status for branch `main`:**

- 5 requirements are *ready* to be implemented
- 30 requirements are *active*
- 2 requirements are *deprecated*
- 3 requirements need *manual* verification
```

The following options should be available to show more detailed information:

- `--detail-ready` ... To show all requirement IDs that are *ready*
- `--detail-active` ... To show all requirement IDs that are *active*
- `--detail-deprecated` ... To show all requirement IDs that are *deprecated*
- `--detail-manual` ... To show all requirement IDs that require *manual* verification

**Example:**

```
**Wiki status for branch `main`:**

- 2 requirements are *ready* to be implemented
- 30 requirements are *active*
- 2 requirements are *deprecated*
- 3 requirements need *manual* verification

***Ready* requirements:**

- new_req_id: Some title
- req_id_v2: Requirement successor
```

Created in response to [issue #17](https://github.com/mhatzl/mantra/issues/17).
