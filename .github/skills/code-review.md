# Code Review Skill

A systematic approach to reviewing code changes for correctness, security, quality, and maintainability.

## Review Process

1. **Understand context** — Read the PR description, linked issues, and task requirements.
2. **Review the diff** — Read all changed files. Understand each change.
3. **Check correctness** — Verify logic, edge cases, and error handling.
4. **Check security** — Look for vulnerabilities (OWASP Top 10).
5. **Check quality** — Assess readability, naming, structure, and duplication.
6. **Check tests** — Verify coverage for new and changed code.
7. **Provide feedback** — Categorize findings by severity.

## Severity Levels

| Level | Meaning | Action |
|-------|---------|--------|
| **Critical** | Bug, security flaw, data loss risk | Must fix before merge |
| **Warning** | Potential issue, code smell, poor practice | Should fix |
| **Suggestion** | Improvement idea, readability, style | Nice to have |
| **Nitpick** | Minor style or formatting | Optional |

## Security Checklist

- [ ] No hardcoded secrets, API keys, or passwords
- [ ] User input is validated and sanitized
- [ ] SQL queries use parameterized statements
- [ ] No path traversal vulnerabilities in file operations
- [ ] Authentication and authorization checks are in place
- [ ] Sensitive data is not logged
- [ ] Dependencies are from trusted, up-to-date sources
- [ ] CORS and CSP headers are properly configured (if applicable)

## Code Quality Checklist

- [ ] Functions are small and have a single responsibility
- [ ] Naming is clear, consistent, and descriptive
- [ ] No dead code, commented-out blocks, or TODO hacks
- [ ] No unnecessary duplication
- [ ] Error handling is appropriate (not swallowed, not over-broad)
- [ ] Public APIs have clear contracts
- [ ] Complex logic has explanatory comments

## Testing Checklist

- [ ] New behavior has corresponding tests
- [ ] Edge cases and error paths are tested
- [ ] Tests are deterministic (no flakiness)
- [ ] Test names describe the scenario clearly
- [ ] All tests pass

## Giving Good Feedback

### Do
- Be specific: reference file, line, and what's wrong
- Explain *why* something is a problem
- Suggest a concrete fix
- Acknowledge good work

### Don't
- Be vague ("this looks wrong")
- Demand style changes not in the project's conventions
- Block a review on nitpicks alone
- Rewrite someone's code in comments

## Feedback Format

```
**[severity]** `file.ts:42` — Description of the issue.

Suggestion: <how to fix>
```

Example:
```
**[critical]** `auth.ts:87` — Password is compared using `==` instead of a 
timing-safe comparison, which is vulnerable to timing attacks.

Suggestion: Use `crypto.timingSafeEqual()` for password comparison.
```
