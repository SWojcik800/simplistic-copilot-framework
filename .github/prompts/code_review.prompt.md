---
description: Review code for quality, security, correctness, and maintainability.
---

# Code Review Prompt

You are tasked with reviewing code changes for quality, security, and correctness.

## Inputs
- **Repository path**: The path to the repo or worktree (e.g., `./tasks/<task-id>/worktrees/<repo>-<branch>/`)
- **Review scope**: A branch, commit range, or set of files to review

## Workflow

### 1. Gather the Changes
- Use `git diff` or `git log` to identify what changed.
- Read the changed files in full context (not just the diff).

### 2. Review Checklist

#### Correctness
- [ ] Does the code do what it's supposed to?
- [ ] Are edge cases handled?
- [ ] Are there off-by-one errors, null/undefined risks, or race conditions?

#### Security
- [ ] No hardcoded secrets, tokens, or credentials
- [ ] Input validation at system boundaries
- [ ] No SQL injection, XSS, or path traversal vulnerabilities
- [ ] Dependencies are from trusted sources

#### Code Quality
- [ ] Code is readable and self-documenting
- [ ] Naming is clear and consistent
- [ ] No unnecessary duplication
- [ ] Functions/methods have a single responsibility
- [ ] No dead code or commented-out blocks

#### Testing
- [ ] New/changed code has corresponding tests
- [ ] Tests cover happy path and edge cases
- [ ] All tests pass

#### Architecture
- [ ] Changes fit the existing patterns and conventions
- [ ] No unintended coupling between modules
- [ ] API contracts are preserved or intentionally changed

### 3. Provide Feedback
For each finding, include:
- **File and line** (or line range)
- **Severity**: critical / warning / suggestion / nitpick
- **Description**: What the issue is
- **Recommendation**: How to fix it

### 4. Summary
- Overall assessment: approve / request changes / needs discussion
- List of critical issues (must fix)
- List of suggestions (nice to have)

## Output Format
```markdown
## Code Review Summary
**Verdict:** approve | request-changes | discuss

### Critical Issues
1. [file:line] — description

### Warnings
1. [file:line] — description

### Suggestions
1. [file:line] — description

### What Looks Good
- <positive observations>
```
