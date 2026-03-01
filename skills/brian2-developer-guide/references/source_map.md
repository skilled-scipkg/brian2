# brian2 source map: Developer Guide

Generated from source roots:
- `brian2`
- `brian2/tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" brian2`
- `rg -n "class|def" brian2/equations brian2/codegen brian2/devices brian2/core`

## Function-level entry points (open in this order)
- `brian2/equations/equations.py` | equation object model and parsing pipeline.
- `brian2/equations/codestrings.py` | expression/string handling in equation internals.
- `brian2/equations/unitcheck.py` | invariant and defensive checks for units.
- `brian2/devices/device.py` | extension points for custom device behavior.
- `brian2/devices/cpp_standalone/device.py` | standalone backend architecture.
- `brian2/devices/cpp_standalone/codeobject.py` | standalone code object generation and execution.
- `brian2/codegen/templates.py` | templating hooks for runtime/standalone codegen.
- `brian2/codegen/translation.py` | abstract-code translation flow.
- `brian2/core/preferences.py` | preference registration/validation lifecycle.
- `brian2/core/core_preferences.py` | global defaults and preference scopes.
- `brian2/utils/logger.py` | logging policy and warning emission paths.

## Behavior checks
- `brian2/tests/test_equations.py` | equation parsing/validation regressions.
- `brian2/tests/test_stateupdaters.py` | updater selection and numerical behavior checks.
- `brian2/tests/test_cpp_standalone.py` | backend invariants across standalone workflows.
- `brian2/tests/test_preferences.py` | preference validation and error semantics.
- `brian2/tests/test_logger.py` | logging message behavior and filtering.
