# ai-auto-dev-framework

Auto-mode safe development framework for Claude Code — a set of conventions, hooks, skills, and CI gates that make running Claude Code in auto-mode nearly risk-free.

Use this repository as a template when starting a new project that relies on Claude Code for automated development.

## What's Included

| Layer | Location | Purpose |
|-------|----------|---------|
| Guard hooks | `.claude/hooks/` | Block dangerous operations in real time |
| Skills | `.claude/skills/` | Structured workflows with human approval gates |
| CI workflows | `.github/workflows/` | Automated quality and security gates |
| devcontainer | `.devcontainer/` | Isolated, reproducible dev environment |
| Agent guides | `docs/agent-guides/` | Detailed instructions for each phase |

## Quick Start

### As a Template

1. Click **Use this template** on GitHub, or:
   ```bash
   gh repo create my-project --template 4sukeSuzuki/ai-auto-dev-framework --private
   ```
2. Clone and install:
   ```bash
   git clone https://github.com/<you>/my-project
   cd my-project
   npm install
   ```
3. Open in devcontainer (optional but recommended):
   ```
   VS Code → Reopen in Container
   ```
4. Start a Claude Code session and follow `CLAUDE.md`.

### Verify Setup

```bash
npm run lint         # Biome lint
npm run typecheck    # TypeScript strict check
npm run test         # Vitest
npm run build        # Compile
```

All four must be green before any push.

## Key Conventions

- **Secrets**: Never hardcode. Use `.env`. Three hook layers enforce this.
- **Commits**: [Conventional Commits](https://www.conventionalcommits.org/) — `type(scope): description`
- **Branches**: GitHub Flow — short-lived feature branches, squash merge to `main`.
- **Coverage**: Lines ≥50% / Branches ≥40% (raises quarterly).
- **Merges**: Human-only. AI never merges PRs.

## Human-in-the-Loop Gates

Auto-mode stops at these points and waits for human approval:

1. Plan approval before implementation
2. Authentication (gh, cloud CLIs)
3. CLAUDE.md review after creation
4. Any CI failure
5. PR merge (always human)
6. Branch protection verification

See [docs/agent-guides/hitl-gates.md](docs/agent-guides/hitl-gates.md) for details.

## Security

- `scan-secrets.sh` — blocks secrets in prompts (UserPromptSubmit)
- `scan-commit.sh` — blocks secrets in staged changes (PreToolUse)
- `block-dangerous-git.sh` — blocks force-push, reset --hard, etc.
- `prompt-injection-defender.sh` — warns on injection patterns in tool output
- `check-package-hallucination.sh` — verifies packages exist before install
- `gitleaks` — full history scan in CI

## License

MIT — see [LICENSE](LICENSE).

Third-party licenses: [THIRD_PARTY_LICENSES.json](THIRD_PARTY_LICENSES.json)
