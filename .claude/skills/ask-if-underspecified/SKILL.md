---
name: ask-if-underspecified
description: Use when the user's request is ambiguous, missing key details, or could be interpreted multiple ways. Generates a targeted question list to gather requirements before starting work. Always use this before plan when the goal is unclear.
---

# Ask If Underspecified Skill

## When to Use
When any of these apply:
- The request lacks acceptance criteria
- Multiple implementations are equally valid
- The scope is unclear (which files? which environments?)
- Security or data implications are not addressed
- The request contradicts existing conventions

## Steps

1. Identify the 1–5 most critical unknowns (not exhaustive — focus on blockers).
2. Format as numbered questions.
3. STOP and wait for answers before proceeding.

## Question Template

```
Before I start, I need to clarify a few things:

1. **[Topic]**: <specific question>?
2. **[Topic]**: <specific question>?
3. **[Topic]**: <specific question>?

(You can answer all at once or one by one.)
```

## Rules

- Maximum 5 questions per round.
- Do not ask questions whose answers are in the codebase — search first.
- Do not ask about style preferences when Biome/tsconfig already decide.
