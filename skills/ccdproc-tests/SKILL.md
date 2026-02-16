---
name: ccdproc-tests
description: This skill should be used when users ask about tests in ccdproc; it prioritizes reproducible, docs-backed validation entry points and then source-level test internals.
---

# ccdproc: Tests

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
- Route to `ccdproc-getting-started` for calibration design questions before writing tests.
- Route to `ccdproc-api-and-scripting` when debugging API behavior or backend semantics.
- Route to `ccdproc-parallel-hpc` for combine performance/memory tuning.

### Triage questions
- Is this a functional correctness issue, regression, memory behavior issue, or backend-compatibility issue?
- Which array backend should tests run with (`CCDPROC_ARRAY_LIBRARY`)? (`ccdproc/conftest.py`)
- Does the case involve file-collection behavior, combiner behavior, or core reduction ops?
- Is the failure limited to Linux/memory-profiler environments? (`ccdproc/tests/test_memory_use.py`)
- Do you need synthetic FITS fixtures or package sample data? (`ccdproc/tests/pytest_fixtures.py`, `ccdproc/utils/sample_directory.py`, `ccdproc/tests/data/README.rst`)

### Canonical workflow
1. Start from `ccdproc/tests/data/README.rst` to understand packaged test-data constraints.
2. Select backend via `CCDPROC_ARRAY_LIBRARY` before running tests. (`ccdproc/conftest.py`)
3. Run focused tests for the impacted subsystem (`test_ccdproc.py`, `test_combiner.py`, `test_image_collection.py`).
4. Reproduce with deterministic fixtures (`triage_setup`, `ccd_data`) before broader runs. (`ccdproc/tests/pytest_fixtures.py`)
5. For memory regressions, use `test_memory_use.py` assumptions (Linux + memory profiler).
6. Expand to wider suites only after localized failures are resolved.

### Minimal working example
```bash
CCDPROC_ARRAY_LIBRARY=numpy pytest -q ccdproc/tests/test_combiner.py
CCDPROC_ARRAY_LIBRARY=dask pytest -q ccdproc/tests/test_ccdproc.py::test_create_deviation
```
- Backend selection is implemented in `ccdproc/conftest.py`.

### Pitfalls and fixes
- Running non-default backend without setting `CCDPROC_ARRAY_LIBRARY`.
  Fix: set environment variable explicitly (`numpy`, `jax`, `dask`, `cupy`). (`ccdproc/conftest.py`)
- Expecting memory tests to run everywhere.
  Fix: memory tests intentionally require Linux + `memory_profiler`. (`ccdproc/tests/test_memory_use.py`)
- Using ad hoc file fixtures that skip cleanup.
  Fix: use `triage_setup`/sample-directory fixtures for teardown safety. (`ccdproc/tests/pytest_fixtures.py`)
- Misreading combiner failures caused by unit/shape mismatch.
  Fix: verify all input `CCDData` objects share shape and unit. (`ccdproc/tests/test_combiner.py`)
- Treating docs sample data as large benchmark data.
  Fix: packaged data is intentionally small. (`ccdproc/tests/data/README.rst`)

### Convergence/validation checks
- Baseline tests pass on `numpy` backend.
- At least one non-NumPy backend smoke test passes for touched codepaths.
- Targeted regression test reproduces the original issue before fix and passes after fix.
- No new unexpected warnings or mask/unit regressions in touched subsystem tests.

## Scope
- Handle questions about testing strategy, fixtures, and validation behavior under the `tests` theme.
- Prefer focused, reproducible subsystem tests before full-suite runs.

## Primary documentation references
- `ccdproc/tests/data/README.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for complete topic references.
- Use test modules as canonical behavior checks.
- If ambiguity remains, inspect `references/source_map.md` and then targeted source files.
- Cite exact file paths in responses.

## Tutorials and examples
- `docs`

## Test references
- `ccdproc/tests`
- `ccdproc/utils/tests`

## Optional deeper inspection
- `ccdproc`

## Source entry points for unresolved issues
- `ccdproc/conftest.py` (backend selection and test-header configuration)
- `ccdproc/tests/pytest_fixtures.py` (reproducible test data/teardown)
- `ccdproc/tests/test_ccdproc.py` (core reduction behavior)
- `ccdproc/tests/test_combiner.py` (combine/clipping/weights behavior)
- `ccdproc/tests/test_image_collection.py` (directory and filtering semantics)
- `ccdproc/tests/test_memory_use.py` (memory-limit regression checks)
- `ccdproc/utils/sample_directory.py` (sample FITS directory generator)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" ccdproc/tests ccdproc`).
