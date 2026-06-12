---
name: code-review
description: 'Conduct thorough, constructive code reviews aligned with engineering best practices. Use when the user mentions "review this code", "PR review", "code quality", "pull request feedback", "code smell", "tech debt", or "review before merge". Also trigger when asked to evaluate readability, security, performance, or testability of any code. For architecture decisions, see architecture-review. For incident post-mortems, see incident-response.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# Code Review Skill

A structured framework for delivering high-signal, constructive code reviews that improve code quality, share knowledge, and ship safer software. Good code reviews catch bugs before production, enforce standards consistently, and accelerate team learning — without becoming a bottleneck.

## Core Principle

**Code review is about the code, not the coder.** The goal is always to improve the system and raise team capability — never to criticize, gatekeep, or showcase superiority. Reviews should leave the author more confident and knowledgeable, not defensive.

## Scoring

**Goal: 10/10.** When reviewing or receiving a review, rate 0–10 based on adherence to the principles below. A 10/10 means the review is thorough, kind, actionable, and fast. Always provide the current score and specific improvements needed to reach 10/10.

## Review Framework

### 1. Correctness

**Core concept:** Does the code do what it's supposed to do, correctly and completely?

**Why it matters:** Bugs merged to main cost 10–100x more to fix than bugs caught in review.

**Key checks:**
- Does the logic match the requirements/ticket?
- Are edge cases handled (null, empty, overflow, concurrency)?
- Are error paths handled gracefully?
- Are there any off-by-one errors, race conditions, or subtle logic bugs?
- Does it handle the unhappy path as carefully as the happy path?

**Application table:**

| Scenario | Check | Signal |
|----------|-------|--------|
| New feature | Matches acceptance criteria | Ticket / spec alignment |
| Bug fix | Root cause addressed, not just symptom | Regression test added |
| Refactor | Behavior preserved | Tests still pass, no observable change |

### 2. Security

**Core concept:** Does the code introduce any security vulnerabilities?

**Why it matters:** Security issues in code are far cheaper to fix before merge than after a breach.

**Key checks:**
- SQL injection — are queries parameterized?
- XSS — is user input escaped before rendering?
- Sensitive data (passwords, tokens, PII) not logged or hardcoded
- Authentication and authorization enforced on every endpoint
- Dependencies not pinned to a vulnerable version
- File paths not constructed from user input (path traversal)

**OWASP Top 10 mental checklist:** Injection, Broken Auth, Sensitive Data Exposure, XXE, Broken Access Control, Security Misconfiguration, XSS, Insecure Deserialization, Using Components with Known Vulnerabilities, Insufficient Logging.

See: [references/security-checklist.md](references/security-checklist.md)

### 3. Readability & Maintainability

**Core concept:** Will the next engineer (or future you) be able to understand, modify, and extend this code?

**Why it matters:** Code is read 10x more than it is written. Unreadable code creates long-term drag on the team.

**Key checks:**
- Names (variables, functions, classes) are clear and intention-revealing
- Functions do one thing (single responsibility)
- Complexity is justified — no unnecessary cleverness
- Comments explain *why*, not *what*
- No dead code, TODO comments lingering from another era
- Consistent style with the surrounding codebase

### 4. Performance

**Core concept:** Does the code perform acceptably under expected (and peak) load?

**Why it matters:** Performance issues discovered in production impact users and are expensive to fix.

**Key checks:**
- No N+1 queries (check database calls in loops)
- Expensive operations not on the hot path
- Large data sets not loaded fully into memory when streaming is possible
- Caching applied where appropriate
- No unnecessary re-renders (frontend)

### 5. Test Coverage

**Core concept:** Are the right behaviors tested, and are tests reliable?

**Why it matters:** Tests are the safety net that enables confident refactoring and shipping.

**Key checks:**
- Happy path tested
- Edge cases and error paths tested
- Tests are deterministic (no flakiness)
- Tests assert behavior, not implementation details
- No mock-everything tests that give false confidence

### 6. Review Tone & Communication

**Core concept:** Feedback is delivered constructively, specifically, and kindly.

**Why it matters:** Harsh reviews create fear, slow down PRs, and damage team culture.

**Key practices:**
- Prefix feedback with severity: `[blocker]`, `[suggestion]`, `[nit]`
- Ask questions instead of issuing commands: "What do you think about...?" vs "Change this to..."
- Explain the *why* behind feedback, not just the what
- Acknowledge good decisions: "Nice use of X here"
- Approve with conditions clearly stated rather than leaving the author guessing

## Common Mistakes

| Mistake | Why It Fails | Fix |
|---------|-------------|-----|
| Reviewing style instead of substance | Wastes time on trivial issues | Use a linter/formatter to automate style; focus review on logic |
| Long review cycles (>24h) | Blocks shipping, kills momentum | Timebox reviews; treat them as high priority |
| Vague feedback ("this is wrong") | Author doesn't know what to fix | Be specific: quote the line, explain the issue, suggest the fix |
| Approving without reading | Rubber-stamp culture; bugs slip through | If pressed for time, review the diff summary and flag high-risk areas |
| Rewriting the PR in review | Demoralizes author, slows velocity | Suggest, don't rewrite; pair if a rework is truly needed |

## Quick Diagnostic

| Question | If No | Action |
|----------|-------|--------|
| Does the code have tests for the new behavior? | Untested code | Request tests before approving |
| Is sensitive data handled safely? | Security risk | Flag as [blocker], do not approve |
| Can I understand this code in 60 seconds? | Readability issue | Request clearer naming or a comment |
| Is there a risk of N+1 queries? | Performance risk | Flag and ask author to verify query count |
| Is feedback delivered with a suggested fix? | Unclear review | Rewrite comment to include the "fix" |

## Reference Files

- [references/security-checklist.md](references/security-checklist.md) — OWASP Top 10 quick reference for code reviewers
