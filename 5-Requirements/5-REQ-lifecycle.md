# `lifecycle`: Handling the lifecycle of collected data

Requirements traceability is done during the whole lifecycle of a project.
Therefore, *mantra* must be able to handle continuous changes to
collected data, while ensuring that the data used to generate
traceability reports remains consistent throughout the project's lifecycle.

## `lifecycle.vcs`: Integration with Version Control Systems

Most projects use version control systems (VCS) to manage their
source code. *mantra* must be integratable in those VCS without
hindering existing development workflows.

Furthermore, *mantra* should not require to store binary files in the VCS
to handle change detection, because binary files are impossible to
humanly review in common VCS like git.

**Implementation Details:**

All collected data must be stored as JSON files in a sub-folder in the `.mantra` folder. These files serve as *caches* that will be imported into the SQL database before collecting new data.

## `lifecycle.versioning`: Versioning of collected data

Collected data must be versioned in a way that integrates with
existing development workflows, because *mantra* must only consider data for the generation of traceability reports that is related to the current version of the project.

### `lifecycle.versioning.id`: Identification of a project version

A project must be uniquely identified by a name and version number.
No semantic versioning can be assumed, because *mantra* must also
be usable for projects that do not follow semantic versioning.

**Implementation Details:**

Each execution of `mantra collect` adds a new entry in the database to which all collected data of this execution is linked to.
This entry is identified by a UTC timestamp, a hash over all collected data, and the project name and version.
When generating traceability reports, *mantra* by default only considers data that is linked to the project name and version that was last added to the database.
