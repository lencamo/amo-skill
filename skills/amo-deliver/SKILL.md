---
name: amo-deliver
description: Use when completed feature or branch work needs final acceptance and closeout, internal or external review feedback rounds, or delivery of a reviewed branch. Automate independent final reviews and verified repairs through convergence. Not for mid-development review, single-feedback verification, or coordination from requirements onward.
metadata:
  version: '0.10.0'
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
2. Arrange proportionate independent review:
   - Reuse a completed independent review when it still covers the target code, requirements, and acceptance scope; do not launch another review solely because delivery entered a new stage. The implementer's self-check is not an independent review. If relevant changes invalidate that coverage, arrange review of the affected scope.
   - Apply amo-review's risk criteria before launching a session. For changes confined to display text, comments, or non-executable prose with unchanged behavior, reuse implementation self-checks and record independent review as not applicable, unless explicitly requested or required by project rules. Do not treat executable instructions, selectors, protocol values, or business rules as harmless prose. For other changes, use one independent session.
   - Select the local `/code-review` effort automatically from the actual risk: `low` for bounded low-risk changes, `medium` for routine features, and `high` for sensitive or complex behavior; use `max` only for a concrete need for deeper analysis. State the selected effort and reason briefly. Respect an explicit effort request; do not run levels in sequence, inherit a previous level, or escalate because of file count alone.
   - Read the orchestration skill and follow its runtime guide to launch a fresh Claude Code session in Orca with the configured model. Assign the built-in local `/code-review`, not the legacy GitHub plugin, cloud Code Review, ultrareview, or OCR delegate. Pass the explicit effort and resolved review target; for a contiguous committed range, use `/code-review <effort> <base-sha>..<target-sha>` with the review baseline already resolved to the appropriate merge base. Preserve explicit commit selections. If workspace changes are included, identify their staged, unstaged, and untracked contents and detect changes to those inputs during review; never silently omit them or substitute a different scope.
   - Give the reviewer only the fixed scope, concise requirements and relevant project constraints, and existing verification evidence: revision, commands, scope, results, and available logs. Request a read-only report of concrete defects and material gaps, with no `--fix`, `--comment`, tests, or builds. Have it identify any focused runtime evidence still needed for a separate verification step. Do not assign a second amo-review pass alongside the built-in review. If the local command, explicit effort, or required scope is unavailable, report the capability gap rather than substituting another reviewer or installing tools.
   - Collect the actual findings through orchestration's completion protocol, ending the turn when it requires it. A background `/code-review` launch or task handle is not a completed report: the worker must wait for its review result before reporting completion. Process returned findings without asking the user to copy them. Report unavailable or interrupted coverage as incomplete, not passed.
   - After each review attempt settles, preserve available findings/output, reconcile its recorded test/build handles, and stop leftover owned verification commands through their runtime cancellation protocol. Confirm exit before reporting process cleanup complete. Follow orchestration's current guide for automatic or explicit release of its proven dedicated terminal; scheduled or pending release is not confirmed release. Honor keep-open and user takeover; preserve pre-existing terminals and any terminal hosting a development/acceptance service that must remain available. Handle terminal release, temporary-worktree cleanup, and log retention independently; do not require workspace or log deletion before releasing an otherwise eligible terminal.
   - Register findings by round, severity, claim, and status; deduplicate and retain Critical/High/Medium. Discard Low silently.
3. Process each internal or external feedback round; external reports are pasted by the user:
   - Read and use amo-check before changing code. Classify findings as must-fix, acceptable tradeoff (record remaining impact in the residual risk list), or false positive (discard silently). Keep unverified claims as gaps. Check step 4's stop-loss condition before further repairs.
   - For must-fix findings, identify the introducing commit and the repair approach. Continue within existing repair authorization; ask only for a changed requirement, scope expansion, or missing permission.
   - Default to repairing in the target branch's existing worktree or main checkout, preserving unrelated changes. If the target branch has no checkout, create a worktree directly on that branch. Create an additional temporary worktree and repair branch only when conflicting concurrent edits or an explicit isolation requirement prevents using the existing checkout; state that reason. Follow the environment's worktree management instructions.
   - For behavioral repairs, add a focused regression test where useful and prove it fails for the intended reason before the fix and passes afterward. Use actual producer data structures and relevant boundary cases. Apply amo-implement's proportionate verification rules; trivial text corrections do not require a new regression suite. Keep test/build execution in this verification step and preserve its actual results.
   - Self-check the repair against affected existing behavior; examine trigger frequency and repeated-run or cross-day state when relevant. Update residual risks; never promise zero defects.
   - Commit and integrate verified repairs only as authorized. Confirm the target branch contains the intended repairs before reporting them delivered. Once no uncommitted or untransferred work remains in temporary resources, clean up the temporary worktrees and repair branches created by this task within Git authorization; preserve the target branch and pre-existing worktrees. If integration or cleanup is blocked, retain the resources and report their names, locations, and reason.
   - Unless the stop-loss rule applies, recheck the repair diff and affected contracts on the repaired revision, retaining valid coverage of unchanged code. Request another independent review only for coverage invalidated by the repair; expand to the whole branch only when new behavior or risk invalidates that broader coverage.
4. Track rounds and severity trends; state when impact is not decreasing. Stop patching if a subsequent review confirms a problem introduced by a repair: use amo-draft to document known limitations and prepare a separate follow-up requirement. Offer limited delivery for the user's decision; do not automatically merge. Explicitly remind the user of this stop-loss rule after two repair rounds.
5. Present the commit chain, per-round results, and remaining limitations for final acceptance. On an explicit push request, confirm the unpushed commits and push the branch; report the actual result.

## Key Rules

- Use the smallest necessary fix for a verified issue; do not refactor unrelated code or expand functionality. Check affected existing behavior and verify that the fix introduces no new regressions.
- Keep the reviewer independent of the delivery session. Share the review target, necessary requirements, repository rules, verification constraints, and objective self-test evidence; exclude delivery discussion and preferred conclusions. For a repair recheck, include the confirmed trigger and required behavior without replaying the entire previous review. Use a fresh session for a new independent review; reusing valid evidence does not start a round.
- Treat elapsed time as an efficiency signal, not a fixed deadline or a quality verdict. If a review takes unexpectedly long, inspect task progress, scope, resource use, and unintended test/build work through the runtime's supported controls. Correct the cause without automatically rerunning, broadening scope, or raising effort; report a stall or remaining gap rather than waiting silently. Runtime failure timeouts remain separate from review quality.
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
