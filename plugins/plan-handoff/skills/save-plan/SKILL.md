---
name: save-plan
description: Save the latest proposed implementation plan from the current Codex session into a repo-local handoff file for a fresh follow-up session. Use when the user asks to save this plan for next session, prepare a plan handoff, or hand off the latest plan without restoring the full session.
shortDescription: Save the latest proposed plan into a repo-local handoff.
iconSmall: ./assets/save-plan-small.svg
iconLarge: ./assets/save-plan.svg
---

# Save Plan

Capture the current session's latest implementation plan into the repository as a minimal handoff artifact.

## Required behavior

1. Search the current session history for `<proposed_plan>` blocks.
2. Treat only the last `<proposed_plan>` block in the current session as the latest valid plan.
3. If no `<proposed_plan>` block exists, or if the latest block is ambiguous or empty, stop and say that no valid latest proposed plan is available. Do not infer or rewrite a plan from nearby discussion.
4. Create the handoff directory structure if it does not exist:
   - `.codex/handoffs/`
   - `.codex/handoffs/archive/`
5. Write the canonical pointer file to `.codex/handoffs/latest-plan.md`.
6. Also write a timestamped archive copy to `.codex/handoffs/archive/YYYYMMDDTHHMMSSZ-plan.md`.
7. Use UTC in the archive filename.
8. Follow the exact handoff format in `../../references/handoff-format.md`.

## Handoff content rules

- Include exactly these sections in the handoff file:
  - `# Plan Handoff`
  - `## Starter Prompt`
  - `## Plan`
- Do not add status summaries, file inventories, risk logs, assumptions, extra commentary, or reconstructed context.
- Use this exact starter prompt text:

```text
Implement the following plan in this repository.
Plan:
[LAST_PROPOSED_PLAN_TEXT]
```

- Replace `[LAST_PROPOSED_PLAN_TEXT]` with the exact text content from the latest `<proposed_plan>` block.

## Output expectations

- Confirm the two paths written:
  - `.codex/handoffs/latest-plan.md`
  - `.codex/handoffs/archive/YYYYMMDDTHHMMSSZ-plan.md`
- Briefly remind the user that a fresh session can now use `resume-plan`.

## Safety rules

- Do not claim freshness beyond "latest pointer in this repository".
- Do not silently continue if the plan is missing or malformed.
- Do not include secrets or encourage storing sensitive information in the plan.
