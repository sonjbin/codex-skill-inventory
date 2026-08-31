---
name: pr-review
description: Review a pull request from its URL by reading the PR description, base and head context, changed files, diff, and relevant existing code. Use when Codex is asked to inspect or review a PR for compatibility with the current codebase, consistency between the stated intent and actual changes, or possible bugs, regressions, side effects, and missing tests.
---

# PR Review

Perform an evidence-based code review from a pull request URL. Prioritize actionable defects and regressions over summaries or style preferences.

## Review workflow

1. Read the repository's agent instructions and relevant project documentation before reviewing.
2. Fetch the PR title, body, base and head branches, commit list, changed-file list, full diff, existing review context when available, and check results. Use the connected GitHub tools first; use `gh` when more precise diff or repository inspection is required.
3. Inspect relevant unchanged code in the base branch or local checkout, including callers, implementations, interfaces, configuration, schemas, migrations, and tests. Do not infer compatibility from the diff alone.
4. State any review-blocking access or missing context. Do not invent unseen PR content, code, test results, or runtime behavior.
5. Review every changed file against all three criteria below.
6. Run focused read-only checks or tests when they are available and proportionate. Distinguish executed verification from static reasoning. Do not modify code, post comments, approve, or request changes unless the user explicitly asks.
7. Report findings in the required output format. Cite the narrowest useful changed-file line or diff location for each finding.

## Review criteria

### 1. Existing-code compatibility

- Compare changed contracts with all relevant consumers and implementations.
- Check public APIs, function signatures, types, serialization formats, schemas, database migrations, configuration, environment variables, dependency versions, and deployment/runtime assumptions.
- Check backward compatibility, default behavior, upgrade and rollback paths, and mixed-version behavior where relevant.
- Verify that existing tests and documented behavior remain valid. Identify affected callers or workflows that the PR did not update.

### 2. PR intent and implementation consistency

- Translate the PR title and body into explicit claimed behavior and scope.
- Map each claim to concrete code and tests in the diff.
- Flag promised behavior that is absent or only partially implemented, code that contradicts the stated behavior, unrelated scope, stale documentation, and tests that do not exercise the claimed behavior.
- Treat description quality separately from implementation correctness; do not assume the description is authoritative when the code disagrees.

### 3. Errors and side effects

- Trace changed control flow and data flow through success, failure, empty, boundary, and retry paths.
- Check validation, exception handling, cleanup, state mutation, ordering, idempotency, concurrency, race conditions, caching, resource usage, performance, security, privacy, observability, and platform-specific behavior where applicable.
- Look for silent behavior changes, partial writes, duplicate work, stale state, lost data, unsafe fallbacks, incompatible defaults, and missing negative or regression tests.
- Prefer concrete failure scenarios over speculative concerns. State the inputs or sequence needed to trigger each problem and its observable impact.

## Finding standards

- Report only issues introduced by the PR or made materially worse by it.
- Assign severity as `critical`, `high`, `medium`, or `low` based on impact and likelihood. Do not label optional cleanup or subjective style as a defect.
- Make each finding independently actionable: identify the problem, evidence, trigger, impact, and a concise remediation direction.
- Verify that a proposed finding is not already handled elsewhere in the changed or existing code.
- Use file and line references whenever available. Keep cited ranges minimal and ensure they overlap the changed code when the review system requires inline-comment-compatible locations.
- If evidence is incomplete, place the item under open questions instead of presenting it as a confirmed defect.

## Output format

Return the review in this order:

1. **Findings** — ordered from highest to lowest severity. For each finding include severity, short title, file/line, evidence and trigger, impact, and remediation direction.
2. **Open questions or assumptions** — include only items that materially affect the review.
3. **Verification** — list code, tests, checks, and documentation inspected or executed; clearly note checks that could not be run.
4. **Summary** — briefly assess compatibility, PR-to-code consistency, and regression risk.

If no actionable findings are found, say so explicitly and describe residual risks or verification gaps. Do not replace findings with a general PR summary.
