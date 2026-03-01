---
name: brian2-tests
description: This skill should be used when users ask about tests in brian2; it prioritizes documentation references and then source inspection only for unresolved details.
---

# brian2: Tests

## High-Signal Playbook
### Route conditions
- Use this skill for test selection, regression reproduction, marker usage, and backend-aware validation.
- Route implementation design or architecture questions to `brian2-developer-guide`.
- Route install/compiler failures before tests run to `brian2-build-and-install`.

### Triage questions
- Is the failure in runtime, standalone, or both?
- Which subsystem changed (equations, synapses, monitors, codegen, preferences)?
- Is there a minimal failing test or reproduction script?
- Is deterministic behavior required (seed control, no stochastic flakiness)?

### Canonical workflow
- Start with a narrow failing test file.
- Re-run only relevant markers/subsets to isolate backend-specific behavior.
- Confirm fix with adjacent regression tests in the same subsystem.

```bash
python -m pytest brian2/tests/test_neurongroup.py -q
python -m pytest brian2/tests/test_synapses.py -q
python -m pytest brian2/tests/test_cpp_standalone.py -q
```

### Validation checkpoints
- Reproduction test fails before fix and passes after fix.
- At least one adjacent subsystem test file also passes.
- Standalone-related changes pass `test_cpp_standalone.py` when relevant.
- Warning/error text assertions remain stable where tests check diagnostics.

## Scope
- Handle questions about test workflows, regression checks, and behavior validation.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs_sphinx/developer/guidelines/testing.rst`
- `docs_sphinx/developer/guidelines/logging.rst`
- `docs_sphinx/developer/standalone.rst`
- `docs_sphinx/user/computation.rst`
- `brian2/tests/pytest.ini`
- `brian2/tests/utils.py`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tests as behavior or regression references first.
- If ambiguity remains, inspect `references/source_map.md` and start with the listed function-level entry points.
- Cite exact file paths in responses.

## Tutorials and examples
- `examples`
- `tutorials`

## Test references
- `brian2/tests`
- `dev/tools/tests`

## Optional deeper inspection
- `brian2`

## Source entry points for unresolved issues
- `brian2/tests/utils.py`
- `brian2/tests/test_base.py`
- `brian2/tests/test_network.py`
- `brian2/tests/test_synapses.py`
- `brian2/tests/test_stateupdaters.py`
- `brian2/tests/test_cpp_standalone.py`
- `brian2/tests/test_templates/test_templates.py`
- `brian2/tests/features/base.py`
- `brian2/codegen/templates.py`
- `brian2/devices/cpp_standalone/device.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" brian2/tests brian2`).
