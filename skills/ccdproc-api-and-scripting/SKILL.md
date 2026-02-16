---
name: ccdproc-api-and-scripting
description: This skill should be used when users ask about api and scripting in ccdproc; it prioritizes docs-backed usage patterns and escalates to implementation files only for unresolved details.
---

# ccdproc: API and Scripting

## Path and startup
- Paths in this skill are repo-root relative.
- If your shell starts inside `skills/`, run:
```bash
REPO_ROOT="$(git rev-parse --show-toplevel)"
cd "$REPO_ROOT"
```
- For environment bootstrap and first simulation checks, open `../ccdproc-index/references/simulation_bootstrap.md`.

## High-Signal Playbook

### Route conditions
- Route to `ccdproc-getting-started` for first reduction walkthroughs and calibration sequencing.
- Route to `ccdproc-parallel-hpc` for large-stack combine strategy, clipping policy, and memory controls.
- Route to `ccdproc-templates` for autosummary/Sphinx template customization.
- Route to `ccdproc-tests` when API behavior needs regression confirmation.

### Triage questions
- Which array backend is required (`numpy`, `dask`, `jax`, `cupy`)? (`docs/array_api.rst`)
- Do you need single-image ops, directory iteration (`ImageFileCollection`), or stack combine (`Combiner`/`combine`)? (`docs/getting_started.rst`, `docs/image_combination.rst`)
- Is metadata logging default, customized, or disabled? (`docs/reduction_toolbox.rst`)
- Do you need function-by-function API lookup or workflow examples? (`docs/api.rst`, `docs/reduction_toolbox.rst`)
- Are operations unit-sensitive (gain, subtraction, arithmetic with uncertainty)? (`docs/getting_started.rst`, `docs/reduction_toolbox.rst`)

### Canonical workflow
1. Choose backend and create/load `CCDData` with explicit units. (`docs/array_api.rst`, `docs/getting_started.rst`)
2. Use core functions (`trim_image`, `subtract_dark`, `flat_correct`, etc.) or `ccd_process` for bundled reductions. (`docs/reduction_toolbox.rst`)
3. For many files, iterate via `ImageFileCollection` and apply the same API sequence. (`docs/getting_started.rst`, `docs/image_management.rst`)
4. Combine via `Combiner`/`combine` and enable clipping/scaling/weights as needed. (`docs/image_combination.rst`)
5. Control metadata logging with `add_keyword` (`None` to disable, dict/string to customize). (`docs/reduction_toolbox.rst`)
6. Use `docs/api.rst` for symbol lookup, then inspect source entry points for edge cases.

### Minimal working example
```python
import dask.array as da
import ccdproc
from astropy.nddata import CCDData

data = da.random.random((1000, 1000))
ccd = CCDData(data, unit="adu")
ccd = ccdproc.trim_image(ccd[:900, :900])
```
- Direct pattern from `docs/array_api.rst`; same function calls work for NumPy inputs.

### Pitfalls and fixes
- Assuming array API backend parity for every function.
  Fix: stick to tested backends first (`numpy`, `dask`, `jax`), treat `cupy` as conditional. (`docs/array_api.rst`)
- Backend missing a median implementation.
  Fix: install `bottleneck` or use backend that provides median. (`docs/array_api.rst`)
- Using unsupported `sparse` arrays.
  Fix: switch backend or contribute support upstream. (`docs/array_api.rst`)
- Logging noise in metadata.
  Fix: pass `add_keyword=None` to opt out or provide explicit key/value logging. (`docs/reduction_toolbox.rst`)
- Unit mismatch in arithmetic/subtraction.
  Fix: normalize units before calling processing APIs. (`docs/getting_started.rst`, `ccdproc/_ccddata_wrapper_for_array_api.py`)

### Convergence/validation checks
- Output array type matches intended backend.
- Output units and uncertainty behavior match expected physics.
- Metadata logging is present or suppressed as configured.
- Small cross-check run (same input, same method) gives consistent statistics across backends.
- Combine outputs preserve expected dimensions/mask behavior.

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Keep responses API/workflow oriented; avoid exhaustive per-function dumps unless requested.

## Primary documentation references
- `docs/reduction_toolbox.rst`
- `docs/array_api.rst`
- `docs/api.rst`
- `docs/_templates/autosummary/class.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `docs`

## Test references
- `ccdproc/tests`
- `ccdproc/utils/tests`

## Optional deeper inspection
- `ccdproc`

## Source entry points for unresolved issues
- `ccdproc/_ccddata_wrapper_for_array_api.py` (backend wrappers and uncertainty propagation glue)
- `ccdproc/core.py` (primary processing API behavior)
- `ccdproc/combiner.py` (`Combiner` and `combine` implementation)
- `ccdproc/image_collection.py` (`ImageFileCollection` filtering/iteration)
- `ccdproc/log_meta.py` (autologging and metadata insertion rules)
- `ccdproc/__init__.py` (public namespace exports and config)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" ccdproc`).
