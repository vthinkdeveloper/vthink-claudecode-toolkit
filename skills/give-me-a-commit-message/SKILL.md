---
name: give-me-a-commit-message
description: Suggest a Conventional Commits message based on current staged and unstaged changes. Does not commit — just outputs the message to copy. Extracts ticket ID from branch name if present. Use when you want a commit message suggestion without committing.
---

# Suggest Commit Message

Analyze the current changes and suggest a commit message. Do NOT commit or push.

## Workflow

### Step 1: Gather Context

Run these in parallel:
- `git diff --staged` — staged changes
- `git diff` — unstaged changes
- `git status` — overview of modified/new/deleted files
- `git branch --show-current` — current branch name
- `git log --oneline -5` — recent commits for style reference

### Step 2: Extract Ticket ID

From the branch name, extract any ticket ID pattern (e.g., `PROJ-1234`, `FEAT-567`, `BUG-42`).
- Pattern: uppercase letters + hyphen + numbers (e.g., `[A-Z]+-\d+`)
- If found, prefix the commit message with it

### Step 3: Generate Message

Write a commit message following these rules:
- If a ticket ID was found, format as: `TICKET-ID: Description`
- Match the style of recent commits in the repo
- First line: concise summary under 72 characters
- If the change is non-trivial, add a blank line then a short body explaining the "why"
- Focus on **why** the change was made, not **what** changed (the diff shows that)

### Step 4: Output

Present the suggested message like this:

**Suggested commit message:**

```
TICKET-ID: Short description of the change

Optional body explaining why, if needed.
```

Then say: "Copy and use with `git commit -m \"...\"`, or ask me to refine it."

Do NOT run `git commit`, `git add`, or `git push`. Only suggest.
