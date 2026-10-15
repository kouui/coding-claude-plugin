# `gh pr` Command Reference

## gh pr view

Display PR details. **ALWAYS use `--json`.**

```
gh pr view [<number> | <url> | <branch>] [flags]
```

**Options:**
 `-c`, `--comments` — (WARNING: opens pager, use `--json comments` instead)
 `-q`, `--jq <expression>` — Filter JSON output using a jq expression
 `--json <fields>` — Output JSON with the specified fields
 `-t`, `--template <string>` — Format JSON output using a Go template
 `-R`, `--repo <[HOST/]OWNER/REPO>` — Select another repository

**Available `--json` fields:**
`additions`, `assignees`, `author`, `autoMergeRequest`, `baseRefName`, `body`, `changedFiles`, `closed`, `closedAt`, `comments`, `commits`, `createdAt`, `deletions`, `files`, `headRefName`, `headRepository`, `headRepositoryOwner`, `id`, `isCrossRepository`, `isDraft`, `labels`, `latestReviews`, `maintainerCanModify`, `mergeCommit`, `mergeStateStatus`, `mergeable`, `mergedAt`, `mergedBy`, `milestone`, `number`, `potentialMergeCommit`, `projectCards`, `projectItems`, `reactionGroups`, `reviewDecision`, `reviewRequests`, `reviews`, `state`, `statusCheckRollup`, `title`, `updatedAt`, `url`

## gh pr diff

View changes in a pull request.

```
gh pr diff [<number> | <url> | <branch>] [flags]
```

**Options:**
 `--color <string> (default "auto")` — {always|never|auto}
 `--patch` — Display diff in patch format
 `-R`, `--repo <[HOST/]OWNER/REPO>` — Select another repository

**Note:** `--name-only` is NOT a valid flag. Use `gh pr view <num> --json files --jq '.files[].path'` instead.

## gh pr comment

Add a comment to a PR. **MUST always provide `--body` or `--body-file`.**

```
gh pr comment [<number> | <url> | <branch>] [flags]
```

**Options:**
 `-b`, `--body <text>` — The comment body text (REQUIRED)
 `-F`, `--body-file <file>` — Read body text from file (use "-" for stdin)
 `--edit-last` — Edit the last comment of the current user
 `--delete-last` — Delete the last comment of the current user
 `--create-if-none` — Create a new comment if none found (use with --edit-last)
 `--yes` — Skip delete confirmation (use with --delete-last)
 `-R`, `--repo <[HOST/]OWNER/REPO>` — Select another repository

## gh pr create

Create a PR. **MUST always provide `--title` and `--body`.**

```
gh pr create [flags]
```

**Options:**
 `-t`, `--title <string>` — Title (REQUIRED)
 `-b`, `--body <string>` — Body (REQUIRED)
 `-F`, `--body-file <file>` — Read body from file
 `-B`, `--base <branch>` — Target branch
 `-H`, `--head <branch>` — Source branch (default: current)
 `-d`, `--draft` — Mark as draft
 `-f`, `--fill` — Use commit info for title and body
 `--fill-first` — Use first commit info
 `--fill-verbose` — Use commits msg+body for description
 `-a`, `--assignee <login>` — Assign people ("@me" for self)
 `-r`, `--reviewer <handle>` — Request reviews
 `-l`, `--label <name>` — Add labels
 `-m`, `--milestone <name>` — Add to milestone
 `-p`, `--project <title>` — Add to project
 `--no-maintainer-edit` — Disable maintainer edit
 `-T`, `--template <file>` — Template file for body
 `--dry-run` — Print details without creating
 `--recover <string>` — Recover from failed run
 `-R`, `--repo <[HOST/]OWNER/REPO>` — Select another repository

## gh pr edit

Edit a pull request.

```
gh pr edit [<number> | <url> | <branch>] [flags]
```

**Options:**
 `-t`, `--title <string>` — Set the new title
 `-b`, `--body <string>` — Set the new body
 `-F`, `--body-file <file>` — Read body from file
 `-B`, `--base <branch>` — Change base branch
 `--add-assignee <login>` — Add assigned users ("@me", "@copilot")
 `--remove-assignee <login>` — Remove assigned users
 `--add-reviewer <login>` — Add reviewers
 `--remove-reviewer <login>` — Remove reviewers
 `--add-label <name>` — Add labels
 `--remove-label <name>` — Remove labels
 `--add-project <title>` — Add to project
 `--remove-project <title>` — Remove from project
 `-m`, `--milestone <name>` — Edit milestone
 `--remove-milestone` — Remove milestone
 `-R`, `--repo <[HOST/]OWNER/REPO>` — Select another repository

## gh pr list

List PRs. Default: open only.

```
gh pr list [flags]
```

**Options:**
 `-s`, `--state <string> (default "open")` — {open|closed|merged|all}
 `-A`, `--author <string>` — Filter by author
 `-a`, `--assignee <string>` — Filter by assignee
 `-B`, `--base <string>` — Filter by base branch
 `-H`, `--head <string>` — Filter by head branch
 `-l`, `--label <strings>` — Filter by label
 `-d`, `--draft` — Filter by draft state
 `--app <string>` — Filter by GitHub App author
 `-S`, `--search <query>` — Search PRs
 `-L`, `--limit <int> (default 30)` — Max items to fetch
 `--json <fields>` — Output JSON
 `-q`, `--jq <expression>` — Filter JSON output
 `-R`, `--repo <[HOST/]OWNER/REPO>` — Select another repository

## gh pr review

Add a review to a PR. **MUST always provide a review type AND `--body`.**

```
gh pr review [<number> | <url> | <branch>] [flags]
```

**Options:**
 `-a`, `--approve` — Approve PR
 `-r`, `--request-changes` — Request changes
 `-c`, `--comment` — Comment only (no approve/reject)
 `-b`, `--body <string>` — Review body (REQUIRED)
 `-F`, `--body-file <file>` — Read body from file
 `-R`, `--repo <[HOST/]OWNER/REPO>` — Select another repository

## gh pr ready

Mark PR as ready for review.

```
gh pr ready [<number> | <url> | <branch>] [flags]
```

**Options:**
 `--undo` — Convert to draft
 `-R`, `--repo <[HOST/]OWNER/REPO>` — Select another repository

## gh pr status

Show status of relevant PRs.

```
gh pr status [flags]
```

**Options:**
 `-c`, `--conflict-status` — Show merge conflict status
 `--json <fields>` — Output JSON
 `-q`, `--jq <expression>` — Filter JSON output
 `-R`, `--repo <[HOST/]OWNER/REPO>` — Select another repository
