# brian2 source map: Build and Install

Generated from source roots:
- `brian2`
- `brian2/tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" brian2/devices brian2/codegen brian2/parsing`
- `rg -n "build|compile|device|standalone|openmp|extension" brian2`

## Function-level entry points (open in this order)
- `brian2/devices/device.py` | device abstraction and active-device configuration.
- `brian2/devices/cpp_standalone/device.py` | standalone build/run pipeline orchestration.
- `brian2/devices/cpp_standalone/codeobject.py` | generated standalone code-object lifecycle.
- `brian2/devices/cpp_standalone/GSLcodeobject.py` | GSL-specific standalone code-object behavior.
- `brian2/devices/cpp_standalone/templates/main.cpp` | generated executable entry point.
- `brian2/devices/cpp_standalone/templates/run.cpp` | simulation run loop in standalone target.
- `brian2/devices/cpp_standalone/templates/makefile` | compiler/link flags and OpenMP build controls.
- `brian2/codegen/runtime/cython_rt/extension_manager.py` | Cython extension compile/cache management.
- `brian2/codegen/runtime/cython_rt/cython_rt.py` | Cython runtime target setup.
- `brian2/codegen/runtime/numpy_rt/numpy_rt.py` | pure-numpy runtime fallback behavior.
- `brian2/codegen/runtime/GSLcython_rt/GSLcython_rt.py` | GSL-enhanced runtime target behavior.
- `brian2/parsing/dependencies.py` | parsing-time dependency tracking for generated code.

## Behavior checks
- `brian2/tests/test_codegen.py` | code generation correctness across targets.
- `brian2/tests/test_cpp_standalone.py` | standalone compile/build/run behavior.
- `brian2/tests/test_devices.py` | device selection and device lifecycle semantics.
- `brian2/tests/test_GSL.py` | GSL-specific runtime/build behavior.
