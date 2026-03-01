---
name: brian2-developer-guide
description: This skill should be used when users ask about developer guide in brian2; it prioritizes documentation references and then source inspection only for unresolved details.
---

# brian2: Developer Guide

## High-Signal Playbook
### Route conditions
- Use this skill for core architecture, extension points, contribution workflow, and test strategy.
- Route user-facing scripting/modeling questions to `brian2-api-and-scripting` or `brian2-inputs-and-modeling`.
- Route runtime/standalone execution decisions to `brian2-simulation-workflows`.
- Route install/toolchain blockers to `brian2-build-and-install`.

### Triage questions
- Is this a bug fix, a new feature, or an extension package integration?
- Which subsystem is affected (equations, codegen/device, synapses, units/preferences, logging)?
- Which targets must stay correct (`numpy`, `cython`, `cpp_standalone`)?
- Is there a minimal reproduction and expected behavior?
- Do we need warning/error semantics or preference validation changes?

### Canonical workflow
- Read developer docs for the affected subsystem (`docs_sphinx/developer/index.rst`, `.../guidelines/index.rst`, `.../equations_namespaces.rst`, `.../standalone.rst`).
- Reproduce with the smallest runnable script/test.
- Map to concrete implementation files (equation parsing/unitcheck, runtime/standalone device, templates).
- Add or adjust tests with appropriate markers (`codegen_independent`, `standalone_compatible`, `multiple_runs`) (`docs_sphinx/developer/guidelines/testing.rst`).
- Ensure warnings follow logging guidance (actionable text, typically `once=True`) (`docs_sphinx/developer/guidelines/logging.rst`).
- Validate across relevant targets with `brian2.test(...)` before finalizing.

### Minimal working example
```python
import numpy as np
import pytest
from numpy.testing import assert_equal
from brian2 import *

@pytest.mark.standalone_compatible
def test_simple_run_parameter_stability():
    group = NeuronGroup(5, 'v : volt')
    group.v = 'i*mV'
    run(1*ms)
    assert_equal(group.v[:], np.arange(5)*mV)
```

### Pitfalls and fixes
- Tests that depend on uncontrolled randomness are flaky; seed or remove stochastic dependence (`docs_sphinx/developer/guidelines/testing.rst`).
- Standalone tests with multiple `run` calls need explicit `device.build(...)` (`docs_sphinx/developer/guidelines/testing.rst`).
- Preference typos/invalid values fail validation; register and validate preference domains correctly (`docs_sphinx/developer/preferences.rst`).
- Warning messages should explain the fix path and be test-covered via `catch_logs` (`docs_sphinx/developer/guidelines/logging.rst`).
- Magic network heuristics can fail with mixed old/new objects; use explicit `Network` in tests or examples (`docs_sphinx/user/running.rst`).
- Standalone variable access assumptions before build/run can fail; respect array-cache constraints (`docs_sphinx/developer/standalone.rst`).

### Convergence and validation checks
- Run relevant tests for each impacted target (`numpy`, `cython`, standalone).
- Check that behavior-level assertions survive codegen-target changes.
- For stochastic changes, compare statistics rather than exact traces.
- Verify warning/error text and category in tests.
- For standalone-related changes, inspect generated template behavior where needed (`main.cpp`, `run.cpp`, stateupdate/synapses templates).

## Scope
- Handle questions about developer architecture, extension points, and contribution workflow.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs_sphinx/developer/index.rst`
- `docs_sphinx/developer/guidelines/index.rst`
- `docs_sphinx/developer/equations_namespaces.rst`
- `docs_sphinx/developer/standalone.rst`
- `docs_sphinx/developer/guidelines/testing.rst`
- `docs_sphinx/developer/guidelines/logging.rst`
- `docs_sphinx/developer/guidelines/defensive_programming.rst`
- `docs_sphinx/developer/preferences.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples`
- `tutorials`

## Test references
- `brian2/tests`
- `dev/tools/tests`

## Optional deeper inspection
- `brian2`

## Source entry points for unresolved issues
- `brian2/equations/equations.py`
- `brian2/equations/unitcheck.py`
- `brian2/equations/codestrings.py`
- `brian2/devices/device.py`
- `brian2/devices/cpp_standalone/device.py`
- `brian2/devices/cpp_standalone/codeobject.py`
- `brian2/devices/cpp_standalone/templates/main.cpp`
- `brian2/devices/cpp_standalone/templates/run.cpp`
- `brian2/devices/cpp_standalone/templates/stateupdate.cpp`
- `brian2/devices/cpp_standalone/templates/synapses.cpp`
- `brian2/tests/test_equations.py`
- `brian2/tests/test_cpp_standalone.py`
- `brian2/tests/test_stateupdaters.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" brian2`).
