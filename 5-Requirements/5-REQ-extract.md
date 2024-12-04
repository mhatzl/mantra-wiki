# `extract`: Extract requirements

Requirements may be defined in various project management tools.
It must be possible to extract defined requirement IDs from those tools,
because only defined requirements may be referenced.

## `extract.origin`: Save the origin of a requirement

As a product owner or developer, I want to know where a requirement is defined,
because more information about the requirement may be found there.

## `extract.wiki`: Extract requirement IDs defined in Markdown based wikis

IDs of requirements defined matching the following regular expression must be extracted from the content of a wiki:

```
^#{1,6} `(?<req_id>[^`"]+)`: \S+
```

## `extract.custom`: Extract requirement IDs from JSON

There are various project management tools, and it is infeasible to implement extractors for each one.
Therefore, a JSON schema must be defined to which tools can export to.
