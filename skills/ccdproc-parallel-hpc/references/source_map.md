# ccdproc source map: Parallel and HPC

All paths are repository-root relative (from `skills/`, run `cd "$(git rev-parse --show-toplevel)"` first).

Generated from source roots:
- `ccdproc`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `combine`
- `Combiner`
- `mem_limit`
- `sigma_clipping`
- `weights`
- `scaling`
- `wcs_project`
- `array_package`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" ccdproc`
- `rg -n "class Combiner|def combine|mem_limit|sigma_clipping|weights|scaling|clip_extrema" ccdproc/combiner.py`
- `rg -n "def wcs_project" ccdproc/core.py`

## Function-level probes
- `pytest -q ccdproc/tests/test_combiner.py -k "limitedmem or sigmaclip or weights or clip_extrema"`
- `pytest -q ccdproc/tests/test_combiner.py::test_combine_limitedmem_fitsimages`
- `pytest -q ccdproc/tests/test_memory_use.py::test_memory_use_in_combine`

## Suggested source entry points
- `ccdproc/combiner.py` | `Combiner`, `combine`, clipping/scaling/weights, and `mem_limit` chunking path.
- `ccdproc/image_collection.py` | `ImageFileCollection` file list generation for batch combine runs.
- `ccdproc/core.py` | `wcs_project` behavior before stacking reprojected frames.
- `ccdproc/tests/test_combiner.py` | edge-case behavior and regression expectations for clipping/weights.
- `ccdproc/tests/test_memory_use.py` | memory-limit regression checks for combine workflows.
