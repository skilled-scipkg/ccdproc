# ccdproc source map: Advanced Topics

All paths are repository-root relative (from `skills/`, run `cd "$(git rev-parse --show-toplevel)"` first).

Generated from source roots:
- `ccdproc`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `authors`
- `ccddata`
- `changelog`
- `citation`
- `conduct`
- `config`
- `contributing`
- `default`
- `developer`
- `image`
- `install`
- `management`
- `modeling`
- `reduction`
- `sphinx`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" ccdproc`
- `rg -n "__all__|fits_ccddata_reader|fits_ccddata_writer|_recognized_fits_file_extensions" ccdproc/ccddata.py`
- `rg -n "class ImageFileCollection|def values|def files_filtered|def ccds|def _fits_summary" ccdproc/image_collection.py`

## Function-level probes
- `pytest -q ccdproc/tests/test_image_collection.py -k "fits_summary or ImageFileCollection"`
- `pytest -q ccdproc/utils/tests/test_slices.py`
- `pytest -q ccdproc/tests/test_ccdproc.py -k "ccd_process or wcs_project"`

## Suggested source entry points
- `ccdproc/ccddata.py` | exported CCDData/FITS reader-writer entry points used in docs.
- `ccdproc/image_collection.py` | `ImageFileCollection` filtering, summaries, and file iteration behavior.
- `ccdproc/utils/sample_directory.py` | deterministic sample FITS directory setup for reproductions.
- `ccdproc/utils/slices.py` | `slice_from_string` FITS-section parsing and conversion behavior.
- `ccdproc/core.py` | `ccd_process` and `wcs_project` behavior used by advanced examples.
- `ccdproc/tests/test_image_collection.py` | regression checks for directory filtering semantics.
- `ccdproc/tests/test_ccdproc.py` | function-level behavior checks tied to reduction docs.
