---
name: amo-best
description: Use when the user challenges an existing proposal, asks whether it is the best solution, asks for a better approach, or wants second-pass review of the chosen best-standard, tradeoffs, scope, compatibility, risk, or refactor depth before implementation.
metadata:
  version: '0.3.0'
---

# Amo Best

Re-check the selected best standard and pressure-test an existing proposal.

## Shared Output Marker

For a complete deliverable, prefix its first line inline with `🏆 [amo-best]`. Do not put the marker in a separate paragraph.

## Use When

- A candidate solution already exists.
- The user asks "is this the best solution?", "is there a better way?", or "best approach?"
- The user challenges tradeoffs, compatibility choices, scope, risk, or refactor depth.

## Do Not Use

- No candidate solution exists yet; first use `amo-feature`, `amo-improve`, `amo-fix`, or `amo-refactor`.
- The user only asks for a direct small edit.
- The task is code review of an implemented diff.

## Best Standard Review

Re-evaluate the candidate against exactly one primary standard:

- **Target-state best**: default for development-stage work when no explicit constraint is stated; prioritize correct boundaries, long-term maintainability, refactoring when needed, and not bending the design around legacy implementation.
- **Constraint best**: use when the user requires fast delivery, compatibility, minimal change, short-term delivery, or limited scope.
- **Evolutionary best**: use when the target design is right, but should be delivered in safe, staged steps.
- **Lowest-risk best**: use when production, data, security, auth/permission, payment, migration, or rollback risk dominates.

If the proposal used the wrong standard, say so before judging the implementation approach.

## Workflow

1. Restate the candidate solution and primary scenario.
2. State the original best standard if known.
3. Select the correct best standard and explain why.
4. Test whether the proposal solves the root goal under that standard.
5. Compare against at most two alternatives only when they are materially better.
6. Give one verdict: keep, adjust, or replace.

## Key Rules

- Do not call a solution "best" without saying which standard it is best under.
- Do not accept a workaround as best unless the selected standard is explicitly constraint best.
- Do not bias toward backward compatibility unless compatibility is part of the selected standard.
- Reject speculative compatibility paths, fallback branches, or legacy handling unless backed by code evidence or explicit user requirements.
- For complex proposals involving queries, batch processing, multi-step data flows, or concurrent operations, check for overlooked query costs, resource use, and concurrency risks that could change the verdict. Assess optimization necessity and evidence against relevant implementation and known workload; state unknown conditions and reject unsupported architectural expansion.
- Recommend one final approach.

## Output

Use the user's language and requested level of detail. Lead with the answer to the current request. For a complete deliverable, follow the format below, preserving label order and omitting inapplicable sections. For a focused follow-up, answer only that question and any qualification needed to interpret the answer; do not repeat the report or restart workflow routing.

```text
🏆 [amo-best] Scenario: best-solution pressure test
Original proposal:
Best standard review:
Verdict: keep / adjust / replace
Root goal fit:
Main tradeoffs:
Better approach:
Final recommendation:
Verification:
```
