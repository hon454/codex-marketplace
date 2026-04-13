# Session Coach Report Template

Use this template in retrospective mode.

## Terminal Summary

Print a concise summary directly in the terminal.

```text
──────────────────────────────────
Session Coach Feedback
──────────────────────────────────
Session: [SESSION_TYPE]

Detected:
  [ANTI_PATTERN] - [where + what happened]
    -> [concrete alternative prompt]

Action Items:
  1. [highest impact improvement]
  2. [second highest improvement]

──────────────────────────────────
```

Rules:

- Omit the `Detected:` block if there are no anti-patterns worth calling out.
- Omit action item 2 if there is only one meaningful action item.
- Keep the terminal output compact and scannable.
- Do not claim a file was saved unless one was actually written.

## Detailed Markdown Report

Use this structure for the full inline feedback.
Save it to `.codex/coach/reports/YYYY-MM-DD-HHmm.md` only when the user explicitly asks to save the report.

```markdown
# Session Coach - Session Feedback

## Session Overview
- **Date**: [timestamp]
- **Type**: [classified session type]
- **Summary**: [one-line summary of what the session did]

## Anti-Patterns Detected

### [ANTI_PATTERN]
**Where**: [specific conversation moment]
**Impact**: [why this cost time, clarity, or verification quality]
**Alternative**:
> [concrete prompt the user could type next time]

## What Worked
- [evidence-backed strength]

## Action Items
1. [highest impact next improvement]
2. [second highest next improvement]
```

Rules:

- Omit `## Anti-Patterns Detected` if there are no evidence-backed problems.
- Omit `## What Worked` if there are no meaningful strengths to highlight.
- If there are no anti-patterns, explicitly say `No anti-patterns detected.` near the top and focus on strengths plus the next best refinement.
- Never invent sections beyond this template unless the user asks.
- After showing the inline report, a short offer to save it is acceptable, but file creation is opt-in.
