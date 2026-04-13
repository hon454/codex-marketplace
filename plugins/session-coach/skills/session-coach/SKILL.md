---
name: session-coach
description: Review how the user used the agent in the current Codex session and provide actionable coaching. Use when the user asks for session feedback, wants to improve prompting or task decomposition, asks how they could have used the agent better, or wants a quick preflight check of AGENTS.md and Codex project setup before starting work.
---

# Session Coach

Coach the user on how they directed the agent, not on code quality and not on the agent's quality.

## Mode Selection

Choose one of two modes from the user's request.

- `preflight`: use when the user asks to prepare, check setup, or get ready before starting work
- `retrospective`: use when the user asks for feedback, analysis, review, or improvement advice about the session

If the request is ambiguous, default to `retrospective`.

## Preflight

Run a lightweight project-health check only.

1. Check whether `AGENTS.md` exists.
2. If `AGENTS.md` exists, check whether it covers:
   - project purpose or architecture
   - coding conventions or style rules
   - key directories or entry points
3. Check whether project Codex configuration such as `.codex/config.toml` exists.
4. Return at most 3 short lines.

Preflight rules:

- Advisory only. Never block the user from proceeding.
- If `AGENTS.md` is missing, say project context would help the agent.
- If `AGENTS.md` is thin, suggest only the most useful missing sections.
- If setup looks healthy, confirm briefly and stop.
- Do not write files in `preflight`.

## Retrospective

Read `../../references/evaluation-criteria.md` before analyzing the session.
Read `../../references/report-template.md` before formatting the output.

1. Classify the session as Exploration, Bug Fix, Feature Implementation, or Refactoring.
2. Review only these dimensions:
   - Prompt Quality
   - Task Decomposition
   - Verification Habits
   - Conversation Flow Efficiency
3. Use the session type to prioritize which dimensions matter most.
4. Identify named anti-patterns only when there is specific conversation evidence.
5. For every improvement, include:
   - where it happened
   - why it mattered
   - a concrete alternative prompt the user could type next time
6. Include strengths only when they are genuinely supported by the session.
7. Limit action items to the highest-impact 2.
8. Show the full feedback inline in the current session using the report structure.
9. Also print a concise terminal summary.
10. Save the report to `.codex/coach/reports/YYYY-MM-DD-HHmm.md` only if the user explicitly asks to save it.

## Guardrails

- Every finding must cite a specific moment from the conversation.
- Do not speculate or generalize beyond the evidence.
- Do not grade, score, or rank the user.
- Do not evaluate code quality.
- Do not evaluate agent performance.
- Do not force findings in every dimension.
- If there are no anti-patterns worth calling out, say so plainly and emphasize strengths plus the next best refinement.
- Do not write a report file by default.
- After showing the feedback, you may briefly mention that you can save it if the user wants.

## References

- Use `../../references/evaluation-criteria.md` for dimensions, anti-pattern names, weighting guidance, and language rules.
- Use `../../references/report-template.md` for the terminal summary and Markdown report structure.
