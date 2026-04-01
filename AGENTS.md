# AGENTS.md

## Purpose

This repository is the marketplace catalog for installable Codex plugins.

Primary responsibilities:

- maintain the root marketplace catalog at `.agents/plugins/marketplace.json`
- keep plugin metadata and documentation consistent for plugins stored under `plugins/`
- avoid turning this repository into a general plugin implementation monorepo unless that scope is explicitly changed

## Current Repository Shape

```text
codex-marketplace/
  .codex/config.toml
  .agents/plugins/marketplace.json
  plugins/
    plan-handoff/
      .codex-plugin/plugin.json
      skills/
      references/
      README.md
      LICENSE
  README.md
  LICENSE
```

Notes:

- The root catalog is the installable marketplace source of truth.
- The `.codex/config.toml` file is the shared Team Config entry point for Codex.
- Each plugin directory should contain its own `.codex-plugin/plugin.json`.
- Prefer documenting the repository as it actually exists. If documentation and filesystem differ, update docs or call out the mismatch instead of assuming the docs are correct.

## Document Roles

Use the repository documents with clear ownership:

- `README.md`: public entry point and Codex app usage summary
- `docs/codex-marketplace-setup.md`: setup rationale and marketplace-source behavior in Codex app
- `docs/adding-a-plugin.md`: standard operating procedure for adding a plugin
- `AGENTS.md`: editing rules, validation expectations, and repository guardrails

When updating one of these documents, check whether the neighboring documents need wording or link updates too.

## Codex App Setup

For Codex app usage in this repository:

- open the repository root so Codex can see both `.codex/` and `.agents/`
- trust the project so Codex loads `.codex/config.toml`
- treat `.agents/plugins/marketplace.json` as the marketplace catalog Codex-facing tooling should update
- expect this repository marketplace to appear as a selectable source in the plugin directory when the repo is added as a Codex project
- if recognition looks stale, restart Codex after adding the project or changing the marketplace file

This repo-scoped Codex app flow is the recommended usage for this repository. If you document the setup elsewhere, keep `README.md`, `AGENTS.md`, and the referenced setup guide aligned.

## Working Rules

1. Start by reading `README.md` and any plugin-local `README.md` before changing metadata or docs.
2. Treat `.agents/plugins/marketplace.json` as the canonical catalog for what this repository exposes.
3. When adding or editing a plugin entry, keep names, paths, category, and install/auth policy aligned with the plugin's `.codex-plugin/plugin.json`.
4. Do not invent files or directories just because a README mentions them. Verify on disk first.
5. Keep changes small and targeted. This repo is metadata-heavy, so unnecessary restructuring is usually a regression.
6. Preserve JSON formatting style already used in the repository: UTF-8 text, trailing-newline files, and 2-space indentation for JSON.

## Plugin Update Checklist

When modifying an existing plugin under `plugins/<plugin-name>/`:

- verify `.codex-plugin/plugin.json` exists and matches the plugin's public identity
- review the plugin `README.md` for outdated structure or workflow claims
- confirm every referenced skill path actually exists
- confirm referenced support files in `references/` exist
- update the root `.agents/plugins/marketplace.json` if the plugin should be installable from this repository

When adding a new plugin:

- create `plugins/<plugin-name>/`
- add `.codex-plugin/plugin.json`
- add plugin `README.md`
- add `LICENSE` if the plugin is meant to stand alone
- add skill directories and any referenced agent/config files
- register the plugin in `.agents/plugins/marketplace.json`

Use [docs/adding-a-plugin.md](docs/adding-a-plugin.md) as the shared source of truth for the full new-plugin flow.
Use [docs/codex-marketplace-setup.md](docs/codex-marketplace-setup.md) as the shared source of truth for the Codex app setup rationale.

## Documentation Standards

- Keep the root `README.md` focused on marketplace scope, not plugin internals.
- Keep plugin `README.md` files focused on plugin behavior, repository layout, and user workflow.
- If a README includes a layout tree, make sure it matches the current filesystem.
- If a plugin is intentionally incomplete or illustrative, say so explicitly instead of implying missing files exist.

## Validation

Before finishing work, run lightweight verification appropriate to the change:

- for catalog changes, read back `.agents/plugins/marketplace.json`
- for plugin metadata changes, read back `.codex-plugin/plugin.json`
- for documentation changes, verify referenced paths exist with `rg --files` or PowerShell directory listing
- if you notice a pre-existing mismatch you are not fixing, mention it clearly in your final handoff

## Avoid

- adding unrelated application code
- changing plugin names or paths without updating the root marketplace catalog
- leaving README examples that point to nonexistent files
- silently "fixing" scope by expanding the repository beyond marketplace metadata and plugin packaging
