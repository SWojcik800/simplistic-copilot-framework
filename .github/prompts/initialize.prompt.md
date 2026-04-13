---
description: Initialize a new repository in the framework — clone, set up branches, and configure.
---

# Initialize Prompt

You are tasked with initializing a new repository for use in this AI development framework.

## Inputs
- **Repository URL**: The remote git URL to clone
- **Repository name**: Short name for local use (used as directory name under `./src/`)
- **Default branch strategy**: Whether to set up git flow branches (`main` + `develop`) or use `main` only

## Workflow

### 1. Clone the Repository
```bash
cd ./src
git clone <repo-url> <repo-name>
cd <repo-name>
```

### 2. Verify Remote
```bash
git remote -v
git branch -a
```

### 3. Set Up Branch Structure

#### Git Flow (recommended)
If the repo doesn't already have a `develop` branch:
```bash
git checkout main
git checkout -b develop
git push -u origin develop
```

#### Main-only
If using a simple trunk-based flow, skip this step.

### 4. Configure Git Settings
Set recommended defaults for the repo:
```bash
git config pull.rebase false
git config merge.ff false
```

### 5. Inspect the Project
- Identify the language, framework, and build system.
- Check for existing CI/CD configuration.
- Look for a `README.md`, `package.json`, `Makefile`, `Cargo.toml`, or equivalent.
- Note the test runner and how to run tests.

### 6. Document the Setup
Create an entry in the framework by reporting:
- Repo name and path (`./src/<repo-name>/`)
- Primary language and framework
- Build command
- Test command
- Branch structure (`main` / `develop` / other)
- Any notable conventions or configuration

### 7. Verify
```bash
# Confirm clean state
git status
git log --oneline -5
```

## Output
Provide a summary of:
1. Repository cloned at `./src/<repo-name>/`
2. Branch structure set up
3. Project overview (language, build, test commands)
4. Any issues encountered
