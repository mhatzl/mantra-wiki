# wiki.link: Manage links to requirements

**References:**

- in branch main: 7 (4 direct)

The reference syntax `[req:req_id](5-REQ-req_id#req_id-requirement-id)` is very similar to a Markdown hyperlink.
This allows to automatically add links to the requirement entry in the wiki, making references more like *wiki-links*.

*mantra* must be able to handle these links automatically, because links might change, and manual *bookkeeping* is too tedious.

Created in response to [issue #1](https://github.com/mhatzl/mantra/issues/1).

## Sub-requirements

- [req:wiki.link.check](5-REQ-wiki.link.check)
- [req:wiki.link.update](5-REQ-wiki.link.update)

## Implementation details

The URL-prefix to the wiki must be given to *mantra*.
Otherwise, it is not possible to check or construct a *wiki-link*.

The *wiki-link* also depends on the wiki provider.
e.g. The GitHub wiki has no concept of *sub-pages*, making every file in the wiki folder a top-level page.

### GitHub wiki

- **Filepath to page:**

  Every file, independent of the path, is converted to a *root* page in the wiki.
  Consequently, only the filename is considered as part of the link.

- **Filename conversion:**

  1. Strip file extension
  1. Replace whitespace with hyphen `-`

- **Heading conversion:**

  1. Remove punctuations
  1. Remove leading whitespace
  1. Convert to lower case
  1. Replace remaining whitespace with hyphen `-`
