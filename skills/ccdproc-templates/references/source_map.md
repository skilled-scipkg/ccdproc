# ccdproc source map: Templates

All paths are repository-root relative (from `skills/`, run `cd "$(git rev-parse --show-toplevel)"` first).

Generated from source roots:
- `ccdproc`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `api`
- `autosummary`
- `module`
- `class`
- `namespace`
- `export`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" ccdproc`
- `rg -n "__all__|from \\.core import|from \\.combiner import|from \\.image_collection import" ccdproc/__init__.py`
- `rg -n "^def ccd_process|^class Combiner|^class ImageFileCollection" ccdproc/core.py ccdproc/combiner.py ccdproc/image_collection.py`

## Function-level probes
- `python -c "from ccdproc import CCDData, Combiner, ImageFileCollection, ccd_process; print(CCDData.__name__, Combiner.__name__, ImageFileCollection.__name__, ccd_process.__name__)"`
- `pytest -q ccdproc/tests/test_ccdproc.py::test_ccd_process`
- `pytest -q ccdproc/tests/test_combiner.py::test_combiner_average`

## Suggested source entry points
- `ccdproc/__init__.py` | controls exported symbol list shown in API/autosummary docs.
- `ccdproc/core.py` | module-level function definitions surfaced in API docs.
- `ccdproc/combiner.py` | `Combiner` and `combine` symbols surfaced in autosummary output.
- `ccdproc/image_collection.py` | `ImageFileCollection` class symbol surfaced in autosummary output.
- `ccdproc/ccddata.py` | `CCDData`/FITS reader-writer exports included in API pages.
