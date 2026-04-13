---
description: Implement a new feature end-to-end.
---

# New Feature Prompt

You are tasked with implementing a new feature.

## Inputs
- **Repository path**: The path to the repo or worktree (e.g., `./tasks/<task-id>/worktrees/<repo>-<branch>/`)
- **Feature description**: What to build and why
- **Acceptance criteria**: What "done" looks like

## Workflow

### 1. Understand the Feature
- Read the feature description and acceptance criteria.
- Explore the codebase to understand existing architecture and patterns.
- Identify where the new code should live and what it needs to integrate with.

### 2. Plan the Implementation
- Break the feature into small, testable increments.
- Identify dependencies, data models, APIs, or UI components involved.
- Note any risks or unknowns.

### 3. Implement
- Follow existing code conventions (naming, structure, patterns).
- Write clean, readable code — no over-engineering.
- Implement one piece at a time and verify as you go.

### 4. Test
- Write unit tests for new logic.
- Add integration tests if the feature spans multiple modules.
- Run the full test suite to catch regressions.

### 5. Validate Against Specification
- Re-read the original feature description and acceptance criteria.
- Walk through **every acceptance criterion** and verify it is met by the implementation.
- Confirm the feature behaves correctly for both happy-path and edge-case scenarios.
- Verify no undocumented behavior was introduced beyond what the specification requires.
- If any criterion is not fully satisfied, go back and address it before continuing.
- If the implementation intentionally deviates from the specification (e.g., technical constraint, better UX), document the deviation and get confirmation before proceeding.

### 6. Commit
- Make atomic commits on the feature branch.
- Use descriptive commit messages:
  ```
  feat: <short description>

  - <detail 1>
  - <detail 2>
  ```

### 7. Create Pull Request
- Push the branch to the remote.
- Present a summary of the changes to the user and **ask for approval** before creating the PR.
- Once approved, create a pull request using the PR template (`.github/PULL_REQUEST_TEMPLATE.md`):
  ```bash
  git push -u origin <branch>
  gh pr create --base develop --head <branch> --title "feat: <description>" --template .github/PULL_REQUEST_TEMPLATE.md
  ```
- Fill in the PR template fields: summary, changes list, type, related task, and testing checklist.
- If the user does not approve, skip PR creation and report the branch is ready for manual review.

## Output
Provide a summary of:
1. What was implemented
2. Key design decisions
3. Files changed
4. Test results
5. PR link (if created) or branch name for manual review
6. Any follow-up work needed