---
name: brian2-api-and-scripting
description: This skill should be used when users ask about api and scripting in brian2; it prioritizes documentation references and then source inspection only for unresolved details.
---

# brian2: API and Scripting

## High-Signal Playbook
### Route conditions
- Use this skill for defining neuron/synapse models in code, simulation object lifecycle, and monitor/output usage.
- Route run-mode/performance/multiprocessing questions to `brian2-simulation-workflows`.
- Route input modeling design (Poisson, timed inputs, multicompartment details) to `brian2-inputs-and-modeling`.
- Route install/compiler/toolchain issues to `brian2-build-and-install`.
- Route contributor internals and test architecture to `brian2-developer-guide`.

### Triage questions
- Which objects are needed (`NeuronGroup`, `Synapses`, `SpikeMonitor`, `StateMonitor`, `Network`)?
- Are external constants/functions used in equations (namespace requirements)?
- Single run or multi-phase run (`store`/`restore`)?
- Required integration method and time step?
- Are unit or unresolved-identifier errors already present?
- Is output expected as spike times/counts, traces, rates, or all of them?

### Canonical workflow
- Write equations with explicit units/flags and valid syntax (`docs_sphinx/user/equations.rst`, `docs_sphinx/user/units.rst`).
- Instantiate `NeuronGroup` with explicit `method`, plus threshold/reset/refractory if needed (`docs_sphinx/user/models.rst`).
- Define synaptic dynamics (`model`, `on_pre`/`on_post`) and call `connect(...)` (`docs_sphinx/user/synapses.rst`).
- Initialize state/synaptic variables (values or string expressions) after object creation/connection.
- Attach monitors with deliberate recording scope (`record=True` vs selected indices) (`docs_sphinx/user/recording.rst`).
- Use explicit `Network` when objects are hidden in containers or when controlling run composition (`docs_sphinx/user/running.rst`).
- For trial loops, use `store`/`restore`; for external constants, pass explicit namespaces (`docs_sphinx/user/running.rst`, `docs_sphinx/advanced/namespaces.rst`).

### Minimal working example
```python
from brian2 import *
start_scope()

tau = 10*ms
eqs = '''
dv/dt = (I - v)/tau : 1
I : 1
'''
G = NeuronGroup(2, eqs, threshold='v > 1', reset='v = 0', method='exact')
G.I = [1.2, 0.8]

S = Synapses(G, G, 'w : 1', on_pre='v_post += w')
S.connect(i=0, j=1)
S.w = 0.2

state_mon = StateMonitor(G, 'v', record=True)
spike_mon = SpikeMonitor(G)

store('init')
run(50*ms)
restore('init')
run(50*ms)

print(spike_mon.count[:], state_mon.v[:, -1])
```

### Pitfalls and fixes
- Equation unit declarations must use base dimensions (`volt`, not `mV` in declaration) (`docs_sphinx/user/equations.rst`).
- Unresolved external names require explicit group/run namespaces (`docs_sphinx/advanced/namespaces.rst`).
- `Synapses` without `connect` creates zero synapses (`docs_sphinx/user/synapses.rst`).
- `StateMonitor` indexing confusion: `M.v[k]` is relative to recorded indices, `M[i].v` uses absolute group index (`docs_sphinx/user/recording.rst`).
- Magic `run()` skips objects hidden in containers; use explicit `Network` and `add` (`docs_sphinx/user/running.rst`).
- Using unsuffixed multiple `xi` noise symbols is invalid (`docs_sphinx/user/equations.rst`).

### Convergence and validation checks
- Run with smaller `dt` and compare key observables (spike count, trace shape) (`docs_sphinx/user/running.rst`).
- Compare behavior across explicit methods (`exact`, `euler`, `exponential_euler`) where relevant (`docs_sphinx/advanced/state_update.rst`).
- For stochastic scripts, set `seed(...)` and validate distribution-level metrics (`docs_sphinx/advanced/random.rst`).
- Verify monitor timings and dimensions (`docs_sphinx/user/recording.rst`).
- Add a targeted regression test when changing reusable scripting patterns.

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs_sphinx/user/models.rst`
- `docs_sphinx/user/equations.rst`
- `docs_sphinx/user/synapses.rst`
- `docs_sphinx/user/running.rst`
- `docs_sphinx/user/recording.rst`
- `docs_sphinx/advanced/namespaces.rst`
- `docs_sphinx/user/import.rst`
- `docs_sphinx/user/units.rst`
- `docs_sphinx/user/plotting_functions.rst`
- `docs_sphinx/advanced/interface.rst`
- `docs_sphinx/developer/functions.rst`

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
- `brian2/groups/neurongroup.py`
- `brian2/synapses/synapses.py`
- `brian2/monitors/statemonitor.py`
- `brian2/monitors/spikemonitor.py`
- `brian2/monitors/ratemonitor.py`
- `brian2/core/network.py`
- `brian2/core/magic.py`
- `brian2/equations/equations.py`
- `brian2/equations/unitcheck.py`
- `brian2/parsing/functions.py`
- `brian2/core/functions.py`
- `brian2/input/spikegeneratorgroup.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" brian2`).
