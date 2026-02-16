---
name: ccdproc-index
description: This skill should be used when users ask how to use ccdproc and the correct generated documentation skill must be selected before going deeper into source code.
---

# ccdproc Skills Index

## Start from `skills/`
- Repository paths in all topic skills are repo-root relative.
- If your shell starts under `skills/`, run:
```bash
REPO_ROOT="$(git rev-parse --show-toplevel)"
cd "$REPO_ROOT"
```
- Then use `skills/ccdproc-index/references/simulation_bootstrap.md` for environment setup and first simulation checks.

## Route the request
- Classify the request into one of the topic skills below.
- Prefer docs-first routing and only inspect source when topic docs leave ambiguity.

## Generated topic skills
- `ccdproc-getting-started`: First-week setup and calibration workflow routing.
- `ccdproc-api-and-scripting`: Function-level API usage, array backends, and programmatic workflows.
- `ccdproc-parallel-hpc`: Memory-aware combination, clipping, and stack/reprojection strategy.
- `ccdproc-tests`: Test harness, fixtures, backend matrix, and regression validation.
- `ccdproc-templates`: Autosummary/Sphinx template customization.
- `ccdproc-license`: Legal licensing text and redistribution checkpoints.
- `ccdproc-advanced-topics`: Consolidated one-doc topics (install, CCDData details, image management, examples, developer/process docs, citation/conduct/authors/changelog, default config).

## Documentation-first inputs
- `docs`

## Tutorials and examples roots
- `docs`

## Test roots for behavior checks
- `ccdproc/tests`
- `ccdproc/utils/tests`

## Escalate only when needed
- Start from topic skill primary references.
- If those references are insufficient, open the topic map pair directly:
- `skills/ccdproc-getting-started/references/doc_map.md` then `skills/ccdproc-getting-started/references/source_map.md`
- `skills/ccdproc-api-and-scripting/references/doc_map.md` then `skills/ccdproc-api-and-scripting/references/source_map.md`
- `skills/ccdproc-parallel-hpc/references/doc_map.md` then `skills/ccdproc-parallel-hpc/references/source_map.md`
- `skills/ccdproc-tests/references/doc_map.md` then `skills/ccdproc-tests/references/source_map.md`
- `skills/ccdproc-templates/references/doc_map.md` then `skills/ccdproc-templates/references/source_map.md`
- `skills/ccdproc-license/references/doc_map.md` then `skills/ccdproc-license/references/source_map.md`
- `skills/ccdproc-advanced-topics/references/doc_map.md` then `skills/ccdproc-advanced-topics/references/source_map.md`
- Use targeted symbol search while inspecting source (e.g., `rg -n "<symbol_or_keyword>" ccdproc`).

## Source directories for deeper inspection
- `ccdproc`
