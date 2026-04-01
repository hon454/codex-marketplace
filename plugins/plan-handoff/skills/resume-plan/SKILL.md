---
name: resume-plan
description: Resume implementation in a fresh Codex session from the repo-local saved plan handoff. Use when the user asks to resume from plan handoff, implement the saved plan, or start from the latest handoff without reconstructing the prior session.
---

# Resume Plan

Resume implementation from the repository's saved handoff artifact and begin the work directly from that plan.

## Required behavior

1. Read `.codex/handoffs/latest-plan.md`.
2. Validate that the file contains all required sections:
   - `# Plan Handoff`
   - `## Starter Prompt`
   - `## Plan`
3. Validate that both the starter prompt and the plan body are present and non-empty.
4. If the file is missing, malformed, or empty, stop safely and tell the user to run `save-plan` again in the source session. Do not infer missing content.
5. Trust `.codex/handoffs/latest-plan.md` as the repository's canonical pointer.
6. Do not infer whether the handoff is stale. If the user updated the plan after the handoff was created, they must create a new handoff first.
7. Use the `## Starter Prompt` section as the execution instruction and proceed directly into implementation work. Do not prepend an extra recap unless the user asks for one.

## Execution rules

- Start implementing from the saved prompt and plan immediately after validation succeeds.
- Treat the handoff as plan-only context, not a full conversation restore.
- Do not add invented background context that is not present in the repository or the handoff file.

## Failure handling

- Missing file: ask for a new handoff to be prepared.
- Broken headings: ask for a new handoff to be prepared.
- Empty plan: ask for a new handoff to be prepared.
- Repository mismatch or missing supporting files: stop and explain the mismatch instead of guessing.
