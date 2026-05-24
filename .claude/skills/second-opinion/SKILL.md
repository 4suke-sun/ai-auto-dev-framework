---
name: second-opinion
description: Use before merging complex or high-risk changes. Spawns a subagent to independently review the diff for correctness, security issues, test coverage, and convention violations. Use after self-review-checklist for extra assurance.
---

# Second Opinion Skill

## When to Use
- Changes touch security-sensitive code (auth, crypto, permissions)
- Diff is larger than 300 lines
- The change is architecturally significant
- You are unsure about a design decision

## Steps

1. Generate the diff:
   ```bash
   git diff main...HEAD
   ```

2. Spawn a review subagent with this prompt:
   ```
   Review the following diff independently. Check for:
   - Security vulnerabilities (injection, secrets, insecure defaults)
   - Logic errors or edge cases not covered by tests
   - Convention violations (Conventional Commits, TypeScript strict, Biome)
   - Missing or inadequate tests
   - License-incompatible dependencies
   
   Diff:
   <paste diff>
   
   Report findings as: [CRITICAL] / [WARNING] / [INFO]. Be terse.
   ```

3. Address all CRITICAL findings before merging.
4. Document WARNING findings in the PR description.

## Rules

- The subagent must not have access to the original implementation context.
- Never dismiss CRITICAL findings without human review.
