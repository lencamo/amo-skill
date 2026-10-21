---
name: amo-review
description: Review implemented functionality for requirement gaps, logic errors, and bugs across workspace changes, specified commits, or an entire feature branch. Use when the user asks whether an implementation is correct or ready to merge. Not for code-style-only reviews, solution design, or diagnosing a known failure to choose a fix.
metadata:
  version: '0.2.0'
---

# Amo Review

Review functional correctness with concrete evidence. Default to reporting findings without changing code.

## Shared Output Marker

Prefix the first output line inline with `🔍 [amo-review]`. Do not put the marker in a separate paragraph.

## Use When

- The user wants to check implemented behavior against requirements or find logic errors, missed cases, and potential bugs.
- The target is workspace changes, specified commits, a commit range, or a feature branch.

## Do Not Use

- Code style, redundancy, abstraction, or type-expression review alone; use `amo-check`.
- Diagnosing a known failure and choosing a fix; use `amo-fix`.
- Designing or reassessing a proposal before implementation.

## Review Scope

Honor the user's explicit scope first. For a generic implementation-review request on a feature branch, review the whole branch; on its base branch, review workspace changes. If neither has changes, report that rather than silently choosing the last commit. Resolve an uncertain base from project context and history; ask only when ambiguity materially changes the scope.

| Scope | Review surface |
| :--- | :--- |
| Workspace | Combined staged and unstaged tracked changes against `HEAD`, plus full untracked files. Account for deletions as well as additions. |
| Specified commits | Each requested commit's changes, or the net diff of an explicitly requested range. Preserve an explicit commit selection rather than expanding it to include intervening commits. |
| Feature branch | Resolve the base and target to commit IDs, find their merge base, and review the net diff from that point to the target. Use history to explain intent, not to report intermediate defects already fixed in the final state. |

Record the resolved mode, baseline, target, and file inventory before reviewing. Read files at the reviewed revision; working files may differ from a selected commit or branch. For commit and branch scopes, state whether uncommitted changes are included and keep them outside scope unless requested.

Use read-only Git inspection and preserve the worktree and index. Missing refs or unreadable files are coverage gaps, not permission to substitute another scope.

## Workflow

1. Resolve the scope and expected behavior from the request, requirements, acceptance criteria, project docs, tests, and existing contracts. Distinguish documented intent from inference. Compare the changes with the stated goal: identify missing requirements, off-target behavior, and unrelated changes. Report scope deviations separately from functional defects.
2. Read the complete selected diffs and relevant context: callers, callees, prior content for deletions, tests, configuration, and storage contracts. Trace inputs, processing, state changes, persistence, and outputs.
3. Check the dimensions below against the actual contracts and expected load. For high-risk changed flows, identify what must remain true before and after the operation, then choose relevant adversarial cases by varying timing, input format, or permission scope. Examples include stale responses overwriting newer state, refresh interrupting an active session, and reused components retaining stale state. Follow affected call sites when signatures, return values, or behavior change. For bug fixes, check directly related paths for the same defect to confirm the fix covers all affected entry points. Do not expand into an unrelated whole-repo audit or repair unrequested areas.
4. Verify each candidate finding against reachable inputs, downstream behavior, and existing guards. For timing-, state-, or environment-dependent behavior, prefer a minimal observable reproduction; deterministic static evidence is also valid. Run focused verification on the reviewed revision when practical; historical results are context, not current verification. Distinguish executed checks, static reasoning, and unavailable checks. When a review conclusion depends on real-dependency behavior that mocks or substitute services do not exercise, report that verification gap.
5. Account for every scoped file as reviewed or skipped with a reason. Before reporting, refresh affected evidence if the target or relevant working files changed.

## Review Dimensions

| Dimension | Look for |
| :--- | :--- |
| Requirements and logic | Missing behavior, wrong results, boundary inputs, error paths, and incomplete fixes. |
| Interfaces and state | Broken callers, contract mismatches, invalid transitions, and inconsistent persistence. |
| Security and data | Permission bypasses, unsafe inputs, sensitive-data exposure, data loss, and incorrect writes. |
| Concurrency and scale | Races, duplicate execution, incorrect shared state, and failures at the expected workload. |
| Performance | Regressions large enough to affect the required behavior or user experience. |
| Tests and verification | Whether critical logic is exercised and the checks would expose its failure. Missing tests alone are a verification gap, not proof of a bug. |

## Key Rules

- Report only concrete defects affecting the scoped behavior. Identify the trigger, code path, wrong result and impact, and why existing protections do not prevent it. Distinguish regressions from pre-existing defects.
- Re-read the relevant lines and callers before reporting. Cite the exact file and line at the reviewed revision; provide a reproduction or code evidence and the smallest sufficient fix.
- Do not turn speculation, intentional tradeoffs, style preferences, or unrelated cleanup into findings. Style issues that cause a concrete behavioral defect can be reported for that defect.
- State scope briefly, order defects by severity, and omit empty groups. Keep missing tests and other unverified areas under verification.
- A clean review is valid. With no verified defects, give a concise no-findings conclusion, the reviewed scope, and relevant verification or coverage gaps. Do not invent findings or claim that all bugs have been ruled out.
- Review requests do not authorize repairs. If repairs are explicitly requested, stay within that scope, review the resulting diff, and repeat the relevant verification before the final verdict.

## Output

Use the user's language for output labels and content.

```text
🔍 [amo-review] Scenario: Functional review
Conclusion:
Review scope:
Must fix:
Suggested fixes:
Verification and uncovered areas:
```
