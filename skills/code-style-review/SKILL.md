---
name: code-style-review
description: A skill for reviewing code, providing feedback on code quality, and suggesting improvements. Use when asked to review code or provide feedback on code quality.
argument-hint: target
---

# Code Style Review

Review code for quality, consistency, and maintainability. Produce a structured, actionable report.

## Workflow

1. **Detect scope** — If the user provides a `target` (file/dir), use that. Otherwise run `git diff --name-only` (staged + unstaged) to discover changed files.
2. **Load rules** — Rules in `./rules/` use `paths` frontmatter to declare which file patterns they apply to. Only load rules whose `paths` match the files being reviewed. This keeps context minimal.
3. **Apply principles** — Always consider the general coding principles in `./references/code-principles.md`.
4. **Review each file** — For each file in scope, check against the loaded rules and principles. Read enough surrounding context (±50 lines) to understand intent.
5. **Produce report** — Output findings using the report template below.

## Report Template

### Summary

> One-paragraph overall assessment. State the most important thing the author should address.

### Findings

| # | Severity | File | Line(s) | Issue | Suggestion |
|---|----------|------|----------|-------|------------|
| 1 | 🔴 Critical | `src/auth.ts` | 42-45 | Unchecked null access on `user.profile` | Use optional chaining: `user?.profile` |
| 2 | 🟡 Warning | `src/api.ts` | 18 | Duplicated error handling logic | Extract to shared `handleApiError()` |
| 3 | 🔵 Suggestion | `src/utils.ts` | 7 | Magic number `86400` | Use named constant `SECONDS_PER_DAY` |

### Severity Guide

- **🔴 Critical** — Bugs, security issues, data loss risks. Must fix before merge.
- **🟡 Warning** — Code smells, maintainability issues, violated conventions. Should fix.
- **🔵 Suggestion** — Style improvements, readability, minor optimizations. Nice to have.

### Stats

```
Files reviewed: N
Critical: N | Warning: N | Suggestion: N
```

## Feedback Style

- Be specific: point to exact lines and explain **why** it's a problem.
- Be constructive: always offer a concrete fix or alternative.
- Be respectful: the goal is to help the author improve, not to criticize.
- Prioritize: list Critical issues first, then Warning, then Suggestion.

## Rules

Rules are loaded from `./rules/` based on file type matching. Each rule file declares which file patterns it applies to via `paths` frontmatter. This ensures only relevant rules are loaded, saving context tokens.

`./rules`