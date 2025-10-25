# `lifecycle`: Handling the lifecycle of collected data

Requirements traceability is done during the whole lifecycle of a project.
Therefore, *mantra* must be able to handle continuous changes to
collected data, while ensuring that the data used to generate
traceability reports remains consistent throughout the project's lifecycle.

## `lifecycle.vcs`: Integration with Version Control Systems

Most projects use version control systems (VCS) to manage their
source code. *mantra* must be integratable in those VCS without
hindering existing development workflows.

### `lifecycle.vcs.storage`: Use human readable format to store collected data

*mantra* should not require to store binary files in a VCS to handle change detection,
because binary files are impossible to humanly review in common VCS like git.
With collected data being stored in a SQL database, the data must be extractable from the database
and added back to the database before new data is collected to prevent wrong data history.

**Implementation Details:**

All collected data must be stored as JSON files in a sub-folder in the `.mantra` folder.
These files serve as *caches* that will be imported into the SQL database before collecting new data.

## `lifecycle.project`: Lifecycle of collected data for a project

The lifecycle of collected data for a project must be stored in a way that allows to distinguish work happening on different versions of a project.
The base of these different versions of a project are referred to as project baselines in *mantra*.
Linking collected data to a project baseline is important to show the state of a project that has multiple version lines.
For example, a project may have a *stable* and *unstable* baseline.

### `lifecycle.project.id`: Identification of a project baseline

A project must be uniquely identified by the name and base of a project.
A project base might for example be a specific branch of a project.

**Note:** Using a project version as identifier and semantic versioning is not possible,
because *mantra* must be usable for projects that do not follow semantic versioning,
and multiple branches of a project may be based on the same version during development.

**Implementation Details:**

Each execution of `mantra collect` adds a new entry in the database to which all collected data of this execution is linked to.
This entry is identified by a UTC timestamp, a hash over all collected data, and the project name and base.
When generating traceability reports, *mantra* by default must only consider data that is linked to the project name and base
which may either be set in `mantra.toml`, passed as arguments to `mantra report`, or be defined based on the used vcs.

### `lifecycle.project.default_base`: Default project base

If no project base is set, *mantra* must use `main` as fallback name,
because it is the common name for the default branch in new git repositories.
