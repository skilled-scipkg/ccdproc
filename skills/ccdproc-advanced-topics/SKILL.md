---
name: ccdproc-advanced-topics
description: This skill should be used when users ask about less-frequent one-doc ccdproc topics; it consolidates advanced and project-process references while preserving concrete source entry points.
---

# ccdproc: Advanced Topics

## Path and startup
- Paths in this skill are repo-root relative.
- If your shell starts inside `skills/`, run:
```bash
REPO_ROOT="$(git rev-parse --show-toplevel)"
cd "$REPO_ROOT"
```
- For environment bootstrap and first simulation checks, open `../ccdproc-index/references/simulation_bootstrap.md`.

## Route the request
- Use this skill for formerly single-doc topics that are important but low-frequency:
  - build/install environment setup
  - `CCDData` I/O/properties/arithmetic details
  - image-directory management and filtering
  - external reduction examples/tutorial links
  - default config behavior
  - contributing/developer process
  - citation, conduct, contributors, changelog
- Route back to core skills when the request becomes workflow-heavy:
  - `ccdproc-getting-started` for end-to-end reduction sequence
  - `ccdproc-api-and-scripting` for callable API behavior
  - `ccdproc-parallel-hpc` for stacking/memory/clipping
  - `ccdproc-tests` for reproducible validation

## Primary documentation references
- `docs/install.rst`
- `docs/ccddata.rst`
- `docs/image_management.rst`
- `docs/reduction_examples.rst`
- `docs/default_config.rst`
- `docs/contributing.rst`
- `docs/citation.rst`
- `docs/conduct.rst`
- `docs/authors_for_sphinx.rst`
- `docs/changelog.rst`

## Fast triage map
- Install/build errors: start `docs/install.rst`
- Data model and units/masks/I-O: start `docs/ccddata.rst`
- Directory scans and FITS filtering: start `docs/image_management.rst`
- Example pipelines and external notebooks/repos: start `docs/reduction_examples.rst`
- Runtime config customization: start `docs/default_config.rst`
- Contribution/reporting workflow: start `docs/contributing.rst`
- Publication attribution/legal/community context: `docs/citation.rst`, `docs/conduct.rst`, `docs/authors_for_sphinx.rst`, `docs/changelog.rst`

## Workflow
- Start with the primary reference that matches the triage map.
- If details are missing, inspect `references/doc_map.md` for full inventory.
- If docs remain ambiguous, inspect `references/source_map.md` and open suggested source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `docs`

## Test references
- `ccdproc/tests`
- `ccdproc/utils/tests`

## Optional deeper inspection
- `ccdproc`

## Source entry points for unresolved issues
- `ccdproc/ccddata.py` (CCDData wrappers and FITS reader/writer exports)
- `ccdproc/image_collection.py` (image selection/filtering/iteration internals)
- `ccdproc/utils/sample_directory.py` (documented sample-directory behavior)
- `ccdproc/core.py` (processing functions referenced by examples)
- `ccdproc/utils/slices.py` (FITS/Python slicing conversion)
- `ccdproc/__init__.py` (public namespace and config)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" ccdproc`).
