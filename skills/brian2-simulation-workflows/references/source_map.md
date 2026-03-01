# brian2 source map: Simulation Workflows

Generated from source roots:
- `brian2`
- `brian2/tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" brian2/core brian2/devices brian2/codegen/runtime`
- `rg -n "run|store|restore|clock|standalone|build_on_run|results_directory" brian2`

## Function-level entry points (open in this order)
- `brian2/core/network.py` | simulation orchestration, run semantics, and network scheduling.
- `brian2/core/magic.py` | implicit-network heuristics and mixed-object failure modes.
- `brian2/core/clocks.py` | simulation timestep and clock coordination behavior.
- `brian2/codegen/runtime/numpy_rt/numpy_rt.py` | numpy runtime execution pipeline.
- `brian2/codegen/runtime/cython_rt/cython_rt.py` | cython runtime setup and execution.
- `brian2/codegen/runtime/cython_rt/extension_manager.py` | extension cache/rebuild behavior.
- `brian2/codegen/runtime/GSLcython_rt/GSLcython_rt.py` | GSL-backed runtime behavior.
- `brian2/devices/device.py` | cross-device run/build interface.
- `brian2/devices/cpp_standalone/device.py` | standalone run/build flow and run-arg handling.
- `brian2/devices/cpp_standalone/templates/run.cpp` | standalone simulation loop behavior.
- `brian2/devices/cpp_standalone/templates/main.cpp` | standalone execution entry point.

## Behavior checks
- `brian2/tests/test_network.py` | run/store/restore and scheduling behavior.
- `brian2/tests/test_cpp_standalone.py` | standalone build and multi-run behavior.
- `brian2/tests/test_clocks.py` | clock/dt behavior checks.
- `brian2/tests/test_monitor.py` | monitoring behavior under different run workflows.
- `brian2/tests/test_devices.py` | device switching and lifecycle behavior.
