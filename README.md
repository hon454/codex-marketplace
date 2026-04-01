# Codex Marketplace

A curated marketplace repository for installable Codex plugins.

## What This Repository Is

This repository contains marketplace metadata for Codex plugins.

It is intentionally separate from individual plugin repositories so plugins can be versioned, released, and maintained independently.

## Structure

```text
codex-marketplace/
  .agents/plugins/marketplace.json
  .gitignore
  LICENSE
  README.md
```

## Marketplace Scope

- Codex marketplace metadata only
- Plugin entries that point to independently managed plugin repositories
- No plugin implementation source in this repository by default

## Usage

Use `.agents/plugins/marketplace.json` as the catalog source for installable Codex plugins.
