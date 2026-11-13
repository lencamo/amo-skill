---
name: amo-review
description: Review implemented functionality for requirement gaps, logic errors, and bugs across workspace changes, specified commits, or an entire feature branch. Use when the user asks whether an implementation is correct or ready to merge. Not for code-style-only reviews, solution design, or diagnosing a known failure to choose a fix.
metadata:
  version: '0.5.0'
---

# Amo Review

Review functional correctness with concrete evidence. Default to reporting findings without changing code.

## Shared Output Marker

For a complete deliverable, prefix its first line inline with `🔍 [amo-review]`. Do not put the marker in a separate paragraph.

## Use When

- The user wants to check implemented behavior against requirements or find logic errors, missed cases, and potential bugs.
- The target is workspace changes, specified commits, a commit range, or a feature branch.

## Do Not Use

- Code style, redundancy, abstraction, or type-expression review alone.
- Verifying existing review feedback and whether action is necessary now; use `amo-check`.
- Diagnosing a known failure and choosing a fix; use `amo-fix`.
- Designing or reassessing a proposal before implementation.

## Review Scope

Honor the user's explicit scope first. For a generic implementation-review request on a feature branch, review the whole branch; on its base branch, review workspace changes. If neither has changes, report that rather than silently choosing the last commit. Resolve an uncertain base from project context and history; ask only when ambiguity materially changes the scope.

| Scope | Review surface |
| :--- | :--- |
| Workspace | Combined staged and unstaged tracked changes against `HEAD`, plus full untracked files. Account for deletions as well as additions. |
| Specified commits | Each requested commit's changes, or the net diff of an explicitly requested range. Preserve an explicit commit selection rather than expanding it to include intervening commits. |
| Feature branch | Resolve the base and target to commit IDs, find their merge base, and review the net diff from that point to the target. Use history to explain intent, not to report intermediate defects already fixed in the final state. |

Record the resolved mode, baseline, target, and file inventory once before reviewing. Use `(path, status)` to distinguish changes, including a tracked deletion followed by an untracked recreation at the same path; record explicit exclusions and their reasons separately. Read files at the reviewed revision; working files may differ from a selected commit or branch. For commit and branch scopes, state whether uncommitted changes are included and keep them outside scope unless requested.

Use read-only Git inspection and preserve the worktree and index. Missing refs or unreadable files are coverage gaps, not permission to substitute another scope.

## Workflow

1. Resolve the scope and expected behavior from the request, requirements, acceptance criteria, project docs, tests, and existing contracts. Read applicable repository and path-specific rules directly and reuse them for files governed by the same rules; an unreadable or unsupported required rule source is a coverage gap. Distinguish documented intent from inference. Compare the changes with the stated goal: identify missing requirements, off-target behavior, and unrelated changes. Report scope deviations separately from functional defects.
2. Read every selected diff, batching files by shared rules, technology, or repeated change pattern. Read shared implementation and context once, then verify each changed caller's bindings, arguments, and special conditions; grouping does not permit sampling callers. Use bounded batches when output would truncate. Trace relevant callers, callees, prior content for deletions, tests, configuration, and storage contracts. When result sources or record lifecycles change, check existing actions on those results under the newly reachable states, including records no longer present in the previous source.
3. Apply the dimensions below to the actual contracts and expected load. Prioritize deeper tracing where shared interfaces, state/lifecycles, concurrency, permissions, or persisted data change. Read only the relevant sections of [stack-specific checks](references/stack-checks.md) for Vue/TypeScript or Python changes, selecting by the actual framework and code rather than the extension alone; other stacks continue with the general dimensions. Trace a concern from its input or producer through the changed logic to its observable consequence, checking caller validation and existing guards before escalating it. For high-risk flows, identify what must remain true and vary relevant timing, input, or permission conditions. For bug fixes, check directly related paths for the same defect. Extend investigation only to resolve a contract, guard, or concrete concern; do not turn a change review into an unrelated whole-repo audit.
4. Verify each candidate finding against reachable inputs, downstream behavior, and existing guards. For timing-, state-, or environment-dependent behavior, prefer a minimal observable reproduction; deterministic static evidence is also valid. Inspect available verification evidence and its coverage. Reuse results when the relevant code, tests, configuration, and environment remain unchanged; a different commit message alone does not invalidate them. Run a focused check when it resolves a concrete concern or coverage gap, following the caller's verification constraints. Use a one-shot command, confirm that the runner honors the requested file scope and concurrency, and preserve its actual exit status and full failure output. Distinguish executed checks, reused results, static reasoning, and unavailable checks. When a review conclusion depends on real-dependency behavior that mocks or substitute services do not exercise, report that verification gap.
5. Reconcile the inventory with reviewed and skipped entries, each skipped entry having a reason; unread or truncated content cannot count as reviewed. Continue through the remaining scope after finding a severe defect. Before reporting, refresh affected evidence if the target or relevant working files changed. Summarize reviewed/total counts, skips, and exclusions; counts describe coverage, not proof of correctness. Delegated reports must also identify the baseline and target and distinguish executed, reused, and unavailable checks. Finish when the agreed scope is accounted for and candidate findings are confirmed, rejected, or explicitly unverified; reopen only for new evidence or invalidated coverage.

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
- State scope briefly, classify defects by actual impact as Critical, High, Medium, or Low, and omit empty groups. Keep missing tests and other unverified areas under verification.
- A clean review is valid. With no verified defects, give a concise no-findings conclusion, the reviewed scope, and relevant verification or coverage gaps. Do not invent findings or claim that all bugs have been ruled out.
- Review requests do not authorize repairs. If repairs are explicitly requested, stay within that scope, review the resulting diff, and repeat the relevant verification before the final verdict.

## Output

Use the user's language and requested level of detail. Lead with the answer to the current request. For a complete deliverable, follow the format below, preserving label order and omitting inapplicable sections. For a focused follow-up, answer only that question and any qualification needed to interpret the answer; do not repeat the report or restart workflow routing.

```text
🔍 [amo-review] Scenario: Functional review
Conclusion:
Review scope:
Must fix:
Suggested fixes:
Verification and uncovered areas:
```
