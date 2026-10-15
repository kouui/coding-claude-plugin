# `gh api` Command Reference

Use `gh api` for operations not covered by `gh pr` or `gh issue`.

## Common Endpoints

```bash
# Get PR review comments (file-level)
gh api repos/OWNER/REPO/pulls/<num>/comments

# Get PR changed files
gh api repos/OWNER/REPO/pulls/<num>/files

# Get PR commits
gh api repos/OWNER/REPO/pulls/<num>/commits

# Get PR reviews
gh api repos/OWNER/REPO/pulls/<num>/reviews

# Get issue/PR comments (issue-level, not file-level)
gh api repos/OWNER/REPO/issues/<num>/comments

# Post a review with file-level comments
gh api repos/OWNER/REPO/pulls/<num>/reviews --method POST --input - <<'EOF'
{
  "body": "Review feedback",
  "event": "COMMENT",
  "comments": [
    {"path": "src/main.py", "line": 42, "body": "Fix this"}
  ]
}
EOF

# Add a comment to issue/PR
gh api repos/OWNER/REPO/issues/<num>/comments -f body="Comment text"
```

## Key Options

 `--jq <expression>` — Filter JSON output
 `--method <string>` or `-X <string>` — HTTP method (GET, POST, PUT, DELETE, PATCH)
 `-f <key=value>` — String request body field
 `-F <key=value>` — Non-string request body field (numbers, booleans)
 `--input <file>` — Read request body from file (use "-" for stdin)
 `--paginate` — Fetch all pages of results

## Useful jq Patterns

```bash
# Extract file paths from PR
gh api repos/OWNER/REPO/pulls/<num>/files --jq '.[].filename'

# Get review comments with location
gh api repos/OWNER/REPO/pulls/<num>/comments --jq '.[] | {path: .path, line: .line, body: .body}'

# Get review states
gh api repos/OWNER/REPO/pulls/<num>/reviews --jq '.[] | {user: .user.login, state: .state}'
```
