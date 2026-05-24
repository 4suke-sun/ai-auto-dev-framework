---
name: self-review-checklist
description: Run before completing any task. Verifies tests pass, coverage meets threshold, no secrets committed, license check clean, commit messages follow Conventional Commits, and PR template is filled. Use this skill before pushing or creating a PR.
---

# Self-Review Checklist Skill

## When to Use
Before pushing any branch or creating a PR.

## Checklist

Run each command and verify it passes:

```bash
npm run lint          # Biome lint — must be green
npm run typecheck     # tsc --noEmit — must be green
npm run test          # All tests pass
npm run test:coverage # Coverage >= lines 50% / branches 40%
npm run build         # Build succeeds
```

Then verify:

- [ ] No secrets in `git diff HEAD~1` (no AKIA*, sk-*, ghp_*, PEM headers)
- [ ] All commits follow Conventional Commits (`git log --oneline`)
- [ ] No files outside approved scope were modified
- [ ] `THIRD_PARTY_LICENSES.json` is up to date if dependencies changed
- [ ] PR template is fully filled (no placeholder text)

## If Anything Fails

Stop. Do not push. Fix the issue first, then re-run this checklist.
