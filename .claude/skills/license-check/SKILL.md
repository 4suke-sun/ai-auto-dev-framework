---
name: license-check
description: Use when adding new npm or Python dependencies. Verifies license compatibility (no GPL/AGPL in production deps), updates THIRD_PARTY_LICENSES.json, and checks NOTICE file. Required before merging any dependency changes.
---

# License Check Skill

## When to Use
Before adding any new dependency to `package.json` or `requirements.txt`.

## Steps

1. **Check the license** of the package before installing:
   ```bash
   npm view <package-name> license
   ```

2. **Blocked licenses** (do not add):
   - GPL-2.0, GPL-3.0
   - AGPL-1.0, AGPL-3.0
   - LGPL (evaluate case-by-case, ask human)
   - Unlicensed / unknown

3. **After adding dependency**, update the license manifest:
   ```bash
   npm run licenses
   ```

4. **Verify `THIRD_PARTY_LICENSES.json`** was updated correctly.

5. **Update `NOTICE`** if a new package requires attribution.

## Allowed Licenses
MIT, Apache-2.0, BSD-2-Clause, BSD-3-Clause, ISC, CC0-1.0, 0BSD, Unlicense (case-by-case)
