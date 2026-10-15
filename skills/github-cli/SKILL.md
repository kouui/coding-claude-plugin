---
name: github-cli
description: Guide for using GitHub CLI (`gh`) commands correctly in non-interactive terminals. Use when executing `gh pr`, `gh issue`, or `gh api` commands via Bash. Prevents common failures (pager hang, editor hang, invalid flags) by enforcing `--json` output, required `--body` parameters, and correct flag usage. Covers pull request operations (view, create, diff, comment, review, edit, list), issue operations (view, create, comment, edit, list), and `gh api` for advanced REST API access.
---

# GitHub CLI for Non-Interactive Terminals

## Critical Rules

Claude Code runs in a **non-interactive terminal** (no TTY). These rules prevent hangs:

1. **ALWAYS use `--json <fields>`** with `gh pr view` and `gh issue view` — plain output opens a pager which hangs
2. **ALWAYS provide `--body`** for `gh pr comment`, `gh pr review`, `gh issue comment` — omitting it opens an editor which hangs
3. **NEVER use** `--editor`, `--web`, or `--watch` flags — they require interactive input
4. **ALWAYS provide `--title` and `--body`** for `gh pr create` and `gh issue create` — omitting them opens interactive prompts

```bash
# CORRECT
gh pr view <num> --json title,body,comments,reviews
gh issue view <num> --json title,body,comments
gh pr comment <num> --body "comment text"

# WRONG - will hang
gh pr view <num>
gh pr view <num> --comments
gh issue view <num>
gh pr comment <num>
gh pr create
```

## Common Mistakes

| Mistake | Why It Fails | Correct Command |
|---------|-------------|----------------|
| `gh pr view <num>` | Opens pager | `gh pr view <num> --json title,body,comments,reviews` |
| `gh pr view <num> --comments` | Opens pager | `gh pr view <num> --json comments` |
| `gh issue view <num>` | Opens pager | `gh issue view <num> --json title,body,comments` |
| `gh pr diff <num> --name-only` | Invalid flag | `gh pr view <num> --json files --jq '.files[].path'` |
| `gh api repos/{owner}/{repo}/...` | Placeholder not resolved | Use actual owner/repo values |

## Cross-Repo Operations

When not in the target repo's directory, use `-R` flag:

```bash
gh pr view 123 -R owner/repo --json title,body
gh issue view 456 -R owner/repo --json title,body,comments
```

## Command Reference

For detailed flags and options for each command, see the reference files:

- **PR commands** (`view`, `diff`, `comment`, `create`, `edit`, `list`, `review`, `ready`, `status`): See [references/gh-pr.md](references/gh-pr.md)
- **Issue commands** (`view`, `list`, `comment`, `create`, `edit`): See [references/gh-issue.md](references/gh-issue.md)
- **API commands** (REST API endpoints for advanced operations): See [references/gh-api.md](references/gh-api.md)
