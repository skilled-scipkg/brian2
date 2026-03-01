# brian2 source map: Theory and Methods

Generated from source roots:
- `brian2`
- `brian2/tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" brian2/stateupdaters brian2/equations brian2/codegen`
- `rg -n "stateupdate|exact|euler|refractory|unitcheck|stochastic|GSL" brian2`

## Function-level entry points (open in this order)
- `brian2/stateupdaters/base.py` | method registration/selection framework.
- `brian2/stateupdaters/exact.py` | exact integration method implementation.
- `brian2/stateupdaters/explicit.py` | explicit-method family implementation.
- `brian2/stateupdaters/exponential_euler.py` | exponential Euler implementation details.
- `brian2/stateupdaters/GSL.py` | GSL-backed method implementation.
- `brian2/equations/equations.py` | equation transformations used by integrators.
- `brian2/equations/unitcheck.py` | dimensional validity constraints on methods.
- `brian2/equations/refractory.py` | refractory formalism and update interaction.
- `brian2/codegen/translation.py` | abstract-code translation relevant to method execution.

## Behavior checks
- `brian2/tests/test_stateupdaters.py` | integrator accuracy/selection regressions.
- `brian2/tests/test_equations.py` | equation parsing and transformation checks.
- `brian2/tests/test_refractory.py` | refractory dynamics behavior checks.
- `brian2/tests/test_GSL.py` | GSL method behavior checks.
- `brian2/tests/test_units.py` | method/equation unit-consistency checks.
