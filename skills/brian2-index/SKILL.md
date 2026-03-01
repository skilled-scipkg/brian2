---
name: brian2-index
description: This skill should be used when users ask how to use brian2 and the correct generated documentation skill must be selected before going deeper into source code.
---

# brian2 Skills Index

## Route the request
- Classify the request into one of the generated topic skills listed below.
- Prefer abstract, workflow-level guidance for large scientific packages; do not attempt full function-by-function coverage unless explicitly requested.

## Generated topic skills
- `brian2-getting-started`: Getting Started (initial setup, quickstarts, and core concepts)
- `brian2-api-and-scripting`: API and Scripting (language bindings, APIs, and programmatic interfaces)
- `brian2-developer-guide`: Developer Guide (developer architecture, extension points, and contribution workflow)
- `brian2-simulation-workflows`: Simulation Workflows (simulation setup, execution flow, and runtime controls)
- `brian2-inputs-and-modeling`: Inputs and Modeling (inputs, system setup, models, and physical parameterization)
- `brian2-build-and-install`: Build and Install (build, installation, compilation, and environment setup)
- `brian2-examples-and-tutorials`: Examples and Tutorials (worked examples, tutorials, and cookbook usage)
- `brian2-theory-and-methods`: Theory and Methods (theoretical background and algorithmic methods)
- `brian2-docs-sphinx`: Docs Sphinx (documentation grouped under the 'docs-sphinx' theme)
- `brian2-tests`: Tests (documentation grouped under the 'tests' theme)

## Topic reference maps
- `brian2-getting-started`: `../brian2-getting-started/references/doc_map.md`, `../brian2-getting-started/references/source_map.md`
- `brian2-api-and-scripting`: `../brian2-api-and-scripting/references/doc_map.md`, `../brian2-api-and-scripting/references/source_map.md`
- `brian2-developer-guide`: `../brian2-developer-guide/references/doc_map.md`, `../brian2-developer-guide/references/source_map.md`
- `brian2-simulation-workflows`: `../brian2-simulation-workflows/references/doc_map.md`, `../brian2-simulation-workflows/references/source_map.md`
- `brian2-inputs-and-modeling`: `../brian2-inputs-and-modeling/references/doc_map.md`, `../brian2-inputs-and-modeling/references/source_map.md`
- `brian2-build-and-install`: `../brian2-build-and-install/references/doc_map.md`, `../brian2-build-and-install/references/source_map.md`
- `brian2-examples-and-tutorials`: `../brian2-examples-and-tutorials/references/doc_map.md`, `../brian2-examples-and-tutorials/references/source_map.md`
- `brian2-theory-and-methods`: `../brian2-theory-and-methods/references/doc_map.md`, `../brian2-theory-and-methods/references/source_map.md`
- `brian2-docs-sphinx`: `../brian2-docs-sphinx/references/doc_map.md`, `../brian2-docs-sphinx/references/source_map.md`
- `brian2-tests`: `../brian2-tests/references/doc_map.md`, `../brian2-tests/references/source_map.md`

## Documentation-first inputs
- `docs_sphinx`

## Tutorials and examples roots
- `examples`
- `tutorials`

## Test roots for behavior checks
- `brian2/tests`
- `dev/tools/tests`

## Escalate only when needed
- Start from the matched topic skill primary references.
- If those references are insufficient, open that topic's doc map path from the `Topic reference maps` section above.
- If documentation still leaves ambiguity, open the same topic's source map path from `Topic reference maps` and inspect the listed function-level source entry points and behavior checks.
- Use targeted symbol search while inspecting source (for example: `rg -n "<symbol_or_keyword>" brian2`).

## Source directories for deeper inspection
- `brian2`
