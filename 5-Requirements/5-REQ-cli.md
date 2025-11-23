# `cli`: Control *mantra* via CLI

It must be possible to control all features of *mantra* via CLI,
because this helps with integration into CI/CD workflows.

## `cli.collect`: Central command to collect all related information

A central `collect` command must be available that collects all information
needed in *mantra*.

**Implementation Details:**

A central `mantra.toml` file located in the folder the command is executed in
should be used for configuration.

### `cli.collect.metadata`: Collect project metadata

It should be possible to specify metadata such as the project name, version, and link in `mantra.toml`,
because this information does not frequently change, but is needed by some CLI commands such as `report`.

### `cli.collect.config`: Store configuration settings

The settings in `mantra.toml` should be stored in the database when collecting information,
because it shows how specific entries were added to *mantra*.

### `cli.collect.dry_run`: Collect data without saving

As a developer, I want to see the impact of introduced changes to the traceability data,
before merging these changes, because this helps to identify if all needed changes were done,
or some were wrongfully introduced.

## `cli.report`: Command to create (custom) reports

- **Parents:** [`cli`, `report`]

A `report` command must be available to create (custom) reports via CLI.

## `cli.validate`: Command to validate collected data

- **Parents:** [`cli`, `analyze.validate`]

A `validate` command must be available to validate collected date via CLI.

## `cli.query`: Command to analyze collected data

- **Parents:** [`cli`, `analyze.custom`]

A `query` command must be available to analyze collected date via CLI.
