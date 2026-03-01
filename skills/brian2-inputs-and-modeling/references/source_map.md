# brian2 source map: Inputs and Modeling

Generated from source roots:
- `brian2`
- `brian2/tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" brian2/equations brian2/input brian2/synapses brian2/codegen`
- `rg -n "Poisson|TimedArray|SpikeGenerator|refractory|synapses|unit" brian2`

## Function-level entry points (open in this order)
- `brian2/equations/equations.py` | equation parsing and variable definitions.
- `brian2/equations/unitcheck.py` | unit constraints for model equations.
- `brian2/equations/refractory.py` | refractory modeling mechanics.
- `brian2/input/poissongroup.py` | stochastic spike-input process behavior.
- `brian2/input/poissoninput.py` | dense Poisson current injection behavior.
- `brian2/input/spikegeneratorgroup.py` | explicit spike-train input behavior.
- `brian2/input/timedarray.py` | time-dependent stimulus lookup behavior.
- `brian2/synapses/synapses.py` | synaptic dynamics and event hooks.
- `brian2/synapses/spikequeue.py` | delayed spike delivery internals.
- `brian2/codegen/translation.py` | abstract-code generation for equations/synapses.
- `brian2/stateupdaters/explicit.py` | explicit methods used in many input/model workflows.

## Behavior checks
- `brian2/tests/test_synapses.py` | synaptic connectivity and dynamics checks.
- `brian2/tests/test_poissongroup.py` | Poisson-group stochastic input behavior.
- `brian2/tests/test_poissoninput.py` | Poisson-input current injection behavior.
- `brian2/tests/test_spikegenerator.py` | explicit spike schedule input behavior.
- `brian2/tests/test_timedarray.py` | time-indexed stimulus behavior.
- `brian2/tests/test_refractory.py` | refractory model behavior.
