---
name: brian2-build-and-install
description: This skill should be used when users ask about build and install in brian2; it prioritizes documentation references and then source inspection only for unresolved details.
---

# brian2: Build and Install

## High-Signal Playbook
### Route conditions
- Use this skill for environment setup, installation failures, compile errors, runtime target setup, and standalone build troubleshooting.
- Route first modeling/API questions to `brian2-getting-started` or `brian2-api-and-scripting`.
- Route run orchestration/restart/performance questions to `brian2-simulation-workflows`.

### Triage questions
- Which OS, Python version, and architecture are in use?
- Is the user installing from PyPI, local source, or editable mode?
- Is failure at import time, Cython compile time, or standalone C++ compile time?
- Is the target runtime `numpy`, `cython`, or `cpp_standalone`?
- Is OpenMP/GSL required?

### Canonical workflow
- Confirm Python and pip baseline.
- Install/upgrade Brian2 in isolated environment.
- Validate import/version.
- Run a minimal runtime simulation.
- Run a minimal standalone build.

```bash
python -V
python -m pip install -U pip setuptools wheel
python -m pip install -e .
python - <<'PY'
from brian2 import *
start_scope()
G = NeuronGroup(1, 'dv/dt = -v/(10*ms) : 1', method='exact')
run(1*ms)
print('runtime_ok')
PY
python - <<'PY'
from brian2 import *
set_device('cpp_standalone', build_on_run=False)
start_scope()
G = NeuronGroup(1, 'dv/dt = -v/(10*ms) : 1', method='exact')
run(1*ms)
device.build(directory='build_brian2_smoketest', compile=True, run=True)
print('standalone_ok')
PY
```

### Validation checkpoints
- `import brian2` succeeds and reports expected version.
- Minimal runtime script exits cleanly.
- Standalone build creates a build directory and runs without compile/link errors.
- If OpenMP is requested, compile output includes OpenMP flags and run completes.

## Scope
- Handle questions about build, installation, compilation, and environment setup.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs_sphinx/introduction/install.rst`
- `docs_sphinx/introduction/scripts.rst`
- `docs_sphinx/user/computation.rst`
- `docs_sphinx/developer/devices.rst`
- `docs_sphinx/developer/standalone.rst`
- `docs_sphinx/developer/openmp.rst`
- `docs_sphinx/advanced/functions.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the listed function-level entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples/standalone`
- `examples/multiprocessing`

## Test references
- `brian2/tests`
- `dev/tools/tests`

## Optional deeper inspection
- `brian2`

## Source entry points for unresolved issues
- `brian2/devices/device.py`
- `brian2/devices/cpp_standalone/device.py`
- `brian2/devices/cpp_standalone/codeobject.py`
- `brian2/devices/cpp_standalone/templates/main.cpp`
- `brian2/devices/cpp_standalone/templates/run.cpp`
- `brian2/devices/cpp_standalone/templates/makefile`
- `brian2/codegen/runtime/cython_rt/extension_manager.py`
- `brian2/codegen/runtime/cython_rt/cython_rt.py`
- `brian2/codegen/runtime/numpy_rt/numpy_rt.py`
- `brian2/parsing/dependencies.py`
- `brian2/tests/test_codegen.py`
- `brian2/tests/test_cpp_standalone.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" brian2`).
