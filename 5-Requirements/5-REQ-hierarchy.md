# `hierarchy`: Requirements hierarchy

It must be possible to store a requirements hierarchy in *mantra*,
because hierarchical relations between requirements is common in projects.

## `hierarchy.multiple_parents`: Allow multiple parents for one requirement

It must be possible to set multiple parent requirements, because it might not always
be feasible to create single-parent hierarchies.
e.g. API-Authentication may affect multiple routes.

## `hierarchy.no_circle`: Prevent circular hierarchies

A requirement hierarchy must not contain circles, because this would break transitive relations.
