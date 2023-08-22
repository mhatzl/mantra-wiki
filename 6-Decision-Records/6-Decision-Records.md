{{

This section contains decision records for the system.

}}

## Guidelines

### Record Title

The title of a decision record file should start with `7.1-DR-` followed by the creation date of the DR
in the format `YYYYMMDD`.
This creates an increasing number to keep records ordered on the wiki.

Often, created records are not finalized. In this case, `A-Z` should be used as placeholder values starting at `A`.
If more draft records are created, increase the placeholder starting at the right most alphabetic character.
Not all numbers may be replaced, since most records should be finalized at least within one year.
e.g. 2023AAAA, 2023AAAB, 202XXXXX

### Workflow

Decision record files should be created as soon as a discussion might converge to a decision.
To prevent unnecessary documentation efforts, add a link to the discussion in the record file if possible,
or mark it with `**WIP**` (Work In Progress).

Once a decision is concrete, document it in the record file, and adapt the title to the current date.
The link to the discussion might be kept for reference, but the `**WIP**` marker must be removed.
With this convention, records with a valid date in the title are known to be final.

### Interplay with Requirements

Decision records may be mentioned in requirements, or requirements might be mentioned in the DR.
However, only requirements have a notion of state (e.g. proposed, ready, active, ...).
This makes decision records active if at least one active requirement links to it, or if the DR links to at least one active requirement.
