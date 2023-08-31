# wiki.link.check: Check validity of *wiki-links*

*mantra* must check every existing *wiki-link* to validate if the link is still correct.

**Note:** To prevent an unnecessary amount of requests to the wiki-host, the links should only be validated
against link rules, but not actually tested. Otherwise, wiki-hosts might consider it as DoS-Attack. 

Created in response to [issue #1](https://github.com/mhatzl/mantra/issues/1).
