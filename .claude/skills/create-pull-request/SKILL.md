---
name: create-pull-request
description: Use when creating a GitHub pull request. Fills the PR template, verifies CI is likely to pass, and runs gh pr create. Never merge the PR — that is the human reviewer's job.
---

# Create Pull Request Skill

## When to Use
After pushing a branch and before asking the user to review.

## Pre-flight Checks

1. Run `self-review-checklist` skill first.
2. Confirm branch is pushed: `git push -u origin <branch>`.
3. Confirm CI would pass locally: `npm run lint && npm run typecheck && npm run test && npm run build`.

## PR Body Template

```
## 変更内容
<what changed>

## 変更理由
<why this change is needed>

## テスト方法
<how to verify the change>

## 影響範囲
<what else might be affected>

## ロールバック手順
<how to revert if needed>

## チェックリスト
- [ ] テストが全て通過
- [ ] lint/typecheck グリーン
- [ ] secrets なし
- [ ] ライセンス互換性確認済み
- [ ] CLAUDE.md の規約に準拠
```

## Create PR

```bash
gh pr create --base main --title "<type>: <description>" --body "$(cat <<'EOF'
<filled template>
EOF
)"
```

## Rules

- **Never merge** — human reviewer merges only.
- Set at least 1 required reviewer.
- Title follows Conventional Commits format.
