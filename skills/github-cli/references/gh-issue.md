# `gh issue` Command Reference

## gh issue view

Display issue details. **ALWAYS use `--json`.**

```
gh issue view {<number> | <url>} [flags]
```

**Options:**
 `-c`, `--comments` — (WARNING: opens pager, use `--json comments` instead)
 `-q`, `--jq <expression>` — Filter JSON output
 `--json <fields>` — Output JSON with the specified fields
 `-t`, `--template <string>` — Format JSON output
 `-R`, `--repo <[HOST/]OWNER/REPO>` — Select another repository

**Available `--json` fields:**
`assignees`, `author`, `body`, `closed`, `closedAt`, `comments`, `createdAt`, `id`, `labels`, `milestone`, `number`, `projectCards`, `projectItems`, `reactionGroups`, `state`, `title`, `updatedAt`, `url`

## gh issue list

List issues. Default: open only.

```
gh issue list [flags]
```

**Options:**
 `-s`, `--state <string> (default "open")` — {open|closed|all}
 `-A`, `--author <string>` — Filter by author
 `-a`, `--assignee <string>` — Filter by assignee
 `-l`, `--label <strings>` — Filter by label
 `-S`, `--search <query>` — Search issues
 `-L`, `--limit <int> (default 30)` — Max items to fetch
 `--json <fields>` — Output JSON
 `-q`, `--jq <expression>` — Filter JSON output
 `-R`, `--repo <[HOST/]OWNER/REPO>` — Select another repository

## gh issue comment

Add a comment to an issue. **MUST always provide `--body` or `--body-file`.**

```
gh issue comment {<number> | <url>} [flags]
```

**Options:**
 `-b`, `--body <text>` — Comment body text (REQUIRED)
 `-F`, `--body-file <file>` — Read body from file
 `--edit-last` — Edit the last comment
 `-R`, `--repo <[HOST/]OWNER/REPO>` — Select another repository

## gh issue create

Create an issue. **MUST always provide `--title` and `--body`.**

```
gh issue create [flags]
```

**Options:**
 `-t`, `--title <string>` — Title (REQUIRED)
 `-b`, `--body <string>` — Body (REQUIRED)
 `-F`, `--body-file <file>` — Read body from file
 `-a`, `--assignee <login>` — Assign people ("@me" for self)
 `-l`, `--label <name>` — Add labels
 `-m`, `--milestone <name>` — Add to milestone
 `-R`, `--repo <[HOST/]OWNER/REPO>` — Select another repository

## gh issue edit

Edit an issue.

```
gh issue edit {<number> | <url>} [flags]
```

**Options:**
 `-t`, `--title <string>` — Set new title
 `-b`, `--body <string>` — Set new body
 `--add-assignee <login>` — Add assigned users
 `--remove-assignee <login>` — Remove assigned users
 `--add-label <name>` — Add labels
 `--remove-label <name>` — Remove labels
 `-R`, `--repo <[HOST/]OWNER/REPO>` — Select another repository
