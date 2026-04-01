# Codex Marketplace

A curated marketplace repository for installable Codex plugins.

## What This Repository Is

This repository contains marketplace metadata for Codex plugins.

It is intentionally separate from individual plugin repositories so plugins can be versioned, released, and maintained independently.

## Documentation Map

Use the documents in this order:

1. `README.md`: repository purpose, Codex app usage, and the main navigation hub
2. `docs/codex-marketplace-setup.md`: why the repo appears as a marketplace source in Codex app
3. `docs/adding-a-plugin.md`: the standard process for adding a new plugin
4. `AGENTS.md`: editing rules and repository guardrails for Codex and human contributors

## Structure

```text
codex-marketplace/
  .codex/config.toml
  .agents/plugins/marketplace.json
  .gitignore
  AGENTS.md
  LICENSE
  README.md
```

## Marketplace Scope

- Codex marketplace metadata only
- Plugin entries that point to independently managed plugin repositories
- No plugin implementation source in this repository by default

## Codex App Recognition

This repository is set up so Codex can recognize it as a repo-scoped marketplace source:

- `.agents/plugins/marketplace.json` is the repository marketplace catalog.
- `.codex/config.toml` is the Team Config entry point that Codex automatically loads for trusted projects.
- `AGENTS.md` documents the repository rules Codex should follow while editing this repo.

Per the Codex plugin docs, each marketplace appears as a selectable source in the plugin directory, and Codex reads repo marketplaces from `$REPO_ROOT/.agents/plugins/marketplace.json`. That means if you add this repository as a project in Codex app and restart Codex, this marketplace should appear in the marketplace source list.

## How To Open In Codex

1. Open the repository root in Codex, not an inner plugin folder.
2. Mark the project as trusted so Codex will load `.codex/config.toml`.
3. Restart Codex if the project or marketplace file was added after Codex was already running.
4. Open the plugin directory and look for this repository marketplace in the selectable source list.
5. Confirm the repository catalog exists at `.agents/plugins/marketplace.json`.

This repo-scoped flow is the recommended way to use this repository in Codex app.

## Source Of Truth

- Use `.agents/plugins/marketplace.json` as the catalog source for installable plugins in this repository.
- Use `.codex/config.toml` for repo-shared Codex configuration.
- Use `AGENTS.md` for repository workflow and editing rules.
- Use `docs/codex-marketplace-setup.md` for setup rationale.
- Use `docs/adding-a-plugin.md` for new plugin additions.

## Commit Convention

Commit subjects are validated by `.githooks/commit-msg`.

Use Conventional Commits for non-merge commits, for example `feat: add plugin entry` or `fix(plugin): align metadata paths`.

## References

- Setup details and rationale: [docs/codex-marketplace-setup.md](docs/codex-marketplace-setup.md)
- New plugin process: [docs/adding-a-plugin.md](docs/adding-a-plugin.md)
