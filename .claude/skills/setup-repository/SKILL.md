---
name: setup-repository
description: テンプレートから作成した新規リポジトリの初期設定を行う。GitHub Settings（Code Scanning、ブランチ保護、Auto-merge）を gh CLI で自動構成する。テンプレート利用直後に1回だけ実行すること。
---

# リポジトリ初期設定スキル

## 使用タイミング
テンプレートからリポジトリを作成した直後に1回だけ実行する。

## 前提条件
- `gh` CLI がインストール済みで認証済みであること
- リポジトリの admin 権限を持っていること

## 手順

### 1. リポジトリ情報の取得

```bash
# リポジトリのオーナー/名前を取得
gh repo view --json nameWithOwner -q '.nameWithOwner'
```

以降のコマンドで `OWNER/REPO` として使用する。

### 2. Code Scanning（CodeQL）の有効化

```bash
# デフォルトセットアップで CodeQL を有効化
gh api -X PATCH /repos/OWNER/REPO/code-scanning/default-setup \
  -f state=configured \
  -f languages[]="javascript-typescript"
```

> **注意:** Free プランのプライベートリポでは Advanced Security が必要なため失敗する場合がある。その場合はスキップして問題ない。

### 3. ブランチ保護ルールの設定

```bash
gh api -X PUT /repos/OWNER/REPO/branches/main/protection \
  --input - << 'EOF'
{
  "required_status_checks": {
    "strict": true,
    "contexts": ["Lint", "Typecheck", "Test & Coverage", "Build"]
  },
  "enforce_admins": true,
  "required_pull_request_reviews": {
    "dismiss_stale_reviews": true,
    "require_code_owner_reviews": true,
    "required_approving_review_count": 1
  },
  "restrictions": null,
  "required_linear_history": true,
  "allow_force_pushes": false,
  "allow_deletions": false
}
EOF
```

### 4. Auto-merge の有効化

```bash
gh repo edit OWNER/REPO --enable-auto-merge
```

### 5. Dependabot の有効化確認

```bash
# Dependabot が有効か確認（dependabot.yml が存在すれば自動で有効）
gh api /repos/OWNER/REPO/vulnerability-alerts -X PUT
```

### 6. 設定確認

```bash
# ブランチ保護の確認
gh api /repos/OWNER/REPO/branches/main/protection --jq '{
  required_checks: .required_status_checks.contexts,
  enforce_admins: .enforce_admins.enabled,
  required_reviews: .required_pull_request_reviews.required_approving_review_count,
  linear_history: .required_linear_history.enabled
}'
```

## 完了条件

- [ ] CodeQL が有効（またはプライベートリポのためスキップ）
- [ ] main ブランチに保護ルールが設定されている
- [ ] Auto-merge が有効
- [ ] Dependabot アラートが有効
- [ ] `gh api /repos/OWNER/REPO/branches/main/protection` でルールが確認できる

## エラー時の対応

| エラー | 原因 | 対処 |
|--------|------|------|
| `Resource not accessible by integration` | トークンの権限不足 | `gh auth refresh -s admin:org,repo` で再認証 |
| `Not Found` | リポが存在しない or admin 権限なし | リポ名とアクセス権を確認 |
| `Advanced Security must be enabled` | Free プランのプライベートリポ | CodeQL 設定をスキップ、または public にする |
