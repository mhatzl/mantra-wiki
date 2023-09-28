# `filter`: Use ignore files to restrict the search for references

**References:**

- in branch [main](https://github.com/mhatzl/mantra/tree/main): 1

Many repositories contain files and folders that should be ignored when searching for references.
e.g. build outputs, git folder, ...

Most projects already use `.gitignore` files to exclude those files and folders.
Therefore, mantra must adhere to settings of a `.gitignore` file that is found in the current or parent directories of a repository.
Additionally, mantra must offer `.ignore` files to specify files and folders that must be ignored in addition to the `.gitignore` file.

Besides `.ignore`, it must also be possible to use `.mantraignore` files to be more strict with ignores for mantra.

**Note:** The `.git` folder is always ignored, because it cannot hold valid references.

Created in response to [issue #19](https://github.com/mhatzl/mantra/issues/19).
