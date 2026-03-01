---
name: brian2-docs-sphinx
description: This skill should be used when users ask about docs sphinx in brian2; it prioritizes documentation references and then source inspection only for unresolved details.
---

# brian2: Docs Sphinx

## High-Signal Playbook
### Route conditions
- Use this skill for documentation navigation and interpretation across user/advanced/developer docs.
- Route implementation scripting requests (defining groups/synapses/monitors) to `brian2-api-and-scripting`.
- Route execution-mode/performance choices to `brian2-simulation-workflows`.
- Route model/input architecture questions to `brian2-inputs-and-modeling`.
- Route contributor-level internals and testing strategy to `brian2-developer-guide`.

### Triage questions
- Is the user asking where behavior is documented, or asking for behavior itself?
- Which doc domain is relevant: import/units, equations/namespaces, state updaters, logging/preferences?
- Do they need user-level guidance or developer-level extension guidance?
- Are warnings/errors from logging/preferences/unit checks part of the request?
- Do they need a runnable sanity script tied to a specific doc section?

### Canonical workflow
- Start at `docs_sphinx/index.rst`, then route to user/advanced sections by question intent.
- For import and namespace ambiguity, prioritize `docs_sphinx/user/import.rst` and `docs_sphinx/advanced/namespaces.rst`.
- For units and equation constraints, prioritize `docs_sphinx/user/units.rst` and `docs_sphinx/user/equations.rst`.
- For integration-method choices, use `docs_sphinx/advanced/state_update.rst`.
- For preferences/logging behavior, use `docs_sphinx/advanced/preferences.rst` and `docs_sphinx/advanced/logging.rst`.
- Escalate to concrete implementation modules only if docs leave ambiguity.

### Minimal working example
```python
from brian2 import *
from brian2.utils.logger import BrianLogger

prefs.codegen.target = 'numpy'
tau = 10*ms
G = NeuronGroup(1,
                'dv/dt = -v/tau : volt',
                namespace={'tau': tau},
                method='euler')
M = StateMonitor(G, 'v', record=0)

BrianLogger.log_level_info()
run(1*ms)
print(float(M.v[0][-1] / mV))
```

### Pitfalls and fixes
- `from brian2 import *` imports pylab symbols and shadows builtin `input`; use `from brian2.only import *` or re-import builtin `input` (`docs_sphinx/user/import.rst`).
- Mixing wildcard imports can disable unit-aware wrappers if import order is wrong; keep Brian import last or use `brian2.numpy_` (`docs_sphinx/user/import.rst`).
- Logging preferences set after import may not apply unless logger is re-initialized (`docs_sphinx/advanced/logging.rst`).
- Unknown preference names or invalid values raise preference errors due validation (`docs_sphinx/developer/preferences.rst`).
- Unit mismatches surface as `DimensionMismatchError`; enforce explicit units (`docs_sphinx/user/units.rst`).
- Equations are parsed abstract code, not arbitrary Python; unsupported syntax/functions fail (`docs_sphinx/user/equations.rst`).

### Convergence and validation checks
- Lock `prefs.codegen.target` and integration `method` before comparing runs (`docs_sphinx/user/computation.rst`, `docs_sphinx/advanced/state_update.rst`).
- Prefer explicit group/run namespaces to eliminate resolution warnings (`docs_sphinx/advanced/namespaces.rst`).
- Validate dimension consistency with quick unit conversions (`/unit` or `_`-suffixed array access) (`docs_sphinx/user/units.rst`).
- If logging preferences are changed in script, call logger initialization and confirm expected output level (`docs_sphinx/advanced/logging.rst`).

## Scope
- Handle questions about documentation grouped under the 'docs-sphinx' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs_sphinx/index.rst`
- `docs_sphinx/user/index.rst`
- `docs_sphinx/advanced/index.rst`
- `docs_sphinx/user/import.rst`
- `docs_sphinx/user/units.rst`
- `docs_sphinx/user/equations.rst`
- `docs_sphinx/advanced/namespaces.rst`
- `docs_sphinx/advanced/state_update.rst`
- `docs_sphinx/advanced/preferences.rst`
- `docs_sphinx/advanced/logging.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples`
- `tutorials`

## Test references
- `brian2/tests`
- `dev/tools/tests`

## Optional deeper inspection
- `brian2`

## Source entry points for unresolved issues
- `brian2/units/fundamentalunits.py`
- `brian2/units/stdunits.py`
- `brian2/units/unitsafefunctions.py`
- `brian2/core/preferences.py`
- `brian2/core/core_preferences.py`
- `brian2/utils/logger.py`
- `brian2/stateupdaters/base.py`
- `brian2/stateupdaters/exact.py`
- `brian2/stateupdaters/explicit.py`
- `brian2/stateupdaters/exponential_euler.py`
- `brian2/sphinxext/docscrape_sphinx.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" brian2`).
