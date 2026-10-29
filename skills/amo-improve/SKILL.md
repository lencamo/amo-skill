---
name: amo-improve
description: Use when the user asks how to improve, extend, adjust, or redesign an existing feature or behavior before coding. Do not use for brand-new features, broken behavior, pure refactors, or second-pass solution challenges.
metadata:
  version: '0.2.1'
---

# Amo Improve

Plan intentional changes to existing functionality without letting old implementation details decide the target design.

## Shared Output Marker

Prefix the first output line inline with `🧰 [amo-improve]`. Do not put the marker in a separate paragraph.

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

1. Identify current behavior and desired behavior.
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

Use the user's language for output labels and content. The labels are the mandatory skeleton: emit every label in order, place all content under its matching label — never unlabeled prose, never merged; keep empty sections with a brief note.

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
