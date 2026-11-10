---
name: amo-deliver
description: Use when completed feature or branch work needs final acceptance and closeout, internal or external review feedback rounds, or delivery of a reviewed branch. Automate independent final reviews and verified repairs through convergence. Not for mid-development review, single-feedback verification, or coordination from requirements onward.
metadata:
  version: '0.3.1'
---

# Amo Deliver

Close a finished branch: local experience, independent final review, feedback rounds, and converged delivery.

## Shared Output Marker

Prefix each stage report's first line inline with `📦 [amo-deliver]`. Do not put the marker in a separate paragraph.

## Use When

- Development is complete and the user asks to wrap up, accept, or deliver the feature.
- amo-workflow reaches final acceptance and closeout.
- Review reports arrive during closeout, or the user asks to push or hand off an already-reviewed branch.

## Do Not Use

- Functional review during development; use amo-review.
- Single-feedback verification without closeout; use amo-check.
- Coordination from requirements to acceptance; use amo-workflow.

## Workflow

1. Resolve the branch and acceptance progress from context and read the project rules. Have the user try the finished work locally; reuse an existing valid acceptance result. Route adjustments to amo-improve or amo-fix, then return to closeout.
2. Run internal final review automatically:
   - Choose one review session for localized, straightforward changes; choose two for complex changes with interacting modules, state transitions, concurrency, or data risks. Reassess each round and state the count and reason under Round status.
   - Read the orchestration skill and follow its runtime guide to start the selected number of fresh Claude Code review sessions in Orca, using the configured model. Give each the same branch, baseline, and target revision, with a read-only assignment to read and use the `/open-code-review-delegate` skill (`/open-code-review-delegate <branch>`).
   - Collect all selected reports through orchestration's completion protocol, ending the turn when that protocol requires it; process the round when all results return without asking the user to copy them. If a required capability is unavailable, report the blocker and preserve the pending task; do not substitute the reviewer or claim completion.
   - Register findings by round, severity, claim, and status; deduplicate and retain only High/Medium. Discard Low silently.
3. Process each internal or external feedback round; external reports are pasted by the user:
   - Read and use amo-check before changing code. Classify findings as must-fix, acceptable tradeoff (record remaining impact in the residual risk list), or false positive (discard silently). Keep unverified claims as gaps. Check step 4's stop-loss condition before further repairs.
   - For must-fix findings, identify the introducing commit and the repair approach. Continue within existing repair authorization; ask only for a changed requirement, scope expansion, or missing permission.
   - Implement in an isolated temporary Git worktree, preserving the main checkout. If the target branch is already checked out, use a temporary repair branch from its revision. Commit and integrate repairs only as authorized; remove the worktree after changes are safely retained, otherwise retain it and report its location.
   - Prove each new regression test fails on the pre-fix code for the intended reason, then passes after the fix. Use actual producer data structures and relevant boundary cases. Run related tests and applicable build/type checks.
   - Self-review the final diff across three dimensions: new mechanism combined with existing behavior, trigger frequency, and steady state across runs or days. Update residual risks; never promise zero defects.
   - Repeat step 2 on the repaired revision unless the stop-loss rule applies.
4. Track rounds and severity trends; state when impact is not decreasing. Stop patching if a subsequent review confirms a problem introduced by a repair: use amo-draft to document known limitations and prepare a separate follow-up requirement. Offer limited delivery for the user's decision; do not automatically merge. Explicitly remind the user of this stop-loss rule after two repair rounds.
5. Present the commit chain, per-round results, and remaining limitations for final acceptance. On an explicit push request, confirm the unpushed commits and push the branch; report the actual result.

## Key Rules

- Use the smallest necessary fix for a verified issue; do not refactor unrelated code or expand functionality. Check affected existing behavior and verify that the fix introduces no new regressions.
- Keep reviewers independent of the delivery session and, when using two, each other. Share only the review target, necessary requirements, and repository rules; exclude delivery discussion, proposed fixes, and previous reports. Use fresh sessions for every review round.
- Verify criticism rather than defending the implementation; do not treat a deferred risk as accepted without the user's decision.
- Separate commit and push authorization. Commit confirmed repairs under project permissions; push, merge, and external handoff require explicit instructions.

## Output

Use the user's language for output labels and content. The labels are the mandatory skeleton: emit every label in order, place all content under its matching label — never unlabeled prose, never merged; keep empty sections with a brief note.

```text
📦 [amo-deliver] Closing loop: <branch>
Round status:
Fix delivery:
Convergence:
Ship:
```

In the final response after the entire amo-deliver workflow completes, append Change summary and Self-test result after Ship, using one sentence each to summarize the entire branch's final changes and self-test results; omit both labels and placeholders before then.
