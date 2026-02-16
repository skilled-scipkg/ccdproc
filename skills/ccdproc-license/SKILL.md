---
name: ccdproc-license
description: This skill should be used when users ask about license in ccdproc; it prioritizes direct license/citation references and then concrete repository entry points.
---

# ccdproc: License

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
- Route to `ccdproc-advanced-topics` for citation, conduct, contributors, or changelog questions.
- Route to `ccdproc-getting-started`/`ccdproc-api-and-scripting` for usage or implementation details unrelated to licensing.

### Triage questions
- Is the user asking about redistribution rights/obligations or publication attribution?
- Do they need the canonical license text or just license identifier?
- Is the request about source headers or packaged documentation inclusion?
- Are they asking citation wording rather than legal license terms?

### Canonical workflow
1. Start with `docs/license.rst` to confirm canonical project licensing statement.
2. Follow the include to `LICENSE.rst` for the full legal text.
3. Distinguish legal license from scholarly citation/acknowledgment requests.
4. Verify source/header references to the BSD-3-clause notice when auditing files.
5. Provide exact file paths for legal/citation handoff.

### Minimal working example
```bash
sed -n '1,40p' docs/license.rst
sed -n '1,160p' LICENSE.rst
```
- `docs/license.rst` is the canonical docs entry and includes `LICENSE.rst`.

### Pitfalls and fixes
- Confusing citation instructions with legal licensing.
  Fix: use license docs for legal terms; route citation to advanced topics. (`docs/license.rst`, `docs/citation.rst`)
- Referencing stale secondary summaries.
  Fix: quote from `LICENSE.rst` directly when exact wording matters.
- Omitting license file in redistribution artifacts.
  Fix: ensure `LICENSE.rst` is included with source/binary distributions.
- Assuming non-BSD obligations.
  Fix: verify against the explicit BSD-3-clause text.

### Convergence/validation checks
- `docs/license.rst` and `LICENSE.rst` agree on BSD-3-clause status.
- Packaging/distribution includes `LICENSE.rst`.
- File headers consistently reference `LICENSE.rst` where expected.
- Citation requests are routed separately from legal license responses.

## Scope
- Handle licensing and redistribution questions for ccdproc.
- Keep answers legal-text anchored and route non-license governance topics out.

## Primary documentation references
- `docs/license.rst`
- `LICENSE.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for topic coverage.
- If ambiguity remains after docs, inspect `references/source_map.md` for repository entry points.
- Cite exact documentation/source file paths in responses.

## Tutorials and examples
- `docs`

## Test references
- `ccdproc/tests`
- `ccdproc/utils/tests`

## Optional deeper inspection
- `ccdproc`

## Source entry points for unresolved issues
- `LICENSE.rst` (full legal terms)
- `ccdproc/__init__.py` (project-level license header pattern)
- `ccdproc/core.py` (license header pattern in core implementation)
- `ccdproc/combiner.py` (license header pattern in major subsystem)
- Prefer targeted source search (for example: `rg -n "Licensed under a 3-clause BSD" ccdproc`).
