---
name: security-check
description: Use when adding dependencies, modifying auth/crypto code, or before any release. Runs gitleaks, npm audit, and reports CodeQL status. Required before merging security-sensitive changes.
---

# Security Check Skill

## When to Use
- Before merging changes that touch auth, crypto, or external API calls
- When adding new npm dependencies
- Periodically (at least once per sprint)

## Steps

### 1. Secret Scan
```bash
# Using gitleaks (must be installed)
gitleaks detect --source . --no-git 2>&1 || echo "gitleaks not installed, skipping"

# Manual pattern check
git diff HEAD~1 | grep -E 'AKIA[A-Z0-9]{16}|AIza[0-9A-Za-z]{35}|(ghp|gho|ghs)_[A-Za-z0-9]{36}' && echo "SECRET FOUND" || echo "Clean"
```

### 2. Dependency Audit
```bash
npm audit --audit-level=high
```
Fix or acknowledge all high/critical findings before proceeding.

### 3. License Check
```bash
npm run licenses
```
Ensure no GPL/AGPL licenses in production dependencies.

### 4. CodeQL
Check GitHub Actions → CodeQL workflow status for the branch.
All CodeQL alerts must be addressed before merge.

## Escalation
If a real secret is found in git history: stop, notify the human immediately. Do not attempt to rewrite history.
