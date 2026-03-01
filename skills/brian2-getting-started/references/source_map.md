# brian2 source map: Getting Started

Generated from source roots:
- `brian2`
- `brian2/tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" brian2`
- `rg -n "class|def" brian2/groups brian2/synapses brian2/monitors brian2/core`

## Function-level entry points (open in this order)
- `brian2/groups/neurongroup.py` | `NeuronGroup` model creation, threshold/reset handling, and state variable setup.
- `brian2/synapses/synapses.py` | `Synapses` creation, `connect(...)`, delays, and synaptic variable behavior.
- `brian2/monitors/statemonitor.py` | state trace recording semantics and indexing behavior.
- `brian2/monitors/spikemonitor.py` | spike event capture and count/timing interfaces.
- `brian2/monitors/ratemonitor.py` | population-rate recording behavior and output units.
- `brian2/core/network.py` | explicit network construction, run orchestration, and object scheduling.
- `brian2/core/magic.py` | magic network heuristics and mixed-object run errors.
- `brian2/core/clocks.py` | `defaultclock.dt` and simulation time-step control.
- `brian2/equations/equations.py` | equation parsing rules and supported syntax.
- `brian2/equations/unitcheck.py` | dimension checking and `DimensionMismatchError` paths.
- `brian2/input/poissongroup.py` | Poisson spike generation entry point for first input models.

## Behavior checks
- `brian2/tests/test_neurongroup.py` | neuron equations, thresholds, reset semantics.
- `brian2/tests/test_synapses.py` | connection patterns, delays, and event behavior.
- `brian2/tests/test_monitor.py` | monitor output correctness and indexing semantics.
- `brian2/tests/test_network.py` | run lifecycle, store/restore, and network composition.
- `brian2/tests/test_units.py` | unit safety and conversion behavior.
