# `cli`: Control *mantra* via CLI

It must be possible to control all features of *mantra* via CLI,
because this helps with integration into CI/CD workflows.

## `cli.collect`: Central command to collect all related information

A central `collect` command must be available that collects all information
needed in *mantra*.

**Implementation Details:**

A central `mantra.toml` file located in the folder the command is executed in
should be used for configuration.
