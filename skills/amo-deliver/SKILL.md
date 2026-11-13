---
name: amo-deliver
description: Use when completed feature or branch work needs final acceptance and closeout, internal or external review feedback rounds, or delivery of a reviewed branch. Automate independent final reviews and verified repairs through convergence. Not for mid-development review, single-feedback verification, or coordination from requirements onward.
metadata:
  version: '0.9.0'
---

# Amo Deliver

Close a finished branch: local experience, independent final review, feedback rounds, and converged delivery.

## Shared Output Marker

For a stage report, prefix its first line inline with `📦 [amo-deliver]`. Do not put the marker in a separate paragraph.

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
   - Reuse a completed independent review when it still covers the target code, requirements, and acceptance scope; do not launch another review solely because delivery entered a new stage. The implementer's self-check is not an independent review. If relevant changes invalidate that coverage, arrange review of the affected scope.
   - Default to one review session. Use two only when the change has two distinct high-risk concerns that warrant complementary review, such as business correctness and concurrency safety, or migration integrity and rollback. File count alone does not justify two: styling and repeated component replacements remain single-review work unless they introduce such risks. Reassess each round; under Round status, state the count and, for two, each review focus and why one session is insufficient.
   - For a new review, read the orchestration skill and follow its runtime guide to start the selected number of fresh Claude Code review sessions in Orca, using the configured model. Give each the same branch, baseline, and target revision, with a read-only assignment to read and use `amo-review`. Its rules govern code review; Orca handles session execution and report return. Missing `amo-review` is a capability gap, not a reason to substitute another review skill or install an external review CLI.
   - Include the verification constraints below and available self-test evidence in each assignment: tested revision, commands, covered scope, results, and artifact locations. The reviewer's independent assessment and evidence handling follow `amo-review`. Run the full suite only when a specific coverage need cannot be met by focused checks.
   - Coordinate supplemental verification across this delivery's review sessions on the same local host: before starting a test or build, the reviewer sends the question, command, and scope through orchestration's request/reply protocol. The coordinator grants one running verification command at a time, including its own checks; tests default to one worker. Reviewers may execute their own checks after that grant while other sessions continue reading code. Record owned task/process handles so cancellation can reach background work. On a timeout, inspect status, resource use, and whether the intended scope/options took effect; confirm the previous command exited before a justified retry. Do not automatically repeat or broaden the run. If a check cannot finish, stop its owned command and collect the code findings and explicit verification/cleanup gaps rather than waiting indefinitely or treating it as passed.
   - Collect all selected reports through orchestration's completion protocol, ending the turn when that protocol requires it; process the round when all results return without asking the user to copy them. If a required capability is unavailable, report the blocker and preserve the pending task; do not substitute the reviewer or claim completion.
   - After each review attempt settles, preserve available findings/output, reconcile its recorded test/build handles, and stop leftover owned verification commands through their runtime cancellation protocol. Confirm exit before reporting process cleanup complete. Follow orchestration's current guide for automatic or explicit release of its proven dedicated terminal; scheduled or pending release is not confirmed release. Honor keep-open and user takeover; preserve pre-existing terminals and any terminal hosting a development/acceptance service that must remain available. Handle terminal release, temporary-worktree cleanup, and log retention independently; do not require workspace or log deletion before releasing an otherwise eligible terminal.
   - Register findings by round, severity, claim, and status; deduplicate and retain Critical/High/Medium. Discard Low silently.
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
- Keep reviewers independent of the delivery session and, when using two, each other. Share the review target, necessary requirements, repository rules, verification constraints, and objective self-test evidence; exclude delivery discussion, proposed fixes, and previous review reports. Use fresh sessions for each new review round; reusing a completed valid review does not start a round.
- If the user reports machine resource pressure, stop the review-owned verification commands before continuing diagnosis. On review cancellation, stop both the assigned agent and its owned background test/build processes using the runtime's ownership and cancellation protocol; preserve unrelated sessions and development services. Confirm exit before reporting that work has stopped. If ownership or exit cannot be verified, report the remaining process and the cleanup gap rather than claiming completion. Cancelled reviews remain incomplete and are not restarted without the user's instruction.
- Keep review/verification outcomes separate from cleanup status. A release failure does not invalidate a completed review or justify another review session. Follow runtime recovery instructions only for the failed cleanup, recording retained resources, reasons, and next actions. For a failed worker attempt, use the runtime's same-task retry protocol after its predecessor is confirmed stopped; respect retry limits rather than creating a new task to bypass them.
- Verify criticism rather than defending the implementation; do not treat a deferred risk as accepted without the user's decision.
- Separate commit and push authorization. Commit confirmed repairs under project permissions; push, merge, and external handoff require explicit instructions.

## Output

Use the user's language and requested level of detail. Lead with the answer to the current request. For a complete deliverable, follow the format below, preserving label order and omitting inapplicable sections. For a focused follow-up, answer only that question and any qualification needed to interpret the answer; do not repeat the report or restart workflow routing.

```text
📦 [amo-deliver] Closing loop: <branch>
Round status:
Fix delivery:
Convergence:
Ship:
```

In the final response after the entire amo-deliver workflow completes, append Change summary, Self-test result, and Deployment notes after Ship. Use one sentence each for the entire branch's final changes and self-test results; omit these three labels and placeholders before then.

Derive Deployment notes from the entire branch's actual changes, configuration, and deployment/migration entry points. List required env names, whether mandatory and their defaults; SQL/migration script paths and execution order/timing, separating automatic startup migrations from manual operations; and other necessary dependency, build, restart, or backfill steps. Mark unverified requirements as gaps; state No additional deployment actions only when verified.
