---
name: brian2-getting-started
description: This skill should be used when users ask about getting started in brian2; it prioritizes documentation references and then source inspection only for unresolved details.
---

# brian2: Getting Started

## High-Signal Playbook
### Route conditions
- Use this skill for first runnable Brian2 scripts/notebooks, core object concepts, and "what should I run first" requests.
- Route install/compiler/environment blockers to `brian2-build-and-install`.
- Route detailed API behavior and scripting patterns to `brian2-api-and-scripting`.
- Route runtime vs standalone/performance workflows to `brian2-simulation-workflows`.
- Route deeper model/input design to `brian2-inputs-and-modeling`.

### Triage questions
- Which environment are you using (script, notebook, IDE) and which Python version?
- Do you need a minimal run, or a run including synapses and monitors?
- Are units/namespace/import errors already appearing?
- Do you need deterministic reruns now (seed/store/restore), or just a first run?
- Do you intend to stay in runtime mode first, or move directly to standalone?

### Canonical workflow
- Confirm prerequisites and install path (`python -m pip install brian2`, Python >=3.12, 64-bit): `docs_sphinx/introduction/install.rst`.
- Start from a tiny `NeuronGroup` model with explicit `method` and units-aware equations: `docs_sphinx/user/models.rst`, `docs_sphinx/user/equations.rst`.
- Add spike generation (`threshold`, `reset`, optional `refractory`): `docs_sphinx/user/models.rst`, `docs_sphinx/user/refractoriness.rst`.
- Add a simple `Synapses` path and explicitly call `connect`: `docs_sphinx/user/synapses.rst`.
- Attach `StateMonitor`/`SpikeMonitor`, then `run(...)`: `docs_sphinx/user/recording.rst`, `docs_sphinx/user/running.rst`.
- If in notebook iterative work, use `start_scope()` between independent runs: `tutorials/1-intro-to-brian-neurons.ipynb`.

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

S = Synapses(G, G, on_pre='v_post += 0.2')
S.connect(i=0, j=1)

state_mon = StateMonitor(G, 'v', record=True)
spike_mon = SpikeMonitor(G)
run(100*ms)

print(spike_mon.count[:], state_mon.v[:, -1])
```

### Pitfalls and fixes
- Unitless time/voltage values raise `DimensionMismatchError`; always include units in arguments and equations (`docs_sphinx/user/units.rst`, `docs_sphinx/user/equations.rst`).
- `from brian2 import *` shadows builtin `input`; re-import with `from builtins import input` or use `from brian2.only import *` (`docs_sphinx/user/import.rst`).
- `Synapses(...)` only defines dynamics; no edges exist until `connect(...)` (`docs_sphinx/user/synapses.rst`).
- Multiple unsuffixed `xi` symbols in one system are invalid; use `xi_1`, `xi_2`, ... (`docs_sphinx/user/equations.rst`).
- Magic `run()` misses objects hidden in containers; use explicit `Network(...).add(...)` (`docs_sphinx/user/running.rst`).
- Dependency import errors usually mean environment mismatch; resolve via package manager upgrades (`docs_sphinx/user/import.rst`, `docs_sphinx/introduction/install.rst`).

### Convergence and validation checks
- Halve `defaultclock.dt` and compare spike counts/trace shape (`docs_sphinx/user/running.rst`).
- Prefer explicit integration method (`exact`, `euler`, etc.) for reproducibility of behavior (`docs_sphinx/advanced/state_update.rst`).
- Verify monitor semantics: `StateMonitor` records at beginning of time step by default (`docs_sphinx/user/recording.rst`).
- For deterministic scripts, rerun with same setup and compare outputs exactly; for stochastic scripts, set `seed(...)` and compare statistics (`docs_sphinx/advanced/random.rst`).

## Scope
- Handle questions about initial setup, quickstarts, and core concepts.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs_sphinx/introduction/index.rst`
- `docs_sphinx/introduction/install.rst`
- `docs_sphinx/introduction/scripts.rst`
- `docs_sphinx/user/models.rst`
- `docs_sphinx/user/synapses.rst`
- `docs_sphinx/user/running.rst`
- `docs_sphinx/user/recording.rst`
- `docs_sphinx/user/units.rst`
- `tutorials/1-intro-to-brian-neurons.ipynb`
- `tutorials/2-intro-to-brian-synapses.ipynb`
- `tutorials/3-intro-to-brian-simulations.ipynb`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `tutorials`
- `examples`

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
- `brian2/core/clocks.py`
- `brian2/core/core_preferences.py`
- `brian2/input/poissongroup.py`
- `brian2/input/spikegeneratorgroup.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" brian2`).
