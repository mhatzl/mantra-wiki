# filter: Use ignore files to restrict the search for references

Many repositories contain files and folders that should be ignored when searching for references.
e.g. build outputs, git folder, ...

Most projects already use `.gitignore` files to exclude those files and folders.
Therefore, mantra must adhere to settings of a `.gitignore` file that is found in the current or parent directories of a repository.
Additionally, mantra must offer `.ignore` files to specify files and folders that must be ignored in addition to the `.gitignore` file. 

**Note:** All `dot-files` are also ignored by default except `.github` and `.gitlab` folders, to ignore mostly editor specific settings.

Created in response to [issue #19](https://github.com/mhatzl/mantra/issues/19).
