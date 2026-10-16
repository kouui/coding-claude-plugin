# coding-claude-plugin

A small development-workflow plugin, trimmed from `kouui/cc-plugin-mycode`.

## Skills

| Skill | Use |
| --- | --- |
| `task:prepare-implementation` | Before coding: create `docs/tasks/<task>/task.md` and `plan.md` from the templates in the skill folder, then commit |
| `github:create-pr` | Create a GitHub pull request |
| `code-general-review` | Review code like a human (`/coding:code-general-review`) |
| `report-review` | Review a report for readability by its intended reader and for well-supported claims (`/coding:report-review <report-file-path>`) |
| `github-cli` | Rules for running `gh pr`, `gh issue` and `gh api` in a non-interactive terminal (no pager, no editor, `--json` output) |

## Agents

| Agent | Use |
| --- | --- |
| `architecture-reviewer` | Review a design or structure |
| `brainstormer` | Explore options before deciding |
| `code-reviewer` | Review code for quality, bugs and standards |
| `plan-reviewer` | Review an implementation plan |

## Install

```bash
claude plugin marketplace add kouui/magic-claude-code-plugin
claude plugin install coding@magic-claude-code-plugin -s user
```

## Notes

- The skill folders are named `task-prepare-implementation` and `github-create-pr`, because Windows file names cannot hold `:`; the same applies to `code-general-review` and `report-review`. The plugin names a skill after its folder, so they are called `/coding:task-prepare-implementation` and `/coding:github-create-pr`; the `name:` line inside each `SKILL.md` is not used for that.
- `github-cli` needs the GitHub CLI (`gh`) on `PATH`.

## Layout

```text
.claude-plugin/plugin.json
skills/task-prepare-implementation/   # SKILL.md, plan.md, task.md
skills/github-create-pr/SKILL.md
skills/code-general-review/SKILL.md
skills/report-review/SKILL.md
skills/github-cli/                    # SKILL.md, references/gh-{api,issue,pr}.md
agents/{architecture-reviewer,brainstormer,code-reviewer,plan-reviewer}.md
```
