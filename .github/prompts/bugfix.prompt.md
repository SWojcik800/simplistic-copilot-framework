---
description: Diagnose and fix bugs in a repository.
---

# Bug Fix Prompt

You are tasked with diagnosing and fixing a bug.

## Inputs
- **Repository path**: The path to the repo or worktree (e.g., `./tasks/<task-id>/worktrees/<repo>-<branch>/`)
- **Bug description**: What's going wrong and how to reproduce it

## Workflow

### 1. Understand the Bug
- Read the bug description carefully.
- Identify the affected area of the codebase using search tools.
- Look for related tests, logs, or error messages.

### 2. Reproduce
- If possible, run the failing test or reproduce the issue in the terminal.
- Confirm the symptoms match the bug report.

### 3. Root Cause Analysis
- Trace the execution flow to find the root cause.
- Check recent changes (git log, git diff) that might have introduced the bug.
- Look for off-by-one errors, null references, race conditions, incorrect logic, or missing edge cases.

### 4. Implement the Fix
- Make the minimal change necessary to fix the bug.
- Do not refactor unrelated code.
- Ensure the fix handles edge cases.

### 5. Verify
- Run existing tests to confirm the fix works and nothing is broken.
- Add or update tests to cover the bug scenario if no test exists.

### 6. Validate Against Specification
- Re-read the original bug description and any linked issues or requirements.
- Confirm the fix addresses the **exact problem described** — not just a symptom.
- Walk through each reproduction step and verify the bug no longer occurs.
- Check that the fix does not introduce new deviations from expected behavior.
- If acceptance criteria were provided, verify each one is satisfied.
- If the fix diverges from the specification (e.g., changes an API contract or alters expected output), flag it and get confirmation before proceeding.

### 7. Commit
- Commit on the feature/fix branch (never on `main` or `develop`).
- Use a descriptive commit message:
  ```
  fix: <short description of fix>

  Resolves: <bug description or issue reference>
  ```

### 8. Create Pull Request
- Push the branch to the remote.
- Present a summary of the changes to the user and **ask for approval** before creating the PR.
- Once approved, create a pull request using the PR template (`.github/PULL_REQUEST_TEMPLATE.md`):
  ```bash
  git push -u origin <branch>
  gh pr create --base develop --head <branch> --title "fix: <description>" --template .github/PULL_REQUEST_TEMPLATE.md
  ```
- Fill in the PR template fields: summary, changes list, type, related task, and testing checklist.
- If the user does not approve, skip PR creation and report the branch is ready for manual review.

## Output
Provide a summary of:
1. Root cause
2. What was changed and why
3. Test results
4. PR link (if created) or branch name for manual review