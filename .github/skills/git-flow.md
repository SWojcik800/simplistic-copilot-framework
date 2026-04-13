# Git Flow Skill

Git flow is a branching model that uses dedicated branches for features, fixes, releases, and hotfixes, with `main` and `develop` as long-lived branches.

## Branch Structure

```
main          ← production-ready code, tagged releases
develop       ← integration branch for features
feature/*     ← new features (branch from develop)
fix/*         ← bug fixes (branch from develop)
release/*     ← release prep (branch from develop, merges to main + develop)
hotfix/*      ← urgent production fixes (branch from main, merges to main + develop)
```

## Branch Naming Conventions

| Type | Pattern | Base Branch | Merges Into |
|------|---------|-------------|-------------|
| Feature | `feature/<descriptive-name>` | `develop` | `develop` |
| Bug Fix | `fix/<descriptive-name>` | `develop` | `develop` |
| Release | `release/<semver>` | `develop` | `main` + `develop` |
| Hotfix | `hotfix/<descriptive-name>` | `main` | `main` + `develop` |

## Naming Rules
- Use lowercase with hyphens: `feature/user-authentication`
- Be descriptive but concise: `fix/null-pointer-on-login`
- For releases, use semantic versioning: `release/2.1.0`

## Merge Strategy
- Always use `--no-ff` (no fast-forward) to create a merge commit and preserve branch history.
- Resolve conflicts locally before pushing.
- Delete the source branch after a successful merge.

## Tagging
- Tag every merge to `main`:
  - Releases: `v1.2.0`
  - Hotfixes: `v1.2.1`
- Use annotated tags: `git tag -a v1.2.0 -m "Release 1.2.0"`

## Commit Message Conventions

Use conventional commit prefixes:
```
feat: add user registration endpoint
fix: handle null email in login flow
refactor: extract auth middleware
docs: update API documentation
test: add integration tests for payments
chore: update dependencies
```

## Rules

1. **Never commit directly to `main` or `develop`.**
2. **Always pull before merging** to avoid conflicts with stale bases.
3. **One branch per task** — don't mix unrelated changes.
4. **Delete merged branches** to keep the repo clean.
5. **Tag releases** on `main` immediately after merging.

## Quick Reference

```bash
# Start feature
git checkout develop && git pull && git checkout -b feature/<name>

# Finish feature
git checkout develop && git pull && git merge --no-ff feature/<name> && git branch -d feature/<name>

# Start release
git checkout develop && git pull && git checkout -b release/<version>

# Finish release
git checkout main && git merge --no-ff release/<version> && git tag -a v<version> -m "Release"
git checkout develop && git merge --no-ff release/<version> && git branch -d release/<version>

# Start hotfix
git checkout main && git pull && git checkout -b hotfix/<name>

# Finish hotfix
git checkout main && git merge --no-ff hotfix/<name> && git tag -a v<version> -m "Hotfix"
git checkout develop && git merge --no-ff hotfix/<name> && git branch -d hotfix/<name>
```
