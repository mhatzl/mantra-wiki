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

## `extract.jira`: Extract requirement IDs defined in Jira

Atlassian Jira is a widely used project management tool.
For *mantra* to be used by companies, it must be possible to extract requirement IDs from Jira.
