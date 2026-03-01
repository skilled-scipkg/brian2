---
name: brian2-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in brian2; it prioritizes documentation references and then source inspection only for unresolved details.
---

# brian2: Examples and Tutorials

## High-Signal Playbook
### Route conditions
- Use this skill for choosing, running, and adapting example/tutorial scripts.
- Route install/compiler blockers to `brian2-build-and-install`.
- Route low-level API behavior questions to `brian2-api-and-scripting`.
- Route numerical-method selection questions to `brian2-theory-and-methods`.

### Triage questions
- Is the goal onboarding, feature demonstration, or benchmark-style simulation?
- Is runtime mode acceptable, or is standalone mode required?
- Should plotting be headless (CI/remote) or interactive?
- Which family best matches the request: `tutorials`, `examples/synapses`, `examples/standalone`, or `examples/frompapers`?

### Canonical workflow
- Pick the closest built-in script family.
- Run with deterministic settings and headless plotting when needed.
- Compare key outputs (spike counts, trace shapes, timing behavior) before modifying model details.

```bash
MPLBACKEND=Agg python examples/synapses/synapses.py
MPLBACKEND=Agg python examples/standalone/simple_case.py
```

### Validation checkpoints
- Script exits without Python/runtime compile errors.
- Generated traces/spike counts are finite and non-empty.
- If standalone example is used, generated code builds and executes successfully.
- Modified example still matches expected qualitative behavior from the original script.

## Scope
- Handle questions about worked examples, tutorials, and cookbook usage.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs_sphinx/introduction/scripts.rst`
- `docs_sphinx/advanced/scheduling.rst`
- `tutorials/1-intro-to-brian-neurons.ipynb`
- `tutorials/2-intro-to-brian-synapses.ipynb`
- `tutorials/3-intro-to-brian-simulations.ipynb`
- `examples/synapses/synapses.py`
- `examples/synapses/STDP.py`
- `examples/standalone/simple_case.py`
- `examples/standalone/simple_case_build.py`
- `examples/frompapers/Brette_2012/README.txt`
- `examples/frompapers/Stimberg_et_al_2018/README.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the listed function-level entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `tutorials`
- `examples/synapses`
- `examples/standalone`
- `examples/frompapers`

## Test references
- `brian2/tests`
- `dev/tools/tests`

## Optional deeper inspection
- `brian2`

## Source entry points for unresolved issues
- `brian2/sphinxext/generate_examples.py`
- `brian2/sphinxext/examplefinder.py`
- `brian2/core/network.py`
- `brian2/groups/neurongroup.py`
- `brian2/synapses/synapses.py`
- `brian2/monitors/statemonitor.py`
- `brian2/monitors/spikemonitor.py`
- `brian2/devices/cpp_standalone/device.py`
- `brian2/tests/test_complex_examples.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" brian2`).
