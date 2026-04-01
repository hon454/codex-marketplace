# Handoff Format

This document is the single source of truth for the plan handoff file format used by this plugin.

## Required file shape

Every handoff file must contain exactly these sections, in this order:

```md
# Plan Handoff

## Starter Prompt
Implement the following plan in this repository.
Plan:
[LAST_PROPOSED_PLAN_TEXT]

## Plan
[LAST_PROPOSED_PLAN_TEXT]
```

## Rules

- `# Plan Handoff` must be the document title.
- `## Starter Prompt` must contain the exact fixed prompt prefix:

```text
Implement the following plan in this repository.
Plan:
```

- The plan text inserted under `## Starter Prompt` must match the latest `<proposed_plan>` content exactly.
- `## Plan` must repeat the exact same latest `<proposed_plan>` content.
- Do not add other sections such as status, file lists, progress logs, risks, or reconstructed context.
