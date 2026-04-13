---
description: Record lessons learned during development into the docs knowledge base.
---

# Learn Prompt

You are tasked with capturing a lesson learned during development and persisting it to the project's knowledge base in `.github/docs/`.

## Inputs
- **Lesson**: What was learned — a rule, pattern, pitfall, convention, or insight
- **Context** (optional): Which task, repo, or situation triggered the learning
- **Category** (optional): e.g., architecture, testing, debugging, performance, security, tooling, conventions

## Workflow

### 1. Understand the Lesson
- Clarify what was learned and why it matters.
- Determine if it's repo-specific or applies broadly across the framework.

### 2. Check for Existing Knowledge
- Read `.github/docs/lessons-learned.md` (create it if it doesn't exist).
- Check if this lesson or a similar one is already documented.
- If it exists, update or refine the existing entry rather than adding a duplicate.

### 3. Categorize
Assign the lesson to a category. Use existing categories from the file, or create a new one if none fits:
- **Architecture** — design decisions, patterns, anti-patterns
- **Testing** — test strategies, pitfalls, flaky test fixes
- **Debugging** — diagnosis techniques, common root causes
- **Performance** — optimizations, bottlenecks found
- **Security** — vulnerabilities found, hardening rules
- **Tooling** — build system, CI/CD, dev environment quirks
- **Conventions** — coding standards, naming, process rules
- **Git** — branching, merge, worktree lessons

### 4. Write the Entry
Add the lesson to `.github/docs/lessons-learned.md` using this format:

```markdown
### <Short title>
**Category:** <category>
**Context:** <repo, task, or situation — optional>

<1-3 sentences describing the lesson, what went wrong or right, and the rule to follow going forward.>
```

Keep entries concise — actionable rules, not essays.

### 5. Verify
- Ensure the entry is clear enough that someone unfamiliar with the context can understand and apply it.
- Ensure no duplication with existing entries.

## Output
Confirm:
1. Which file was updated (or created)
2. The lesson title and category
3. Whether it was a new entry or an update to an existing one
