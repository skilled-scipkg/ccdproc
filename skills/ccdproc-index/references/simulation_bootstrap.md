# ccdproc simulation bootstrap

Use this when your shell starts under `skills/` and you need a runnable baseline quickly.

## 1) Move to repo root and prepare environment
```bash
REPO_ROOT="$(git rev-parse --show-toplevel)"
cd "$REPO_ROOT"
python -m venv .venv
source .venv/bin/activate
python -m pip install -U pip
python -m pip install -e ".[test]"
```

## 2) Run a minimal reduction simulation
```bash
python - <<'PY'
import numpy as np
from astropy import units as u
from astropy.nddata import CCDData
import ccdproc

rng = np.random.default_rng(42)
raw = CCDData(rng.normal(loc=1000, scale=7, size=(80, 120)), unit="adu")
raw.header["exposure"] = 30.0
reduced = ccdproc.ccd_process(
    raw,
    trim="[1:100,1:80]",
    gain=1.7 * u.electron / u.adu,
    readnoise=4.5 * u.electron,
    error=True,
)
print(reduced.shape, reduced.unit)
PY
```

## 3) Validation checkpoints
- The script prints a 2D shape and `electron` unit.
- No exception from `ccdproc.ccd_process`.
- `reduced.uncertainty` exists and is finite for typical pixels.

## 4) Quick behavior checks before larger simulations
```bash
pytest -q ccdproc/tests/test_ccdproc.py::test_ccd_process
pytest -q ccdproc/tests/test_combiner.py::test_combine_limitedmem_fitsimages
```
