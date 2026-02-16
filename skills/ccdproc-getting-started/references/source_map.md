# ccdproc source map: Getting Started

All paths are repository-root relative (from `skills/`, run `cd "$(git rev-parse --show-toplevel)"` first).

Generated from source roots:
- `ccdproc`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `ccd_process`
- `create_deviation`
- `subtract_overscan`
- `trim_image`
- `subtract_dark`
- `flat_correct`
- `gain_correct`
- `ImageFileCollection`
- `log_to_metadata`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" ccdproc`
- `rg -n "def ccd_process|def create_deviation|def subtract_overscan|def trim_image|def subtract_dark|def flat_correct|def gain_correct" ccdproc/core.py`
- `rg -n "log_to_metadata|slice_from_string" ccdproc/log_meta.py ccdproc/utils/slices.py`

## Function-level probes
- `pytest -q ccdproc/tests/test_ccdproc.py -k "ccd_process or create_deviation or subtract_overscan or trim_image or subtract_dark or flat_correct or gain_correct"`
- `pytest -q ccdproc/tests/test_ccdproc.py::test_ccd_process_parameters_are_appropriate`
- `pytest -q ccdproc/tests/test_image_collection.py -k "ImageFileCollection"`

## Suggested source entry points
- `ccdproc/core.py` | primary reduction functions used in the first calibration workflow.
- `ccdproc/log_meta.py` | metadata logging behavior and opt-out semantics.
- `ccdproc/image_collection.py` | directory-based workflows via `ImageFileCollection`.
- `ccdproc/utils/slices.py` | FITS/Python section parsing (`slice_from_string`).
- `ccdproc/_ccddata_wrapper_for_array_api.py` | array-backend wrappers affecting arithmetic behavior.
- `ccdproc/ccddata.py` | CCDData reader/writer exports used by I/O examples.
- `ccdproc/tests/test_ccdproc.py` | function-level regression checks for core reduction steps.
