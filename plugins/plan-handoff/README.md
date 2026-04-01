# Plan Handoff

`plan-handoff` is a public Codex plugin that recreates the feel of "implement in new thread" without native thread creation.

It does this with exactly two instruction-only skills:

- `save-plan`
- `resume-plan`

## What it does

This plugin is not a full session restore system.

It is a latest-plan-only handoff workflow:

1. In the source session, save the latest `<proposed_plan>` into the repository.
2. In a fresh session, read that saved handoff and immediately start implementing from it.

v1 defaults:

- marketplace-first
- standalone public repo
- repo-local handoff
- latest pointer plus archive
- fresh-session auto-implement

## Repository layout

The marketplace catalog for this plugin lives at the repository root in `.agents/plugins/marketplace.json`.
The plugin package itself lives under `plugins/plan-handoff/` and contains the files below.

```text
plan-handoff/
  .codex-plugin/plugin.json
  assets/plan-handoff-small.svg
  assets/plan-handoff.svg
  skills/save-plan/assets/save-plan-small.svg
  skills/save-plan/assets/save-plan.svg
  skills/save-plan/SKILL.md
  skills/save-plan/agents/openai.yaml
  skills/resume-plan/assets/resume-plan-small.svg
  skills/resume-plan/assets/resume-plan.svg
  skills/resume-plan/SKILL.md
  skills/resume-plan/agents/openai.yaml
  references/handoff-format.md
  README.md
  LICENSE
```

## Workflow

### 1. Prepare in the source session

Use `save-plan` when the current session already contains a valid `<proposed_plan>` block and you want to save it for the next session.

The skill must:

- find the last `<proposed_plan>` block in the current session
- write `.codex/handoffs/latest-plan.md`
- also write `.codex/handoffs/archive/YYYYMMDDTHHMMSSZ-plan.md`

If there is no valid `<proposed_plan>`, it must fail safely instead of inventing one.

### 2. Resume in a fresh session

Use `resume-plan` in a fresh session to read `.codex/handoffs/latest-plan.md` and begin implementation immediately from the saved starter prompt.

If the file is missing, malformed, or empty, it must stop and ask for a new handoff instead of guessing.

## Important constraints

- This plugin does not restore the whole previous conversation.
- The canonical input is always `.codex/handoffs/latest-plan.md`.
- The archive exists for recovery, not as the default resume target.
- If the plan changes later, run `save-plan` again before resuming.
- Do not put secrets or sensitive information into the saved plan.

## Example trigger phrases

- Prepare:
  - `save this plan for next session`
  - `prepare a plan handoff`
  - `handoff the latest plan`
- Resume:
  - `resume from plan handoff`
  - `implement the saved plan`
  - `start from latest handoff`

## License

MIT. See `LICENSE`.


