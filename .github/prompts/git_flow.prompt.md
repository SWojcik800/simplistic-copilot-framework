---
description: Manage branches, pull requests, merges, and releases using git flow conventions.
---

# Git Flow Prompt

You are tasked with managing git branch operations following git flow conventions.

## Inputs
- **Repository path**: The path to the repo or worktree (e.g., `./src/<repo>/`)
- **Operation**: What git flow action to perform

## Supported Operations

### Start a Feature Branch
```bash
cd ./src/<repo>
git checkout develop
git pull origin develop
git checkout -b feature/<feature-name>
```

### Start a Bug Fix Branch
```bash
cd ./src/<repo>
git checkout develop
git pull origin develop
git checkout -b fix/<bug-name>
```

### Start a Hotfix Branch
```bash
cd ./src/<repo>
git checkout main
git pull origin main
git checkout -b hotfix/<hotfix-name>
```

### Start a Release Branch
```bash
cd ./src/<repo>
git checkout develop
git pull origin develop
git checkout -b release/<version>
```

### Finish a Feature / Fix (Merge to Develop)
```bash
cd ./src/<repo>
git checkout develop
git pull origin develop
git merge --no-ff feature/<feature-name>
# Resolve conflicts if any
git push origin develop
git branch -d feature/<feature-name>
```

### Finish a Release (Merge to Main + Develop)
```bash
cd ./src/<repo>
git checkout main
git pull origin main
git merge --no-ff release/<version>
git tag -a v<version> -m "Release <version>"
git push origin main --tags
git checkout develop
git merge --no-ff release/<version>
git push origin develop
git branch -d release/<version>
```

### Finish a Hotfix (Merge to Main + Develop)
```bash
cd ./src/<repo>
git checkout main
git pull origin main
git merge --no-ff hotfix/<hotfix-name>
git tag -a v<version> -m "Hotfix <version>"
git push origin main --tags
git checkout develop
git merge --no-ff hotfix/<hotfix-name>
git push origin develop
git branch -d hotfix/<hotfix-name>
```

## Branch Naming Conventions

| Type | Pattern | Example |
|------|---------|---------|
| Feature | `feature/<name>` | `feature/user-auth` |
| Bug Fix | `fix/<name>` | `fix/login-crash` |
| Hotfix | `hotfix/<name>` | `hotfix/critical-security-patch` |
| Release | `release/<version>` | `release/1.2.0` |

## Rules
- **Never commit directly to `main` or `develop`.**
- Always use `--no-ff` for merges to preserve branch history.
- Tag all releases and hotfixes on `main`.
- Delete branches after successful merge.
- Pull before merging to avoid stale-base conflicts.

## Output
Provide a summary of:
1. What operation was performed
2. Branches involved
3. Current state (merged, tagged, cleaned up)
4. Any conflicts encountered and how they were resolved
