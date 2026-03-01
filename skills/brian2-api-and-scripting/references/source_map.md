# brian2 source map: API and Scripting

Generated from source roots:
- `brian2`
- `brian2/tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" brian2`
- `rg -n "class|def" brian2/groups brian2/synapses brian2/monitors brian2/core brian2/equations`

## Function-level entry points (open in this order)
- `brian2/groups/neurongroup.py` | group construction, threshold/reset/refractory API surface.
- `brian2/synapses/synapses.py` | synapse model API, event pathways, and connect semantics.
- `brian2/monitors/statemonitor.py` | continuous variable recording API.
- `brian2/monitors/spikemonitor.py` | spike stream and count accessors.
- `brian2/monitors/ratemonitor.py` | firing-rate monitor API and summary behavior.
- `brian2/core/network.py` | explicit `Network` lifecycle control.
- `brian2/core/magic.py` | implicit run behavior and object discovery.
- `brian2/equations/equations.py` | equation-language parsing entry points.
- `brian2/equations/unitcheck.py` | unit-compatibility checks for equation definitions.
- `brian2/parsing/functions.py` | support for callable functions in equations.
- `brian2/core/functions.py` | function registration and codegen-facing wrappers.
- `brian2/input/spikegeneratorgroup.py` | scripted spike-input API behavior.

## Behavior checks
- `brian2/tests/test_neurongroup.py` | API behavior for model equations and state updates.
- `brian2/tests/test_synapses.py` | event-driven and clock-driven synapse behavior.
- `brian2/tests/test_monitor.py` | monitor API output and shape expectations.
- `brian2/tests/test_namespaces.py` | explicit and implicit namespace resolution.
- `brian2/tests/test_functions.py` | custom/default function registration and execution.
