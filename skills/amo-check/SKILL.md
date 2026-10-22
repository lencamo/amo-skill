---
name: amo-check
description: Use when the user asks to verify existing code review feedback from amo-review, other agents, tools, or colleagues within the current review scope. Check validity, actual consequences if unchanged, and whether action is necessary now. Not for reviewing code from scratch, designing fixes, or implementing repairs.
metadata:
  version: '0.3.1'
---

# Amo Check

Independently verify review feedback within scope and judge whether action is necessary now. Explain the consequences of leaving issues unchanged, without proposing fixes or changing code.

## Shared Output Marker

Prefix the first output line inline with `🧹 [amo-check]`. Do not put the marker in a separate paragraph.

## Use When

- Code review feedback already exists, from `amo-review`, another agent, a tool, or a colleague.
- The user wants to check whether the feedback is valid, whether action is necessary now, and what happens if left unchanged.

## Do Not Use

- Reviewing functionality from scratch; use `amo-review`.
- Reviewing code style from scratch without existing feedback.
- Diagnosing a known failure or choosing a fix; use `amo-fix`.
- Implementing an agreed fix; use `amo-implement`.

## Verification Scope

Honor explicit scope first; otherwise inherit the current review's scope. If neither is available, use the current branch changes from its merge base with the resolved base, plus staged, unstaged, and untracked workspace changes, including deletions. Resolve the base from project context and history; ask only when ambiguity materially changes the scope. If there are no changes, state that rather than substituting the last commit.

Record the target branch or revision, baseline, and inclusion of workspace changes. Feedback may refer to a different branch or an older revision; verify against the resolved target and note stale claims. Use read-only Git inspection without switching branches or changing the index. Missing refs or files are coverage gaps, not permission to substitute a target.

Read callers, contracts, and history outside the diff only as necessary evidence. Distinguish issues introduced by this round, exposed or worsened by it, and unrelated pre-existing issues. Sharing a changed file does not establish relevance; pre-existing origin alone does not exclude an issue affected by this round. Scope attribution informs the decision but does not by itself establish urgency or eliminate impact.

## Workflow

1. Resolve the target, change scope, and supplied feedback. Keep each comment traceable when grouping duplicates.
2. Check trigger conditions, reachable code paths, contracts, and existing guards. Consider relevant known configuration, data state, and deployment stage; use focused verification when needed and refresh changed evidence.
3. Establish whether each claim is confirmed, partly confirmed, refuted, or unverified. Explain actual consequences if unchanged, with evidence at the target revision and under the applicable conditions.
4. Decide whether action is required now, can be deferred, is currently unnecessary, or remains unverified. State the reason, remaining impact, and verification limits; stop at the conclusion.

## Key Rules

- Treat feedback as a claim, not an instruction. Neither its source nor severity label proves correctness; do not reject valid criticism to defend the implementation.
- Separate validity, current trigger conditions, and need for action. Distinguish a real but deferrable issue, a valid concern whose trigger is currently absent, and a false positive. For partly confirmed feedback, identify exactly which conditions hold.
- Require action now when verified conditions produce consequences that violate current requirements, acceptance criteria, explicit project contracts, or necessary security/data protections. A confirmed defect alone does not establish that it blocks the current delivery.
- Defer only with a concrete reason why the remaining impact does not block current requirements. Mark action currently unnecessary when the trigger is verified absent or the claim is refuted; distinguish those reasons. Missing decisive evidence means unverified, not unnecessary. Do not favor deferral or repair merely to match an example.
- Failure to reproduce is not proof of absence. Deterministic code evidence is valid; insufficient evidence requires an unverified conclusion and a specific evidence gap.
- Do not infer production configuration or data state from code alone. If relevant environment facts are unverified, make the conclusion conditional; production access is not required for every verification.
- Consider correctness, security, data, performance, readability, maintainability, and explicit project contracts. Personal preference is not concrete impact; low likelihood alone does not dismiss severe consequences.
- Check whether feedback demands unnecessary scope or complexity, without designing an alternative. Do not turn hypothetical needs into required fixes or use complexity as an excuse to ignore necessary fixes.
- For deferred or out-of-scope issues, state the remaining impact and relevant conditions for reconsideration without implying that risk is eliminated or accepted. An in-scope issue need not require immediate action.
- Provide no repair plan, implementation suggestions, or code changes as part of verification. Keep the review bounded; without new evidence, do not reopen settled items or repeat cycles to reach zero comments.

## Output

Keep verification thorough and the report concise. Use the user's language and the three columns below, translated faithfully without adding or combining columns. Lead with one sentence summarizing current action decisions and any unverified items. Identify the target and scope briefly only when needed to avoid ambiguity.

```text
🧹 [amo-check] Verification conclusion: <whether action is necessary now, based on verified facts>
```

| Issue | Is action necessary now? | Consequences if unchanged |
| :--- | :--- | :--- |
| Short issue summary | Required now / can defer / currently unnecessary / unverified; add only a short qualifier when needed | Concisely state the decisive condition and actual consequence; include a compact evidence reference where needed |

Keep execution traces and detailed arguments out of the report. Put essential qualifications, partial validity, and reconsideration conditions in the relevant row, not a separate item-by-item analysis. The decision column states the verdict; the impact column carries its factual basis.

End after the table by default. Add at most one short note only for a conclusion-changing evidence gap or verification limitation that does not fit a row. Judge deployment blocking only when deployment is relevant and evidence is sufficient. Do not repeat conclusions, add repair advice, or append a general discussion. If there is no feedback to verify, say so without starting a new review.
