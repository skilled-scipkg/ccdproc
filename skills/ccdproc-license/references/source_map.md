# ccdproc source map: License

All paths are repository-root relative (from `skills/`, run `cd "$(git rev-parse --show-toplevel)"` first).

Generated from source roots:
- `ccdproc`
- repository root legal files

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `license`
- `3-clause`
- `bsd`
- `header`

## Fast source navigation
- `rg -n "Licensed under a 3-clause BSD" ccdproc`
- `rg -n "^# Licensed under a 3-clause BSD" ccdproc/core.py ccdproc/combiner.py ccdproc/image_collection.py ccdproc/ccddata.py`
- `rg -n "def ccd_process|def combine|class ImageFileCollection" ccdproc/core.py ccdproc/combiner.py ccdproc/image_collection.py`

## Function-level probes
- `pytest -q ccdproc/tests/test_ccdproc.py::test_ccd_process`
- `pytest -q ccdproc/tests/test_combiner.py::test_combine_average_ccddata`
- `pytest -q ccdproc/tests/test_image_collection.py -k "ImageFileCollection"`

## Suggested source entry points
- `LICENSE.rst` | canonical legal text for redistribution terms.
- `ccdproc/core.py` | file header plus representative public function implementation (`ccd_process`).
- `ccdproc/combiner.py` | file header plus representative public function implementation (`combine`).
- `ccdproc/image_collection.py` | file header plus `ImageFileCollection` class implementation.
- `ccdproc/ccddata.py` | file header and `CCDData`/FITS I/O export declarations.
