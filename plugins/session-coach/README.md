# Session Coach

`session-coach` is a Codex plugin that helps users improve how they work with an AI coding agent.

It does not review code quality. It reviews the user's agent usage during the session and turns that into concrete next-step coaching.

## What It Does

This plugin exposes a single explicit skill:

- `session-coach`

The skill supports two behaviors behind the same entry point:

1. `preflight`: run a lightweight setup check before work starts
2. `retrospective`: analyze the current session and write a coaching report

If the user's request is ambiguous, the skill defaults to retrospective feedback.

## Plugin Layout

```text
session-coach/
  .codex-plugin/plugin.json
  assets/
    session-coach-small.svg
    session-coach.svg
  skills/
    session-coach/
      SKILL.md
      agents/
        openai.yaml
  references/
    evaluation-criteria.md
    report-template.md
  README.md
  LICENSE
```

## Workflow

### 1. Preflight

Use `$session-coach` before implementation when the user wants a quick setup check.

The skill should:

- check whether `AGENTS.md` exists
- look for project guidance quality in `AGENTS.md`
- check whether project Codex configuration such as `.codex/config.toml` exists
- respond in at most 3 short lines

The preflight is advisory only and must not block the user.

### 2. Retrospective

Use `$session-coach` after or during a session when the user wants feedback on how they used the agent.

The skill should:

- classify the session type
- analyze prompt quality, task decomposition, verification habits, and conversation flow efficiency
- identify anti-patterns only when there is conversation evidence
- include concrete alternative prompts
- write a detailed report to `.codex/coach/reports/YYYY-MM-DD-HHmm.md`
- print a concise terminal summary

## Constraints

- Evaluate only the user's direction of the agent.
- Do not turn the output into a code review.
- Do not evaluate the agent's quality.
- Do not assign scores or grades.
- Do not force findings when the session was already effective.

## Example Trigger Phrases

- `use $session-coach to check whether this repo is ready before we start`
- `use $session-coach to review how I used the agent in this session`
- `use $session-coach and tell me what I should prompt differently next time`

## License

MIT. See `LICENSE`.
