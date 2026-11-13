---
name: amo-review
description: Review implemented functionality with risk-proportionate static checks for requirement gaps, logic errors, and bugs across workspace changes, specified commits, or a feature branch. Use when the user asks whether an implementation is correct or ready to merge. Not for code-style-only reviews, solution design, or diagnosing a known failure to choose a fix.
metadata:
  version: '0.6.0'
---

# Amo Review

Review functional correctness with concrete evidence and depth proportional to the change's risk. Used alone, perform the review; during delivery, provide the standards without duplicating the independent review arranged by amo-deliver. Default to static analysis and a report without changing code.

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

Record the resolved mode, baseline, target, and inclusion of uncommitted changes once. Read files at the reviewed revision; working files may differ from a selected commit or branch. Preserve explicitly excluded changes and report material unread or unavailable scope without counting it as reviewed.

Use read-only Git inspection and preserve the worktree and index. Missing refs or unreadable files are coverage gaps, not permission to substitute another scope.

## Review Depth

- Classify the change by behavior and consequences, not file count or diff size. Display-only text, comments, and non-executable prose need replacement, omission, and unintended-change checks. Text used by selectors, protocols, templates, or business decisions, and executable instructions, can change behavior and require the corresponding review.
- For local changes, inspect the changed logic and directly affected contracts. For routine features, follow changed inputs, state, and outputs. For permissions, money, data integrity, migrations, or concurrency, trace the relevant protections and failure paths even when the diff is small.
- Select only applicable dimensions below. Consult the relevant [stack-specific checks](references/stack-checks.md) only when a changed behavior or concrete concern calls for them; do not expand every change into all checks or a repository audit.

## Workflow

1. Resolve the scope, expected behavior, and applicable project rules. Reuse shared context and distinguish requirements from inference. Check for omissions, off-target behavior, and unrelated changes.
2. Read the scoped diff in bounded batches. Group repeated replacements and check their coverage; read callers, dependencies, history, or configuration only to understand changed behavior or resolve a concrete concern. Check deleted behavior as well as additions.
3. Verify candidate defects against reachable inputs, existing guards, and observable consequences. Deterministic code evidence is sufficient; a runtime reproduction is not a prerequisite for every finding. Reject unsupported candidates and keep conclusion-changing uncertainties as gaps.
4. Reuse available verification evidence when relevant code, tests, configuration, and environment are unchanged; a commit-message change alone does not invalidate it. Default to no test or build execution during review. If a concrete concern needs runtime evidence, identify the focused check for a separate verification step. Follow explicit user or project verification requirements without silently broadening them, and distinguish static reasoning, reused results, and missing evidence.
5. Report confirmed findings, the actual reviewed scope, and material exclusions or gaps. Refresh affected evidence if the target changes. Finish when the scoped checks and candidate findings are settled; an empty findings list is a valid outcome. Do not reopen unchanged scope to seek more comments or to reach an arbitrary duration.

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
