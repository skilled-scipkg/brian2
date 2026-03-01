---
name: brian2-theory-and-methods
description: This skill should be used when users ask about theory and methods in brian2; it prioritizes documentation references and then source inspection only for unresolved details.
---

# brian2: Theory and Methods

## High-Signal Playbook
### Route conditions
- Use this skill for numerical integration choices, stochastic method behavior, refractory formalism, and method-level accuracy tradeoffs.
- Route concrete API wiring questions to `brian2-api-and-scripting`.
- Route execution target/build concerns to `brian2-simulation-workflows` or `brian2-build-and-install`.

### Triage questions
- Deterministic ODEs or stochastic equations?
- Need exact trajectory matching or stable distribution-level behavior?
- Is `exact` applicable, or are `euler`/`exponential_euler`/GSL candidates required?
- What is the acceptable accuracy-cost tradeoff?

### Canonical workflow
- Start from method docs and equation constraints.
- Run a small model with two candidate methods.
- Perform `dt` sensitivity checks and compare target observables.

```bash
python - <<'PY'
from brian2 import *
start_scope()
for method in ('exact', 'euler', 'exponential_euler'):
    start_scope()
    defaultclock.dt = 0.1*ms
    G = NeuronGroup(1, 'dv/dt = -v/(10*ms) : 1', method=method)
    G.v = 1
    M = StateMonitor(G, 'v', record=True)
    run(20*ms)
    print(method, float(M.v[0][-1]))
PY
```

### Validation checkpoints
- Chosen method reproduces expected qualitative behavior.
- Halving `dt` does not materially change key metrics.
- Unit checks pass with no hidden dimension mismatches.
- For stochastic systems, statistics (not exact traces) remain stable across runs/seeds.

## Scope
- Handle questions about theoretical background and algorithmic methods.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs_sphinx/user/numerical_integration.rst`
- `docs_sphinx/advanced/state_update.rst`
- `docs_sphinx/user/equations.rst`
- `docs_sphinx/user/refractoriness.rst`
- `docs_sphinx/advanced/random.rst`
- `docs_sphinx/developer/GSL.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tests as behavior checks when method behavior is ambiguous.
- If ambiguity remains after docs/tests, inspect `references/source_map.md` and start with the listed function-level entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples/advanced`
- `examples/frompapers`

## Test references
- `brian2/tests`
- `dev/tools/tests`

## Optional deeper inspection
- `brian2`

## Source entry points for unresolved issues
- `brian2/stateupdaters/base.py`
- `brian2/stateupdaters/exact.py`
- `brian2/stateupdaters/explicit.py`
- `brian2/stateupdaters/exponential_euler.py`
- `brian2/stateupdaters/GSL.py`
- `brian2/equations/equations.py`
- `brian2/equations/unitcheck.py`
- `brian2/equations/refractory.py`
- `brian2/codegen/translation.py`
- `brian2/tests/test_stateupdaters.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" brian2`).
