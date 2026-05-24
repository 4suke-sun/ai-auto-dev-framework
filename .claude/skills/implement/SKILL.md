---
name: implement
description: Use during the implementation phase. Enforces test-first approach, strict scope adherence, Biome formatting, and TypeScript strict mode compliance. Run after plan is approved.
---

# Implement Skill

## When to Use
After `plan` skill approval, when writing code.

## Rules

- **Test first**: Write or update tests before changing production code.
- **Scope**: Only modify files identified in the approved plan.
- **TypeScript**: `strict: true`, no `any`, no `@ts-ignore`.
- **Format**: Run `npm run check` after every file edit.
- **No secrets**: Never hardcode credentials; use environment variables.
- **No premature abstraction**: Three duplications minimum before extracting.
- **Comments**: Only for non-obvious WHY, never WHAT.

## Checklist Before Marking Done

- [ ] All new/modified code has corresponding tests
- [ ] `npm run typecheck` passes
- [ ] `npm run lint` passes
- [ ] No secrets or PII in changed files
- [ ] Only planned-scope files were modified
