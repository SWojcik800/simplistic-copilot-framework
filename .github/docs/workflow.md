# Framework Workflow

This document describes how the AI Development Framework operates end-to-end.

## Overview

The framework enables parallel AI-assisted development across multiple repositories and tasks. It uses git worktrees for isolation, an orchestrator agent for coordination, and reusable prompts for consistent execution.

## End-to-End Workflow

### 1. Clone a Repository

Use the **initialize** prompt or clone manually:
```bash
cd ./src
git clone <repo-url> <repo-name>
cd <repo-name>
git checkout develop  # ensure develop branch exists
```

The repo now lives at `./src/<repo-name>/`.

### 2. Define Tasks

Create a task directory in `./tasks/`:

```bash
mkdir -p ./tasks/my-app-fix-login/worktrees
```

Add a `task.md`:
```markdown
# Task: Fix login crash

- **Repo:** my-app
- **Type:** bugfix
- **Branch:** fix/login-crash

## Description
App crashes when user submits empty login form.

## Acceptance Criteria
- [ ] Empty form submission is handled gracefully
- [ ] Error message displayed to user
```

### 3. Orchestrate

The orchestrator agent (`.github/agents/orchestrator.agent.md`) will:
1. Scan `./tasks/` for task directories
2. Read or create `orchestrator_state.yaml` in each
3. Create a worktree inside `./tasks/<task-id>/worktrees/`
4. Delegate to the appropriate prompt based on task type
5. Track progress by updating `orchestrator_state.yaml`

### 4. Parallel Execution

Each task's worktree lives inside its own task directory:

```
tasks/
  my-app-fix-login/
    task.md
    orchestrator_state.yaml
    worktrees/
      my-app-fix-login-crash/       ← bugfix worktree
  my-app-user-auth/
    task.md
    orchestrator_state.yaml
    worktrees/
      my-app-feature-user-auth/     ← feature worktree
```

The main clone at `./src/my-app/` stays on `develop`. All worktrees share the same git data.

### 5. Work Execution

Each delegated prompt follows its own workflow:
- **Initialize**: clone → set up branches → inspect project
- **Bugfix**: diagnose → reproduce → fix → test → commit → PR
- **Feature**: plan → implement → test → commit → PR
- **Refactor**: baseline tests → restructure → verify → commit → PR
- **Review**: gather changes → checklist → feedback
- **Git Flow**: branch → work → merge → tag → clean up

Prompts that modify code (bugfix, feature, refactor) will **ask for user approval** before creating a pull request.

### 6. Merge and Clean Up

After a task is complete:
1. PR is merged (manually or via the git flow prompt)
2. Remove the worktree:
   ```bash
   cd ./src/<repo-name>
   git worktree remove ../../tasks/<task-id>/worktrees/<worktree-name>
   ```
3. Update `orchestrator_state.yaml`: set `status: completed`
4. Delete the merged branch

## Directory Reference

| Path | Purpose |
|------|---------|
| `./src/<repo>/` | Main clone of a repository |
| `./tasks/<task-id>/` | Task directory with definition and state |
| `./tasks/<task-id>/worktrees/<name>/` | Worktree for this task |
| `./tasks/<task-id>/orchestrator_state.yaml` | Persisted task state |
| `.github/agents/` | Agent definitions (orchestrator) |
| `.github/prompts/` | Reusable prompt templates |
| `.github/skills/` | Domain knowledge (git, review) |
| `.github/docs/` | This documentation |
| `.github/PULL_REQUEST_TEMPLATE.md` | PR template |

## Adding a New Repository

```bash
cd ./src
git clone <url> <name>
```

Or use the initialize prompt to set up the repo with git flow branches.

## Adding a New Prompt

1. Create `.github/prompts/<name>.prompt.md` with YAML frontmatter and workflow steps.
2. Register it in `AGENTS.md` under the Prompts table.
3. Add its type to the orchestrator's delegation mapping.
