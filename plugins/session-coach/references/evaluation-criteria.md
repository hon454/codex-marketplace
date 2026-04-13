# Session Coach Evaluation Criteria

Use this document for retrospective mode only.

## Session Types

Classify the session into one of these types before writing feedback.

| Session Type | Primary Dimensions | Secondary Dimensions |
|---|---|---|
| Exploration / Investigation | Prompt Quality, Conversation Flow Efficiency | — |
| Bug Fix | Verification Habits, Conversation Flow Efficiency | Prompt Quality |
| Feature Implementation | Task Decomposition, Verification Habits | Prompt Quality |
| Refactoring | Verification Habits, Prompt Quality | Task Decomposition |

Use this weighting to decide which findings deserve space first. Do not calculate scores.

## Dimension 1: Prompt Quality

Principle: A strong prompt gives enough context for autonomous progress without micro-piloting every implementation step.

Evaluate:

- Intent clarity
- Abstraction level
- Reference points
- Adaptive refinement

Anti-patterns:

| Name | Description |
|---|---|
| Blank Target | The request is vague and does not define a clear goal. |
| Micro-Pilot | The user dictates implementation details instead of delegating meaningful autonomy. |
| Parrot Retry | The user repeats a failed prompt without changing the framing. |
| Groundless Ask | The user requests work without relevant project context, files, or patterns. |

## Dimension 2: Task Decomposition

Principle: A task should be sized so the agent can complete it accurately and the user can verify it without guesswork.

Evaluate:

- Unit appropriateness
- Ordering
- Plan-first behavior
- Scope control

Anti-patterns:

| Name | Description |
|---|---|
| Whole Pizza | The user asks for too much in one pass, leaving no natural verification points. |
| Dust Grain | The user splits work into tiny steps that waste round trips. |
| Scope Creep | New unrelated requirements keep arriving mid-task. |
| Planless Sprint | The user jumps straight into implementation when design discussion would help. |

## Dimension 3: Verification Habits

Principle: Verification should happen after each meaningful work unit, not only at the very end.

Evaluate:

- Verification frequency
- Verification diversity
- Failure response
- Regression awareness

Anti-patterns:

| Name | Description |
|---|---|
| Blind March | The user keeps moving forward without checking the previous result. |
| Final Boss | The first meaningful verification happens only after all implementation is done. |
| Blind Trust | The user accepts the agent's claims without checking artifacts or outputs. |
| Symptom Fix | The user says "fix it" repeatedly without investigating root cause. |

## Dimension 4: Conversation Flow Efficiency

Principle: Use the context window deliberately and reach the goal with fewer unnecessary turns.

Evaluate:

- Round-trip efficiency
- Information delivery
- Failure recovery strategy
- Session awareness

Anti-patterns:

| Name | Description |
|---|---|
| Info Drip | Context that could be provided once is spread over many turns. |
| Infinite Loop | The same failed approach is retried three or more times. |
| Context Burnout | The session keeps growing long after a fresh session would help. |
| Manual March | Independent work is requested sequentially even though it could be grouped. |

## Evidence Rules

- Every finding must point to a specific moment in the session.
- Use direct conversation evidence, not inferred personality traits.
- If a dimension has no evidence-backed issue, skip it.
- Strengths should also be evidence-backed.

## Language Rules

- Keep file headings, anti-pattern names, and structural labels in English.
- Write explanations, alternatives, and action items in the user's conversation language when it is clear.
- If the conversation language is mixed or unclear, follow the system locale.

## Scope Rules

- Evaluate only how the user directed the agent.
- Do not turn this into a code review.
- Do not critique the agent's internal quality.
- Do not assign numeric scores or grades.
