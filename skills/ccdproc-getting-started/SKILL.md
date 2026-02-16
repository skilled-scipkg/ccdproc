---
name: ccdproc-getting-started
description: This skill should be used when users ask about getting started in ccdproc; it prioritizes docs-backed first reductions and escalates to implementation files only for unresolved behavior details.
---

# ccdproc: Getting Started

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
- Route to `ccdproc-api-and-scripting` for backend-specific array API behavior, metadata logging internals, or symbol-level API questions.
- Route to `ccdproc-parallel-hpc` for multi-file stacking, memory-limited combine, or WCS alignment/stacking.
- Route to `ccdproc-advanced-topics` for install, CCDData deep dives, and image-management operations.
- Route to `ccdproc-tests` when the user needs regression-backed validation.

### Triage questions
- Are inputs arrays, FITS files, or already `CCDData` objects? (`docs/getting_started.rst`, `docs/overview.rst`)
- What are the data/calibration units (`adu`, `electron`, `photon`), and are they compatible? (`docs/getting_started.rst`, `docs/reduction_toolbox.rst`)
- Is uncertainty propagation required (`create_deviation`)? (`docs/reduction_toolbox.rst`)
- Is overscan/trim given as FITS sections or Python slices? (`docs/reduction_toolbox.rst`)
- Should dark subtraction be scaled by exposure time? (`docs/reduction_toolbox.rst`)
- Are you reducing one frame or a directory of files? (`docs/getting_started.rst`)

### Canonical workflow
1. Create/read `CCDData` with explicit unit metadata. (`docs/getting_started.rst`)
2. Optionally build uncertainty with `create_deviation(gain, readnoise)`. (`docs/reduction_toolbox.rst`)
3. Subtract overscan, then trim to science region. (`docs/reduction_toolbox.rst`)
4. Subtract bias and dark (enable dark scaling when exposures differ). (`docs/reduction_toolbox.rst`)
5. Apply gain/flat corrections; set flat floor if needed with `min_value`. (`docs/reduction_toolbox.rst`)
6. For one-shot calibration, run `ccd_process` with combined options. (`docs/reduction_toolbox.rst`)
7. Validate units, uncertainty, masks, and metadata log entries before downstream steps.

### Minimal working example
```python
import numpy as np
from astropy import units as u
from astropy.nddata import CCDData
import ccdproc

img = CCDData(np.random.default_rng().normal(size=(100, 232)), unit="adu")
img.header["exposure"] = 30.0

reduced = ccdproc.ccd_process(
    img,
    oscan="[201:232,1:100]",
    trim="[1:200,1:100]",
    error=True,
    gain=2.0 * u.electron / u.adu,
    readnoise=5 * u.electron,
)
```
- Pattern from `docs/reduction_toolbox.rst` and `docs/getting_started.rst`.

### Pitfalls and fixes
- Missing unit on input data breaks physically valid calibration.
  Fix: always set unit when constructing/reading `CCDData`. (`docs/getting_started.rst`, `docs/ccddata.rst`)
- `overscan_axis` follows Python axis order even with FITS sections.
  Fix: compute axis in Python terms (0-based, reversed order vs FITS). (`docs/reduction_toolbox.rst`)
- Trim bounds can silently clip because NumPy slicing is permissive.
  Fix: verify intended trim ranges before calling `trim_image`. (`docs/reduction_toolbox.rst`)
- Dark scaling is not automatic.
  Fix: set `scale=True` (`subtract_dark`) or `dark_scale=True` (`ccd_process`). (`docs/reduction_toolbox.rst`)
- Assuming in-place edits causes stale state.
  Fix: every operation returns a copy; always rebind output. (`docs/getting_started.rst`)

### Convergence/validation checks
- Unit transitions match expectation after gain correction.
- Uncertainty is present/finite where valid data exists.
- Mask shape equals data shape and masked fraction is plausible.
- Metadata contains expected reduction logs unless disabled. (`docs/reduction_toolbox.rst`)
- Overscan/background levels drop after calibration.

## Scope
- Handle questions about initial setup, quickstarts, and first reduction workflows.
- Keep responses workflow-first; route detailed API internals to specialized skills.

## Primary documentation references
- `docs/index.rst`
- `docs/overview.rst`
- `docs/getting_started.rst`
- `docs/reduction_toolbox.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for complete topic coverage.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `docs`

## Test references
- `ccdproc/tests`
- `ccdproc/utils/tests`

## Optional deeper inspection
- `ccdproc`

## Source entry points for unresolved issues
- `ccdproc/core.py` (`ccd_process`, `create_deviation`, `subtract_overscan`, `trim_image`, `subtract_dark`, `flat_correct`)
- `ccdproc/image_collection.py` (`ImageFileCollection` for directory workflows)
- `ccdproc/log_meta.py` (`log_to_metadata`, metadata recording)
- `ccdproc/utils/slices.py` (`slice_from_string` FITS/Python slicing behavior)
- `ccdproc/_ccddata_wrapper_for_array_api.py` (array-backend wrappers for arithmetic)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" ccdproc`).
