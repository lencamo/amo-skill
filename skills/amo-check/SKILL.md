---
name: amo-check
description: Use when the user asks to verify existing code review feedback, decide whether findings need fixes, or address review comments from amo-review, other agents, tools, or colleagues. Check validity, actual impact, and repair costs before acting. Not for reviewing code from scratch, solution design, or diagnosing a known failure.
metadata:
  version: '0.2.0'
---

# Amo Check

Independently evaluate code review feedback and decide what to address. Default to reporting decisions without changing code.

## Shared Output Marker

Prefix the first output line inline with `🧹 [amo-check]`. Do not put the marker in a separate paragraph.

## Use When

- Code review feedback already exists, from `amo-review`, another agent, a tool, or a colleague.
- The user wants to verify findings, decide which changes are warranted, or address review feedback.

## Do Not Use

- Reviewing functionality from scratch; use `amo-review`.
- Reviewing code style from scratch without existing feedback.
- Diagnosing a known failure and choosing a fix; use `amo-fix`.
- Designing or reassessing a proposal before implementation.

## Workflow

1. Identify each claim, expected behavior, trigger conditions, and reviewed revision. Group duplicate comments while keeping each traceable.
2. Check the relevant code, callers, contracts, and existing guards against the claim. Confirm whether the trigger is reachable in the current target; use focused verification when needed.
3. Explain what happens if the issue is left unchanged: affected users or flows, consequences, severity, and applicable conditions. Distinguish current requirements from hypothetical needs.
4. Evaluate the proposed remedy separately from the finding. Compare its benefit with added complexity, maintenance cost, and regression risk; recommend the smallest sufficient solution when a change is warranted.
5. Give an evidence-based disposition for each item. When repairs are authorized, implement the warranted changes within scope, verify the result, and distinguish completed work from remaining recommendations.

## Key Rules

- Treat feedback as a claim to verify. Neither the source nor its severity label establishes correctness; do not dismiss valid criticism to defend the existing implementation.
- Separate finding validity, need for action, and remedy choice. A valid finding does not make the suggested fix appropriate.
- Failure to reproduce is not proof of absence. Deterministic code evidence is valid; when evidence is insufficient, mark the item unverified and state what would resolve it. Refresh evidence if relevant code changes.
- Consider correctness, security, data, performance, readability, maintainability, and explicit project contracts. Distinguish personal preference from concrete impact; low likelihood alone does not dismiss severe consequences.
- Do not add speculative guards, compatibility layers, or abstractions merely to clear comments. Complexity cost is not a reason to ignore necessary fixes.
- For deferred findings, state the remaining impact and when to reconsider. Do not claim a risk is accepted without the user's or project's decision.
- Rechecking feedback does not authorize repairs or expand scope. Honor existing repair authorization without asking again; otherwise report decisions and suggested fixes.
- Stay focused on the supplied feedback and necessary context. Without new evidence, do not reopen settled items or repeat review cycles just to reach zero comments.

## Output

Use the user's language for output labels and content. Omit empty sections.

```text
🧹 [amo-check] Scenario: review feedback verification
Conclusion:
Target revision and scope:
```

| Comment | Validity and evidence | Impact if unchanged | Disposition |
| :--- | :--- | :--- | :--- |
| Comment ID or summary | Confirmed / refuted / unverified, with file/line or verification evidence | Actual consequences and conditions | Fix / defer / decline / verify further, with rationale |

For warranted changes, give the smallest sufficient remedy and material tradeoffs. Include completed repairs, verification results, and unresolved evidence gaps when applicable.
