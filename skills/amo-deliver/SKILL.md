---
name: amo-deliver
description: Use when completed feature or branch work needs final acceptance and closeout, internal or external review feedback rounds, or delivery of a reviewed branch. Automate independent final reviews and verified repairs through convergence. Not for mid-development review, single-feedback verification, or coordination from requirements onward.
metadata:
  version: '0.13.0'
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

## Push-Only Requests

When the user only asks to push an existing branch, confirm its identity, remote/upstream, and outgoing commits. If applicable verification is already complete and no new change invalidates it, push within authorization and report the result without restarting experience, review, or acceptance. If verification is missing, report the gap without claiming delivery readiness or treating the push request as authorization for new review/test rounds. Honor any mandatory project checks. Do not commit pending changes or merge/deploy as part of a push request.

## Workflow

1. Resolve the target, project rules, existing authorization, acceptance progress, and available verification. Reuse valid decisions and evidence. Offer the applicable running entry for user acceptance without adding an approval prerequisite to an already authorized commit/push. Investigate only unresolved behavior before routing to amo-improve or amo-fix.
2. Reuse completed independent review that still covers the target code, requirements, and acceptance scope. Otherwise select the review path below and arrange at most one independent reviewer for the initial scoped review. The implementer's self-check is not independent review. A stage transition or commit alone does not require another session.
3. Evaluate returned feedback using amo-check in the coordinating session. Verify candidate findings and disputed evidence, not the entire diff again; do not start another review or require a separate verification report for this step. Deduplicate by trigger, violated contract, and consequence. Judge severity by verified impact rather than incoming labels. Retain confirmed unmet requirements/acceptance criteria and Critical/High/Medium defects; discard non-blocking Low suggestions and false positives without a rejection appendix. Leave unverified claims as gaps.
4. Repair confirmed defects within existing authorization. Identify the introducing revision and affected contract, then use amo-implement to inspect its direct callers and make the smallest complete repair. Add a focused regression test where useful and establish failure before the fix and success afterward. Reuse unaffected checks; run tests/builds in this verification step, not in the reviewer. Apply the repair-recheck rules below.
5. Deliver when required defects are resolved and applicable evidence covers the target. State material gaps or remaining risks for the user's decision; elapsed time, round count, or an empty findings list alone cannot establish readiness. Report each completed repair round proactively with one sentence on changes and one on actual self-test results. Present actual commit/push status and acceptance needs without a full report per stage.

## Review Path

Apply amo-review's risk criteria by behavior and consequences, not file count:

| Change | Default review |
| :--- | :--- |
| Display text, comments, non-executable prose, or bounded presentation-only changes | Reuse implementation self-checks and applicable page verification; record independent review as not applicable unless explicitly requested or required by project rules. Confirm event semantics, link targets, requests, persistence, permissions, and business rules are unchanged. |
| Bounded logic changes or local repairs | One independent reviewer inspects the diff and directly affected contracts using amo-review. Trace data-loss and other critical failure paths even in a small patch. |
| Permissions, money, tenant isolation, migrations, or complex concurrency and business flows | Independent in-depth review of the relevant protections and connected paths. Select dimensions for the concrete risks rather than running every checklist. |

Prefer direct review in one fresh independent session for bounded changes. Use the host's available delegation; read the corresponding runtime guide when needed. Do not ask that reviewer to start another review process by default. For complex work, an available built-in local `/code-review` is an optional executor of the same standards, not a mandatory extra pass. Respect the user's requested reviewer, tool, model, effort, and project requirements. If a required capability is unavailable, report the gap rather than silently substituting it or installing tools. For Orca or local Claude `/code-review`, first read [review-runtime.md](references/review-runtime.md).

Give the reviewer the fixed baseline/target, requirements and confirmed constraints with their basis, relevant project rules, and objective verification evidence (revision, command, scope, result, available logs). Include prior decisions needed to avoid reopening unchanged issues, not delivery discussion or preferred conclusions. Preserve explicit commit selections; identify staged, unstaged, and untracked inputs when included, and detect changes during review. Require read-only findings with a trigger, violated contract, wrong result, impact, and source location, plus material coverage gaps. No tests, builds, fixes, or nested delegation unless explicitly assigned. Accept a concise no-findings result. Do not require a standalone long report or another full pass to reformat it.

Maintain one compact record of reviewed scope/revision, valid verification, and findings with their decision, basis, and status. Reuse unchanged coverage and settled decisions; reopen an item only when new evidence changes its trigger, contract, consequence, or decision basis. A prior dismissal does not excuse a newly demonstrated requirement violation.

## Repair Recheck

- Check that the original trigger is resolved, directly affected callers retain their behavior, and relevant regression evidence covers the repaired target. A bounded repair with clear code evidence, focused passing tests, and no new risk can close with this targeted check; identify it as implementer verification, not a new independent review.
- Request independent recheck when a repair changes or exposes critical protections, complex state transitions, or material behavior not covered by the existing review and regression evidence, or when required by the user/project. Fix its scope to the repair and affected contracts; expand only for a concrete broader impact. Do not re-review every commit or unchanged branch scope.
- If another round finds the same root cause or a repair-induced defect, stop the mechanical patch/review loop and reassess the cause, direct callers, and repair boundary. Continue a complete repair within existing authorization; ask only for a changed requirement, scope expansion, or missing permission. Do not automatically split off a new requirement or offer a known blocking defect as deliverable. If a prerequisite cannot be supplied, preserve state and report the blocker. Do not force approval after a fixed number of rounds.

## Working State and Runtime

Repair in the target branch's existing checkout, preserving unrelated work. If it has no checkout, create one directly on that branch under the environment's worktree rules. Add a temporary repair checkout only for conflicting concurrent edits or an explicit isolation requirement, stating why. Commit/integrate only as authorized and confirm the target contains the repairs before claiming delivery. Clean up only task-created temporary resources with no uncommitted or untransferred work; otherwise retain and report their location and reason.

Track available startup, review, and handoff timings in the existing record when diagnosing latency. Treat elapsed time as an efficiency signal, not a fixed quality deadline. If unexpectedly slow, inspect supported progress once for scope expansion, duplicate work, stalled calls, or unintended verification, then address the cause. Do not blindly poll, restart, raise effort, or expand scope. Report incomplete coverage honestly. Follow the selected runtime's completion, cancellation, and cleanup protocol; preserve unrelated or user-owned sessions and services.

## Key Rules

- Use the smallest necessary fix for a verified issue; do not refactor unrelated code or expand functionality. Check affected existing behavior and verify that the fix introduces no new regressions.
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

In the final response after the entire amo-deliver workflow completes, append Change summary, Self-test result, and Deployment notes after Ship. Use one sentence each for the entire branch's final changes and self-test results. These three labels are reserved for that final branch-level report; before then, omit the labels and placeholders, while per-round repair reports keep their own plain wording under the workflow's per-round reporting rule.

Derive Deployment notes from the entire branch's actual changes, configuration, and deployment/migration entry points. List required env names, whether mandatory and their defaults; SQL/migration script paths and execution order/timing, separating automatic startup migrations from manual operations; and other necessary dependency, build, restart, or backfill steps. Mark unverified requirements as gaps; state No additional deployment actions only when verified.

Keep applicable sections brief; reference existing evidence instead of reproducing round reports or discarded findings.
