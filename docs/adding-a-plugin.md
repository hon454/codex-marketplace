# Adding A Plugin

## Goal

Use this process when adding a new plugin to this repository's Codex marketplace.

This document is the shared reference for both `README.md` and `AGENTS.md`.

## How To Use This Document

- Read `README.md` first for repository context.
- Use `docs/codex-marketplace-setup.md` if you need the Codex app marketplace-source behavior explained.
- Use this document for the actual plugin-addition workflow.
- Use `AGENTS.md` for repository guardrails while performing the work.

## Canonical Flow

1. Create a new plugin directory under `plugins/<plugin-name>/`.
2. Add the required manifest at `plugins/<plugin-name>/.codex-plugin/plugin.json`.
3. Add plugin components at the plugin root as needed:
   - `skills/`
   - `.app.json`
   - `.mcp.json`
   - `assets/`
4. Add or update `plugins/<plugin-name>/README.md`.
5. Register the plugin in `.agents/plugins/marketplace.json`.
6. Restart Codex if you want the updated repo marketplace to appear in the plugin directory source list right away.

## Naming Rules

- Use a stable kebab-case plugin `name`.
- Keep the folder name and `.codex-plugin/plugin.json` `name` aligned.
- Do not rename an existing plugin casually. Treat plugin names as stable identifiers.

## Required Files

Minimum required structure:

```text
plugins/<plugin-name>/
  .codex-plugin/plugin.json
```

Common repo-local plugin structure:

```text
plugins/<plugin-name>/
  .codex-plugin/plugin.json
  skills/
  references/
  README.md
  LICENSE
```

Only `plugin.json` belongs inside `.codex-plugin/`.

## Manifest Expectations

At minimum, the plugin manifest should identify the plugin and point at bundled components.

Recommended published-manifest fields:

- `name`
- `version`
- `description`
- `author`
- `homepage`
- `repository`
- `license`
- `keywords`
- `skills`
- `mcpServers`
- `apps`
- `interface`

Useful `interface` fields:

- `displayName`
- `shortDescription`
- `longDescription`
- `developerName`
- `category`
- `capabilities`
- `websiteURL`
- `privacyPolicyURL`
- `termsOfServiceURL`
- `defaultPrompt`
- `brandColor`

## Marketplace Registration

Register every installable repo plugin in:

- `.agents/plugins/marketplace.json`

Each plugin entry should include:

- `name`
- `source.source`
- `source.path`
- `policy.installation`
- `policy.authentication`
- `category`

Repo-local plugin entries should normally use:

- `source.source: "local"`
- `source.path: "./plugins/<plugin-name>"`
- `policy.installation: "AVAILABLE"`
- `policy.authentication: "ON_INSTALL"`

One marketplace file can contain one plugin or many. Add one object per plugin under `plugins[]`.

## Documentation Requirements

- Add a plugin-local `README.md` that explains what the plugin does.
- Keep any repository layout trees accurate.
- Do not claim files exist if they do not exist on disk.
- If the plugin is experimental or incomplete, say so explicitly.

## Validation Checklist

Before finishing:

- confirm `plugins/<plugin-name>/.codex-plugin/plugin.json` exists
- confirm all referenced paths in the manifest exist
- confirm `source.path` in `.agents/plugins/marketplace.json` resolves to the plugin directory
- confirm plugin `README.md` matches the actual filesystem layout
- read back `.agents/plugins/marketplace.json` after editing

## Codex App Behavior

This repository's marketplace is repo-scoped. Per Codex plugin docs, repo marketplaces live at `$REPO_ROOT/.agents/plugins/marketplace.json` and appear as selectable sources in the plugin directory.

That means after adding a plugin here and restarting Codex, the updated plugin list should be visible through this repository marketplace when the repo is open as a Codex project.

## References

- Build plugins: <https://developers.openai.com/codex/plugins/build>
- Create a plugin manually: <https://developers.openai.com/codex/plugins/build#create-a-plugin-manually>
- Marketplace metadata: <https://developers.openai.com/codex/plugins/build#marketplace-metadata>
- Plugin structure: <https://developers.openai.com/codex/plugins/build#plugin-structure>
