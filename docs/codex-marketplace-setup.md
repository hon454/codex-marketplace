# Codex Marketplace Setup

## Goal

Make this repository open cleanly in the Codex app as a shared marketplace repository for local plugin work.

## How To Use This Document

- Read `README.md` first for the short operational summary.
- Use this document for the setup rationale and Codex app behavior.
- Use `docs/adding-a-plugin.md` for plugin creation and marketplace-entry changes.
- Use `AGENTS.md` for repository editing rules while making those changes.

## Repository Conventions

- Marketplace catalog: `.agents/plugins/marketplace.json`
- Shared Codex config: `.codex/config.toml`
- Repository instructions: `AGENTS.md`

## Why This Works

Official Codex docs state:

- project-scoped config can live in `.codex/config.toml`
- Codex loads project-scoped config only for trusted projects
- Team Config checked into `.codex/` is automatically picked up when a user opens that repository

Within the local Codex plugin scaffolding/spec used for plugin creation, the marketplace catalog path is standardized as:

- `<repo-root>/.agents/plugins/marketplace.json`

That means this repository is configured around two stable entry points:

1. `.codex/config.toml` so Codex recognizes repo-scoped shared configuration
2. `.agents/plugins/marketplace.json` so Codex plugin tooling has the expected marketplace catalog location

## References

- Codex config reference: <https://developers.openai.com/codex/config-reference/>
- Codex Team Config / admin setup: <https://developers.openai.com/codex/enterprise/admin-setup/#step-4-standardize-local-configuration-with-team-config>
- Codex local environments: <https://developers.openai.com/codex/app/local-environments/>

## Steps In Codex App

1. Open the repository root: `D:\codex-marketplace`
2. Trust the project
3. Start a new local thread, or reopen the project if it was already open before trust was granted
4. Work from the repository root so Codex sees:
   - `.codex/config.toml`
   - `.agents/plugins/marketplace.json`
   - `AGENTS.md`

## Verification

You should be able to verify the setup by checking:

- Codex is operating in the repository root
- project-scoped `.codex/config.toml` is present
- the marketplace catalog exists at `.agents/plugins/marketplace.json`
- plugin entries point to local plugin paths like `./plugins/<plugin-name>`

## Notes

- Trust is per-user local state, so it cannot be fully enforced from inside the repository.
- If Codex does not seem to pick up the repository config, the most likely cause is that the project is not trusted yet or the repo was already open before the config existed.
- `README.md` gives the short version; `AGENTS.md` gives editing rules; `docs/adding-a-plugin.md` gives the plugin-addition workflow; this document explains the setup logic.
