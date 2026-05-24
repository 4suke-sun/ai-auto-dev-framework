---
name: git-commit
description: Use before every git commit. Verifies staged changes pass lint, typecheck, and secret scan, then writes a Conventional Commits message. Never use git commit --amend.
---

# Git Commit Skill

## When to Use
Before running `git commit`.

## Steps

1. Run `npm run lint` — fix any errors before proceeding.
2. Run `npm run typecheck` — fix any errors before proceeding.
3. Run `git diff --cached` — verify only intended files are staged.
4. Check for secrets: no AKIA*, sk-*, ghp_*, PEM headers in diff.
5. Write commit message following Conventional Commits:
   ```
   type(scope): description
   
   [optional body]
   ```
   Types: `feat` `fix` `chore` `refactor` `docs` `test` `style` `ci` `perf`
6. Commit: `git commit -m "$(cat <<'EOF'\n<message>\nEOF\n)"`

## Rules

- One logical change per commit.
- Never use `--amend` on published commits.
- Never skip hooks (`--no-verify`).
- If secret detected in staged changes → unstage, remove secret, re-stage.
