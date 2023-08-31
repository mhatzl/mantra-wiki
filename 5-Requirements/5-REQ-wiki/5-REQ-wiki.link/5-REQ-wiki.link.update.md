# wiki.link.update: Automatically update *wiki-links*

*mantra* must be able to automatically add and update *wiki-links*.

## Implementation details

The URL-prefix to the wiki must be given to *mantra*.
Otherwise, it is not possible to check or construct a *wiki-link*.

The *wiki-link* also depends on the wiki provider.
e.g. The GitHub wiki has no concept of *sub-pages*, making every file in the wiki folder a top-level page.
