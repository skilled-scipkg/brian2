---
name: brian2-simulation-workflows
description: This skill should be used when users ask about simulation workflows in brian2; it prioritizes documentation references and then source inspection only for unresolved details.
---

# brian2: Simulation Workflows

## High-Signal Playbook
### Route conditions
- Use this skill for runtime vs standalone execution choices, run/restart patterns, scheduling, profiling, and reproducibility.
- Route model-equation/synapse formulation details to `brian2-inputs-and-modeling`.
- Route API object-construction issues to `brian2-api-and-scripting`.
- Route compiler/install blockers to `brian2-build-and-install`.

### Triage questions
- Single run, multi-phase run, or repeated full simulations?
- Runtime target (`numpy`/`cython`) or `cpp_standalone`?
- Need multiprocessing or batch sweeps?
- Are stochastic components present (seed/reproducibility requirements)?
- Do you need full traces or summary metrics (memory constraints)?
- Are there mixed-object magic run errors or scheduling/time-step concerns?

### Canonical workflow
- Start in runtime mode unless standalone-only constraints dominate (`docs_sphinx/user/computation.rst`).
- For single standalone run, use `set_device('cpp_standalone')`; for multiple `run` calls use `build_on_run=False` then `device.build()`.
- Use explicit `Network` whenever objects are hidden in containers or when magic-run heuristics fail (`docs_sphinx/user/running.rst`).
- Use `store`/`restore` for repeated trials without rebuilding model state (`docs_sphinx/user/running.rst`).
- For repeated standalone full simulations, compile once then call `device.run(...)`, varying equation parameters via `run_args` (`docs_sphinx/user/computation.rst`).
- For parallel standalone runs, provide unique `results_directory` and set active device in worker process context (`docs_sphinx/user/computation.rst`, `examples/multiprocessing/02_using_standalone.py`).
- Use profiling and scheduling summaries to identify bottlenecks and ordering issues (`docs_sphinx/user/running.rst`).

### Minimal working example
```python
from brian2 import *
import numpy as np

set_device('cpp_standalone', build_on_run=False)
seed(111)

group = NeuronGroup(10, '''
dv/dt = -v/tau : 1
tau : second (shared, constant)
''', method='exact')
group.v = 'rand()'

run(100*ms)
device.build(run=False)

for tau_value in (5, 10, 20)*ms:
    device.run(run_args={group.tau: tau_value})
```

### Pitfalls and fixes
- Mixing previously-run and new stateful objects with magic `run()` raises an error; use explicit `Network` (`docs_sphinx/user/running.rst`).
- Changing `dt` mid-simulation must preserve integer time-step compatibility (`docs_sphinx/user/running.rst`).
- Standalone mode cannot use Python `network_operation` and some array-based initialization idioms (`docs_sphinx/user/computation.rst`, `docs_sphinx/user/input.rst`).
- Accessing state variables before standalone build/run can raise `NotImplementedError` (`docs_sphinx/user/computation.rst`).
- Parallel standalone runs sharing one results directory conflict; set per-run `results_directory` (`docs_sphinx/user/computation.rst`).
- For reproducibility in Brian-generated randomness, use `seed(...)` (not only `numpy.random.seed`) (`docs_sphinx/advanced/random.rst`).
- `record=True` on large groups can exhaust memory; reduce indices or monitor dt (`docs_sphinx/user/recording.rst`).

### Convergence and validation checks
- Re-run with smaller `defaultclock.dt` and confirm stable observables.
- Compare runtime and standalone outputs on key metrics (rates/counts/statistics) rather than strict trace identity for stochastic models.
- Verify deterministic reruns with fixed `seed(...)` when expected.
- Use `profile=True` + `profiling_summary(...)` to confirm bottleneck shifts after optimization.
- Check scheduling (`when`, `order`, monitor timing) with `scheduling_summary(...)` for event-order-sensitive models.

## Scope
- Handle questions about simulation setup, execution flow, and runtime controls.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs_sphinx/user/running.rst`
- `docs_sphinx/user/recording.rst`
- `docs_sphinx/user/computation.rst`
- `docs_sphinx/advanced/random.rst`
- `docs_sphinx/advanced/namespaces.rst`
- `docs_sphinx/developer/standalone.rst`
- `examples/standalone/simple_case.py`
- `examples/standalone/simple_case_build.py`
- `examples/standalone/standalone_multiplerun.py`
- `examples/multiprocessing/02_using_standalone.py`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples/standalone`
- `examples/multiprocessing`
- `tutorials/3-intro-to-brian-simulations.ipynb`

## Test references
- `brian2/tests`
- `dev/tools/tests`

## Optional deeper inspection
- `brian2`

## Source entry points for unresolved issues
- `brian2/core/network.py`
- `brian2/core/magic.py`
- `brian2/core/clocks.py`
- `brian2/codegen/runtime/numpy_rt/numpy_rt.py`
- `brian2/codegen/runtime/cython_rt/cython_rt.py`
- `brian2/codegen/runtime/cython_rt/extension_manager.py`
- `brian2/codegen/runtime/GSLcython_rt/GSLcython_rt.py`
- `brian2/devices/device.py`
- `brian2/devices/cpp_standalone/device.py`
- `brian2/devices/cpp_standalone/templates/main.cpp`
- `brian2/devices/cpp_standalone/templates/run.cpp`
- `brian2/tests/test_network.py`
- `brian2/tests/test_cpp_standalone.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" brian2`).
