# ccdproc source map: Tests

All paths are repository-root relative (from `skills/`, run `cd "$(git rev-parse --show-toplevel)"` first).

Generated from source roots:
- `ccdproc`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `pytest`
- `fixture`
- `array_library`
- `memory`
- `combiner`
- `image_collection`
- `ccd_process`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" ccdproc/tests ccdproc`
- `rg -n "CCDPROC_ARRAY_LIBRARY|testing_array_library" ccdproc/conftest.py`
- `rg -n "triage_setup|ccd_data|sample_directory" ccdproc/tests/pytest_fixtures.py ccdproc/utils/sample_directory.py`

## Function-level probes
- `CCDPROC_ARRAY_LIBRARY=numpy pytest -q ccdproc/tests/test_ccdproc.py::test_ccd_process`
- `CCDPROC_ARRAY_LIBRARY=dask pytest -q ccdproc/tests/test_ccdproc.py::test_create_deviation`
- `pytest -q ccdproc/tests/test_combiner.py::test_combine_limitedmem_fitsimages`
- `pytest -q ccdproc/tests/test_image_collection.py::test_fits_summary`

## Suggested source entry points
- `ccdproc/conftest.py` | backend selection and pytest environment configuration.
- `ccdproc/tests/pytest_fixtures.py` | deterministic fixtures (`triage_setup`, `ccd_data`) and teardown safety.
- `ccdproc/tests/test_ccdproc.py` | function-level checks for core reduction APIs.
- `ccdproc/tests/test_combiner.py` | combine/clipping/weights behavior checks.
- `ccdproc/tests/test_image_collection.py` | directory and FITS-filtering behavior checks.
- `ccdproc/tests/test_memory_use.py` | memory regression behavior checks for `combine`.
- `ccdproc/utils/sample_directory.py` | sample FITS directory generation for reproducible tests.
