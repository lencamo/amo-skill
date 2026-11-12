---
name: amo-deliver
description: Use when completed feature or branch work needs final acceptance and closeout, internal or external review feedback rounds, or delivery of a reviewed branch. Automate independent final reviews and verified repairs through convergence. Not for mid-development review, single-feedback verification, or coordination from requirements onward.
metadata:
  version: '0.6.0'
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
   - Default to one review session. Use two only when the change has two distinct high-risk concerns that warrant complementary review, such as business correctness and concurrency safety, or migration integrity and rollback. File count alone does not justify two: styling and repeated component replacements remain single-review work unless they introduce such risks. Reassess each round; under Round status, state the count and, for two, each review focus and why one session is insufficient.
   - Read the orchestration skill and follow its runtime guide to start the selected number of fresh Claude Code review sessions in Orca, using the configured model. Give each the same branch, baseline, and target revision, with a read-only assignment to read and use the `/open-code-review-delegate` skill (`/open-code-review-delegate <branch>`).
   - Include the verification constraints below and available self-test evidence in each assignment: tested revision, commands, covered scope, results, and artifact locations. Reviewers must independently inspect code and test coverage; existing results are evidence, not a correctness verdict. Reuse valid evidence for the target revision instead of mechanically rerunning checks. Reviewers may independently reproduce a concrete concern or add a focused check; state the question it resolves. Run the full suite only when a specific coverage need cannot be met by focused checks.
   - Coordinate supplemental verification across review sessions on the same local host: run one test or build command at a time, with one test worker by default. Do not start another copy while a command is still running. On a timeout, inspect its status and resource use before deciding whether a retry is justified; do not automatically repeat or broaden the run. Preserve full failure output and the command's actual exit status. Record owned task/process handles so cancellation can reach background work.
   - Collect all selected reports through orchestration's completion protocol, ending the turn when that protocol requires it; process the round when all results return without asking the user to copy them. If a required capability is unavailable, report the blocker and preserve the pending task; do not substitute the reviewer or claim completion.
   - Register findings by round, severity, claim, and status; deduplicate and retain only High/Medium. Discard Low silently.
3. Process each internal or external feedback round; external reports are pasted by the user:
   - Read and use amo-check before changing code. Classify findings as must-fix, acceptable tradeoff (record remaining impact in the residual risk list), or false positive (discard silently). Keep unverified claims as gaps. Check step 4's stop-loss condition before further repairs.
   - For must-fix findings, identify the introducing commit and the repair approach. Continue within existing repair authorization; ask only for a changed requirement, scope expansion, or missing permission.
   - Default to repairing in the target branch's existing worktree or main checkout, preserving unrelated changes. If the target branch has no checkout, create a worktree directly on that branch. Create an additional temporary worktree and repair branch only when conflicting concurrent edits or an explicit isolation requirement prevents using the existing checkout; state that reason. Follow the environment's worktree management instructions.
   - Prove each new regression test fails on the pre-fix code for the intended reason, then passes after the fix. Use actual producer data structures and relevant boundary cases. Run related tests and applicable build/type checks.
   - Self-review the final diff across three dimensions: new mechanism combined with existing behavior, trigger frequency, and steady state across runs or days. Update residual risks; never promise zero defects.
   - Commit and integrate verified repairs only as authorized. Confirm the target branch contains the intended repairs before reporting them delivered. Once no uncommitted or untransferred work remains in temporary resources, clean up the temporary worktrees and repair branches created by this task within Git authorization; preserve the target branch and pre-existing worktrees. If integration or cleanup is blocked, retain the resources and report their names, locations, and reason.
   - Repeat step 2 on the repaired revision unless the stop-loss rule applies.
4. Track rounds and severity trends; state when impact is not decreasing. Stop patching if a subsequent review confirms a problem introduced by a repair: use amo-draft to document known limitations and prepare a separate follow-up requirement. Offer limited delivery for the user's decision; do not automatically merge. Explicitly remind the user of this stop-loss rule after two repair rounds.
5. Present the commit chain, per-round results, and remaining limitations for final acceptance. On an explicit push request, confirm the unpushed commits and push the branch; report the actual result.

## Key Rules

- Use the smallest necessary fix for a verified issue; do not refactor unrelated code or expand functionality. Check affected existing behavior and verify that the fix introduces no new regressions.
- Keep reviewers independent of the delivery session and, when using two, each other. Share the review target, necessary requirements, repository rules, verification constraints, and objective self-test evidence; exclude delivery discussion, proposed fixes, and previous review reports. Use fresh sessions for every review round.
- If the user reports machine resource pressure, stop the review-owned verification commands before continuing diagnosis. On review cancellation, stop both the assigned agent and its owned background test/build processes using the runtime's ownership and cancellation protocol; preserve unrelated sessions and development services. Confirm exit before reporting that work has stopped. If ownership or exit cannot be verified, report the remaining process and the cleanup gap rather than claiming completion. Cancelled reviews remain incomplete and are not restarted without the user's instruction.
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

In the final response after the entire amo-deliver workflow completes, append Change summary, Self-test result, and Deployment notes after Ship. Use one sentence each for the entire branch's final changes and self-test results; omit these three labels and placeholders before then.

Derive Deployment notes from the entire branch's actual changes, configuration, and deployment/migration entry points. List required env names, whether mandatory and their defaults; SQL/migration script paths and execution order/timing, separating automatic startup migrations from manual operations; and other necessary dependency, build, restart, or backfill steps. Mark unverified requirements as gaps; state No additional deployment actions only when verified.
