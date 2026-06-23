# `extract`: Extract *mantra* information

To reduce duplicate computation and improve debugging of built-in requirement, and trace extraction,
*mantra* should offer an `extract` command that extracts information and outputs it according to the *mantra* schema.

## `extract.requirements`: Extract requirement information

Provide a subcommand to extract requirement information.
The output should be a JSON file adhering to the requirement schema.

## `extract.traces`: Extract trace information

Provide a subcommand to extract trace information.
The output should be a JSON file adhering to the trace schema.
