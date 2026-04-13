# Git Worktree Skill

Git worktrees allow checking out multiple branches of the same repository simultaneously in separate directories. This enables parallel work on multiple tasks without stashing or switching branches.

## When to Use Worktrees

- Working on multiple tasks concurrently (e.g., a feature + a bugfix)
- Reviewing code on one branch while developing on another
- Running tests on one branch while editing another
- Any time you need two branches of the same repo accessible at once

## Workspace Convention

| Path | Purpose |
|------|---------|
| `./src/<repo>/` | Main clone (primary working tree) |
| `./tasks/<task-id>/worktrees/<repo>-<branch>/` | Worktree for a specific task |

Worktrees are always created **inside the task directory** to keep each task self-contained.

## Creating a Worktree

### For a new branch (inside a task)
```bash
cd ./src/<repo>
git worktree add ../../tasks/<task-id>/worktrees/<repo>-<branch> -b <branch> <base>
```
- `<task-id>`: the task directory name
- `<branch>`: new branch name (e.g., `feature/add-auth`)
- `<base>`: starting point (e.g., `develop`, `main`, a commit SHA)

### For an existing branch
```bash
cd ./src/<repo>
git worktree add ../../tasks/<task-id>/worktrees/<repo>-<branch> <branch>
```

### Examples
```bash
# New feature branch off develop
cd ./src/my-app
git worktree add ../../tasks/my-app-auth/worktrees/my-app-feature-auth -b feature/auth develop

# Existing branch for review
cd ./src/my-app
git fetch origin
git worktree add ../../tasks/my-app-review-login/worktrees/my-app-fix-login fix/login-crash
```

## Listing Worktrees
```bash
cd ./src/<repo>
git worktree list
```

## Removing a Worktree
After merging and the work is done:
```bash
cd ./src/<repo>
git worktree remove ../../tasks/<task-id>/worktrees/<repo>-<branch>
```

If the directory was already deleted:
```bash
cd ./src/<repo>
git worktree prune
```

## Important Rules

1. **Each branch can only be checked out in one worktree at a time.** You cannot have the same branch in two worktrees.
2. **The main clone and all worktrees share the same `.git` data.** Commits made in any worktree are visible to all others.
3. **Always create worktrees inside `./tasks/<task-id>/worktrees/`** so the orchestrator can find and manage them.
4. **Clean up worktrees** after tasks are completed to avoid clutter.
5. **Do not delete worktree directories manually** — always use `git worktree remove` or `git worktree prune`.

## Combining with Git Flow

Typical multi-task setup:
```bash
# Main clone stays on develop
cd ./src/my-app && git checkout develop

# Task 1: feature work
git worktree add ../../tasks/auth-feature/worktrees/my-app-feature-auth -b feature/auth develop

# Task 2: bugfix
git worktree add ../../tasks/login-fix/worktrees/my-app-fix-login -b fix/login-crash develop

# Task 3: hotfix off main
git worktree add ../../tasks/security-hotfix/worktrees/my-app-hotfix-security -b hotfix/security-patch main
```

Now three tasks can proceed in parallel, each in its own task directory.

## Troubleshooting

| Problem | Solution |
|---------|----------|
| "branch is already checked out" | The branch is in another worktree. Use `git worktree list` to find it. |
| "not a git repository" | You're not inside a repo. `cd` into `./src/<repo>` first. |
| Stale worktree references | Run `git worktree prune` from the main clone. |
