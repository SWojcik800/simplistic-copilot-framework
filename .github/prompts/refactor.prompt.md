---
description: Restructure code without changing external behavior.
---

# Refactor Prompt

You are tasked with refactoring code to improve its structure, readability, or maintainability — without changing external behavior.

## Inputs
- **Repository path**: The path to the repo or worktree (e.g., `./tasks/<task-id>/worktrees/<repo>-<branch>/`)
- **Refactor scope**: What to refactor and why (e.g., extract module, reduce duplication, simplify logic)

## Workflow

### 1. Understand the Current State
- Read the code targeted for refactoring.
- Understand its purpose, callers, and dependencies.
- Run existing tests to establish a passing baseline.

### 2. Plan the Refactor
- Define the goal (clarity, reduced duplication, better separation of concerns, etc.).
- Identify the minimal set of changes needed.
- Ensure the public API / external behavior remains unchanged.

### 3. Refactor
- Make changes incrementally — one logical change at a time.
- Preserve all existing behavior.
- Follow existing project conventions.
- Common refactors:
  - Extract function/method/class
  - Rename for clarity
  - Remove dead code
  - Simplify conditionals
  - Reduce nesting
  - Break up large files

### 4. Verify
- Run the full test suite after each significant change.
- If tests fail, the refactor introduced a behavioral change — fix it.
- Add tests if the existing coverage is insufficient to validate the refactor.

### 5. Validate Against Specification
- Re-read the original refactor scope and goals.
- Confirm the refactored code still satisfies all **existing behavioral contracts** — same inputs produce the same outputs.
- Verify every public API, function signature, and data contract is preserved (unless explicitly scoped for change).
- Walk through callers and dependents to ensure nothing is broken by structural changes.
- If the refactor scope included specific goals (e.g., reduce duplication, improve readability), verify each goal is achieved.
- If any behavioral change was unavoidable, document it and get confirmation before proceeding.

### 6. Commit
- Commit on the feature branch (never on `main` or `develop`).
- Use a descriptive commit message:
  ```
  refactor: <short description>

  - <what changed structurally>
  - <why it's better>
  ```

### 7. Create Pull Request
- Push the branch to the remote.
- Present a summary of the changes to the user and **ask for approval** before creating the PR.
- Once approved, create a pull request using the PR template (`.github/PULL_REQUEST_TEMPLATE.md`):
  ```bash
  git push -u origin <branch>
  gh pr create --base develop --head <branch> --title "refactor: <description>" --template .github/PULL_REQUEST_TEMPLATE.md
  ```
- Fill in the PR template fields: summary, changes list, type, related task, and testing checklist.
- If the user does not approve, skip PR creation and report the branch is ready for manual review.

## Output
Provide a summary of:
1. What was refactored and why
2. Before/after structure (brief)
3. Test results confirming no behavioral change
4. PR link (if created) or branch name for manual review