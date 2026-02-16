---
name: ccdproc-templates
description: This skill should be used when users ask about templates in ccdproc; it prioritizes docs-backed autosummary customization and escalates to source only for behavior details.
---

# ccdproc: Templates

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
- Route to `ccdproc-api-and-scripting` for runtime API behavior or symbol-level usage.
- Route to `ccdproc-getting-started` for reduction workflows.
- Route to `ccdproc-advanced-topics` for contribution/build-doc process questions.

### Triage questions
- Is the change for class pages, module pages, or all autosummary pages? (`docs/_templates/autosummary/class.rst`, `docs/_templates/autosummary/module.rst`, `docs/_templates/autosummary/base.rst`)
- Do you need a minimal override or a full custom template?
- Is the issue in generated API content (`docs/api.rst`) or in Sphinx template rendering itself?
- Should behavior remain aligned with Astropy autosummary core templates?

### Canonical workflow
1. Identify target template file (`class.rst`, `module.rst`, or shared `base.rst`).
2. Keep inheritance from `autosummary_core/*` and override only what is necessary. (`docs/_templates/autosummary/*.rst`)
3. Regenerate docs and inspect API output pages tied to `docs/api.rst`.
4. If output drift is broad, revert to inheritance-only template and add minimal block override.
5. If symbol coverage is missing, check package exports and module layout.

### Minimal working example
```jinja
{% extends "autosummary_core/module.rst" %}
{# Keep inheritance from Astropy autosummary core and only add minimal overrides. #}
```
- This is the current baseline pattern in `docs/_templates/autosummary/module.rst`.

### Pitfalls and fixes
- Replacing inherited templates with copied upstream files causes maintenance drift.
  Fix: preserve `{% extends "autosummary_core/..." %}` and patch only needed blocks.
- Editing the wrong template file (class vs module) gives no visible change.
  Fix: match template to the generated page type.
- Treating docs-template issues as runtime API bugs.
  Fix: validate `docs/api.rst` and public exports separately.
- Broad customizations hide upstream improvements from Astropy template updates.
  Fix: keep overrides minimal and review diffs against generated pages.

### Convergence/validation checks
- Target API page renders successfully after template change.
- Generated class/module pages still include expected member sections.
- Only intended formatting changed; symbol inventory is unaffected.
- No template syntax errors in docs build output.

## Scope
- Handle questions about documentation templates under the `templates` theme.
- Focus on minimal, maintainable autosummary customizations.

## Primary documentation references
- `docs/_templates/autosummary/module.rst`
- `docs/_templates/autosummary/base.rst`
- `docs/_templates/autosummary/class.rst`
- `docs/api.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for complete template inventory.
- If ambiguity remains after docs, inspect `references/source_map.md` for package entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `docs`

## Test references
- `ccdproc/tests`
- `ccdproc/utils/tests`

## Optional deeper inspection
- `ccdproc`

## Source entry points for unresolved issues
- `ccdproc/__init__.py` (controls what appears in public API docs)
- `ccdproc/core.py` (major symbol definitions included by API docs)
- `ccdproc/combiner.py` (combiner symbols visible in autosummary output)
- `ccdproc/image_collection.py` (image-management API entries)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" ccdproc`).
