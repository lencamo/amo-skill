---
name: amo-improve
description: Use when the user asks how to improve, extend, adjust, or redesign an existing feature or behavior before coding. Do not use for brand-new features, broken behavior, pure refactors, or second-pass solution challenges.
metadata:
  version: '0.3.0'
---

# Amo Improve

Plan intentional changes to existing functionality without letting old implementation details decide the target design.

## Shared Output Marker

For a complete deliverable, prefix its first line inline with `🧰 [amo-improve]`. Do not put the marker in a separate paragraph.

## Use When

- Current behavior exists, but the desired behavior is different.
- The user wants to improve, extend, adjust, or redesign an existing feature.
- The work may involve compatibility, migration, interaction changes, or touching existing modules.

## Do Not Use

- The behavior is entirely new; use `amo-feature`.
- Existing behavior is wrong, broken, or unexpected; use `amo-fix`.
- Structure is the primary problem with no behavior change; use `amo-refactor`.
- A proposed solution needs challenge; use `amo-best`.

## Best Standard

Select and state one before recommending a solution:

- **Target-state best**: default for development-stage work when no explicit constraint is stated; prioritize correct boundaries, long-term maintainability, refactoring when needed, and not bending the design around legacy implementation.
- **Constraint best**: use when the user requires fast delivery, compatibility, minimal change, short-term delivery, or limited scope.
- **Evolutionary best**: use when the target design is right, but should be delivered in safe, staged steps.
- **Lowest-risk best**: use when production, data, security, auth/permission, payment, migration, or rollback risk dominates.

## Workflow

1. Identify current behavior and desired behavior. For queries, history, or migrations, state what users will see with existing data immediately after deployment and with newly collected or created data; surface a limitation that changes usefulness before recommending the implementation, and distinguish verified results from projections.
2. Select the best standard and explain why.
3. Inspect implementation, ownership boundaries, and rendered behavior when UI is involved.
4. Decide whether to adapt existing code, reshape it, or stage the target design.
5. Recommend one approach with tradeoffs, blast radius, and verification.

## Key Rules

- Target behavior comes before preserving incidental implementation.
- Do not add compatibility work unless the chosen best standard requires it.
- Do not add speculative compatibility paths, fallback branches, or legacy handling without evidence from the codebase or explicit user requirements.
- Keep unrelated cleanup out of scope.
- For complex scenarios involving queries, batch processing, multi-step data flows, or concurrent operations, assess query costs, resource use, and concurrency risks against relevant implementation and known workload. Include material issues in design tradeoffs or verification, state unknown conditions, and avoid unsupported optimization or architectural expansion.
- If implementation reveals a better approach, pause and explain before switching.

## Output

Use the user's language and requested level of detail. Lead with the answer to the current request. For a complete deliverable, follow the format below, preserving label order and omitting inapplicable sections. For a focused follow-up, answer only that question and any qualification needed to interpret the answer; do not repeat the report or restart workflow routing.

```text
🧰 [amo-improve] Scenario: existing behavior change
Best standard:
Current behavior:
Target behavior:
Recommended approach:
Tradeoffs:
Impact scope:
Verification:
Next: use amo-best for second-pass pressure testing if needed
```
