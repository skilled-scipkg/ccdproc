# Evidence: ccdproc-api-and-scripting

## Primary docs
- `docs/reduction_toolbox.rst`
- `docs/array_api.rst`
- `docs/api.rst`
- `docs/_templates/autosummary/class.rst`

## Primary source entry points
- `skills/ccdproc-api-and-scripting/references/doc_map.md`
- `ccdproc/_ccddata_wrapper_for_array_api.py`
- `ccdproc/__init__.py`
- `ccdproc/core.py`
- `ccdproc/log_meta.py`
- `ccdproc/image_collection.py`
- `ccdproc/combiner.py`
- `ccdproc/ccddata.py`
- `ccdproc/utils/__init__.py`
- `ccdproc/conftest.py`
- `ccdproc/utils/slices.py`
- `ccdproc/utils/sample_directory.py`

## Extracted headings
- Read the data of the fits file as CCDData object
- Open the file again (assuming the bitfield is saved in the same FITS file)
- Save the mask as "mask" attribute of the ccd
- Create some source signal
- and another one
- create some random signals
- remove low signal
- create a CCD object based on the data
- Create some plots
- Do more processing with ccdproc functions
- ...

## Executable command hints
- python zero-based numbering.

## Warnings and pitfalls
- error image instead.
- means you can supply an invalid shape for, e.g. trimming, and an error
- ...                            error=True,
