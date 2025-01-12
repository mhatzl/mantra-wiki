## Overall Architecture

```mermaid
flowchart LR
    
    Repo@{ shape: docs, label: "Repository Text/Code Files"}

    Annotation["Optional: Trace Annotations
    e.g. [req(my_req_id)]"]
    RustAnnotations["Crate: mantra-rust-macros
    For Rust Code"]
    
    MantraCfg@{ shape: doc, label: "mantra.toml
    Configuration for mantra"}
    
    ReqFile@{ shape: docs, label: "Optional: Requirement File
    [Markdown]"}

    ReqJson@{ shape: docs, label: "Optional: Requirements
    [JSON RequirementSchema]"}

    TraceJson@{ shape: docs, label: "Optional: Traces
    [JSON TraceSchema]"}

    TestCoverage@{ shape: docs, label: "Optional: Test Coverage
    [JSON CoverageSchema]"}

    Review@{ shape: docs, label: "Optional: Review
    [TOML ReviewSchema]"}

    Mantra["mantra
    CLI Tool"]

    db[("mantra.db
    SQLite")]

    Report@{ shape: doc, label: "report.html"}
    ReportJson@{ shape: doc, label: "report.json"}

    MantraSchema["Crate: mantra-schema
    Defines all Mantra Schemas"]

    LangTracing["Crate: mantra-lang-tracing
    Generic Syntax Tracing"]
    RustTracing["Crate: mantra-rust-trace
    Rust Code Tracing"]

    subgraph ct[Code Tracing]
        direction TB

        TreeSitter["tree-sitter
        Creates Generic AST"]
        GenericTracing["For all Text Files
        (mantra internal)"]

        TreeSitter-.->|"Generic Parsing"|LangTracing
        TreeSitter-->|"Rust Code Parsing"|RustTracing

        LangTracing-->|"Adapt for Rust Code
        More Languages to come"|RustTracing

        LangTracing-->|Generic Tracing|GenericTracing
    end

    subgraph Your Code Files
        direction LR

        RustAnnotations-->|Rust proc-macros|Annotation
        Repo-->|Manually annotate code|Annotation
    end

    Annotation-->|mantra collect|ct
    ct-->|"mantra collect (internnally)"|Mantra

    MantraSchema-.->ReqJson
    MantraSchema-.->TraceJson
    MantraSchema-.->TestCoverage
    MantraSchema-.->Review

    MantraCfg-->|"`**mantra collect** & **report**`"|Mantra
    ReqFile-->|mantra collect|Mantra
    ReqJson-->|mantra collect|Mantra
    TraceJson-->|mantra collect|Mantra
    TestCoverage-->|mantra collect|Mantra
    Review-->|mantra collect|Mantra

    Mantra<-->|"Traceability Information
    Uses SQLX"|db

    Mantra-->|"mantra report
    (Custom) Tera Template"|Report
    Mantra-->|"mantra report
    Fix JSON Schema"|ReportJson
```

### Main *mantra* Commands

- `mantra collect`

  Used to collect traceability information.
  The command uses the configuration in `mantra.toml` to know what files/folders to search for information.

  The result is a SQLite database that contains all collected traceability information.

- `mantra report`

  Used to generate a (custom) traceability report.
  Supported output formats are currently only HTML and JSON.

  The Tera templating engine is used to generate HTML reports.
  It is possible to provide custom templates that may access the data from the JSON report.

### Trace Collection

Trace collection is integrated into *mantra* for all text file types.
This includes code files for most programming languages.

By default, *mantra* uses regular expressions to detect requirement traces.
This enables *mantra* to support tracing for various languages out of the box.

To get advanced trace information, such as associated code elements and spans,
*mantra* uses [tree-sitter](https://tree-sitter.github.io/tree-sitter/index.html) to create a generic AST per file.
This AST may then be traversed to detect requirements traces.

The associated span information that is collected with the tree-sitter approach
enables *mantra* to combine code coverage data from tests with the collected traces
to calculate the requirement coverage.

Currently, the AST approach is only implemented for Rust code. 
