# brian2 source map: Examples and Tutorials

Generated from source roots:
- `brian2`
- `brian2/tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" examples tutorials brian2/sphinxext`
- `rg -n "example|tutorial|standalone|synapses|monitor" brian2`

## Function-level entry points (open in this order)
- `brian2/sphinxext/generate_examples.py` | example indexing and docs-facing discovery flow.
- `brian2/sphinxext/examplefinder.py` | matching examples to API/doc references.
- `brian2/core/network.py` | run scheduling semantics shared by most examples.
- `brian2/groups/neurongroup.py` | neuron model behavior used in introductory tutorials.
- `brian2/synapses/synapses.py` | synapse behavior used in tutorial/example scripts.
- `brian2/monitors/statemonitor.py` | trace recording behavior in plotting examples.
- `brian2/monitors/spikemonitor.py` | spike recording behavior in many tutorial scripts.
- `brian2/devices/cpp_standalone/device.py` | standalone example build/run behavior.

## Behavior checks
- `brian2/tests/test_complex_examples.py` | broad execution coverage for representative example flows.
- `brian2/tests/test_network.py` | network-run semantics reflected in tutorials.
- `brian2/tests/test_synapses.py` | synapse behavior exercised in example scripts.
- `brian2/tests/test_monitor.py` | monitor behavior reflected in plotting/analysis examples.
- `brian2/tests/test_cpp_standalone.py` | standalone example backend checks.
