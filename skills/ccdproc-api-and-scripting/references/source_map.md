# ccdproc source map: API and Scripting

All paths are repository-root relative (from `skills/`, run `cd "$(git rev-parse --show-toplevel)"` first).

Generated from source roots:
- `ccdproc`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `array`
- `array_package`
- `ImageFileCollection`
- `Combiner`
- `combine`
- `log_to_metadata`
- `CCDData`
- `namespace`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" ccdproc`
- `rg -n "class _CCDDataWrapperForArrayAPI|def _wrap_ccddata_for_array_api|def _unwrap_ccddata_for_array_api" ccdproc/_ccddata_wrapper_for_array_api.py`
- `rg -n "class Combiner|def combine|def log_to_metadata|class ImageFileCollection" ccdproc/combiner.py ccdproc/log_meta.py ccdproc/image_collection.py`

## Function-level probes
- `CCDPROC_ARRAY_LIBRARY=numpy pytest -q ccdproc/tests/test_wrapped_external_funcs.py`
- `CCDPROC_ARRAY_LIBRARY=dask pytest -q ccdproc/tests/test_ccdproc.py::test_create_deviation`
- `pytest -q ccdproc/tests/test_combiner.py -k "combine or weights or scaling"`

## Suggested source entry points
- `ccdproc/_ccddata_wrapper_for_array_api.py` | backend wrappers and uncertainty handoff for array API inputs.
- `ccdproc/core.py` | callable reduction API functions (`ccd_process`, `create_deviation`, arithmetic helpers).
- `ccdproc/combiner.py` | `Combiner` and `combine` implementation for scripted stacks.
- `ccdproc/image_collection.py` | `ImageFileCollection` iteration/filtering behavior for scripted loops.
- `ccdproc/log_meta.py` | `log_to_metadata` insertion behavior and metadata payload normalization.
- `ccdproc/__init__.py` | exported API surface and namespace wiring.
- `ccdproc/tests/test_wrapped_external_funcs.py` | backend wrapper behavior regression checks.
- `ccdproc/tests/test_ccdproc.py` | function-level API behavior checks used during scripting triage.
