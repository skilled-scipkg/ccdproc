---
name: ccdproc-parallel-hpc
description: This skill should be used when users ask about parallel and hpc in ccdproc; it prioritizes docs-backed image-combination strategy and memory-aware execution details.
---

# ccdproc: Parallel and HPC

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
- Route to `ccdproc-getting-started` for single-image calibration pipelines.
- Route to `ccdproc-api-and-scripting` for array-backend integration details (`dask`, `jax`, `cupy`).
- Route to `ccdproc-tests` for memory-regression validation or backend CI checks.

### Triage questions
- How many images and what dimensions are being combined? (`docs/image_combination.rst`)
- Is memory bounded (`combine(..., mem_limit=...)`) or can everything fit in RAM?
- Which combine method is required (`average`, `median`, `sum`)?
- Which clipping strategy is needed (min/max, sigma, extrema, iterative sigma)? (`docs/image_combination.rst`)
- Are weights image-wise or pixel-wise, and is method compatible with weighting?
- Is WCS reprojection required before stacking? (`docs/image_combination.rst`)

### Canonical workflow
1. Load/prepare consistent-unit `CCDData` inputs.
2. Choose interface:
   - `Combiner` for direct object control.
   - `combine` for file-based input with explicit `mem_limit`.
3. Configure clipping (`minmax_clipping`, `sigma_clipping`, or `clip_extrema`).
4. Apply optional scaling and weights (average/sum only).
5. Combine with selected method and inspect resulting mask/metadata.
6. For aligned stacks, reproject each frame (`wcs_project`) before combine.
7. Validate memory behavior and output statistics on a subset, then scale out.

### Minimal working example
```python
from ccdproc import ImageFileCollection, combine

ifc = ImageFileCollection("path/to/images")
stack = combine(
    ifc.files_filtered(include_path=True),
    method="average",
    mem_limit=1e9,
    sigma_clip=True,
    sigma_clip_low_thresh=3,
    sigma_clip_high_thresh=3,
)
```
- Pattern from `docs/image_combination.rst` and `ccdproc/combiner.py` API.

### Pitfalls and fixes
- Median combine can be slow without `bottleneck`.
  Fix: install `bottleneck` for better NaN-aware reductions. (`docs/image_combination.rst`, `ccdproc/combiner.py`)
- Weighting with median is unsupported.
  Fix: use average/sum when weights are required. (`docs/image_combination.rst`)
- Sigma clipping defaults may be too aggressive or too weak.
  Fix: tune low/high thresholds and central/deviation functions per dataset.
- Unit or shape mismatches across frames cause combiner errors.
  Fix: normalize units and dimensions before constructing `Combiner`. (`ccdproc/combiner.py`)
- Reprojection flux assumptions may not match science needs.
  Fix: validate flux conservation for selected reprojection method. (`docs/image_combination.rst`)

### Convergence/validation checks
- `NCOMBINE` metadata equals expected contributing frame count.
- Mask fraction after clipping stabilizes (especially with iterative clipping).
- Output background/noise statistics improve vs individual calibrated frames.
- Peak/average memory remains within acceptable bounds for chosen `mem_limit`.
- Results are stable when re-running with same inputs/settings.

## Scope
- Handle questions about MPI/OpenMP/GPU execution, scaling, and batch-style image combination in ccdproc contexts.
- Focus on memory-aware combination and clipping/stacking behavior.

## Primary documentation references
- `docs/image_combination.rst`
- `docs/array_api.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for complete topic coverage.
- Use examples as executable patterns.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with ranked entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `docs`

## Test references
- `ccdproc/tests`
- `ccdproc/utils/tests`

## Optional deeper inspection
- `ccdproc`

## Source entry points for unresolved issues
- `ccdproc/combiner.py` (`Combiner`, `combine`, clipping/scaling/weights, `mem_limit` path)
- `ccdproc/image_collection.py` (`ImageFileCollection` file selection and iteration)
- `ccdproc/core.py` (`wcs_project` and supporting transforms)
- `ccdproc/tests/test_combiner.py` (edge-case behavior and regression expectations)
- `ccdproc/tests/test_memory_use.py` (memory-limit behavior checks)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" ccdproc`).
