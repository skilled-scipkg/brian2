# brian2 source map: Docs Sphinx

Generated from source roots:
- `brian2`
- `brian2/tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" brian2/units brian2/stateupdaters brian2/core brian2/sphinxext`
- `rg -n "units|preferences|logging|stateupdate|namespace" brian2`

## Function-level entry points (open in this order)
- `brian2/units/fundamentalunits.py` | core unit system and dimensional arithmetic.
- `brian2/units/stdunits.py` | named standard-unit declarations.
- `brian2/units/unitsafefunctions.py` | unit-safe wrappers for numeric/math functions.
- `brian2/core/preferences.py` | preference API and persistence behavior.
- `brian2/core/core_preferences.py` | default preference sets used in docs examples.
- `brian2/utils/logger.py` | logging behavior documented in advanced logging docs.
- `brian2/stateupdaters/base.py` | state updater selection framework.
- `brian2/stateupdaters/exact.py` | exact integrator behavior.
- `brian2/stateupdaters/explicit.py` | explicit integrator family behavior.
- `brian2/stateupdaters/exponential_euler.py` | exponential Euler specifics.
- `brian2/sphinxext/docscrape_sphinx.py` | docstring-to-sphinx transformation behavior.

## Behavior checks
- `brian2/tests/test_units.py` | unit behavior mapped to user-unit docs.
- `brian2/tests/test_preferences.py` | preference behavior mapped to advanced docs.
- `brian2/tests/test_logger.py` | logging behavior mapped to advanced logging docs.
- `brian2/tests/test_stateupdaters.py` | state updater behavior mapped to state-update docs.
- `brian2/tests/test_namespaces.py` | namespace resolution behavior from docs examples.
