# brian2 source map: Tests

Generated from source roots:
- `brian2`
- `brian2/tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" brian2/tests brian2/codegen brian2/devices brian2/core`
- `rg -n "pytest|standalone_compatible|codegen_independent|multiple_runs" brian2/tests`

## Function-level entry points (open in this order)
- `brian2/tests/utils.py` | shared decorators/helpers for backend-aware tests.
- `brian2/tests/test_base.py` | foundational invariants and shared behavior checks.
- `brian2/tests/test_network.py` | run lifecycle and multi-run behavior checks.
- `brian2/tests/test_synapses.py` | synapse behavior regression surface.
- `brian2/tests/test_stateupdaters.py` | integrator behavior regression surface.
- `brian2/tests/test_cpp_standalone.py` | standalone backend behavior checks.
- `brian2/tests/test_templates/test_templates.py` | template resolution and override behavior.
- `brian2/tests/features/base.py` | feature-test scaffolding for integration-level checks.
- `brian2/codegen/templates.py` | template loading path exercised by template tests.
- `brian2/devices/cpp_standalone/device.py` | standalone behaviors exercised by backend tests.

## Behavior checks
- `brian2/tests/test_neurongroup.py` | core model behavior sanity check.
- `brian2/tests/test_monitor.py` | monitor behavior sanity check.
- `brian2/tests/test_devices.py` | device selection and lifecycle checks.
- `brian2/tests/test_codegen.py` | code generation regression checks.
- `brian2/tests/test_preferences.py` | preference and configuration behavior checks.
