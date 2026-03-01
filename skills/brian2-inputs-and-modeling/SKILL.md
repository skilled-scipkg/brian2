---
name: brian2-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in brian2; it prioritizes documentation references and then source inspection only for unresolved details.
---

# brian2: Inputs and Modeling

## High-Signal Playbook
### Route conditions
- Use this skill for equation design, units/parameters, input stimuli, synaptic modeling, and model-validation strategy.
- Route pure scripting/lifecycle mechanics to `brian2-api-and-scripting`.
- Route runtime vs standalone execution/performance to `brian2-simulation-workflows`.
- Route install/toolchain issues to `brian2-build-and-install`.

### Triage questions
- Point-neuron or multicompartment model?
- Deterministic ODE, stochastic equations (`xi`), or hybrid?
- Input type: `PoissonGroup`, `PoissonInput`, `SpikeGeneratorGroup`, `TimedArray`, or explicit equations?
- Synapse style: static weights, plasticity, event-driven traces, delays?
- Which observables define correctness (spike rate, Vm trace, synaptic state, timing)?
- Are units or invalid-connection errors already appearing?

### Canonical workflow
- Define equations first, with base units and explicit parameters/subexpressions (`docs_sphinx/user/equations.rst`, `docs_sphinx/user/models.rst`).
- Resolve external constants through group/run namespaces or make them equation parameters (`docs_sphinx/advanced/namespaces.rst`).
- Choose input mechanism based on structure and scale (`docs_sphinx/user/input.rst`).
- Build synapses and explicitly call `connect`, then set weights/delays after connections exist (`docs_sphinx/user/synapses.rst`).
- Choose event-driven vs clock-driven synaptic updates based on equation structure and monitoring needs (`docs_sphinx/user/synapses.rst`).
- Add monitors and run, then compare with expected qualitative/quantitative behavior.

### Minimal working example
```python
from brian2 import *
start_scope()

tau = 10*ms
P = PoissonGroup(100, rates=15*Hz)
G = NeuronGroup(1,
                'dv/dt = -v/tau : 1',
                threshold='v > 1',
                reset='v = 0',
                method='exact')

S = Synapses(P, G, 'w : 1', on_pre='v_post += w')
S.connect()
S.w = '0.02 + 0.01*rand()'

spike_mon = SpikeMonitor(G)
run(1*second)
print(spike_mon.num_spikes)
```

### Pitfalls and fixes
- Unit declarations in equations must use base units (e.g. `volt`, not `mV`) (`docs_sphinx/user/equations.rst`).
- `Synapses(...)` does not create connections; call `connect(...)` explicitly (`docs_sphinx/user/synapses.rst`).
- Automatic event-driven updates only support independent 1D linear equations (`docs_sphinx/user/synapses.rst`, `docs_sphinx/user/equations.rst`).
- `PoissonGroup` is unsuitable for very high per-neuron rates where >1 spike per dt is likely; split input across more units (`docs_sphinx/user/input.rst`).
- Generator-based `connect` can create invalid indices; use `skip_if_invalid=True` if intentional (`docs_sphinx/user/synapses.rst`).
- Multiple plain `xi` noise terms are invalid; suffix noise symbols (`docs_sphinx/user/equations.rst`).
- Python `network_operation` logic does not work in standalone mode (`docs_sphinx/user/input.rst`, `docs_sphinx/user/computation.rst`).

### Convergence and validation checks
- Halve `dt` and check stability of spikes/traces/rates.
- For stochastic models, validate distributions (mean/variance/rate) instead of exact trajectories.
- Validate synaptic structure counts (`len(S)`, incoming/outgoing patterns) before long runs.
- If using normalized weights (`N_incoming`), check post-neuron totals explicitly.
- Compare simple leak/input cases against known analytical trend or tutorial reference behavior.

## Scope
- Handle questions about inputs, system setup, models, and physical parameterization.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs_sphinx/user/models.rst`
- `docs_sphinx/user/equations.rst`
- `docs_sphinx/user/units.rst`
- `docs_sphinx/user/input.rst`
- `docs_sphinx/user/synapses.rst`
- `docs_sphinx/user/refractoriness.rst`
- `docs_sphinx/user/multicompartmental.rst`
- `docs_sphinx/advanced/random.rst`
- `examples/synapses/synapses.py`
- `examples/synapses/STDP.py`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `tutorials/2-intro-to-brian-synapses.ipynb`
- `examples/synapses`

## Test references
- `brian2/tests`
- `dev/tools/tests`

## Optional deeper inspection
- `brian2`

## Source entry points for unresolved issues
- `brian2/equations/equations.py`
- `brian2/equations/unitcheck.py`
- `brian2/equations/refractory.py`
- `brian2/input/poissongroup.py`
- `brian2/input/poissoninput.py`
- `brian2/input/spikegeneratorgroup.py`
- `brian2/input/timedarray.py`
- `brian2/synapses/synapses.py`
- `brian2/synapses/spikequeue.py`
- `brian2/codegen/translation.py`
- `brian2/codegen/runtime/cython_rt/templates/synapses.pyx`
- `brian2/tests/test_synapses.py`
- `brian2/tests/test_poissongroup.py`
- `brian2/tests/test_poissoninput.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" brian2`).
