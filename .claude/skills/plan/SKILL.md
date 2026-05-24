---
name: plan
description: Use before starting any non-trivial task. Drafts requirements and acceptance criteria from the user's request, then waits for human approval before implementation begins. Required for tasks that touch multiple files, introduce new dependencies, or carry security implications.
---

# Plan Skill

## When to Use
Run this skill before implementing any non-trivial feature, fix, or refactor.

## Steps

1. **Restate the goal** — Summarize what the user is asking for in 1–2 sentences.
2. **Draft acceptance criteria** — List concrete, testable conditions that define "done".
3. **Identify scope** — List files and modules that will change.
4. **Flag risks** — Note any security, performance, or breaking-change concerns.
5. **Propose implementation plan** — Step-by-step ordered list.
6. **STOP and wait for human approval** — Do not write code until the user confirms the plan.

## Output Format

```
## Goal
<one-sentence summary>

## Acceptance Criteria
- [ ] <criterion 1>
- [ ] <criterion 2>

## Scope
- <file/module>: <what changes>

## Risks
- <risk or "None">

## Plan
1. <step>
2. <step>
```

Awaiting approval. Reply "approved" or provide corrections.
