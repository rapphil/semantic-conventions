# YAML Model for Semantic Conventions

The YAML descriptions of semantic convention contained in this directory are intended to
be used by the various OpenTelemetry language implementations to aid in automatic
generation of semantics-related code.

⚠ If you want to read the semantic conventions and not edit them, please see
the generated markdown output in the [specification](../specification/README.md) folder.

## Writing semantic conventions

Semantic conventions for the spec MUST adhere to the
[attribute naming](https://github.com/open-telemetry/opentelemetry-specification/tree/v1.21.0/specification/common/attribute-naming.md),
[attribute requirement level](https://github.com/open-telemetry/opentelemetry-specification/tree/v1.21.0/specification/common/attribute-requirement-level.md),
and [metric requirement level](https://github.com/open-telemetry/opentelemetry-specification/tree/v1.21.0/specification/metrics/metric-requirement-level.md) conventions.

Refer to the [syntax](https://github.com/open-telemetry/build-tools/tree/v0.18.0/semantic-conventions/syntax.md)
for how to write the YAML files for semantic conventions and what the YAML properties mean.

A schema file for VS code is configured in the `/.vscode/settings.json` of this
repository, enabling auto-completion and additional checks. Refer to
[the generator README](https://github.com/open-telemetry/build-tools/tree/v0.18.0/semantic-conventions/README.md) for what extension you need.

## Generating markdown

These YAML files are used by the make target `table-generation` to generate consistently
formatted Markdown tables for all semantic conventions in the specification. Run it from the root of this repository using the command

```
make table-generation
```

For more information, see the [semantic convention generator](https://github.com/open-telemetry/build-tools/tree/v0.18.0/semantic-conventions)
in the OpenTelemetry build tools repository.
Using this build tool, it is also possible to generate code for use in OpenTelemetry
language projects.

See also:

* [Markdown Tables](https://github.com/open-telemetry/build-tools/tree/main/semantic-conventions#markdown-tables)
* [Code Generator](https://github.com/open-telemetry/build-tools/tree/main/semantic-conventions#code-generator)
